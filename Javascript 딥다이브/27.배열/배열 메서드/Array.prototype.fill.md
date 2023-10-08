ES6에 도입된 fill 메서드는 인수로 전달받은 값을 배열의 처음부터 끝까지 요소로 채운다. 이때 원본 배열이 변경된다.

```javascript
const arr = [1, 2, 3];  
  
// 인수로 전달받은 값  0을 배열의 처음부터 끝까지 요소로 채운다.  
arr.fill(0);  
  
// fill 메서드는 원본 배열을 직접 변경한다.  
console.log(arr); //[0, 0, 0]
```

두 번째 인수로 요소 채우기를 시작할 인덱스를 전달할 수 있다.
```javascript
const arr = [1, 2, 3];  
  
// 인수로 전달받은 값  0을 배열의 처음부터 끝까지 요소로 채운다.  
arr.fill(0, 1);  
  
// fill 메서드는 원본 배열을 직접 변경한다.  
console.log(arr); //[1, 0, 0]
```

세 번째 인수로 요소 채우기를 멈출 인덱스를 전달할 수 있다.
```javascript
const arr = [1, 2, 3, 4, 5];  
  
// 인수로 전달받은 값  0을 배열의 처음부터 끝까지 요소로 채운다.  
arr.fill(0, 1, 3);  
  
// fill 메서드는 원본 배열을 직접 변경한다.  
console.log(arr); //[1, 0, 0, 4, 5]
```

fill 메서드를 사용하면 배열을 생성하면서 특정 값으로 요소를 채울 수 있다.
```javascript
const arr = new Array(3);  
console.log(arr); // [ , , ]  
  
// 인수로 전달받은 값 1을 배열의 처음부터 끝까지 요소로 채운다.  
const result = arr.fill(1);   
  
// fill 메서드는 원본 배열을 직접 변경한다.  
console.log(arr); //[1, 1, 1]  
  
// fill 메서드는 변경된 원본 배열을 반환한다.  
console.log(result); //[1, 1, 1]
```

fill 메서드로 요소를 채울 경우 모든 요소를 하나의 값만으로 채울 수밖에 없다는 단점이 있다. 하지만 Array.from 메서드를 사용하면 두 번째 인수로 전달한 콜백 함수를 통해 요소값을 만들면서 배열을 채울 수 있다. Array.from 메서드는 두 번째 인수로 전달한 콜백 함수에 첫 번째 인수에 의해 생성된 배열의 요소값과 인덱스를 순차적으로 전달하면서 호출하고, 콜백 함수의 반환값으로 구성된 배열을 반환한다.

```javascript
// 인수로 전달받은 정수만큼 요소를 생성하고 0부터 1씩 증가하면서 요소를 채운다.  
const sequences = (length = 0) => Array.from({length}, (_, i) => i);  
// const sequences = (length = 0) => Array.from(new Array(length), (_, i) => i);  
  
console.log(sequences(3)); //[0, 1, 2]
```