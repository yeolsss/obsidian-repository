ES6에서 도입된 find 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출 하여 반환값이 true인 첫 번째 요소를 반환한다. 콜백 함수의 반환값이 true인 요소가 존재하지 않는다면 undefined를 반환한다.

forEach, map filter 메서드와 마찬가지로 find 메서드의 콜백 함수는 find 메서드를 호출한 요소값과 인덱스, find 메서드를 호출한 배열 자체, 즉 this를 순차적으로 전달받을 수 있다.

```javascript
const users = [  
  {id: 1, name: 'Lee'},  
  {id: 2, name: 'Kim'},  
  {id: 2, name: 'Choi'},  
  {id: 3, name: 'Park'}  
];  
  
// id가 2인 첫 번째 요소를 반환한다. find 메서드는 배열이 아니라 요소를 반환한다.  
users.find(user => user.id === 2); // {id: 2, name:'Kim'}
```

filter 메서드는 콜백 함수의 호출 결과가 true인 요소만 추출한 새로운 배열을 반환한다. 따라서 filter 메서드의 반환값은 언제나 배열이다. 하지만 find 메서드는 콜백 함수의 반환값이 true인 첫 번째 요소를 반환하므로 find의 결과값은 배열이 아닌 해당 요소값이다.

```javascript
// filter 메서드는 배열을 반환한다.  
[1, 2, 2, 3].filter(item => item === 2); // [2, 2]  
  
// find 메서드는 요소를 반환한다.  
[1, 2, 2, 3].find(item => item === 2); // 2
```

forEach, map, filter 메서드와 마찬가지로 find 메서드의 두 번째 인수로 find 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달할 수 있다. 더 나은 방법은 화살표 함수를 사용하는 것이다.
