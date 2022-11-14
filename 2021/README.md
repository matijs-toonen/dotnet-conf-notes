- [Warning](#warning)
- [.Net 6 conf 2021 notes](#net-6-conf-2021-notes)
- [Source](#source)

# Warning
The following notes have been taken in 2021 in which I did not have a structure on how I would document the dotnet conf.
From 2022 and onwards, these notes will be taken in the defined structure and in proper english.
But for now these notes will stay the same in plain old Dutch.

I have added the source playlist, but will not modify the content of these notes as I do not see the advantage of doing so.

# .Net 6 conf 2021 notes
* Repo Source:
    * https://github.com/dotnet-presentations/dotNETConf
* Windows subsystem for android
    * Soort emulator, maar kan geen google playstore api's gebruiken
    * Moet windows 11 voor geinstalleerd zijn
* Minimal api's
    * Mogelijke dependency injection via `AddSingletonInstance`
* Podcast repository zal opensource komen (url nog niet gevonden)
* C# 10
    * Usings 
        * Implicit usings
        * Global usings (`global` keyword gebruiken is genoeg)
    * With keyword voor alles niet alleen records
    * Parameterless struct constructors
        * Geeft ander resultaat dan `default`
    * Lambdas
        * `Ref` parameters in funcs (delegates als `var` getyped)
            * e.g. `var parse = (ref string input) => int.Parse(input);`
        * `Attributes` op lambda
            * e.g. `var parse = [Obsolete] (string input) => int.Parse(input);`
        * aangeven welk `return` type een `var lambda` moet zijn
            * e.g. `var parse = object (bool b) => b ? 1 : "two";` 
            * ^ heeft 2 verschillende return types waardoor het niet duidelijk is voor de compiler
            * opgelost door het return type `object` te typen voor de input variabel
        * `Method groups` in combinatie met `var`
            * e.g. `var read = Console.Read`
            * ^ met meerdere overloads kan de compiler niet werken
                * e.g. `var write = Console.Write` (heeft 16 overloads)
* Blazor
    * `SupplyParameterFromQuery` op een parameter -> `@inject NavigationManager NavigationManager`
        * `var address = NavigationManager.GetUriWithQueryParameter(nameof(StartDate), startDate)`
        * `NavigationManager.NavigateTo(address)`
    * Mogelijk om `blazor components` te maken en te gebruiken in `javascript` (voor migration)
    * `.NET webassembly build tools` downloaden via de `visual studio installer` voor kleinere publish output
    * `Blazor Fluent UI Components` zijn components van microsoft
    * JS initializers kun je schrijven door een `filename.lib.js` te maken met de `beforeStart` en `afterStarted`
        * `export function beforeStart(options) {}`
    * Testing
        * BUnit is een unit test framework voor front end blazor
* Tests
    * UI
        * Bunit unit test framework voor front end blazor
        * Playwright is een tool om integratie tests te maken, de app opened en jij record de stappen
    * mutent testing
    * concurrency testing
        * coyote
* Minimal Apis
    * [FromBody] 
    * [FromServices] => wordt gezien als dependency injection als die bestaat en is dus overbodig
    * `HttpResponse` / `HttpContext` / enz zijn speciale types en worden ook als dependency injection toegevoegd
* Tools
    * HttpRepl kun je in command line requests makkelijk uitvoeren
        * Source: https://github.com/dotnet/HttpRepl
* Maui
    * Podcast app is een blazor app als dependency in de xaml blazor webview
    * Meerder mogelijke design keuzes via Microsoft.Maui.Graphics.Controls (is experimental):
        * Fluent
        * Material
        * Cupertino
    * Controls zijn volledig overrideable inclusief custom drawing
* Interactive Notebook C# dotnet interactive book (.dib)
    * Source: https://github.com/dotnet/interactive
* Webassembly
    * Mogelijk om native dlls te importeren door de `NativeFileReference` in de csproj
    * ^ om een dll van rust te gebruiken via de `extern` keyword
* ML.NET
    * Machine learning in .net
    * 20 secondes laten leren kan al accuraat zijn
* Diagnostics
    * OpenTelementry -> niet vendor specifiek
        * `System.Runtime.Metrics` vervanger van `EventCounters`
        * Mogelijk om te configureren voor minimal api
            * Kan geconfigureerd worden voor alle `sql queries` zonder de db context aan te raken
            * Kan geconfigureerd worden voor alle `http requests` zonder de db context aan te raken
            * Zipkin erg goede telementry exporter
            * Meterics
                * Zipkin kan niet werken met metrics
                * Prometheus kan metrics laten zien
                * `var meter = new Meter("ComputerVision")`
                * `meter.CreateCounter<long>("PayloadCounter, "bytes")`;
                * `meter.CreateHistogram<double>("ConfidenceHistogram");`
    * `dotnet monitor`
* gRPC
    * Client side load balancing using a discovery dns (kubernetes heeft een discovery dns voor pods die hiervoor gebruikt kan worden)
    * Mogelijk om retry policy te configureren
    * Http 3 wordt ondersteunt
        * Resource docs: https://aka.ms/grpcdocs
        * Example docs:  https://aka.ms/grpcexamples
* Kubernetes
    * Helm
        * versimplen van kubernetes configuraties
    * Dapr
        * versimplen van kubernetes infrastructuur voor de ontwikkelaar
* Azure
    * Azure containers
        * Is om containers te publishen met kubernetes zonder kubernetes zelf te hoeven hosten
    * Azure B2C (Business to customer)
        * Free tot 50.000 users
        * Blazor Azure B2C Authentication and Authorization - Michael Washington
    * Azure config kun je gebruiken samen met Feature Management
* Benchmarks
    * Crank
        * Kan PR changes benchmarken
        * Custom load generators and measurements
            * SignalR, WebSockets, gRPC, H2, H3, ...
        * mogelijk om een dotnet trace te maken die je in visual studio kan proberen
* Github
    * Actions
        * Action-mate
        * Act
        * Playwrite testing automatiseren
* Feature Management
    * kun je apis mee beschermen wanneer een feature niet aan staat
    * Kun je laten pollen, zodat je at runtime een feature kan uit zetten
        * Kan handmatig
        * Kan op basis van datum / tijd
    * Kan laten werken via Azure config
* Database
    * Oqtane is een ORM zoals EF Core, maar support meerdere databases

# Source
[Playlist](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVFtp9MDEBNbA2sSqYvXSXO)