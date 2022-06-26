## Upload .7z file

```
POST https://xyz.com/alfresco/api/-default-/public/alfresco/versions/1/nodes/-root-/children
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW
Authorization: Basic admin admin

------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="ERC:DocType"

Hello, world
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="relativePath"

x/y/z
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="autoRename"

false
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="fileData"; filename="XYZ.7z"
Content-Type: application/x-7z-compressed

< resource/Interactive_travel_sample.7z
------WebKitFormBoundary7MA4YWxkTrZu0gW--
```

Alfresco not include `mimeTypeName` in reponse body, here are diffrence between `.md` and `.7z`

## Markdown

```json
HTTP/1.1 201 Created
Server: nginx
Date: Wed, 27 Jan 2021 08:42:11 GMT
Content-Type: application/json;charset=UTF-8
Transfer-Encoding: chunked
Connection: close
Cache-Control: no-cache
Expires: Thu, 01 Jan 1970 00:00:00 GMT
Pragma: no-cache

{
  "entry": {
    "isFile": true,
    "createdByUser": {
      "id": "admin",
      "displayName": "Administrator"
    },
    "modifiedAt": "2021-01-27T08:42:09.904+0000",
    "nodeType": "cm:content",
    "content": {
      "mimeType": "text/x-markdown",
      "mimeTypeName": "Markdown",
      "sizeInBytes": 239,
      "encoding": "UTF-8"
    },
    "parentId": "272fa3c7-e5cd-4748-963e-197a1c7b1be6",
    "aspectNames": [
      "cm:versionable",
      "cm:auditable",
      "ERC:DocType"
    ],
    "createdAt": "2021-01-27T08:42:06.000+0000",
    "isFolder": false,
    "modifiedByUser": {
      "id": "admin",
      "displayName": "Administrator"
    },
    "name": "CMD.md",
    "id": "3b32c88f-870a-4d5d-9330-e19f4f60b740",
    "properties": {
      "cm:versionLabel": "1.0",
      "ERC:DocType": "Hello, world",
      "cm:versionType": "MAJOR"
    }
  }
}

```

## 7z

```json
HTTP/1.1 201 Created
Server: nginx
Date: Wed, 27 Jan 2021 08:50:38 GMT
Content-Type: application/json;charset=UTF-8
Transfer-Encoding: chunked
Connection: close
Cache-Control: no-cache
Expires: Thu, 01 Jan 1970 00:00:00 GMT
Pragma: no-cache

{
  "entry": {
    "isFile": true,
    "createdByUser": {
      "id": "admin",
      "displayName": "Administrator"
    },
    "modifiedAt": "2021-01-27T08:50:37.217+0000",
    "nodeType": "cm:content",
    "content": {
      "mimeType": "application/x-7z-compressed",
      "sizeInBytes": 1209149,
      "encoding": "UTF-8"
    },
    "parentId": "272fa3c7-e5cd-4748-963e-197a1c7b1be6",
    "aspectNames": [
      "cm:versionable",
      "cm:auditable",
      "ERC:DocType"
    ],
    "createdAt": "2021-01-27T08:50:37.217+0000",
    "isFolder": false,
    "modifiedByUser": {
      "id": "admin",
      "displayName": "Administrator"
    },
    "name": "XYZ.7z",
    "id": "5616b0ea-8d46-42e7-b967-67df4cea04e7",
    "properties": {
      "cm:versionLabel": "1.0",
      "ERC:DocType": "Hello, world",
      "cm:versionType": "MAJOR"
    }
  }
}
```