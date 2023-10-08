slice 메서드는 인수로 전달된 범위의 요소들을 복사하여 배열로 반환한다. 원본 배열은 변경되지 않는다.
이름이 유사한 splice 메서드는 원본 배열을 변경하므로 주의해야한다.

slice 메서드는 두 개의 매개변수를 갖는다.
- start: 복사를 시작할 인덱스다. 음수인 경우 배열의 끝에서의 인덱스를 나타낸다. 예를 들어, slice(-2)는 배열의 마지막 두 개의 요소를 복사하여 배열로 반환한다.
- end: 복사를 종료할 인덱스다. 이 인덱스에 해당하는 요소는 복사되지 않는다. end는 생략 가능하며 생략 시 기본 값은 length 프로퍼티 값이다.
```javascript
const arr = [1, 2, 3];  
  
// arr[0] 부터 arr[1] 이전(arr[1] 미포함) 까지 복사하여 반환한다.  
arr.slice(0, 1); //[1]  
  
// arr[1]부터 arr[2] 이전(arr[2] 미포함)까지 복사하여 반환한다.  
arr.slice(1, 2); //[2] 
  
// 원본은 변경되지 않는다.  
console.log(arr); //[1, 2, 3]
```

slice 메서드는 첫 번째 인수(start)로 전달받은 인덱스부터 두 번째 인수 (end)로 전달받은 인덱스 이전(end 미포함)까지 요소들을 복사하여 배열로 반환한다.

slice 메서드의 두 번째 인수(end)를 생략하면 첫 번째 인수(start)로 전달받은 인덱스부터 모든 요소를 복사하여 배열로 반환한다.

```javascript
const arr = [1, 2, 3];  
  
// arr[1]부터 이후의 모든 요소를 복사하여 반환한다.  
arr.slice(1); // [2, 3]
```

slice 메서드의 첫 번쨰 인수가 음수인 경우 배열의 끝에서부터 요소를 복사하여 배열로 반환한다.

```javascript
const arr = [1, 2, 3];  
  
// 배열의 끝에서부터 요소를 한 개 복사하여 반환한다.  
arr.slice(-1); // [3]  
  
// 배열의 끝에서부터 요소를 두 개 복사하여 반환한다.  
arr.slice(-2); // [2, 3]
```

slice 메서드의 인수를 모두 생략하면 원본 배열의 복사본을 생성하여 반환한다.

```javascript
const arr = [1, 2, 3];  
  
//인수를 모두 생략하면 원본 배열의 복사본을 생성하여 반환한다.  
const copy = arr.slice();  
console.log(copy); //[1, 2, 3]  
console.log(copy === arr); //false
```

이때 생성된 복사본은 얕은 복사를 통해 생성된다.

```javascript
const todos = [  
  {id: 1, content: 'HTML', completed: false},  
  {id: 2, content: 'CSS', completed: true},  
  {id: 3, content: 'Javascript', completed: false}  
];  
  
// 얕은 복사(shallow copy)  
const _todos = todos.slice();  
// const _todos = [...todos];  
  
// _todos와 todos는 참조값이 다른 별개의 객체다.  
console.log(todos === _todos); //false  
  
// 배열 요소의 참조값이 같다. 즉, 얕은 복사가 되었다.  
console.log(todos[0] === _todos[0]) // true
```

slice 메서드가 복사본을 생성하는 것을 이용하여 arguments, HTMLCollection, NodeList 닽은 유사 배열 객체를 배열로 변환할 수 있다.


```javascript
const sum =() =>{  
  // 유사 배열 객체를 배열로 변환(ES5)  
  var arr = Array.prototype.slice.call(arguments);  
  console.log(arr); //?  
  
  return arr.reduce((pre, cur) => {  
    return pre + cur  
  }, 0);  
}  
  
console.log(sum(1, 2, 3)); // 6
```

Array.from 메서드를 사용하면 더욱 간단하게 유사 배열 객체를 배열로 변환할 수 있다. Array.from 메서드는 유사 배열 객체 또는 이터러블 객체를 배열로 변환한다.

```javascript
const sum = () =>{  
  const arr = Array.from(arguments);  
  console.log(arr); //[1, 2, 3]  
  
  return arr.reduce((pre, cur) => pre + cur, 0);  
}  
console.log(sum(1, 2, 3)); //6
```

이터러블 객체는 ES6의 스프레드 문법을 사용하여 간단하게 배열로 변환할 수 있다.

```javascript
const sum = () =>{  
  // 이터러블을 배열로 변환(ES6 스프레드 문법)  
  const arr = [...arguments];  
  console.log(arr); // [1, 2, 3]  
  
  return arr.reduce((pre, cur) => pre + cur, 0);  
}  
console.log(sum(1, 2, 3)); //6
```

---
[[얕은 복사와 깊은 복사]]

