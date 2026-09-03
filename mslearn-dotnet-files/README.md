# CSE 325 — W01 Assignment: Build .NET Applications with C#

This repository contains the code for the Week 01 assignment, covering the
Microsoft Learn "Build .NET Applications with C#" learning path.

## Projects

### `ContosoPizza/`
An ASP.NET Core Web API built with controllers, implementing full CRUD
operations (GET, POST, PUT, DELETE) for a pizza inventory using an
in-memory data store.

- `Models/Pizza.cs` — the Pizza data model
- `Services/PizzaService.cs` — in-memory data service (seeded with 3 pizzas:
  Classic Italian, Veggie, and Pepperoni)
- `Controllers/PizzaController.cs` — REST API controller with GET all,
  GET by id, POST, PUT, and DELETE actions
- `ContosoPizza.http` — sample requests for testing each endpoint

**Run it:**
```
cd ContosoPizza
dotnet run --launch-profile https
```
Then test endpoints via `ContosoPizza.http` or a browser at
`https://localhost:{PORT}/pizza`.

### `mslearn-dotnet-files/`
A .NET console app that searches a directory tree for `.json` sales files,
totals the sales, and generates two report files:
- `salesTotalDir/totals.txt` — running log of the grand total each time the
  program runs
- `salesTotalDir/salesSummary.txt` — a formatted sales summary report
  (custom addition for this assignment) showing the total sales and a
  per-file breakdown, built with `StringBuilder`

**Run it:**
```
cd mslearn-dotnet-files
dotnet run
```

## Notes

See `notes.md` in the repo root for assignment evidence: sample
request/response pairs with status codes for each pizza API operation, and
the sales summary report function code and output.

## Requirements

- .NET 8.0 SDK
- Visual Studio Code (recommended) with the C# extension
