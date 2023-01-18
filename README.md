# CS_CreacionDeArcYdirectorios.NET-E2
Lectura y escritura en archivos

## **Lectura de datos de archivos**

Los archivos se leen a través del método `ReadAllText` de la clase `File`.

```csharp
File.ReadAllText($"stores{Path.DirectorySeparatorChar}201{Path.DirectorySeparatorChar}sales.json");
```

El objeto que se devuelve de `ReadAllText`
 es una cadena.

```json
{
  "total": 22385.32
}
```

## ****Análisis de datos en archivos****

Puede agregar el paquete *Json.NET*
 al proyecto mediante NuGet:

```bash
dotnet add package Newtonsoft.Json
```

Después, agregue `using Newtonsoft.Json`
 a la parte superior del archivo de clase:

```csharp
using Newtonsoft.Json;
```

Y use el método `JsonConvert.DeserializeObject`
:

```csharp
var salesJson = File.ReadAllText($"stores{Path.DirectorySeparatorChar}201{Path.DirectorySeparatorChar}sales.json");
var salesData = JsonConvert.DeserializeObject<SalesTotal>(salesJson);

Console.WriteLine(salesData.Total);

class SalesTotal
{
  public double Total { get; set; }
}
```

## ****Escritura de datos en archivos****

En el ejercicio anterior ha aprendido a escribir archivos; pero simplemente ha escrito uno vacío. Para escribir datos en un archivo, use el mismo método `WriteAllText`
, pero pase los datos que quiera escribir.

```csharp
var data = JsonConvert.DeserializeObject<SalesTotal>(salesJson);

File.WriteAllText($"salesTotalDir{Path.DirectorySeparatorChar}totals.txt", data.Total.ToString());

// totals.txt
// 22385.32
```

## ****Anexión de datos en archivos****

En el ejemplo anterior, el archivo se sobrescribe cada vez que se escribe en él. En ocasiones no es lo que le interesará y querrá anexar datos al archivo, no reemplazarlo por completo. Puede anexar datos con el método `File.AppendAllText`
. De forma predeterminada, `File.AppendAllText`
 creará el archivo si aún no existe.

```csharp
var data = JsonConvert.DeserializeObject<SalesTotal>(salesJson);

File.AppendAllText($"salesTotalDir{Path.DirectorySeparatorChar}totals.txt", $"{data.Total}{Environment.NewLine}");

// totals.txt
// 22385.32
// 22385.32
```
