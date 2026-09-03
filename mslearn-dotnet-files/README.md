# CSE 325 — W01 Assignment: Build .NET Applications with C#

This repository contains the code for the Week 01 assignment, covering the
Microsoft Learn "Build .NET Applications with C#" learning path.

## Project

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


## 2. Sales Summary Report Function

### Sample output — `salesTotalDir/salesSummary.txt`

```
Sales Summary
----------------------------
 Total Sales: $xx,xxx.xx

 Details:
  stores/sales.json: $x,xxx.xx
  201/sales.json: $x,xxx.xx
  202/sales.json: $x,xxx.xx
  203/sales.json: $x,xxx.xx
  204/sales.json: $x,xxx.xx
```
*(Replace the sample values above with the actual numbers from your generated `salesSummary.txt` file.)*

