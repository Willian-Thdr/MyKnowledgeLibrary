# Convertendo Json

## Converter Json para uma string

```
using System.Text.Json;

// JSON
string json = """
{
    "thisVersion": "1.0",
    "actualVersion": "1.1",
    "author": "Willian"
}
""";

// Ler o JSON
JsonDocument document = JsonDocument.Parse(json);

// Pegar informações específicas
string thisVersion = document.RootElement
    .GetProperty("thisVersion")
    .GetString()!;

string actualVersion = document.RootElement
    .GetProperty("actualVersion")
    .GetString()!;

Console.WriteLine(thisVersion);
Console.WriteLine(actualVersion);
```

## Para API podemos usar isto

```
using System.Net.Http;
using System.Text.Json;

using HttpClient client = new();

string json = await client.GetStringAsync("URL_DO_JSON");

JsonDocument document = JsonDocument.Parse(json);

string version = document.RootElement
    .GetProperty("tag_name")
    .GetString()!;

Console.WriteLine(version);
```

## Nota

> Em todo o caso que quisermos ler um arquivo ou dado json e transferir para a string, para não escrevermos o formato do arquivo numa variável, podemos indicar o local do arquivo usando File, Path e Directory. E então usar a extensão de variável .ReadAllLines ou ReadToEnd. Assim a string terá toda a estrutura do Json.