# forEach()

> 배열의 각 요소에 대해 `callback`을 실행합니다. <br/>
> 배열을 순회하므로 중간에 `break`문을 사용할 수 없습니다.

```javascript
array.forEach(callback(currentvalue[, index[, array]])[, thisArg])
```

```javascript
const animals = ["lion", "tiger"];

animals.forEach((animal) => {
  console.log(animal);
  // lion
  // tiger
});
```

# map()

> 배열의 각 요소에 대해 `callback`을 실행하고 실행결과를 **새 배열을 리턴**합니다.
> <br/>
> 배열을 순회하므로 중간에 `break`문을 사용할 수 없습니다.

```javascript
array.map(callback(currentValue[, index[, array]])[, thisArg])
```

```javascript
const animals = ["lion", "tiger"];

result = animals.map((animal) => {
  console.log(animal);
  // lion
  // tiger
});
console.log(result); // [undefined, undefined]
```
