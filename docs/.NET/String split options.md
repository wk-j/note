Options

```fsharp
open System
open type System.StringSplitOptions

let input = "a [stop] b [stop] c [stop]"

let split (spliter:string) o =
    let x = input.Split(spliter, o)
    printfn "%A" x

split "[stop]" StringSplitOptions.None
split "[stop]" StringSplitOptions.RemoveEmptyEntries
split "[stop]" StringSplitOptions.TrimEntries
split "[stop]" (TrimEntries ||| RemoveEmptyEntries)
```