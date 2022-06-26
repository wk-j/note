#json #jq

## ดึงข้อมที่อยู่ภายใน Json Array ด้วย jq

ตัวอย่าง Input

```json
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
```

ดึงเฉพาะ  `id` ที่อยู่ภายใต้ `data.content`

```
cat src/jq-array-element/input.json \
    | jq ".data | .[] | .content | .[] | .id"
```

Output

```
719114
719118
```