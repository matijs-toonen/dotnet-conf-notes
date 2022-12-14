- [Aspnet](#aspnet)
  - [Auth](#auth)
    - [ValidIssuer](#validissuer)
  - [Devtunnels](#devtunnels)
  - [Request](#request)
    - [MapRoute](#maproute)
      - [Scaffold the routes](#scaffold-the-routes)
  - [Response](#response)
  - [Http/3](#http3)
    - [WebTransport](#webtransport)
  - [Rate limiting](#rate-limiting)
    - [Fixed Time Window](#fixed-time-window)
    - [Sliding Time Window](#sliding-time-window)
    - [Concurrency limit](#concurrency-limit)
    - [Token Bucket Limit](#token-bucket-limit)
    - [Partitions](#partitions)
  - [Output Caching](#output-caching)
    - [Work With Rate Limiting](#work-with-rate-limiting)
  - [Migration](#migration)
    - [Visual Studio Extension](#visual-studio-extension)
    - [Steps](#steps)
      - [Preparation](#preparation)
      - [Migrating The Code](#migrating-the-code)
    - [Source](#source)
  - [Dynamically Adding Code](#dynamically-adding-code)
    - [Source](#source-1)
  - [Configuration](#configuration)
    - [IOptions](#ioptions)
      - [Named Configuration](#named-configuration)
    - [Validation](#validation)
    - [Source](#source-2)
  - [Network Improvements](#network-improvements)
    - [Source](#source-3)
- [Containers](#containers)
  - [Chiseled](#chiseled)
    - [Rootless](#rootless)
      - [Without Chiseled Images](#without-chiseled-images)
    - [Source](#source-4)
- [Blazor](#blazor)
  - [Custom Component](#custom-component)
  - [Progress Bar](#progress-bar)
  - [WebAssembly](#webassembly)
    - [SIMD / Vectorization](#simd--vectorization)
    - [Multithreading [ALPHA]](#multithreading-alpha)
      - [Considerations](#considerations)
      - [Example](#example)
    - [JavaScript Interop](#javascript-interop)
    - [AOT Compilation](#aot-compilation)
  - [Playwright Testing](#playwright-testing)
    - [Tracing](#tracing)
    - [Integration with MSTest](#integration-with-mstest)
    - [Recording Playwright Steps](#recording-playwright-steps)
  - [Styling](#styling)
    - [Sass](#sass)
    - [CSS](#css)
      - [CSS Isolation](#css-isolation)
      - [CSS Variables](#css-variables)
- [Azure](#azure)
  - [Container Apps](#container-apps)
    - [Possibilities](#possibilities)
    - [Ingress](#ingress)
    - [Dapr](#dapr)
    - [Container Apps vs Azure Kubernetes Service](#container-apps-vs-azure-kubernetes-service)
      - [Rule of Thumb](#rule-of-thumb)
  - [CDN for Blob Storage](#cdn-for-blob-storage)
  - [App Configuration](#app-configuration)
  - [Azure Functions](#azure-functions)
    - [Durable Functions](#durable-functions)
      - [Exception Handling](#exception-handling)
        - [Source](#source-5)
  - [Static Web Apps](#static-web-apps)
    - [Container Apps](#container-apps-1)
    - [Linking](#linking)
    - [Enterprise Grade Edge](#enterprise-grade-edge)
    - [Authentication](#authentication)
    - [Source](#source-6)
- [MAUI](#maui)
  - [Blazor Hybrid](#blazor-hybrid)
- [Orleans](#orleans)
- [C#](#c)
  - [Required Properties](#required-properties)
  - [Static Abstract Members on Interfaces](#static-abstract-members-on-interfaces)
  - [Performance](#performance)
    - [Static Lambdas](#static-lambdas)
      - [Before](#before)
      - [After](#after)
      - [Performance Difference](#performance-difference)
    - [On-Stack Replacement (OSR)](#on-stack-replacement-osr)
    - [Source](#source-7)
  - [File Scoped Classes](#file-scoped-classes)
  - [Interop](#interop)
    - [DisableRuntimeMarshalling](#disableruntimemarshalling)
    - [Source](#source-8)
    - [CustomMarshaller](#custommarshaller)
- [GitHub](#github)
  - [Dependabot](#dependabot)
  - [Codespaces](#codespaces)
- [Microsoft Devbox](#microsoft-devbox)
  - [Auto Stop Time](#auto-stop-time)
  - [GitHub Integration](#github-integration)
- [Low Code](#low-code)
  - [Architecture](#architecture)
- [WinUI 3](#winui-3)
  - [Dark / Light Mode](#dark--light-mode)
  - [Rive Animations](#rive-animations)
- [CoreWCF](#corewcf)
  - [Dependency Injection](#dependency-injection)
    - [Injected Attribute](#injected-attribute)
  - [Features](#features)
  - [Upgrade Assistant](#upgrade-assistant)
- [gRPC](#grpc)
  - [Server Reflection](#server-reflection)
    - [Enabling Server Reflection](#enabling-server-reflection)
  - [Postman](#postman)
  - [gRPC Json Transcoding](#grpc-json-transcoding)
    - [Swagger](#swagger)
  - [Azure App Service](#azure-app-service)
- [NativeAOT](#nativeaot)
  - [Source](#source-9)
- [Microservices](#microservices)
  - [Authentication / Authorization](#authentication--authorization)
    - [Source](#source-10)
    - [Important Reminders](#important-reminders)
      - [Authorization Response](#authorization-response)
      - [Conclusion](#conclusion)
      - [Resources](#resources)
- [Polyglot Notebooks](#polyglot-notebooks)
  - [Input](#input)
  - [Nuget packages](#nuget-packages)
  - [UI](#ui)
  - [GitHub](#github-1)
  - [Dynamically Create Notebook Commands](#dynamically-create-notebook-commands)
- [Infer#](#infer)
  - [Visual Studio](#visual-studio)
  - [Custom Rules](#custom-rules)
  - [DevOps Integration](#devops-integration)
- [ML.NET](#mlnet)
  - [TorchSharp](#torchsharp)
  - [TensorFlow](#tensorflow)
  - [NER & Question Answering](#ner--question-answering)
  - [Object Detection](#object-detection)
- [T4](#t4)
  - [Power Tools](#power-tools)
  - [Entity Framework 7](#entity-framework-7)
- [CloudEvents](#cloudevents)
  - [Architecture](#architecture-1)
- [IOT](#iot)
- [ComputeSharp](#computesharp)
  - [Performance](#performance-1)
- [Database](#database)
  - [EF 7](#ef-7)
    - [Execute Extensions](#execute-extensions)
      - [UpdateAsync](#updateasync)
      - [DeleteAsync](#deleteasync)
    - [Source](#source-11)
  - [Graph](#graph)
    - [Dropping Data](#dropping-data)
      - [Note](#note)
- [Source](#source-12)
- [TODO](#todo)

# Aspnet
## Auth
use the console to generate the bearer token via the dotnet command
`dotnet user-jwts create`

### ValidIssuer
Configuring the `ValidIssuer` property in the `Authentication` property of the launchsettings to `dotnet-user-jwts` will recognize these tokens generated from the command line to be valid
![ValidIssuer](./Resources/AspNet/Authentication/ValidIssuer.png)

## Devtunnels
Configuration settings on the csproj which will generate a public url which points to your own machine

## Request
### MapRoute
`MapRoute`
Configure a prefix to the routes for a certain model
It is possible to chain `MapGroup` calls to apply rules like logging to all requests and then a subset of request for specific rules

#### Scaffold the routes
Use visual studio to scaffold the routes in the same way a standard controller works

## Response
`TypedResults` is for swagger metadata
`Task<Results<Ok<Model>, NotFound>>` can be configured on the endpoint itself which is also for metadata in swagger so swagger is aware what the possible result types are

## Http/3
Is now officially supported, it is still opt-in and should be configured in the kestrel configuration

### WebTransport
WebTransport is now in the experimental phase
![WebTransport](./Resources/AspNet/Http/WebTransport.png)

## Rate limiting
`AddRateLimiter` can be used to now configure a rate limiting.

### Fixed Time Window
Based on time, e.g. twice per hour, but the hour starts counting when you first send a request
Think of 1:23 PM you send 2 requests, it resets 2:23 PM

### Sliding Time Window
Based on static time, e.g. twice per hour, but the hour is statically defined to be reset every hour.
Think of the reset timer being based on clock hours, in this case it resets 1 PM and 2 PM etc.
In this case you can send 2 requests at 1:55 PM. At 2 PM it resets and you can resend 2 requests

### Concurrency limit
Only allow 10 concurrent requests for any user.
Multiple users will consume these requests and the 11 user will be denied.

### Token Bucket Limit
Every request takes a bucket which will be replenished at a fixed time.
Think of the following: every 2 minute return 5 tokens to the bucket.
Even when the requests are still running there will be 5 new tokens available.
The tokens cannot exceed a predefined bucket limit

### Partitions
Define a limit by a custom value, e.g.

1. Based in IP
2. Based on Token

![RateLimiting](./Resources/AspNet/Http/RateLimiting.png)

## Output Caching
This will cache the result of the api and will respond to future requests with a cached response

### Work With Rate Limiting
Order is important when calling the `UseOutputCache` and `UseRateLimiter` methods.
When you call `UseOutputCache` first it will not use `Rate Limiting`.
When calling the `UseOutputCache` after the `UseRateLimiter` call it will both cache and respect the rate limiting configured

## Migration 
A new way to migrate an existing project of ASP.NET to ASP.NET Core has been added which utilises YARP.
This is called incremental migration and works to following way:

1. Requests directed to routes which have **NOT** yet been migrated will be forwarded to the **old** existing code running on ASP.NET
2. Requests directed to routes which have been migrated will be handled within the YARP app as this app also includes the code.

Forwarding these requests is done by YARP which stands in front of the app as reverse proxy
![YARP Reverse Proxy](./Resources/AspNet/Migration/YarpReverseProxy.png)

### Visual Studio Extension
Using the `Microsoft Project Migrations` extension in Visual Studio will help you migrate your existing projects in Visual Studio.
![Migration Context Menu](./Resources/AspNet/Migration/MigrationContextMenu.png)

### Steps
There are a couple of steps you can take to migrate safely from ASP.NET to ASP.NET Core.
Because not all features from ASP.NET are available in ASP.NET Core, it is recommended to migrate in the following order to ensure the features still work.

#### Preparation

1. Migrate the project using the extension to create a new ASP.NET Core application which at that moment routes all traffic from the ASP.NET Core app to the ASP.NET app using YARP
2. Ensure all features still work the same way

#### Migrating The Code
The following steps apply to all the code you have in your ASP.NET app and will be done repetitively.

1. Migrate a single controller, view, or class using the extension. The extension will update the YARP rules for you.
2. Resolve any issues for that single migrated object
3. Test the use cases for that object
4. Deploy

### Source

1. [Youtube Video](https://www.youtube.com/watch?v=XQyCgwB_szI&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=48)

## Dynamically Adding Code
It is possible to add code to your ASP.NET Core app without the code knowing about it via a couple of things:

1. dotnet environment variables 
2. Runtime package store
3. Custom manifest artifect
4. Code using certain interfaces to get called

Image below shows a high level overview of the steps you need to do to use the custom assemblies in your runtime package store
![Dynamic Code Pipeline](./Resources/AspNet/DynamicCode/DynamicPipeline.png)

### Source

Each step mentioned above is explained in the youtube video below.
1. [Youtube Video](https://www.youtube.com/watch?v=LMuYH6b31AU&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=59)

## Configuration
Indept explanation will be in the source as there are alot of different ways you can use the Configuration.

### IOptions
There are a couple of different IOptions implementations which have other benefits
![IOptions Types](./Resources/AspNet/Configuration/IOptionsTypes.png)

#### Named Configuration
Using the IOption types which support `Named` configurations can be configured and retrieved as follows:
![Configuring Named Configuration](./Resources/AspNet/Configuration/NamedConfigurationBinding.png)
![Retrieving Named Configuration](./Resources/AspNet/Configuration/RetrieveNamedConfiguration.png)

### Validation
It is possible to validate your configuration with custom logic or data annotations
![Configuration Validation](./Resources/AspNet/Configuration/ConfigurationValidation.png)

### Source

1. [Youtube Video](https://www.youtube.com/watch?v=1aNMO2cBmv0&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=61)
2. [GitHub Source](https://github.com/Codebytes/dotnet-configuration-in-depth)

## Network Improvements
There are alot of improvements in the network stack in .NET 7.0, here are a couple of highlights:

1. HTTP/3 support
2. HTTP/2 WebSocket support
3. Experimental QUIC implementation (based on msquic)

Detailed information can be found in the sources, but here are some images for clarity (images are taken from the source):
![HTTP/3 vs HTTP/2](./Resources/AspNet/Network/Http3VsHttp2.png)
![Quic Protocol](./Resources/AspNet/Network/QuicProtocol.png)
![HTTP/3 When and Why](./Resources/AspNet/Network/WhenAndWhyHttp3.png)

### Source

1. [Youtube Video](https://www.youtube.com/watch?v=mTdcWlIiX7c&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=62)
2. [MSQuic](https://github.com/microsoft/msquic)
3. [YARP](https://github.com/microsoft/reverse-proxy)

# Containers
## Chiseled 
.NET 7.0 now has the option to use a chiseled version of dotnet, this is a highly optimized minimal version for your app.
The goal is to minimize the attack service and remove unnecessary features like bash.
This would typically only be used in release mode and not at development mode.

![Chiseled Size](./Resources/Microservices/Containers/ChiseledImageSize.png)
![Implement](./Resources/Microservices/Containers/Usages.png)

### Rootless
The chiseled image does not have a root user (for valid security reasons) which will result in the port which is exposed by default which is 80 / 443 to change.
This is because by default only root users can use the ports up to 1024.

![Rootless Port](./Resources/Microservices/Containers/Rootless.png)

#### Without Chiseled Images
.NET team is working on creating images where the user is always non root.
Planned but not promised for .NET 8.0

### Source

1. [Youtube Video](https://www.youtube.com/watch?v=FLGFzlWF4Gs&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=65)
2. [Rootless Without Chiseled Images](https://github.com/dotnet/dotnet-docker/issues/2249)

# Blazor
## Custom Component
Integrate an blazor component with other code stacks that are hosted on the same domain
![Blazor Configuration](./Resources/AspNet/Blazor/CustomComponent/CustomComponent.png)
![Injecting Blazor](./Resources/AspNet/Blazor/CustomComponent/InjectingBlazor.png)
![Referencing Component](./Resources/AspNet/Blazor/CustomComponent/ComponentReference.png)

The image above not only shows how to reference the custom blazor component but also configures parameters which are sent to the blazor component

## Progress Bar
It is now possible to configure a progress bar on the blazor site when the site is being loaded. Using an existing template will automatically configure this for you,
but it is also possible to manually create this progress bar with manual UI components and CSS.
Using the following variable in CSS which is build in, you can get the current state of the loading in procentage.
![ProgressBarCssVariable](./Resources/AspNet/Blazor/ProgressBar/ProgressCssVariable.png)

## WebAssembly
### SIMD / Vectorization
WebAssembly now supports SIMD via the already existing apis

### Multithreading [ALPHA]
Not supported out of the box, but can be configured to be used. **NOT PRODUCTION READY**
Multithreading is implemented using `WebWorkers` and `SharedArrayBuffer` which is supported on all major browsers.
![Threading](./Resources/AspNet/Blazor/Multithreading/Features.png)

#### Considerations
There are a couple of things you **currently** need to do to enable multithreading
![Considerations](./Resources/AspNet/Blazor/Multithreading/CurrentConsiderations.png)

#### Example
You can find a quick demo of an example app running the uno platform with webassembly in .NET 7.0 with multi threading enabled
[here](https://raytracerbenchmark-wasm.platform.uno/).
This example shows the capabilities of offloading work to multiple threads, as long as your CPU can handle it.

### JavaScript Interop
Possible to export a lambda from C# to JS which will be executed in JS to run C# code.
![Export Lambda](./Resources/AspNet/Blazor/JSInterop/ExportLambda.png)
![Execute Lambda JS](./Resources/AspNet/Blazor/JSInterop/ExecuteLambdaInJs.png)

### AOT Compilation
Compiling your webassembly app in AOT improves the performance of the app by alot!

## Playwright Testing
Playwright is a testing framework for UI testing. It is possible to record UI steps like clicking buttons which will automatically generate test code which can be automated.

### Tracing
It is possible to look through traces made by playwright in which you can see the following information:

1. The steps which got executed
2. How long these steps took to execute
3. The devtools of your browser at that point (think about console errors)
4. A snapshot of your website at that time, so you can see what went wrong in the UI.

![Playwright Tracing](./Resources/AspNet/Blazor/Playwright/PlaywrightTracing.png)
By default Playwright creates a browser in background to perform tests, it is possible to configure that the browser should be visually launched.

### Integration with MSTest
It is possible to create unit tests with the playwright.
Using `await Page.PauseAsync()` in the test will pause the execution to allow you as the developer to debug in the browser for issues.

### Recording Playwright Steps
![Playwright Recording](./Resources/AspNet/Blazor/Playwright/PlaywrightRecording.gif)

## Styling
### Sass
It is possible to compile sass files for Blazor projects right from the csproj file in your MSBuild commands.
![MSBuild Sass](./Resources/AspNet/Blazor/Styling/Sass/MSBuildSass.png)

### CSS
#### CSS Isolation
It is possible to create a CSS file which would only be applied to that single component. These CSS files are linked to the corresponding razor component based on the name with a suffix of `.css`
e.g. `Counter.razor` would have an isolated css file named `Counter.razor.css`.
The compiler will scope the css to only the html in the razor file based on an unique identifier generated at compile time.
![CSS Isolation](./Resources/AspNet/Blazor/Styling/Css/CssIsolation.png)

#### CSS Variables
Creating variables is possible by using a prefix of `--` with an name of the variable and the value e.g. `--foo: #000;`. 
This will create a variable named `--foo` and can later on be referenced using the `var` keyword e.g. `var(--foo, [fallback value])`
It is also possible to define a scope in which this variable is set to a specific value:

1. using `:root { --foo: #000; }` will globally set the variable `--foo` to `#000`
2. using `.baz { --foo: #FFF; }` will set the variable of `--foo` to `#FFF` **ONLY** when it is applied on the baz class.
![CSS Variables](./Resources/AspNet/Blazor/Styling/Css/Variables.png)
![Scoped Variables](./Resources/AspNet/Blazor/Styling/Css/ScopedVariables.png)

# Azure
## Container Apps
Azure Container apps are container images running in a cluster. These containers are running on Kubernetes in the background, but do not require Kubernetes configuration.

### Possibilities
![Possibilities](./Resources/Azure/ContainerApps/Possibilities.png)
![Features](./Resources/Azure/ContainerApps/Features.png)

### Ingress
Configuring Ingress:
![Enable Ingress](./Resources/Azure/ContainerApps/IngressRules.png)

### Dapr
Enabling Dapr requires a in Azure Configuration:
![Enable Dapr](./Resources/Azure/ContainerApps/EnableDapr.png)
Using Dapr requires a request header to be set:
![Dapr Headers](./Resources/Azure/ContainerApps/UseDapr.png)
Dapr also integrates with Application Insights which will automatically collect logs and traces.

### Container Apps vs Azure Kubernetes Service
Container apps runs on top of Kubernetes, but provides a bunch of abstractions so you as a developer don't have to worry about the infrastructure yourself.
You still get alot of capabilties of running your app in Kubernetes.

#### Rule of Thumb
If you don't wanna manage the infrastructure, you can start with Container Apps.
When you later on need to have more control you can easily switch to Kubernetes as the things that Container Apps support like Dapr, Ingress, etc.
are all supported in Kubernetes.
Moving from Kubernetes to Container Apps for the other way around is also possible.

## CDN for Blob Storage
It is possible to create a CDN for the Blob Storage which will serve all the files within the Blob Storage via the Azure CDN

## App Configuration
Using `Microsoft.Azure.AppConfig` nuget package will allow the usage of the `App Configuration` for this app.
`DefaultAzureCredential` will be resolved in two different ways:

1. When running locally, it will use the currently logged in Visual Studio user account
2. When deployed to the Cloud, it will use the managed identity configured for that app.
![AddAppConfiguration](./Resources/Azure/AppConfiguration/AddAppConfiguration.png)

## Azure Functions
Isolated process is now completely decoupled from the host and will from now on allow any runtime version as long as Azure supports it.
Middleware is now also supported

### Durable Functions
Durable functions are orchestrators which calls multiple activities and manages these activities.
Durable functions are now available in the isolated process model
![Isolated Features](./Resources/Azure/Functions/Isolated.png)

#### Exception Handling
As the orchestrator calls multiple activities which are other functions there is no direct link between these two.
It is however still possible to use the `try - catch` syntax to `catch` an exception thrown in the activity you manage.

This is possible because the result of any function is saved as a state and will be deserialized and rethrown in the orchestrator.
This is very powerful!
![Exception Handling](./Resources/Azure/Functions/ExceptionHandling.png)

##### Source

1. [Youtube Video](https://www.youtube.com/watch?v=JIQzz7yIHpo&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=55)

## Static Web Apps
Along support for `Function Apps` as the backend, static web apps now has **preview** support for using the following Azure Services as the backend:

1. Api Management Service
2. App Service
3. Container Apps

### Container Apps
Using container apps you can create microservices in a serverless environment.
Connecting this with the static web apps is very powerful!

### Linking
To Link your static web app to a backend mentioned above (including Function Apps), you will need to upgrade your static web app to Standard tier.

### Enterprise Grade Edge
It is possible to enable the Enterprise Grade Edge which uses Azure Frontdoor and Azure CDN in combination with the static web app.
![Enterprise Grade Edge](./Resources/Azure/StaticWebApps/EnterpriseGradeEdge.png)

### Authentication
Authentication can be done by the backend identity.
Supported identity providers out of the box for free tier:

1. GitHub
2. Twitter
3. Azure AD
  
Custom providers are supported at standard tier.
![Authentication Flow](./Resources/Azure/StaticWebApps/Authentication.png)

### Source

1. [Youtube Video](https://www.youtube.com/watch?v=FjGjguW1Xa0&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=75)

# MAUI
## Blazor Hybrid
Shell can be used to add native navigation based on the environment your app is currently running on.
[AirQualityApp](https://github.com/jamesmontemagno/Airqualityapps)

# Orleans
Framework for `horizontally` scaling your ASP.NET Core application.
Orleans hides the service discovery when calling endpoints on other services. 
Think about calling an object which lives in an application behind a load balancer, orleans will contact the right application for you and return the response.
![Distributed Calls](./Resources/Orleans/DistributedCalls.png)
![Features](./Resources/Orleans/Features.png)

# C#
## Required Properties
Init only properties now support the `required` keyword which will enforce the user to set the value of the property through the object initializer.
Can even be used on properties of an `Attribute`.
Required is inherited by default and is still required on child classes.
It is possible to ignore `required` properties **ONLY** when setting a `SetsRequiredAttribute` on a constructor which then will fill in all the required properties.

## Static Abstract Members on Interfaces
`static abstract` members enforce the implementors of the interface to implement this static member in their own way.
This can even be done on operators like the `+` operator. Great example of this use case is the `IAdditionOperators` interface which enforces the `+` operator on any number (double, int, etc.)
Overloading a checked version of your operator is supported by simply adding the `checked` keyword to your method signature.
![Static Abstract Interface Members](./Resources/C%23/Compiler/StaticOperators.png)

## Performance
Detailed blog about all the improvements can be found here:
[.NET 7 Improvements](https://devblogs.microsoft.com/dotnet/performance_improvements_in_net_7/)

### Static Lambdas
Since C# 9 it is possible to use the `static` keyword on a lambda call which will allow the caller to only capture the specified variables and send it as part of the lambda.
This all happens at runtime and does not need support for an overload func which has the variable you want to capture as part of the argument.
Because this does not capture state it will not allocate any unnecessary memory for the compiled anonymous class.

#### Before
![Closure Allocation](./Resources/C%23/Performance/ClosureAllocation.png)

#### After
![Without Closure Allocation](./Resources/C%23/Performance/NoClosureAllocation.png)

#### Performance Difference
![Performance Difference](./Resources/C%23/Performance/PerformanceDifference.png)

### On-Stack Replacement (OSR)
Loop iterations are now tracked for the tiered compilation, this is on by default.
This means that loops which previously did not get any tiered compilation to improve the throughput will now on the fly improve the method code when the Jitter hits the compilation tier threshhold.
![On-Stack Replacement](./Resources/C%23/Compiler/OnStackReplacement.png)

### Source

1. [Stephen Toub Runtime](https://www.youtube.com/watch?v=yNPEdaxkTZw&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=25)
2. [Daniel Marbach Azure SDK](https://www.youtube.com/watch?v=z0r4lx618Us&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=56)

## File Scoped Classes
Mostly used for source generators to ensure there is no way that files have conflicting names when generating a backing class.
The `file` keyword results in the class only being available within that file.

## Interop
New attribute called `LibraryImport`, using `LibraryImport` will use source generators to generate the code needed at compile time and not dynamically at runtime like `DllImport` does.
This improves a couple of things:

1. Performance as the runtime doesn't need to generate code at runtime
2. Debugging as this code can be stepped through
3. The generated source code is included in the stacktrace which will improve tracing
4. Easy to create a custom variant of the generated code as you would copy and modify it and call your custom variant

### DisableRuntimeMarshalling
`DisableRuntimeMarshalling` is an attribute which needs to be assigned to the whole assembly which will guarantee that the struct will be passed as an blittable struct.
Not that clear at the moment how this works and when to use it

### Source

1. [Youtube Video](https://www.youtube.com/watch?v=ucNcRtnifXY&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=47)

### CustomMarshaller
Using `LibraryImport` you need to create a custom marshaller for custom types, this allows for more control over your marshalling.
You can also specify which marshaller you want to use when converting your type to the unmanaged type, this is done via 2 ways:

1. `NativeMarshalling` attribute on the type itself, assigning this will set this marshaller as the default marshaller for this type
2. `MarshalUsing` attribute on the type in your method signature in the `LibraryImport`, assigning this will override the default marshaller for this type with the specified marshaller

# GitHub
## Dependabot
Using dependabot can create PR's for updating nuget package changes which will include the changelogs, commits, and release notes of all the newer versions of your nuget package.
Dependabot can also create warnings for security vulnerabilities, which will be created as security advisories in GitHub.

## Codespaces
Everybody gets 60 minutes of codespaces for free per month!

# Microsoft Devbox
It is possible to create a dev box setup by your IT department for specific needs and projects.
Before creating a dev box you need to select a project and dev box pool out of the projects and hardware pools setup.

This dev box will have everything needed for your project ready. Think of the following:

1. Frontend dev pool -> Visual Studio Code, npm, etc.
2. Backend dev pool -> Visual Studio, dotnet, etc.
3. etc.

## Auto Stop Time
Dev box pools can be set to have an auto stop time which will automatically shut down an idle dev box,
when the dev box is still being used the user will receive a notification about the shut down and can delay the shut down timer so the developer can continue working.

## GitHub Integration
It is possible to create a dev box from GitHub actions to easily review your changes on the fly.

# Low Code
Below is a rule of thumb which will guide when to use low code and when not to use low code:
![When To Use](./Resources/LowCode/WhenToUseLowCode.png)

## Architecture
As Power Apps or other kinds of low-code applications don't have code to execute the business logic it is recommended to create custom connectors behind the low-code applications.
![Custom Connectors](./Resources/LowCode/CustomConnectors.png)

The image above shows how to use the low-code for the frontend but execute the business logic behind the frontend in a Rest API (can be .NET).
This way can even leverage from a microservices architecture in which you run the backend business logic as microservices.

![Backend Architecture](./Resources/LowCode/MicroservicesArchitecture.png)

# WinUI 3
It is possible to create custom widgets for windows.
Supports .NET 7 with C# 11.
It is part of a nuget package, so you as the developer will decide when to update.

## Dark / Light Mode
Adding a new item via the `New Item (Template Studio)` option and selecting the `Settings` Page will automatically add a settings page navigation cockwheel.
The settings page automatically adds `Dark` and `Light` theme settings. These settings will work any native components which have not been set to a color manually.

## Rive Animations
Rive Animations are awesome! The animations have properties which will show different animations based on these property values.

# CoreWCF
Possibility to create a WCF Server and Client in .NET 7
Deployment of WCF is moved to ASP.NET Core, it is implemented as a middleware and will therefore support all the same features as ASP.NET Core does.

## Dependency Injection
CoreWCF allows your connected WCF service to be injected via dependency injection, this in turn will allow other services to be injected as dependency injected services into the connected WCF service.
Example of this would be to inject the `ILogger` class into the connected WCF service so you can use this logger to log endpoint information.

### Injected Attribute
It is possible to get the `HttpContext` or any other DI type when the method gets called.
There are 3 steps to enable this feature:

1. Add a package reference to `CoreWCF.Primitives`
2. Change the `Service` class to `partial`, this is done as the parameters do not match the interface signature and the `partial` keyword will allow code generation to create the method which matches the interface and internally call your method with the requested parameters
3. Add the `Injected` attribute to the `parameter` which you want to be injected.
![Dependency Injection Attribute](./Resources/WCF/DependencyInjectionAttribute.png)
![Dependency Injection Interface](./Resources/WCF/DependencyInjectionInterface.png)

## Features
![Features](./Resources/WCF/Features.png)

## Upgrade Assistant
Upgrading WCF to CoreWCF is now supported as part of the upgrade assistant.

# gRPC
## Server Reflection
With gRPC server reflection you can expose metadata about your gRPC contracts that are being hosted. You no longer have to share the `proto` file manually to every client when using `gRPC Server Reflection`.

### Enabling Server Reflection
There are a couple of steps you need to take before server reflection is enabled on your gRPC server:

1. Add the `Grpc.AspNetCore.Server.Reflection` nuget package to your server project.
2. Add the `AddGrpcReflection` method to your services.
3. Map the `MapGrpcReflectionService` method to your app.
![Enabling Server Reflection](./Resources/GRPC/EnablingServerReflection.png)

## Postman
Postman now supports gRPC Requests! Using [Server Reflection](#server-reflection) allows you to retrieve the metadata from your gRPC server in Postman and from there on get the endpoints.
![Server Reflection](./Resources/GRPC/PostmanServerReflection.png)

## gRPC Json Transcoding
With Json Transcoding it is possible to expose the gRPC methods via gRPC as well as classic REST.
The following steps enable the Json Transcoding feature:

1. Add the `Microsoft.AspNetCore.Grpc.JsonTranscoding` nuget package to your server project.
2. Add `AddJsonTranscoding` method to your `AddGrpc` method chain.
3. Configure the endpoint route and type of your gRPC method on REST

![Enabling Transcoding](./Resources/GRPC/EnableTranscoding.png)
![Rest Json Transcoding](./Resources/GRPC/JsonTranscodingRoute.png)

Notice that the `Name` property directly links to the `Name` property of the input type (`HelloRequest`)

### Swagger
Because Rest api's show up in swagger it is now possible to add swagger for your Rest api's.
The following steps enable swagger for the Json Transcoded methods:

1. Add the `Microsoft.AspNetCore.Grpc.Swagger` nuget package to your server project.
2. Add the `AddGrpcSwagger` method to your services.
3. Add the default `AddSwaggerUI` and `UseSwaggerUI` methods.

![Enabling Swagger](./Resources/GRPC/Swagger.png)

## Azure App Service
gRPC is now supported on Azure App Service.
This is done by replacing the existing proxy with a YARP proxy that supports gRPC out of the box (built on dotnet).

# NativeAOT
Compiling C# to an AOT exe will lose features like dynamic code e.g. Reflection or Assembly loading.
It will however have a lower memory usage, faster startup time, and better native interopability

Information is interesting, but to hard to explain.

## Source

1. [Youtube Video](https://www.youtube.com/watch?v=AFDvMHETupA&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=52)

# Microservices
## Authentication / Authorization

Very interesting, but to hard to explain.

### Source

1. [Youtube Video](https://www.youtube.com/watch?v=DVqvRZ0w-7g&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=53)

### Important Reminders
#### Authorization Response
It is smart to return the permissions for the items available to the current user when returning the items you want to show.
![Authorization In Response](./Resources/Microservices/Auth/PermissionsInResponse.png)

#### Conclusion
![Authorization Conclusion](./Resources/Microservices/Auth/Conclusion.png)

#### Resources
[Authorization in a microservices world](https://www.alexanderlolis.com/authorization-in-a-microservices-world)

# Polyglot Notebooks
Rebranding of `.NET Interactive`.
Uses `.NET Interactive` as engine to run multiple different languages in the same interactive notebook.

## Input
It is possible to ask the user for input using the `@input:[store location]`. Store location is the location in which the data will be stored, kind of like a variable.
In the Visual Studio Code extension you can open the values of the Polyglot notebook and where the values are currently stored
![Current Values](./Resources/C%23/Interactive/CurrentValues.png)

## Nuget packages
Possible to use nuget packages, you need to install them first using the `#r "nuget: [package name]"` command.
![Nuget](./Resources/C%23/Interactive/Nuget.png)

## UI
Possible to show collections in a table like manner. To do this you need to create a command which ends with a collection and uses (for C#) `.ToTabularDataResource().Display();`
![Collection Table](./Resources/C%23/Interactive/CollectionTable.png)

## GitHub
Visualization for Interactive notebooks has been updated and are now supported on GitHub.
It does not support scrolling when you have not outlined your code well enough

## Dynamically Create Notebook Commands
It is possible to use the kernel and generate new notebook commands while executing a command.
The gif below generates a new `pie` command when running the `C#` command
![Dynamic Commands](./Resources/C%23/Interactive/DynamicCommands.gif)

# Infer#
Infer# is a tool to do static code analysis with reasoning to find potentional bugs and or security vulnerabilities.
Infer# will not only look at the code but also at the usages of this code on which it will base the warnings.
![Security Vulnerabilities](./Resources/Infer%23/SecurityVulnerabilities.png)

## Visual Studio
Infer# has an `Visual Studio` and `Visual Studio Code` extension which enables you to run the Infer# analysis from your visual studio
![Visual Studio](./Resources/Infer%23/VisualStudio.png)
![Errors and Warnings](./Resources/Infer%23/Analysis.png)

## Custom Rules
It is possible to modify the `.inferconfig` and create custom rules which are then used when running the analysis.

## DevOps Integration
Infer# has DevOps integration and can be used together with things like GitHub Actions

# ML.NET
## TorchSharp
`TorchSharp` is a .NET library that provides access to the library that powers `PyTorch`
![TorchSharp](./Resources/MachineLearning/TensorFlowNET.png)

## TensorFlow
You can also use `TensorFlow` in C# via `TensorFlow.NET`. TensorFlow.NET has great support for every environment.
![TensorFlow.NET](./Resources/MachineLearning/TensorFlowNET.png)

## NER & Question Answering
Using the `Named-entity Recognition` feature in ML.NET 2.0 allows for a question answering based on a given context.
![Question Answering](./Resources/MachineLearning/NerAndQuestionAnswering.png)

## Object Detection
Object detection is on the roadmap of ML.NET and will use a given context to check for objects.
![Computer Vision](./Resources/MachineLearning/ComputerVision.png)

# T4
T4 or TT files are templates for creating files mixed with C#.
You can compare it to `Razor` files that use C# to conditionally render HTML.
![Text Template Transformation Toolkit Example](./Resources/TextGeneration/TemplateWithOutputText.png)

## Power Tools
Using the `EF Core Power Tools` extension you can reverse engineer an existing database.
These reverse engineered models can be turned into T4 templates.

## Entity Framework 7
Designed to be database first.
EF 7 has perpared a couple of examples which use the T4 templates for generating multiple database contexts and models.
Using the build in scaffold feature in Visual Studio will run the templates and generate the corresponding database contexts and models.

Create or modify the existing T4 files to suit your needs.

# CloudEvents
CloudEvents is an standardised format for sending and receiving events.

## Architecture
Using the following architecture will decouple the publisher and subscribers from the broker and introduce intermediate adapters / handlers to format the data in the CloudEvents format.
Examples of use cases:

1. You have a legacy publisher app that you don't want to change but you still want to use CloudEvents
2. Reduce the complexity of the handler as the handler only receives the usefull information for it
![Architecture](./Resources/Microservices/Events/ArchitecturePubSub.png)

# IOT
Meadow microcontrollers have full dotnet support which allows you to code your hardware components in dotnet 
![Tempature Board](./Resources/IOT/TempatureBoard.png)
![Code](./Resources/IOT/HardwareConnection.png)

# ComputeSharp
ComputeSharp lets you write C# code which gets converted to hlsl shaders for DirectX at compile time.
It has full support for all the hlsl features and even has intellisence
![Paint.NET](./Resources/ComputeSharp/PaintNET.png)
![Compute Shader](./Resources/ComputeSharp/ComputeShader.png)

## Performance
Using the GPU instead of the CPU can improve the performance for specific workloads.
The following image shows the possible gains in certain workloads
![CPU vs GPU](./Resources/ComputeSharp/PerfCpuVsGpu.png)

# Database
## EF 7
### Execute Extensions
Finally possible to `Update` and `Delete` records without first retrieving them via `Get`!!
This reduces the additional round trip of first retrieving the data and then working on it.

#### UpdateAsync
To update on the data you need to use the `ExecuteUpdateAsync` method on the non materialized dataset (not retrieved).
This method requires a parameter in which you specify what properties of the result model should be changed to what value.
This way you don't need to retrieve the data first to then change the data and send it back to the database.

![UpdateAsync](./Resources/Database/ExecuteAsync/Update.png)

#### DeleteAsync
![DeleteAsync](./Resources/Database/ExecuteAsync/Delete.png)

### Source

1. [Youtube Video](https://www.youtube.com/watch?v=1U02rnSaz9Q&list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn&index=67)

## Graph
Graph databases store their data in graphs. 
Graphs are basically vertexes with edges that link data to another.
Think of it as traversing in interests tree in which topics that are edges of a generialized vertex. Can be linked to me as edge because of my interests.
This way you can easier traverse the relation to edges.

![Graph Relations](./Resources/Database/Graph/GraphLink.png)

### Dropping Data
As graphs are linked to each other via edges, you only need to drop the vertexes which will in turn drop their edges.

#### Note
Not sure if this is Azure CosmosDB specific or not, but in this documenation I will talk in the context of Azure CosmosDB

# Source

1. [Playlist](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVlqu_V8EXUDDnPsYwemxjn)

# TODO
Missed sessions:

![Missing](./Resources/MissedSessions/Missing.png)