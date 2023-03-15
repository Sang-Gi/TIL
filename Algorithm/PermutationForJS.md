# Permutation
> 서로 다른 `n`개의 물건 중에서 `r`개를 택하여 한 줄로 배열하는 것을 `n`개의 물건에서 `r`개 택하는 순열이라 하고, 이 순열의 수를 기호로 `nPr`와 같이 나타낸다. 조합은 순서에 상관없이 선택한 것이라면, **순열은 순서가 중요하다.** 실제로 순열을 구하는 공식도 조합으로부터 도출 가능하다.

## Example
```
Input: [1, 2, 3, 4] 
Output: [
    [ 1, 2, 3 ], [ 1, 2, 4 ],
    [ 1, 3, 2 ], [ 1, 3, 4 ],
    [ 1, 4, 2 ], [ 1, 4, 3 ],
    [ 2, 1, 3 ], [ 2, 1, 4 ],
    [ 2, 3, 1 ], [ 2, 3, 4 ],
    [ 2, 4, 1 ], [ 2, 4, 3 ],
    [ 3, 1, 2 ], [ 3, 1, 4 ],
    [ 3, 2, 1 ], [ 3, 2, 4 ],
    [ 3, 4, 1 ], [ 3, 4, 2 ],
    [ 4, 1, 2 ], [ 4, 1, 3 ],
    [ 4, 2, 1 ], [ 4, 2, 3 ],
    [ 4, 3, 1 ], [ 4, 3, 2 ] 
  ]
```
## Pseudo Code
먼저, 재귀의 종료 조건은 조합을 구하는 함수와 동일하다. 왜냐하면, **한 개씩 선택한다고 하면 순서가 의미가 없어지기 때문이다.**

`[1,2,3,4]` 에서 3개를 선택해서 순열을 만드는 코드의 내부를 의사코드로 적어보면 다음과 같다.
1, 2, 3, 4를 각각 순서대로 픽스하고 나머지 요소만으로 이루어진 배열에서 `seletNumber - 1`만큼을 선택하여 또 순열을 구한다. (재귀)

## Code
```javascript
const getPermutations = function (arr, selectNumber) {
    const results = [];
    if (selectNumber === 1) return arr.map((el) => [el]); 
    // n개중에서 1개 선택할 때(nP1), 바로 모든 배열의 원소 return. 1개선택이므로 순서가 의미없음.

    arr.forEach((fixed, index, origin) => {
      const rest = [...origin.slice(0, index), ...origin.slice(index+1)] 
      // 해당하는 fixed를 제외한 나머지 배열 
      const permutations = getPermutations(rest, selectNumber - 1); 
      // 나머지에 대해서 순열을 구한다.
      const attached = permutations.map((el) => [fixed, ...el]); 
      //  돌아온 순열에 떼 놓은(fixed) 값 붙이기
      results.push(...attached); 
      // 배열 spread syntax 로 모두다 push
    });

    return results; // 결과 담긴 results return
}
```