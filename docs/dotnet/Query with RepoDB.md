#repodb  #mysql

Query with field operation

```fsharp
#r "nuget: RepoDb.MySQL"

open MySql.Data.MySqlClient
open RepoDb
open RepoDb.Attributes
open RepoDb.Enumerations

RepoDb.MySqlBootstrap.Initialize()

[<Map("OR_DX_BANK")>]
type Bank = {
    Id: int
    Name: string
}

let connectionString = "Host=;User=alfresco;Password=;Database=alfresco"
let connection = new MySqlConnection(connectionString)

// let x = connection.Query<Bank>({| Id = 10 |})
let x = connection.Query<Bank>(QueryField("Id", Operation.GreaterThan, 0))
for item in x do
    printfn "%i %s" item.Id item.Name
```

Query with LINQ

```fsharp

#r "nuget: RepoDb.MySQL"
#load "ConnectionString.fsx"

open MySql.Data.MySqlClient
open RepoDb
open RepoDb.Attributes
open RepoDb.Enumerations
open ConnectionString
open System.Linq

RepoDb.MySqlBootstrap.Initialize()

[<Map("IDOC_EMPLOYEE_DATA")>]
type Employee = {
    [<Map("CODE")>]
    Code: int

    [<Map("FNAME")>]
    FName : string

    [<Map("LNAME")>]
    LName: string
}

let connection = new MySqlConnection(Env.Uat)

let codes = [|
    610001
    610006
    610019
    610050
|]

let x = connection.Query<Employee>(fun x -> codes.Contains(x.Code))

for item in x do
    printfn "%s %s" item.FName item.LName
```