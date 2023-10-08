filter 메서드는 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다. 그리고 **콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열을 반환한다.** 이때 원본 배열은 변경되지 않는다.

```javascript
const numbers = [1, 2, 3, 4, 5];  
  
//filter 메서드는 numbers 배열의 모든 요소를 순회하면서 콜백 함수를 반복 호출한다.  
// 그리고 콜백 함수의 반환값이 true인 요소로만 구성된 새로운 배열을 반환한다.  
// 다음 경우 numbers 배열에서 홀수인 요소만 필터링 한다.(1은 true로 평가된다.)  
const odds = numbers.filter(item => item % 2);  
console.log(odds); // [1, 3, 5]
```

forEach, map 메서드와 마찬가지로 filter 메서드는 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다. forEach 메서드는 언제나 undefined를 반환하고, map 메서드는 콜백 함수의 반환값들로 구성된 새로운 배열을 반환하지만 filter 메서드는 콜백 함수의 반환값이 true인 요소만 추출한 새로운 배열을 반환한다.

filter메서드는 자신을 호출한 배열에서 필터링 조건을 만족하는 특정 요소만 추출하여 새로운 배열을 만들고 싶을 때 사용한다. 위 예제에서 filter 메서드의 콜백 함수는 요소값을 2로 나눈 나머지를 반환한다. 이때 반환값이 true, 즉 홀수인 요소만 추출하여 새로운 배열을 반환한다. 따라서 **filter 메서드가 생성하여 반환한 새로운 배열의 length 프로퍼티 값은 filter 메서드를 호출한 배열의 length 프로파티 값과 같거나 작다.**

![[Screen Shot 2023-09-20 at 3.54.00 PM.png]]

forEach, map 메서드와 마찬가지로 filter 메서드의 콜백 함수는 filter 메서드를 호출한 배열의 요소값과 인덱스, filter 메서드를 호출한 배열 자체, 즉 this를 순차적으로 전달받을 수 있다. 다시 말해, filter 메서드는 콜백 함수를 호출할 떄 3개의 인수, 즉 filter 메서드를 호출한 배열의 요소값과 인덱스, filter 메서드를 호출한 배열(this)을 순차적으로 전달한다.

```javascript
// filter 메서드는 콜백 함수를 호출하면서 3개(요소값, 인덱스, this)의 인수를 전달한다.  
[1, 2, 3].filter((item, index, arr) => {  
  console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);  
  return item % 2;  
});  
  
/*  
요소값: 1, 인덱스: 0, this: [1,2,3]  
요소값: 2, 인덱스: 1, this: [1,2,3]  
요소값: 3, 인덱스: 2, this: [1,2,3]  
*/
```

forEach, map 메서드와 마찬가지로 filter 메서드의 두 번째 인수로 filter 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달할 수 있다. map 메서드에서 살펴보았듯이 더 나은 방법은 화살표 함수를 사용하는 것이다.

filter 메서드는 자신을 호출한 배열에서 특정 요소를 제거하기 위해 사용할 수도 있다.

```javascript
class Users{  
  constructor() {  
    this.users = [  
      {id: 1, name: 'gwon'},  
      {id: 2, name: 'kim'}  
    ];  
  }  
  // 요소 추출  
  findById(id){  
    // id가 일치하는 사용자만 반환한다.  
    return this.users.filter(user => user.id === id);  
  }  
  
  // 요소 제거  
  remove(id){  
    // id가 일치하지 않는 사용자를 제거한다.  
    this.users = this.users.filter(user => user.id !== id);  
  }  
}  
  
const users = new Users();  
  
let user = users.findById(1);  
console.log(user); // [ { id: 1, name: 'gwon' } ]  
  
// id가 1인 사용자를 제거한다.  
users.remove(1);  
  
user = users.findById(1);  
console.log(user); // []
```

filter 메서드를 사용해 특정 요소를 제거할 경우 특정 요소가 중복되어 있다면 중복된 요소가 모두 제거된다. 특정 요소를 하나만 제거하려면 indexOf 메서드를 통해 특정 요소의 인덱스를 취득한 다음 splice 메서드를 사용한다.

