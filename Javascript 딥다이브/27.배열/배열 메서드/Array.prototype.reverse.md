reverse 메서드는 원본 배열의 순서를 반대로 뒤집는다. 이때 원본 배열이 변경된다. 반환값은 변경된 배열이다.
```javascript
const arr = [1, 2, 3];  
const result = arr.reverse();  
  
// reverse 메서드는 원본 배열을 직접 변경한다.  
console.log(arr); //[3, 2, 1]  
// 반환값은 변경된 배열이다.  
console.log(result); // [3, 2, 1]
```