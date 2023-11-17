- [Asp.Net](#aspnet)
  - [Middlewares](#middlewares)
    - [Antiforgery](#antiforgery)
    - [Keyed services](#keyed-services)
    - [Request timeouts](#request-timeouts)
    - [Short circuit](#short-circuit)
    - [Exception handlers](#exception-handlers)
  - [Hosted services](#hosted-services)
  - [Blazor](#blazor)
    - [Authentication and authorization](#authentication-and-authorization)
      - [Source](#source)
    - [Stream rendering](#stream-rendering)
    - [Static Server Side Rendering](#static-server-side-rendering)
    - [Enhanced navigation](#enhanced-navigation)
    - [Rendering mode](#rendering-mode)
- [Containers](#containers)
  - [Base image](#base-image)
  - [Chiseled image](#chiseled-image)
    - [Size difference](#size-difference)
- [.NET Aspire](#net-aspire)
  - [Deployment](#deployment)
- [Performance](#performance)
  - [Asp.NET](#aspnet-1)
    - [Request delegate generator (RDG)](#request-delegate-generator-rdg)
  - [Garbage collection](#garbage-collection)
    - [Dynamically adapting to application sizes (DATAS)](#dynamically-adapting-to-application-sizes-datas)
      - [Source](#source-1)
  - [Dynamic profile guided optimizations (PGO)](#dynamic-profile-guided-optimizations-pgo)
  - [SearchValues](#searchvalues)
- [C# language](#c-language)
  - [Aliases](#aliases)
  - [Primary constructors](#primary-constructors)
  - [Collection builders](#collection-builders)
    - [Spread operator](#spread-operator)
- [Entity Framework](#entity-framework)
  - [Json columns](#json-columns)
  - [Array of primitives](#array-of-primitives)
  - [Parameters stored in JSON values](#parameters-stored-in-json-values)
  - [MongoDB](#mongodb)
- [AI](#ai)
  - [Semantic kernal](#semantic-kernal)
- [OpenTelemetry](#opentelemetry)
  - [Logging](#logging)
- [Resilience](#resilience)
  - [Http client](#http-client)
- [Json](#json)
  - [Object creation handling](#object-creation-handling)
  - [Required property](#required-property)
  - [Unmapped json member handling](#unmapped-json-member-handling)
  - [Interface hierarchy](#interface-hierarchy)
- [Pattern matching](#pattern-matching)
  - [Switch expression](#switch-expression)
- [Runtime](#runtime)
  - [Native AOT (ahead of time) vs JIT (just in time) compilation](#native-aot-ahead-of-time-vs-jit-just-in-time-compilation)
    - [Advantages of AOT](#advantages-of-aot)
      - [Smaller apps](#smaller-apps)
      - [Faster startup](#faster-startup)
      - [Less memory use](#less-memory-use)
    - [How does AOT work](#how-does-aot-work)
    - [Impact of **not** having a JIT](#impact-of-not-having-a-jit)
    - [Other considerations](#other-considerations)
    - [Conclusion](#conclusion)
- [Development tunnels](#development-tunnels)
- [.NET MAUI](#net-maui)
- [NuGet](#nuget)
  - [Auditing](#auditing)
    - [Custom vulnerability](#custom-vulnerability)
  - [Conditional package updating](#conditional-package-updating)
  - [Package source mapping](#package-source-mapping)
    - [Automatically configure the source mapping](#automatically-configure-the-source-mapping)
    - [Disallow transitive source packages from different source](#disallow-transitive-source-packages-from-different-source)
- [TODO](#todo)
  - [1](#1)
    - [Source](#source-2)
  - [2](#2)
  - [3](#3)


# Asp.Net
## Middlewares
### Antiforgery
Anti forgery is now added as a possible middleware, this middleware is used to validate the tokens against forgery.
![Anti forgery](./Resources/AspNet/Middlewares/AntiForgery/AntiForgery.png)

### Keyed services
KeyedServices allow the possibility to have multiple different services injected under the same `Interface` while being injected in another collection. This collection is named, so you can retrieve the correct variant of that interface
![Keyed services](./Resources/AspNet/Middlewares/KeyedServices/KeyedServices.png)

### Request timeouts
It is now possible to configure a request timeout on the server side. This means that any request that takes longer than the configured timeout will be cancelled via setting the `CancellationToken` to cancelled. If the API correctly handles this. This configuration can be done per endpoint or endpoint group as well as be set as default policy for all endpoints. Furthermore it also supports disabling it for specific endpoints.
![Request timeouts](./Resources/AspNet/Middlewares/RequestTimeouts/RequestTimeouts.png)

### Short circuit
Configuring an endpoint as a short circuit endpoint will execute the api, but only do that and not add any overhead by logging the call.
![Short circuit](./Resources/AspNet/Middlewares/ShortCircuit/ShortCircuit.png)

### Exception handlers
Configuring exception handlers will ensure that when an exception is thrown by your application, the handler receives that exception before the connection is closed and it will decide how to handle the response.
The handler method returns `true` when it has responded to the request itself and the request has now completed and `false` when the default `UseExceptionHandler` should redirect the request to the error page.
![Configuring an exception handler](./Resources/AspNet/Middlewares/ExceptionHandler/ConfiguringTheHandlers.png)
![Custom exception handler](./Resources/AspNet/Middlewares/ExceptionHandler/CustomHandler.png)

## Hosted services
The new `IHostedLifecycleService` interface for more control over when the hosted service should run. This interface introduces the `Starting`, `Started`, `Stoping`,  and `Stopped` methods. This means the service can choose to run before the application started (e.g. when you need to migrate the database before the application can run) or choose to run a job after the application has started (e.g. just a background job that is not dependent on the application state). This improves startup time.
![IHostedLifecycleService](./Resources/AspNet/HostedServices/IHostedLifecycleService.png)

Also, as hosted services start in FIFO (first in first out) and stop in LIFO (last in first out) order and the startup of the application itself (`app.Run()`) is also done as an `HostedService` which is **always** appended as the last `HostedService` in the stack. It will mean that all the HostedServices have to be started before the application can be started in order. When you have HostedServices that take a while to run it will impact the whole startup time.
The reverse happens when the application stops. The application is configured (by default) to have a maximum stop time of 30 seconds which means that because the stopping is done in order and the application itself stops first. Any HostedService that takes a time chips away from this maximum stop time. This means that the last service might have only 2 seconds left to run or might not even run at all.
In .NET 8 it is possible to configuring the hosted services to be started / stopped concurrently. This can be done in the `HostOptions`.

Now possible to configure the `StartupTimeout` of the application, this will shut the application down if it does not start in the specified time.
This can be useful for situations where startup time is critical and you want to prevent regression or when some `HostedService` that is required for the app to run is actually taking up too much time which might indicate an issue.
![Concurrent hosted services](./Resources/AspNet/HostedServices/ConcurrentServices.png)

## Blazor
![Frontend development in blazor with .net 8](./Resources/AspNet/Blazor/FrontendDevelopmentInBlazor.png)

### Authentication and authorization
Blazor now has a dedicated component for showing authorized views. Using the `AuthorizeView` component you can specify that a user should be **authenticated and authorized** according to the policy/role configured. This can be configured via multiple ways via the `Authorize` attribute on your component/page or via the `AuthorizeView`:
![Authorize attribute](./Resources/AspNet/Blazor/Authorization/AuthorizeAttribute.png)
![Nested role requirement](./Resources/AspNet/Blazor/Authorization/NestedRoleRequirement.png)
![Nested policy requirement](./Resources/AspNet/Blazor/Authorization/NestedPolicyRequirement.png)

#### Source
[MSDN source](https://learn.microsoft.com/en-us/aspnet/core/blazor/security/?view=aspnetcore-8.0)

### Stream rendering
Stream rendering will allow a component to be set to loading which will render a temporary loading div.
After the loading is done, the component will be automatically rerendered with the new items. This can be done via adding: `@attribute [StreamRendering]` to your page. ![StreamRendering](./Resources/AspNet/Blazor/StreamRendering/StreamRendering.png)

Using stream rendering also allows the possibility to stream updates to the frontend. This means that you could have a long running task which adds part of the page each `5` seconds. Using stream rending it is possible to do run this page/component and get the frontend to update it's data each 5 seconds based on the new content available.

![Stream rendering with task](./Resources/AspNet/Blazor/StreamRendering/StreamRendingWithTask.png)
![Stream rendering gif](./Resources/AspNet/Blazor/StreamRendering/StreamRenderingGif.gif)

Using stream rendering is useful for the following reasons:
![Stream rendering use cases](./Resources/AspNet/Blazor/StreamRendering/StreamRenderingUseCases.png)

### Static Server Side Rendering
It is now possible to do traditional SSR (server side rendering) via the new static SSR project. 

Traditional SSR:
![Traditional SSR](./Resources/AspNet/Blazor/SSR/SSR.png)

With this new way of working it still possible to use `WebAssembly` or `Blazor Server (via websockets over SignalR)` per page or component to get the best of both worlds (in this case 3 worlds).
![Per page interactivity](./Resources/AspNet/Blazor/SSR/PerPageInteractivity.png)

### Enhanced navigation
With the new enhanced navigation features in .NET 8, any page change will now by default only the dom which has changed and only request the new page data by recognizing the existing data and only request what is not yet known. This results in a SPA-like responsiveness without needing a SPA.
Also, via the `data-permanent` attribute on a form it is possible to retain data across page navigation. Use case for this could be where you have a search bar which should retain it's search throughout all the pages. Normally when switching the page it would also lose the search data.
![Permanent data](./Resources/AspNet/Blazor/Navigation/DataPermanent.png)
![Enhanced navigation](./Resources/AspNet/Blazor/Navigation/EnhancedNavigation.png)

### Rendering mode
Using the rendering mode it is possible to specify which rendering mode should be used for the component. 

1. Choosing `Server` mode would create a websocket connection **only** for that page or component to render that component on the server. When leaving that page or component it will shut the websocket down. 
2. Choosing `WebAssembly` mode requires the component to live in the `.Client` project as everything in that project will be send to the client when working with your app.
3. Choosing `Auto` mode will run the component via `Server` mode for the first time and download the content via the `WebAssembly` on the background. The second time it requests the same page or component it will use the `WebAssembly` mode as it already has everything it needs.
   1. **Note**: this requires **both** the websocket and the component or page to be put in the `.Client` project.

![Interactive components](./Resources/AspNet/Blazor/RenderingMode/InteractiveComponents.png)
![Auto mode](./Resources/AspNet/Blazor/RenderingMode/AutoMode.png)
![Setting render mode via code](./Resources/AspNet/Blazor/RenderingMode/SettingRenderModeInCode.png)

# Containers
## Base image
The base image now **no** longer uses the `root user` to run the application.
This also means the base image now runs on port `8080` instead of `80`.
![Container Image Changes](./Resources/Containers/Images.png)
**Note**: It is still possible to run your commands (e.g. `interactive terminal (-it)`) as the `root user`. This way you can still execute the commands that require root access.
![Run as root user](./Resources/Containers/RootUser.png)

## Chiseled image
Chiseled images have been stripped of all features you would normally expect inside an linux based image (e.g. curl, touch, cat, apt-get / apt-update, etc...). This means that even if you run your command as the `root user`, the command will just not exist and will therefore fail. This is both good for security as it is for size of the image as it reduces the attack surface by having less possibilities.
![Missing feature](./Resources/Containers/Chiseled/ChiseledMissingFeature.png)

### Size difference
![Normal image size](./Resources/Containers/Chiseled/Size/BaseImageSize.png)
Ignore the `sdk` size as this is only relevant for building the app, not running the app. Also, the `whoami` is wrong as it is no longer `root`, but `app` starting .NET 8 ([like mentioned above](#base-image)).
![Chiseled image size](./Resources/Containers/Chiseled/Size/ChiseledSize.png)
When the app is AOT compiled the size is even more reduced:
![Chiseled AOT size](./Resources/Containers/Chiseled/Size/ChiseledAOTSize.png)

# .NET Aspire
Aspire.NET is an orchestrator which offers insights into other apps and provides an easy to use dashboard for looking into traces. The Aspire project is meant as a development tool and should therefore not be deployed to production itself.
![Aspire Dashboard](./Resources/Aspire/Dashboard.png).
The Aspire `AppHost` project can wire up other projects as dependencies which will create a private network in which each project can call each other under a name (like how this is done in `docker-compose`).

AppHost:
![Aspire AppHost](./Resources/Aspire/AppHostConfiguration.png)

Client configuration:
![Aspire client](./Resources/Aspire/ClientConfiguration.png)

## Deployment
The Aspire project is not meant to be deployed on it's own, however the Azure runtime has integrated knowledge about an Aspire project. Deploying the Aspire AppHost to Azure will run all the required dependencies via Azure `Container Apps`.

# Performance
## Asp.NET
### Request delegate generator (RDG)
Using request delegate generator will configure the app to use interceptors which will be generated at compile time via source generators to replace the **currently** only minimal api mappings like `MapPut`, `MapPost` with the optimized version which will improve the startup time for the application.
![RDG meaning](./Resources/Performance/RequestDelegateGenerator/Definition.png)
![RDG startup time](./Resources/Performance/RequestDelegateGenerator/StartupTime.png)

## Garbage collection
### Dynamically adapting to application sizes (DATAS)
DATAS is a new feature which enables the garbage collector to dynamically shrink the heap size depending on the load. Previously .NET always reserved a lot of memory when using the server garbage collection feature, this was in preparation to possible load it might receive. However when no such load comes it just has a lot of heap memory reserved doing nothing.

#### Source
[Medium blog explaining the details](https://maoni0.medium.com/dynamically-adapting-to-application-sizes-2d72fcb6f1ea)

## Dynamic profile guided optimizations (PGO)
On by default for .NET 8 🥳!
It will optimize it really quickly and only add the necessary instrumentation needed to keep track of the usage of the optimized code. This will allow the JITer to see patterns and optimize based on those patterns (if it considers it worthy to be optimized).

PGO can now also see and optimize based on happy flows for type hierarchy. It will look at the underlying type and if it is (almost) always the same type. It will then include the underlying type as the base call and only if it is not that type infer the actual type and call the method on that type. This reduces the need for type checking.

Setting `DOTNET_JitDisasmSummary=1` as environment variable (or by csproj config) will show the actual methods which are being compiled and when they are compiled. This also shows you the tier of which PGO the method is being compiled in.

![JIT dissassembly summary](./Resources/Performance/ProfileGuidedOptimizations/JitDisasmSummary.png)

Setting the `DOTNET_JitDisasm="[method name]"` where `[method name]` is replaced by the name of the method you want the assembly from will show you the compilation in assembly specific for the method you specified.

This also shows the tiered compilation so any recompilation will also be shown with the new assembly.
![JIT disassembly for method](./Resources/Performance/ProfileGuidedOptimizations/JitDisasm.png)

## SearchValues
Searching multiple characters inside a string via the `IndexOf` is optimized for a low amount of characters (e.g. searching for `a` or `b`), but not for an `x` amount of characters. Creating a SearchValues object with all these characters that need to be searched for will be accepted in the `IndexOf` (or others like, `LastIndexOf`) overloads and allow the `IndexOf` code to choose the most optimal way for searching based on the size of the search.
![SearchValues](./Resources/Performance/SearchValues/SearchValues.png)

# C# language
## Aliases
Now possible to specify he primitive type instead of the fully qualified namespace for a type. Example of this would be that you could now specify:
```csharp
using Grade = decimal; // Instead of `System.Decimal`
```

It is also possible to create an alias for a pointer:
```csharp
using unsafe Grade = decimal*;
```

And even specify a `ValueTuple` as an alias including the property names which was previously not possible:
```csharp
using Grade = (string Course, decimal Value); 
```

## Primary constructors
Primary constructors is a way to define parameters on a class which will be accessible inside that class. The primary constructor removes the boiler plate code needed in your class by defining a field for the dependencies and assigning them in the constructor. Instead you only define them at the class definition and reference them inside the class (as captured context).

It is even possible to pass along the parameters to the parent class you inherit from via calling that constructor in the hierarchy definition.

As all parameters inside the primary constructor are captured context they will be considered as normal parameters instead of a field reference. This means that you can do anything you would also be able to do on a parameter (e.g. setting the value). The C# design team is thinking about a readonly annotation, but for now this can only be done by creating a custom field inside the class. When assigning it the same name, the field will get priority when being called instead of the parameter (from the captured context).

![Primary constructors](./Resources/CSharpLanguage/PrimaryConstructors/PrimaryConstructors.png)
![Field over parameter](./Resources/CSharpLanguage/PrimaryConstructors/FieldOverParameter.png)

All the parameters in the primary constructor are required, so any new constructor needs to eventually call the primary constructor for that type.

## Collection builders
Starting C# 12 collections can be initialized by simply specifying the items via `[]`. The `[]` will use the `Create` method specified on the type it needs to create. For certain types like `List<T>` the compiler has deep understanding of it and it will generate the code required, but for custom collections it requires an attribute called: `CollectionBuilder`.
![Collection builder attribute](./Resources/CSharpLanguage/CollectionBuilders/CollectionBuilderAttribute.png)

Usage of this collection builder will look like the following:
![Collection initializers](./Resources/CSharpLanguage/CollectionBuilders/CollectionInitializers.png)

### Spread operator
It is possible to join a collection inside the defined collection builder via the `..` (spread operator). The compiler will find the best way to join those collections together and create a flatmapped collection.
![Spread operator](./Resources/CSharpLanguage/CollectionBuilders/SpreadOperator.png)

# Entity Framework
## Json columns
EF 8 supports all the LINQ queries on an JSON field even when that field which is stored has a nested property which is a collection. It is now possible to query even the nested collections via LINQ. Projections are also supported on nested JSON properties. This uses the `WITH` (for SQL Server) keyword to create a temporary table on which it projects the JSON properties that are being used.
![JSON properties](./Resources/Database/EntityFramework/JsonProperties.png)
![JSON nested collection with projection in code](./Resources/Database/EntityFramework/NestedJsonQueriesAndProjectionCode.png)
![JSON nested collection with projection in SQL](./Resources/Database/EntityFramework/NestedJsonQueriesAndProjectionSql.png)

## Array of primitives 
Most relational databases do not natively support array as a data type. This meant that having a collection of primitives would force you to have a work around (e.g. create a collections table and reference it).

Starting EF 8 it is now possible to map have this inside the same table. If the database does not support such type EF will create a JSON field and store the data in a JSON. As EF is responsible for this field it also has in depth knowledge of the type which is useful for retrieving it as it can easily parse to the correct type and do a query on it.
![Primitive collection stored](./Resources/Database/EntityFramework/PrimitiveCollection.png)
![Primitive collection model](./Resources/Database/EntityFramework/PrimitiveCollectionModel.png)
![Primitive collection query](./Resources/Database/EntityFramework/PrimitiveCollectionCode.png)
![Primitive collection sql](./Resources/Database/EntityFramework/PrimitiveCollectionSql.png)

## Parameters stored in JSON values
Databases typically cache execution plans for queries so when the same query is executed again it will not have to create a new execution plan.
The cached execution plan can only be used if the query is identical (excluding the parameters). When doing an `IN` operation on a collection field EF 7 added the query parameters inside the SQL query. EF 8 however puts the parameters inside an JSON array and just references the parameter inside the query. This way the database uses the native JSON operators to unpack the parameters before executing the query, however as the query is the same the database can now use the execution plan cache again!
![Plan cache query](./Resources/Database/EntityFramework/PlanCacheQuery.png)
![Plan cache json sql parameter](./Resources/Database/EntityFramework/PlanCacheJsonParameter.png) 

## MongoDB
There is a new MongoDB provider for EF!

# AI
## Semantic kernal
AI is generally hard to configure as there are a lot of steps involved with getting the data correctly (some simple steps required):
1. Generate chunks of text for as your input tokens
2. Get the embeddings for this text
3. Vectorize these embeddings and store them in a vector db
4. Get embeddings from the input text
5. Compare the embeddings vector in the database to get similarities.

Semantic kernel helps abstract these things away and provide you an API which does this for you. This API can then talk to the configured connectors behind the scenes (like Azure OpenAI). This simplifies the process.
![Semantic kernel](./Resources/AI/SemanticKernal/SemanticKernal.png)
![Copilot stack](./Resources//AI/SemanticKernal/CopilotStack.png)

# OpenTelemetry
## Logging
Instead of using the `ILogger.LogInformation` (or other `LogXxx` methods), you should use the `LoggerMessage` attribute which logs the correct statement for you without boxing the objects into an `object`. 
![LoggerMessage attribute](./Resources/OpenTelemetry/Logging/LoggerMessageAttribute.png)

# Resilience
## Http client
Using the `Microsoft.Extensions.Http.Resilience` will allow setting resilience configuration for the `Http clients` based on the underlying Polly package.
![Resilience handler](./Resources/Resilience/HttpClient/ResilienceHandler.png)
![Resilience handler 2](./Resources/Resilience/HttpClient/ResilienceHandler2.png)
It is also possible to set the default standards which is configured in the package, you can override these settings via the `Configure` method
![Standard resilience handler](./Resources/Resilience/HttpClient/StandardResilienceHandler.png)

When wanting to send the requests in parallel use `HedgingHandler`. Hedging will run the requests that are slow in parallel. **Note** this should only be used when the requests that are being send are idempotent.
![Hedging handler](./Resources/Resilience/HttpClient/HedgingHandler.png)
![Different strategies](./Resources/Resilience/HttpClient/DifferentStrategies.png)

The resilience handler also respects the `retry-after` header by default. This header is sent back by the server if the server has rate limiting configured (correctly). This can be turned off, if this is not the behaviour that you want.


The package has support for OpenTelemetry and will trace or log data that is relevant.

# Json
## Object creation handling
System.Text.Json does by default ignore the deserialization of properties that are readonly.
However if that property has a default value assigned to it which can be mutated, it can instead of assign the property with a new value take that value and populate it with the data. This can be done via the `JsonObjectCreationHandling` attribute.
![Creation handling](./Resources/Json/ObjectCreationHandling.png)
This attribute can also be moved to the source generator so this configuration is not tied to the object.
![Creation handling on source generator](./Resources/Json/ObjectCreationHandlingSourceGenerator.png)

## Required property
The `required` keyword for properties is finally enforced 🥳!

## Unmapped json member handling
Using the `JsonUnmappedMemberHandling` attribute it is possible to specify the behaviour requested for the deserialization around unmapped json members.
This means you can enforce the contract to be the same as the input and not accept unwanted properties.
![Json unmapped members handling](./Resources/Json/JsonUnmappedMembers.png)

## Interface hierarchy
Base hierarchy types will now be included in the serialization of an interface.
![Interface hierarchy](./Resources/Json/InterfaceHierarchy.png)

# Pattern matching
## Switch expression
**Note** the features below here were already available since `C# 9`, but unknown to me hence I wrote them down.

When using a switch expression it is possible to capture the default value in a variable via capturing it as `var [variable name]` instead of discarding it via `_`. 
**Note**: When capturing the default value as a variable in a switch expression the variable will always be nullable as the switch expression pattern matching also checks if the type is not `null`. This means that when it is `null` but of that type it will still go to the default clause which is the variable defined. Because of this, this variable is always nullable and should be used with nullability in mind.
![Switch expression default variable](./Resources/PatternMatching/SwitchExpression/DefaultVariable.png)

Also, when having a condition on a sub property which is nullable it will automatically check the nullability for you and not throw an exception.
![Subproperty nullable condition](./Resources/PatternMatching/SwitchExpression/NullableNestedProperty.png)

# Runtime
## Native AOT (ahead of time) vs JIT (just in time) compilation
### Advantages of AOT
Compiling to AOT has multiple advantages over JIT:
![Advantages of AOT](./Resources/runtime/CompilationProcess/AdvantagesOfAOT.png)
Explanation of the advantages over JIT:

#### Smaller apps
Compiling to the specific platform reduces the need of having code for all possible platforms and decide at runtime which code should be used.
Also, as there is no runtime anymore the compiler does not include the JIT code.
**Note**: Compiling a method AOT can also result in more code generated as it requires every possible outcome to be compiled compared to JIT which will decide what code should be used at runtime. This is complimented by the aggressive trimming process after it has compiled, this process will remove all code which will in theory never be used.
Trimming itself also has downsides so take these downsides in mind before choosing.
![Impact of trimming](./Resources/Runtime/CompilationProcess/ImpactOfTrimming.png)

#### Faster startup
As the app trims away all unnecessary code, it will require less startup time. Also, when running a JIT application the JITTer needs to startup on it's own before it can actually start the application.
Lastly because the code is already compiled to the platform it will run on it will simply start the code instead of first having to figure out how the application should start.

#### Less memory use
The JITTer reserves more memory for the application to easily expand, as well as the JITTer also being a process that is running which requires memory on its own.
This combined results in more memory usage than is required for the application.

### How does AOT work
![Explanation of AOT](./Resources/Runtime/CompilationProcess/ExplanationOfAOT.png)

### Impact of **not** having a JIT
![Impact of no JIT](./Resources/Runtime/CompilationProcess/ImpactOfNoJIT.png)
As the name suggests the JITTer will compile the code `just in time` this means that it can perform code optimizations and dynamic code generation.
As well as `Reflection`.

### Other considerations
![Other considerations](./Resources/Runtime/CompilationProcess/OtherConsiderations.png)

### Conclusion
It is a tradeoff. When running short-lived applications that will start a lot to do a quick task before shutting down, it might be worthwhile to compile to AOT.
However when you have code which continuously runs and has a lot of throughput it might be better to compile it to JIT as it can perform code optimizations (or tiered compilation (Dynamic PGO)) on hot paths. Also, when you need to use features such as `Reflection.Emit` you would have to go with JIT either way.
**Note**: `Expression.Compile` will work in AOT, but it will have reduced performance 

# Development tunnels
Hot reload is now possible for dev tunnels 🥳! This means that you don't need to redeploy your dev tunnel app each time you make changes to it.

# .NET MAUI
Using the new experimental `HybridWebView` it is possible to render static web assets (HTML, JS, CSS, etc) inside MAUI. This means you can cross develop on an app even in different languages and just add them to MAUI!
![HybridWebView](./Resources/MAUI/HybridWebView.png)

# NuGet
## Auditing
NuGet now audits packages for vulnerabilities. If a package has a vulnerability it will notify the developer that a package has a vulnerability inside it. It even shows the severity the vulnerability and how to remediate this vulnerability.
The report is also shown when restoring (or adding/removing) the packages via the cli.
![Vulnerability report](./Resources/NuGet/VulnerabilityReport.png)

### Custom vulnerability
Via the new vulnerability api it is possible to manually provide vulnerability information on your package. This means that any NuGet source will be able to show this information.
![Custom vulnerability](./Resources/NuGet/CustomVulnerabilityReport.png)

## Conditional package updating
From NuGet 6.8 it is possible to conditionally set the version of the package that your application relies on.
This means you have an application which targets multiple frameworks as well as have matching package targeting for each framework version.
![Conditional package updating](./Resources/NuGet/ConditionalPackageVersioning.png)

## Package source mapping
Package source mapping allows the package to be mapped to a specific source. This means that even if a package with the same name exists on another source it will not trust that package and retrieve the package from the correct source.
This is useful for security reasons as this prevents the possibility of an malicious user uploading a package with the same name as the package your application depends on while having included malicious code. Without this feature it is possible that the wrong source would be used. Only happens if another source was configured that also has this package e.g. the application has 2 sources configured:
1. A public source for public packages
2. A private source for internal packages

![Package source mapping](./Resources/NuGet/PackageSourceMapping.png)

### Automatically configure the source mapping
![Automatically set source mapping](./Resources/NuGet/AutomaticallySetSourceMapping.png)

### Disallow transitive source packages from different source
The global package folder now checks to see if the dependency of a package has previously already been installed (is it in the cache) and if it has been installed, if the cached variant is from the configured source. If not it will disallow that package.
![Disallow transitive package from different source](./Resources/NuGet/DisallowTransitivePackageDiffSource.png) 

# TODO
## 1
From this: ![TODO from 1](./Resources/Todo/TodoFrom1.png)
To this: ![TODO until 1](./Resources/Todo/TodoUntil1.png)

### Source
[Day 2 (includes all the missed sessions)](https://www.youtube.com/watch?v=vU-iZcxbDUk)

## 2
From this: ![TODO from 2](./Resources/Todo/TodoFrom2.png)

## 3
From this: ![TODO from 3](./Resources/Todo/TodoFrom3.png)
Until this: ![TODO until 3](./Resources/Todo/TodoUntil3.png)