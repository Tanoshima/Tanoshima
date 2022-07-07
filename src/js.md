## [ 0, 1, 2, 3, 4 ]のような連番を生成

```
[...Array(5)].map((_, i) => i) //=> [ 0, 1, 2, 3, 4 ]
[...Array(5)].map((_, i) => i + 1) //=> [ 1, 2, 3, 4, 5 ]
```

## {} の空判定

```
  const obj = {}
  console.log(obj === {})
  // => false

  const isEmpty = (o: object) => {
    return Object.keys(o).length === 0
  }
  console.log(isEmpty({}))
  // => true
```
