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
Vi skapar även två ny kataloger i katalogen,
```
mkdir API
mkdir client
```

**Steg 2.** Skapa API applikationen

Nu skall vi skapa REST API applikationen med hjälp av .NET Core. För att detta skall fungera så måste .NET Core vara installerad på datorn.

Om inte så gå till länken [dotnet.microsoft](https://dotnet.microsoft.com/download)

