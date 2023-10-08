reduce 메서드는 자신을 호출한 배열을 모든 요소를 순회하며 인수로 전달받은 콜백 함수를 반복 호촐한다.
그리고 콜백 함수의 반환값을 다음 순회 시에 콜백 함수의 첫 번째 인수로 전달하면서 콜백 함수를 호출하여 **하나의 결과값을 만들어 반환한다.** 이때 원본 배열은 변경되지 않는다.

reduce 메서드는 첫 번째 인수로 콜백 함수, 두 번째 인수로 초기값을 전달받는다. reduce 메서드의 콜백 함수에는 4개의 인수, 초기값 또는 콜백 함수의 이전 반환값, reduce 메서드를 호출한 배열의 요소값과 인덱스, reduce 메서드를 호출한 배열 자체, 즉 this가 전달된다.

예제의 reduce 메서드는 2개의 인수, 즉 콜백 함수와 초기값 0을 전달받아 자신을 호출한 배열의 모든 요소를 누적한 결과를 반환한다.

```javascript
const sum = [1, 2, 3, 4].reduce(  
    (accumulator, currentValue, index, array) =>  
     accumulator + currentValue  
    , 0);  
  
console.log(sum); // 10
```

reduce 메서드의 콜백 함수는 4개의 인수를 전달받아 배열의 length만큼 총 4회 호출된다. 이때 콜백 함수로 전달되는 인수와 콜백 함수의 반환값은 다음과 같다.

![[Screen Shot 2023-09-20 at 4.59.00 PM.png]]

![[Screen Shot 2023-09-20 at 4.59.17 PM.png]]

이처럼 reduce 메서드는 초기값과 배열의 첫 번째 요소값을 콜백 함수에게 인수로 전달하면서 호출하고 다음 순회에는 콜백 함수의 반환값과 두 번째 요소값을 콜백 함수의 인수로 전달하면서 호출한다. 이러한 과정을 반복하여 **reduce 메서드는 하나의 결과값을 반환한다.**

reduce 메서드는 자신을 호출한 배열의 모든 요소를 순회하며 하나의 결과값을 구해야 하는 경우에 사용한다.

### 평균 구하기
```javascript
const values = [1, 2, 3, 4, 5, 6];  
const average = values.reduce((acc, cur, i, {length}) =>{  
  // 마지막 순회가 아니면 누적값을 반환하고 마지막 순회면 누적값으로 평균을 구해 반환한다.  
  return i === length - 1 ? (acc + cur) / length : acc + cur;  
}, 0);  
  
console.log(average); // 3.5
```

### 최대값 구하기
```javascript
const values = [1, 2, 3, 4, 5, 6];  
  
const max = values.reduce((acc, cur) => (acc > cur ? acc : cur), 0);  
console.log(max); // 6
```
최대값을 구할 때는 reduce 메서드보다 Math.max 메서드를 사용하는 방법이 더 직관적이다.

```javascript
const values = [1, 2, 3, 4, 5, 6];  
  
const max = Math.max(...values);  
console.log(max); // 6
```

### 요소의 중복 횟수 구하기

```javascript
const fruits = ['banana', 'apple', 'orange', 'orange', 'apple'];  
  
const count = fruits.reduce((acc, cur) => {  
  // 첫 번째 순회 시 acc는 초기값인 {} 이고 cur은 첫 번째 요소인 'banana'다.  
  // 초기값으로 전달받은 빈 객체에 요소값인 cur을 프로퍼티 키로, 요소의 개수를 프로퍼티 값으로 할당한다.  
  // 만약 프로퍼티 값이 undefined(처음 등장하는 요소)이면 프로퍼티 값을 1로 초기화한다.  
  acc[cur] = (acc[cur] || 0) + 1;  
  return acc;  
}, {});  
  
// 콜백 함수는 총 5번 호출되고 다음과 같이 결과값을 반환한다.  
/*  
{banana: 1} => {banana: 1, apple: 1} => {banana: 1, apple: 1, orange: 1}  
=> {banana: 1, apple: 1, orange: 2} => {banana: 1, apple: 2, orange: 2}  
*/  
  
console.log(count); // {banana: 1, apple: 2, orange: 2}
```

### 중첩 배열 평탄화
```javascript
const values = [1, [2, 3], 4, [5, 6]];  
  
const flatten = values.reduce((acc, cur) =>acc.concat(cur), []);  
// [1] => [1, 2, 3] => [1, 2, 3, 4] => [1, 2, 3, 4, 5, 6]  
  
console.log(flatten); // [1, 2, 3, 4, 5, 6]
```

중첩 배열을 평탄화할 때는 reduce 메서드보다 ES10(ECMAScript 2019)에서 도입된 Array.prototype.flat 메서드를 사용하는 방법이 더 직관적이다.

