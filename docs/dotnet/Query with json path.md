#json

## Query array elements with Json Path

```fsharp
#r "nuget: Newtonsoft.Json"

open Newtonsoft.Json
open Newtonsoft.Json.Linq

let json = """
{
    "data": [
        {
            "content": [
                {
                    "id": 719114
                }
            ],
            "field": {
                "id": "stationLayout",
                "name": "ผังบริเวณสถานีบริการ (ระบุตำแหน่งร้าน)"
            }
        },
        {
            "content": [
                {
                    "id": 719118
                }
            ],
            "field": {
                "id": "gd2PDF",
                "name": "อัปโหลดเอกสารสัญญาเช่าพื้นที่และอาคารในสถานีบริการ (PDF)"
            }
        }
    ]
}
"""

let obj = JObject.Parse(json)
let token = obj.SelectTokens("$.data[*].content[*].id")

for item in token do
    printfn "Id = %s" (item.ToString())
```

Output

```
Id = 719114
Id = 719118
```