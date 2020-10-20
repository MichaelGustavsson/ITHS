# Exempel på Azure Deployment av en JavaScript applikation

Applikationen består av en server del och en frontend del.
Server delen är en **.NET Core REST API** applikation och frontend delen är en **Angular** Application

.NET Core applikationen har endast ett syfte i denna demo. Att hantera Javascript applikationen (Angular) och skicka den till webbläsaren.

### Instruktioner steg för steg.

**Steg 1.** Sätt upp katalog struktur

I terminal eller konsol fönstret skapa en mapp för applikationen.

` mkdir CarSales `

Gå in i skapad katalog ` cd CarSales `

I katalogen kör vi ` git init ` för att initiera versionhantering av applikationen.

**Steg 2.** Skapa API applikationen

Nu skall vi skapa REST API applikationen med hjälp av .NET Core. För att detta skall fungera så måste .NET Core vara installerad på datorn.

Om inte så gå till [dotnet.microsoft](https://dotnet.microsoft.com/download). Välj senaste stabila(LTS) versionen som är tillgänglig, just nu vid skrivandets stund så är det 3.1. Välj operativsystem som används, i mitt fall macOS. Klicka på alternativet **Build Apps** och klicka på Download .NET Core SDK.

[![dotnet-core-download.png](https://i.postimg.cc/d3FRpCWN/dotnet-core-download.png)](https://postimg.cc/gXM66xb3)

Detta kan ta en stund att ladda ner och installera, men följ anvisningarna på skärmen.

När installationen är klar så är det dags att köra kommandot för att skapa ett REST API med .core.

I terminalen eller konsolfönstret se till att vi står i katalogen CarSales och kör följande kommando: `dotnet new sln`. Detta kommando kommer att skapa en solution fil. En solution fil är en Visual Studio fil som används för att hålla ihop olika .net core projekt.

När solution filen är skapad skriver vi följande kommande `dotnet new webapi -o API`. Flaggan -o(output) innebär att REST API projektet kommer att skapas i en egen katalog API.

När terminal eller konsol fönstret är klart och vi ser att det står **Restore succeded** så är vårt api färdigt.

Glöm inte att versionshantera! 

```
 git add .
 git commit -m "Created API projekt"
 
```

Vi kan nu prova att vårt API fungerar. Gå till katalogen API genom att skriva ` cd API `

Skriv nu följande kommando i terminalen ` dotnet run `.

[![dotnet-run.png](https://i.postimg.cc/nVTQpNMh/dotnet-run.png)](https://postimg.cc/9zRfB8G6)

Vi ser nu att api applikationen är uppe och kör. Öppna nu en webbläsare och skriv in följande i webbläsarens adress fält. ` https://localhost:5001/weatherforecast `

Om vi ser följande bild så har vi nu ett fungerande api som returnerar en array med json objekt.

[![Weather-Forecast.png](https://i.postimg.cc/TP8Kt6NC/Weather-Forecast.png)](https://postimg.cc/0zf5NLsw)

Vi kan nu gå tillbaka till terminal eller konsol fönstret och skriva in följande kommando `Ctrl+c ` för att stoppa vårt REST API.

Nu är det dags att skapa en klient applikation.

**Steg 3**

I detta steg skall vi skapa en klient applikation med hjälp av Angular. För att kunna göra det behöver vi använda verktyget angular cli om det inte är installerat öppna webbläsaren och gå till

[angular.cli](https://cli.angular.io/)


[![Angular-cli.png](https://i.postimg.cc/ryhzvWYd/Angular-cli.png)](https://postimg.cc/qg3kKtr0)

I terminal eller konsol fönstret skriv kommandot ` npm install -g @angular/cli ` och tryck på Enter. Kommandot kommer att installera angular cli verktyget globalt på vår dator.

Det tar en stund att installera verktyget men håll ut.

När installationen är klar se till att vi står i katalogen CarSales. Skriv in följande kommando ` ng new client ` detta kommando kommer att skapa en ny Angular applikation med namnet **client** 
i katalogen client. Vid frågan om vi vill ha *routing* svara ja, vid frågan om vilket stylesheet vi vill använda. Håller vi det enkelt och väljer *CSS*.

Själva installationen av applikation kan ta en stund beroende på vilken uppkoppling som används.

[![ng-new.png](https://i.postimg.cc/DwczPXsy/ng-new.png)](https://postimg.cc/21Vmz32P)

När väl installation är klar kan vi flytta oss till katalogen **client** och där skriva in följande kommando ´ ng serve -o ´, flaggan -o gör att när applikation är kompilerad så kommer standard
webbläsaren att öppnas och presentera vår nya fantastiska applikation!

[![ng-app.png](https://i.postimg.cc/xCXTQpZc/ng-app.png)](https://postimg.cc/tZHHtkpj)

Så nu har ett REST API och en klient applikation. Nu är det dags att koppla REST API projektet så att det kan presentera klient applikationen när vi anger REST API adressen i webbläsaren.

Men innan vi nu gör en push och commit på våra projekt skall vi gå in i API projektet och lägga till en ***.gitignore*** fil så vi slipper att spara undan kompilerad kod och dll filer i vårt repository.

Se till att stå i katalogen ***CarSales***. Där skriver vi nu kommandot ` code . ` för att öppna upp projektet i VS Code.

**Steg 3.**

Högerklicka på mappen API och välj skapa ny fil

[![VSCode-new-folder.png](https://i.postimg.cc/L5vyVvH3/VSCode-new-folder.png)](https://postimg.cc/hQzbDLQX)

Ge filen namnet ***.gitignore*** och öppna filen i editor fönstret.
skriv in *obj* och *bin* för att slippa versionshantera kompilerade filer.

Nu kan vi versionshantera våra projekt, antingen använd VS Code's git extension eller använd terminal fönstret och placera våra filer i git repository. 

För att få vårt API att hantera vår klient applikation så måste vi öppna filen ***startup.cs*** som finns i API projektets rot.

I editor fönstret leta efter metoden ***Configure*** och alldeles före app.UseEndpoints() anropet. Skriv in följande:

```
  app.UseDefaultFiles();
  app.UseStaticFiles();
  
```

Detta är för att normalt så returnerar ett API endast json eller xml via sina **endpoints**. Nu vill vi istället att vår index.html som finns i vårt klient projekt skall returneras. Detta är vad ***app.UseDefaultFiles()*** tillåter oss att göra. ***app.UseStaticFiles()*** tillåter oss att använda statiska filer som *.html, bilder samt css.

Nästa steg är att se till att när vi gör en *build* av vårt Angular klient projekt att de kompilerade filerna hamnar i mappen ***wwwroot*** i vårt API projekt.

Expandera vårt *client* projekt och öppna filen **angular.json** i editor fönstret.

[![angular-json.png](https://i.postimg.cc/pXksgPwV/angular-json.png)](https://postimg.cc/pphQjMV3)

Lokalisera egenskapen **outputPath** under **build** ändra "dist/client" till **"../API/wwwroot"**. Detta gör att våra kompilerade filer kommer att kopieras till wwwroot i API projektet när vi bygger klient applikationen.

[![angular-build-path.png](https://i.postimg.cc/65BHj811/angular-build-path.png)](https://postimg.cc/fkgjkRsx)

Nu är vi klara för att skapa en byggversion av vår klient applikation.

I terminal eller konsol fönstret gå in i katalogen *CarSales/client* och skriv följande kommando: ` ng build --prod ` och tryck Enter.

Nu skapas en produktion version av klient applikationen. När det är klart gå tillbaka till VS Code och expandera API projektet och nu har vi fått en katalog som heter *wwwroot*. Om vi expanderar wwwroot kan vi se våra kompilerade klient filer.

[![wwwroot.png](https://i.postimg.cc/HsJJC2KJ/wwwroot.png)](https://postimg.cc/F74Fyjhm)


**Steg 4.**
Nu ska vi testköra vår applikation, i terminal eller konsolfönstret navigera till *CarSales/API* katalogen.
Skriv in kommandot ` dotnet run ` för att starta vårt API. När API projektet körs öppna en webbläsare och ange följande adress i addressfältet **https://localhost:5001** och tryck Enter.

Woow!!!

[![klient-app-lokalt.png](https://i.postimg.cc/HnbkVZC3/klient-app-lokalt.png)](https://postimg.cc/D4yTNc0b)

Nu har vi skapat en klient applikation som är hanterad av vårt api.














