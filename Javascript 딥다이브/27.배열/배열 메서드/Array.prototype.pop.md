pop 메서드는 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다. 원본 배열이 빈 배열이면 undefined를 반환한다. pop 메서드는 원본 배열을 직접 변경한다.

```javascript 
const arr = [1, 2];

// 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다.
let result = arr.pop();
console.log(result); //2

// pop 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1]
```
pop 메서드와 push 메서드를 사용하면 스택을 쉽게 구현할 수 있다.