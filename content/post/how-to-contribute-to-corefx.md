---
title: "Getting started contributing to CoreFX"
author: "Nick Kirby"
url: "/getting-started-contributing-to-corefx/"
date: 2018-09-15T07:37:36+01:00
image: "https://avatars0.githubusercontent.com/u/9141961?s=400&v=4"
description: The CoreFX repo is huge (over 15,000 C# classes)and the aim of this blog post is to bring together much of the information needed to get started contributing. 
tags: ['OSS']
aliases:
- /how-to-contribute-to-corefx/
draft: false
---

[CoreFX](https://github.com/dotnet/corefx) is a repo containing the open-source class libraries for .NET core. The CoreFX repo is huge (containing over 15,000 C# classes) and the aim of this blog post is to bring together much of the information needed to get started contributing. 

CoreFX is made up of 1000’s of classes which many .NET developers depend on a daily basis, such as the classes in the `System.Collections` namespaces.

> Note: Some classes that you’d expect to be in CoreFX such as String and List are actually in [mscorlib](https://github.com/dotnet/coreclr/tree/master/src/System.Private.CoreLib) in the [CoreCLR](https://github.com/dotnet/coreclr). These types (and others) live in mscorlib as they are intrinsically linked to the CLR and need to be accessed from native CLR code. If you’re interested, see [this document on mscorlib](https://github.com/dotnet/coreclr/blob/master/Documentation/botr/mscorlib.md) from [The Book of the Runtime](https://github.com/dotnet/coreclr/tree/master/Documentation/botr) for more details.

Now that’s out of the way let's see how we can get started contributing! 

### 1. Set up your (Windows) development environment:

1. [Install Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads: 
   
    - .NET desktop development
        - NET Framework 4-4.6 Development Tools

    - Desktop development with C++ 
        - VC++ 2017 v141 Toolset (x86, x64)
        - Windows 10 SDK or Windows 8.1 SDK

    - .NET Core cross-platform development 
        - All Required components
  
2. [Install CMake](https://cmake.org/download/#latest) and add it to your path environment variable

> Instructions for setting up on all platforms [here](https://github.com/dotnet/corefx/wiki/Setting-up-the-development-environment)

### 2. The Dev Workflow

The [Dev Workflow](https://github.com/dotnet/buildtools/blob/master/Documentation/Dev-workflow.md) describes the development process for the repo. 

![alt text](https://github.com/dotnet/buildtools/raw/master/Documentation/images/Dev-workflow.jpg "CoreFX development workflow")

### 3. The Developer Guide

The [Developer Guide](https://github.com/dotnet/corefx/blob/master/Documentation/project-docs/developer-guide.md) gives a more in depth explanation for how to clean, build and run tests. 

Examples:


**Full clean build and test:**

```
clean -all
build
build-tests
```

**Build an individual library and test:**

```
build System.Collections
```

### 4. Find something to work on

- Contributions are made through the usual pull request model on GitHub and (at time of writing) there are over 2000 [open issues](https://github.com/dotnet/corefx/issues). 
- People new to the project should probably check out the [easy label](https://github.com/dotnet/corefx/labels/easy) which contains many issues for improving test coverage making them a great way to get familiar to the project without too much knowledge of the contribution workflow. If you do pick up a code coverage issue the [code coverage doc](https://github.com/dotnet/corefx/blob/master/Documentation/building/code-coverage.md) and [code coverage report](https://ci.dot.net/job/dotnet_corefx/job/master/job/code_coverage_windows/Code_Coverage_Report/) will definitely come in handy. 
- When you've found an issue or you need help you can [find the area owners here](https://github.com/dotnet/corefx/blob/master/Documentation/project-docs/issue-guide.md#areas) or contact [@karelz](https://github.com/karelz) or [@danmosemsft](https://github.com/danmosemsft).

   


## Links 

- [Project repo](https://github.com/dotnet/corefx)
- [New contributor contributing guide](https://github.com/dotnet/corefx/wiki/New-contributor-Docs#contributing-guide)
- [Documentation index](https://github.com/dotnet/corefx/tree/master/Documentation)
- [Developer Guide](https://github.com/dotnet/corefx/blob/master/Documentation/project-docs/developer-guide.md)
- [Dev Workflow](https://github.com/dotnet/buildtools/blob/master/Documentation/Dev-workflow.md)