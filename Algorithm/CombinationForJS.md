# Combination

> 서로 다른 `n`개의 물건에서 순서를 생각하지 않고 `r`개를 택할 때, 이것은 `n`개에서 `r`개를 택하는 조합이라 하고, 이 조합의 수를 기호로 `nCr`와 같이 나타낸다.
> 바로 예를 살펴보도록 하자. `4Combination3 = 4C3`을 코드로 구현한다면 다음과 같은 인풋과 아웃풋을 가지게 된다.

## Example

```
Input: [1, 2, 3, 4]
Output: [ [1, 2, 3], [1, 2, 4], [1, 3, 4], [2, 3, 4] ]
```

## Pseudo Code

배열의 처음부터 하나씩 선택(고정)하면서 뒤의 나머지의 배열에 대해서 조합을 구해서 붙이면 되는 것이다. 이렇게 나머지에 대해서 일을 위임할 때에는 재귀(Recursion)함수를 사용하는 것이 좋다! 왜냐하면 계속해서 반복 될 일(조합을 구하는 코드)에 대해서 한번만 명시 해 놓고, 들어가는 인자(나를 뺀 나머지)를 바꾸어 주기만 하면 되기 때문이다.

```
시작
  1을 선택(고정)하고 -> 나머지 [2, 3, 4] 중에서 2개씩 조합을 구한다.
  [1, 2, 3] [1, 2, 4] [1, 3, 4]
  2를 선택(고정)하고 -> 나머지 [3, 4] 중에서 2개씩 조합을 구한다.
  [2, 3, 4]
  3을 선택(고정)하고 -> 나머지 [4] 중에서 2개씩 조합을 구한다.
  []
  4을 선택(고정)하고 -> 나머지 [] 중에서 2개씩 조합을 구한다.
  []
종료
```

## Code

```javascript
const getCombinations = function (arr, selectNumber) {
  const results = [];
  if (selectNumber === 1) return arr.map((el) => [el]);
  // n개중에서 1개 선택할 때(nC1), 바로 모든 배열의 원소 return

  arr.forEach((fixed, index, origin) => {
    const rest = origin.slice(index + 1);
    // 해당하는 fixed를 제외한 나머지 뒤
    const combinations = getCombinations(rest, selectNumber - 1);
    // 나머지에 대해서 조합을 구한다.
    const attached = combinations.map((el) => [fixed, ...el]);
    //  돌아온 조합에 떼 놓은(fixed) 값 붙이기
    results.push(...attached);
    // 배열 spread syntax 로 모두다 push
  });

  return results; // 결과 담긴 results return
};
```