```javascript
[1, [2,3,4,5]].flat(); // [1, 2, 3, 4, 5]  
  
// 인수 2는 중첩 배열을 평탄화하기 위한 깊이 값이다.  
[1, [2, 3, [4, 5]]].flat(2); // [1, 2, 3, 4, 5]
```

### 중복 요소 제거 
```javascript
const values = [1, 2, 1, 3, 5, 4, 5, 3, 4, 4];  
  
const result = values.reduce(  
    (unique, val, i, _values) =>  
    // 현재 순회 중인 요소의 인덱스가 i가 val의 인덱스와 같다면 val은 처음 순회하는 요소다.  
    // 현재 순회 중인 요소의 인덱스 i가 val의 인덱스와 다르면 val은 중복된 요소다.  
    // 처음 순회하는 요소만 초기값 []이 전달된 unique 배열에 담아 반환하면 중복된 요소는 제거된다.  
      _values.indexOf(val) === i ? [...unique, val] : unique, []  
);  
  
console.log(result); // [1, 2, 3, 5, 4]
```

중복 요소를 제거할 때는 reduce 메서드보다 filter 메서드를 사용하는 방법이 더 직관적이다.

```javascript
const values = [1, 2, 1, 3, 5, 4, 5, 3, 4, 4];  
  
// 현재 순회 중인 요소의 인덱스 i가 val의 인덱스와 같다면 val은 처음 순회하는 요소다. 이 요소만 필터링한다.  
const result = values.filter((val, i, _values) => _values.indexOf(val) === i);  
console.log(result); // [1, 2, 3, 5, 4]
```

또는 중복되지 않는 유일한 값들의 집합인 Set을 사용할 수도 있다. 중복 요소를 제거할 때는 이 방법을 추천한다.

```javascript
const values = [1, 2, 1, 3, 5, 4, 5, 3, 4, 4];  
  
// 중복을 허용하지 않는 Set 객체의 특성을 활용하여 배열에서 중복된 요소를 제거할 수 있다.  
const result = [...new Set(values)];  
console.log(result); // [1, 2, 3, 5, 4]
```

이처럼 map, filter, some, every, find 같은 모든 배열의 고차 함수는 reduce 메서드로 구현할 수 있다.

reduce 메서드의 두 번째 인수로 전달하는 초기값은 첫 번째 순회에 콜백 함수의 첫 번째 인수로 전달된다. 주의할 것은 두 번째 인수로 전달하는 초기값이 옵션이라는 것이다. 즉, reduce 메서드의 두 번째 인수로 전달하는 초기값은 생량할 수 있다. 

```javascript
// reduce 메서드의 두 번째 인수, 즉 초기값을 생량했다.  
const sum = [1, 2, 3, 4].reduce((acc, cur) => acc + cur);  
console.log(sum); // 10
```

![[Screen Shot 2023-09-20 at 6.46.14 PM.png]]

하지만 **reduce 메서드를 호출할 때는 언제나 초기값을 전달하는 것이 안전하다.** 

```javascript
const sum = [].reduce((acc, cur) => acc + cur);   
//Uncaught TypeError: Reduce of empty array with no initial value
```

이처럼 빈 배열로 reduce 메서드를 호출하면 에러가 발생한다. 이때 reduce 메서드에 초기값을 전달하면 에러가 발생하지 않는다.

```javascript
const sum = [].reduce((acc, cur) => acc + cur, 0);  
console.log(sum); // 0
```

reduce 메서드로 객체의 특정 프로퍼티 값을 합산하는 경우를 생각해 보자.

```javascript
const products = [  
  {id: 1, price: 100},  
  {id: 2, price: 200},  
  {id: 3, price: 300}  
];  
  
// 1번째 순회 시 acc는 {id: 1, price: 100}, cur은 {id: 2, price: 200}이고  
// 2번째 순회 시 acc는 300, cur은 {id: 3, price: 300} 이다.  
// 2번째 순회 시 acc에 함수의 객체가 아닌 숫자값이 전달된다. 이때 acc.price는 undefined다.  
const priceSum = products.reduce((acc, cur) =>   
    acc.price + cur.price);  
  
console.log(priceSum); // NaN
```

이처럼 객체의 특정 프로퍼티 값을 합산하는 경우에는 반드시 초기값을 전달해야 한다.

```javascript
const products = [  
  {id: 1, price: 100},  
  {id: 2, price: 200},  
  {id: 3, price: 300}  
];  
  
// 1번째 순회 : acc => 0, cur => {id: 1, price: 100}// 2번째 순회 : acc => 100, cur => {id: 2, price: 200}// 3번째 순회 : acc => 300, cur => {id: 3, price: 300}const priceSum = products.reduce((acc, cur) =>  
    acc + cur.price, 0);  
  
console.log(priceSum); // 600
```

이처럼 reduce 메서드를 호출할 때는 초기값을 생략하지 말고 언제나 전달하는 것이 안전하다.
