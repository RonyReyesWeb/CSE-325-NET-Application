# W01 Assignment Notes — Build .NET Applications with C#

## 1. Web API with ASP.NET Core Controllers — Evidence

### Pizza list (existing content + additional record)

The `PizzaService` in-memory data store was seeded with an additional third
pizza (`Pepperoni`) beyond the two provided by the module (`Classic Italian`
and `Veggie`).

**GET all pizzas** — `GET {{ContosoPizza_HostAddress}}/pizza/`

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
  {
    "id": 1,
    "name": "Classic Italian",
    "isGlutenFree": false
  },
  {
    "id": 2,
    "name": "Veggie",
    "isGlutenFree": true
  },
  {
    "id": 3,
    "name": "Pepperoni",
    "isGlutenFree": false
  }
]
```

### CRUD operation evidence (request + response + status code)

**GET by id** — `GET {{ContosoPizza_HostAddress}}/pizza/3`

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
  "id": 3,
  "name": "Pepperoni",
  "isGlutenFree": false
}
```
Status: **200 OK**

---

**POST (create)** — `POST {{ContosoPizza_HostAddress}}/pizza/`

Request body:
```json
{
    "name": "Hawaiian",
    "isGlutenFree": false
}
```

Response:
```
HTTP/1.1 201 Created
Content-Type: application/json; charset=utf-8
Location: https://localhost:7056/Pizza/4

{
  "id": 4,
  "name": "Hawaiian",
  "isGlutenFree": false
}
```
Status: **201 Created**

---

**PUT (update)** — `PUT {{ContosoPizza_HostAddress}}/pizza/4`

Request body:
```json
{
    "id": 4,
    "name": "Hawaiian Deluxe",
    "isGlutenFree": false
}
```

Response:
```
HTTP/1.1 204 No Content
```
Status: **204 No Content**

---

**DELETE** — `DELETE {{ContosoPizza_HostAddress}}/pizza/4`

Response:
```
HTTP/1.1 204 No Content
```
Status: **204 No Content**

---

## 2. Sales Summary Report Function (Part 2)

Added to `Program.cs` in the `mslearn-dotnet-files` project, on top of the
finished "Work with files and directories" module code. `CalculateSalesTotal`
was extended to also track each file's individual total in a dictionary,
which `GenerateSalesSummaryReport` then uses to build the report with a
`StringBuilder`.

```csharp
using Newtonsoft.Json;
using System.Text;

var currentDirectory = Directory.GetCurrentDirectory();
var storesDirectory = Path.Combine(currentDirectory, "stores");

var salesTotalDir = Path.Combine(currentDirectory, "salesTotalDir");
Directory.CreateDirectory(salesTotalDir);

var salesFiles = FindFiles(storesDirectory);

var fileTotals = new Dictionary<string, double>();
var salesTotal = CalculateSalesTotal(salesFiles, fileTotals);

File.AppendAllText(Path.Combine(salesTotalDir, "totals.txt"), $"{salesTotal}{Environment.NewLine}");

GenerateSalesSummaryReport(Path.Combine(salesTotalDir, "salesSummary.txt"), salesTotal, fileTotals);

Console.WriteLine("Sales summary report generated.");

IEnumerable<string> FindFiles(string folderName)
{
    List<string> salesFiles = new List<string>();

    var foundFiles = Directory.EnumerateFiles(folderName, "*", SearchOption.AllDirectories);

    foreach (var file in foundFiles)
    {
        var extension = Path.GetExtension(file);
        if (extension == ".json")
        {
            salesFiles.Add(file);
        }
    }

    return salesFiles;
}

double CalculateSalesTotal(IEnumerable<string> salesFiles, Dictionary<string, double> fileTotals)
{
    double salesTotal = 0;

    foreach (var file in salesFiles)
    {
        string salesJson = File.ReadAllText(file);

        SalesData? data = JsonConvert.DeserializeObject<SalesData?>(salesJson);

        double fileTotal = data?.Total ?? 0;

        // Use the store folder name + file name so files with the
        // same name (sales.json) in different stores stay distinct
        string label = $"{Path.GetFileName(Path.GetDirectoryName(file))}/{Path.GetFileName(file)}";

        fileTotals[label] = fileTotal;
        salesTotal += fileTotal;
    }

    return salesTotal;
}

void GenerateSalesSummaryReport(string reportPath, double totalSales, Dictionary<string, double> fileTotals)
{
    var report = new StringBuilder();

    report.AppendLine("Sales Summary");
    report.AppendLine("----------------------------");
    report.AppendLine($" Total Sales: {totalSales:C}");
    report.AppendLine();
    report.AppendLine(" Details:");

    foreach (var entry in fileTotals)
    {
        report.AppendLine($"  {entry.Key}: {entry.Value:C}");
    }

    File.WriteAllText(reportPath, report.ToString());
}

record SalesData(double Total);
```

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
