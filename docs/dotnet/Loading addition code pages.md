## Register  code pages

```fsharp
#r "nuget: System.Text.Encoding.CodePages"

open System.Text
Encoding.RegisterProvider(CodePagesEncodingProvider.Instance)
```
