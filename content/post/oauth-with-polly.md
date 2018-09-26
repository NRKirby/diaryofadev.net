---
title: "OAuth with Polly"
author: "Nick Kirby"
url: "/2017/05/oath-with-polly/"
date: 2017-05-01T07:37:36+01:00
image: "http://www.thepollyproject.org/content/images/2016/10/Polly-Logo@2x.png"
description: Polly is a resilience and transient-fault-handling library written in C#. Learn how to use the C# library Polly to help implement OAuth refresh token logic.
aliases:
- /2017/05/01/using-polly-for-oauth-access-token-logic/
draft: false
---

<a href="http://www.thepollyproject.org/" title="The Polly Project" target="_blank"><img src="http://www.thepollyproject.org/content/images/2016/10/Polly-Logo@2x.png" alt="Polly Logo" style="margin: 0 auto;"></a>

Polly is a resilience and transient-fault-handling library written in C# which makes expressing well-known connection policies such as Retry, Circuit Breaker (and more) incredibly easy.

I had to write a client library for consuming a 3rd-party API and found myself writing conditional checks for whether the access token expired, the code ended up looking a bit like this:

```
var response = await httpClient.GetAsync(someApiEndPoint)
 
if (response.StatusCode == HttpStatusCode.Unauthorized)
    RefreshAccessToken();
 
response = await httpClient.GetAsync(someApiEndPoint);
 
if (response.StatusCode == HttpStatusCode.Unauthorized)
    throw new ExpiredRefreshTokenException();
```

As you can see this is pretty messy – there are 2 conditional checks dealing with either the access token expiring or the refresh token expiring.

## Polly

I’d been aware of Polly for some time but never had a real reason to use it and this seemed like a perfect use case for using a **Retry policy** to deal with this use case.

Polly has the concept of a policy which is a way of expressing the how to handle different situations whilst making some sort of call (think IPC, Http etc).

One of the policy primitives available is called **Retry** which, as you would expect, lets you deal with retry logic.

## The code

We can express the logic above as a policy easily, like this:

```
var retry = Policy
        .HandleResult(r => r.StatusCode == HttpStatusCode.Unauthorized)
        .RetryAsync(2, async (exception, retryCount) =>
        {
            // access token expired
            if (retryCount == 1)
            {
                await RefreshAccessToken();
            }
            // refresh token expired
            if (retryCount == 2)
            {
                throw new ExpiredRefreshTokenException();
            }
        });
```

Now we can make any API endpoint calls using this policy like this:

```
retry.ExecuteAsync() => // the call we want to make using the policy
```

## Why? 

The way I see it there are 2 clear benefits of using Polly to define policies:

1. Policies are reusable – we can make calls through a policy wherever we need , rather than having conditional checks everywhere in our code.
2. Expressiveness – the core logic of what we are trying to do becomes more expressive / declarative.

## Links

- [The Polly Project](http://www.thepollyproject.org/)
- [Polly (GitHub)](https://github.com/App-vNext/Polly)
- [Polly Samples](https://github.com/App-vNext/Polly-Samples)