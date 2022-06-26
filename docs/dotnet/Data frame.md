## Data frame

Install

```bash
dotnet intall Microsoft.Data.Analysis
```

Usage

```csharp
using Microsoft.Data.Analysis;

var frame = DataFrame.LoadCsv("input.csv", ',', header: true);
```

Issue

- Not support quoted string contains `,`