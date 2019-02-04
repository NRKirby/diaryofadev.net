---
title: "Do I want a slot setting, or not?"
author: "Nick Kirby"
url: "/do-i-want-a-slot-setting-or-not/"
date: 2019-02-04T11:37:36+01:00
image: "https://diaryofadev.blob.core.windows.net/images/slot-setting.JPG"
description: Azure app settings and connection strings can have a SLOT SETTING, but which one should you use? 
tags: ['azure']
aliases:
draft: false
---

App settings and connection strings are an important part of any CI pipeline. Over the years I've seen sites been brought down because an incorrect app setting got swapped from staging to production when it shouldn't have. 

In Azure there's a **SLOT SETTING** checkbox by every app setting and connection strinh. This is used to control how settings move (or not) when staging and production get swapped. 

<img src="https://diaryofadev.blob.core.windows.net/images/slot-setting.JPG" alt="Azure slot setting" style="width: 40%;margin: 0 auto;">

## Question

From time to time I find myself asking a colleague the same question:

> "Do I want a slot setting, or not?"

Of course, I should [RTFM](https://docs.microsoft.com/en-us/azure/app-service/deploy-staging-slots) but this info is buried halfway down (no excuses, I know). This blog post will mean I don't have to ask him again! (Thanks [Jon](https://twitter.com/jonhilt)!)


## Answer

- With slot setting enabled (checked), the setting **will not move from the slot**. For example, enable it in Production if you don't want the setting to swap with Staging.

- With slot setting disabled (unchecked), the setting **will move each time** a swap happens. 

