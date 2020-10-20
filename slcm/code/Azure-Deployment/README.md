# Exempel på Azure Deployment av en JavaScript applikation

Applikationen består av en server del och en frontend del.
Server delen är en **.NET Core REST API** applikation och frontend delen är en **Angular** Application

.NET Core applikationen har endast ett syfte i denna demo. Att hantera Javascript applikationen (Angular) och skicka den till webbläsaren.

### Instruktioner steg för steg.

**Steg 1.** Sätt upp katalog struktur

I terminal eller konsol fönstret skapa en mapp för applikationen.

`mkdir CarSales`

Gå in i skapad katalog `cd CarSales`

I katalogen kör vi `git init` för att initiera versionhantering av applikationen.

**Steg 2.** Skapa API applikationen

Nu skall vi skapa REST API applikationen med hjälp av .NET Core. För att detta skall fungera så måste .NET Core vara installerad på datorn.

Om inte så gå till [dotnet.microsoft](https://dotnet.microsoft.com/download). Välj senaste stabila(LTS) versionen som är tillgänglig, just nu vid skrivandets stund så är det 3.1. Välj operativsystem som används, i mitt fall macOS. Klicka på alternativet **Build Apps** och klicka på Download .NET Core SDK.

[![dotnet-core-download.png](https://i.postimg.cc/d3FRpCWN/dotnet-core-download.png)](https://postimg.cc/gXM66xb3)

Detta kan ta en stund att ladda ner och installera, men följ anvisningarna på skärmen.

När installationen är klar så är det dags att köra kommandot för att skapa ett REST API med .core.

I terminalen eller konsolfönstret se till att vi står i katalogen CarSales och kör följande kommando: `dotnet sln`. Detta kommando kommer att skapa en solution fil. En solution fil är en Visual Studio fil som används för att hålla ihop olika .net core projekt.

När solution filen är skapad skriver vi följande kommande `dotnet new webapi -o API`. Detta kommer att skapa ett REST API projekt i katalogen API.