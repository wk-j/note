Set

```javascript
let x ={
  value: [
    {
      CustNumber: "000009H521"
    },
    {
      CustNumber: "000009H521"
    }
  ]
}

let u = Array.from(new Set(x.value.map(x => x.CustNumber)))
console.log(u)
```