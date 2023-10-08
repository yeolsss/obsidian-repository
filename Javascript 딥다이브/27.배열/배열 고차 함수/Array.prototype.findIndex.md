ES6에서 도입된 findIndex 메서드는 자신을 호출한 요소를 순회하면서 인수로 전달된 콜백 함수를 호출하여 반환값이 true인 첫 번째 요소의 인덱스를 반환한다. 콜백 함수의 반환값이 true인 요소가 존재하지 않는다면 -1을 반환한다.

forEach, map, filter 메서드와 마찬가지로 findIndex 메서드의 콜백 함수는 findIndex 메서드를 호출한 요소값과 인덱스, findIndex 메서드를 호출한 배열 자체, 즉 this를 순차적으로 전달받을 수 있다.

```javascript
const users = [  
  {id: 1, name: 'Lee'},  
  {id: 2, name: 'Kim'},  
  {id: 2, name: 'Choi'},  
  {id: 3, name: 'Park'}  
];  
  
// id가 2인 요소의 인덱스를 구한다.  
users.findIndex(user => user.id === 2); // 1  
  
// name이 'Park'인 요소의 인덱스를 구한다.  
users.findIndex(user => user.name === 'Park'); // 3  
  
// 위와 같이 프로퍼티 키와 프로퍼티 값으로 요소의 인덱스를 구하는 경우 다음과 같이 콜백 함수를 추상화할 수 있다.  
function predicate(key, value){  
  //key와 value를 기억하는 클로저를 반환  
  return item => item[key] === value;  
}  
  
// id가 2인 요소의 인덱스를 구한다.  
users.findIndex(predicate('id', 2)); // 1  
  
// name이 'Park'인 요소의 인덱스를 구한다.  
users.findIndex(predicate('name', 'Park')); //3
```

forEach, map, filter 메서드와 마찬가지로 findIndex 메서드의 두 번째 인수로 findIndex 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달할 수 있다. 더 나은 방법은 화살표 함수를 사용하는 것이다.

