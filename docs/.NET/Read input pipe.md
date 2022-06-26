## อ่านข้อมูลผ่าน Pipe (|)

Input.txt

```
Line1
Line2
```

Program.fsx

```fsharp
let builder = StringBuilder()
let mutable line = Console.ReadLine()

while not(isNull line)  do
  builder.AppendLine(line) |> ignore
  line <- Console.ReadLine()

let pipe = builder.ToString()
printfn "%s" pipe
```

Test

```
cat Input.txt | dotnet fsi Progrem.fsx
```

Output

```
Line1
Line2
```