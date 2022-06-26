#ropo-db

## Batch update

```fsharp
#r "nuget: RepoDb.MySQL"
#load "ConnectionString.fsx"

MySqlBootstrap.Initialize()

open MySql.Data.MySqlClient
open RepoDb
open RepoDb.Attributes
open ConnectionString

[<Map("XUSER")>]
type User = {
    UserName: string
    FirstName: string
}

let connection = new MySqlConnection(Env.Hello)

let data = [|
    {  UserName = "u1"; FirstName = "F1" }
    {  UserName = "u2"; FirstName = "F2" }
    {  UserName = "u3"; FirstName = "F3" }
|]

let c = connection.UpdateAll(data, batchSize = 100)
printfn "Commit = %i" c
```