함수형 프로그래밍은 순수 함수와 보조 함수의 조합을 통해 로직 내에 존재하는 **조건문과 반복문을 제거**하여 복잡성을 해결하고 **변수의 사용을 억제**하여 상태 변경을 피하려는 프로그래밍 패러다임이다.

조건문이나 반복문은 로직의 흐름을 이해하기 어렵게 한다. 특히 for문은 반복을 위한 변수를 선언해야 하며, 조건식과 증감식으로 이루어져 있어서 함수형 프로그래밍이 추구하는 바와 맞지 않는다. 
```javascript
const numbers = [1, 2, 3];  
const pows = [];  
  
// for 문으로 배열 순회  
for (let i = 0; i < numbers.length; i++) {  
  pows.push(numbers[i] ** 2);  
}  
  
console.log(pows); // [1, 4, 9]
```

forEach 메서드는 for 문을 대체할 수 있는 고차 함수다. forEach 메서드는 자신의 내부에서 반복문을 실행한다. 즉, forEach 메서드는 반복문을 추상화한 고차 함수로서 내부에서 반복문을 통해 자신을 호출한 배열을 순회하면서 수행해야 할 처리를 콜백 함수로 전달받아 반복 호출한다. for 문으로 구현된 위 예제를 forEach 메서드로 구현하면 다음과 같다.

```javascript
const numbers = [1, 2, 3];  
const pows = [];  
  
// forEach 메서드는 numbers 배열의 모든 요소를 순회하면서 콜백 함수를 반복 호출한다.  
numbers.forEach(item => pows.push(item ** 2));  
console.log(pows); // [1, 4, 9]
```

위 예제의 경우 forEach 메서드는 numbers 배열의 모든 요소를 순회하며 콜백 함수를 반복 호출한다. numbers 배열의 요소가 3개이므로 콜백 함수도 3번 호출 된다. 이때 콜백 함수를 호출하는 forEach 메서드는 콜백 함수에 인수를 전달할 수 있다. 

forEach 메서드의 콜백 함수는 forEach 메서드를 호출한 배열의 요소값과 인덱스, forEach 메서드를 호출한 배열 자체, 즉 this를 순차적으로 전달받을 수 있다. 다시 말해, forEach 메서드는 콜백 함수를 호출할 때 3개의 인수, 즉 forEach 메서드를 호출한 배열의 요소값과 인덱스, forEach 메서드를 호출한 배열(this)을 순차적으로 전달한다.

```javascript
//forEach 메서드는 콜백 함수를 호출하면서 3개(요소값, 인덱스, this)의 인수를 전달한다.  
[1, 2, 3].forEach((item, index, arr) => {  
  console.log(`요소값: ${item}, 인덱스: ${index}, this: ${JSON.stringify(arr)}`);  
});  
  
/*  
요소값: 1, 인덱스: 0, this: [1,2,3]  
요소값: 2, 인덱스: 1, this: [1,2,3]  
요소값: 3, 인덱스: 2, this: [1,2,3]  
*/
```

> #### JSON.stringify 메서드
> JSON.stringify 메서드는 객체를 JSON 포멧의 문자열로 변환한다. 위 예제에서는 객체인 arr 배열을 문자열로 출력하기 위해 사용했다.

forEach 메서드는 원본 배열(forEach 메서드를 호출한 배열, 즉 this)을 변경하지 않는다. 하지만 콜백 함수를 통해 원본 배열을 변경할 수는 있다. 

```javascript
const numbers = [1, 2, 3];  
  
// forEach 메서드는 원본 배열을 변경하지 않지만 콜백 함수를 통해 원본 배열을 변경할 수는 있다.  
// 콜백 함수의 세 번째 매개변수 arr은 원본 배열 numbers를 가리킨다.  
// 따라서 콜백 함수의 세 번째 매개변수 arr을 직접 변경하면 원본 배열 numbers가 변경된다.  
numbers.forEach((item, index, arr) => {  
  arr[index] = item ** 2  
});  
console.log(numbers); //[1, 4, 9]
```

forEach 메서드의 반환값은 언제나 undefined다.

```javascript
const result = [1, 2, 3].forEach(console.log);  
console.log(result); // undefined
```

forEach 메서드의 두 번째 인수로 forEach 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달할 수 있다.

```javascript
class Numbers {  
  numberArray = [];  
  multiply(arr){  
    arr.forEach( function(item) {  
      // TypeError: Cannot read property 'numberArray' of undefined  
      this.numberArray.push(item * item);  
    })  
  }  
}  
  
const numbers = new Numbers();  
numbers.multiply([1, 2, 3]);
```

forEach 메서드의 콜백 함수는 일반 함수로 호출되므로 콜백 함수 내부의 this는 undefined를 가리킨다. this가 전역 객체가 아닌 undefined를 가리키는 이유는 클래스 내부의 모든 코드에는 암묵적으로 `strict mode`가 적용되기 때문이다.

forEach 메서드의 콜백 함수 내부의 this와 multiply 메서드 내부의 this를 일치시키려면 forEach 메서드의 두 번째 인수로 forEach 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달한다. 아래 예제의 경우 forEach 메서드의 두 번째 인수로 multiply 메서드 내부의 this를 전달하고 있다.

```javascript
class Numbers {  
  numberArray = [];  
    
  multiply(arr){  
    arr.forEach( function(item) { 
      this.numberArray.push(item * item);  
  
    }, this); // forEach 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달  
  }  
}  
  
const numbers = new Numbers();  
numbers.multiply([1, 2, 3]);  
console.log(numbers.numberArray); //[1, 4, 9]
```

더 나은 방법은 ES6의 화살표 함수를 사용하는 것이다. 화살표 함수는 함수 자체의 this 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 this를 참조하면 상위 스코프, 즉 multiply 메서드 내부의 this를 그대로 참조한다.

```javascript
class Numbers{  
  numberArray = [];  
  
  multiply(arr) {  
    // 화살표 함수 내부에서 this를 참조하면 상위 스코프의 this를 그대로 참조한다.  
    arr.forEach(item => this.numberArray.push(item * item));  
  }  
}  
  
const numbers = new Numbers();  
numbers.multiply([1, 2, 3]);  
console.log(numbers.numberArray); //[1, 4, 9]
```

forEach 메서드의 동작을 이해하기 위해 forEach 메서드 [폴리필](#폴리필이란?)을 살펴보자.


```javascript
[1,2,3].forEach(item => {  
  console.log(item);  
  if (item > 1) break; // Uncaught SyntaxError: Illegal break statement  
});  
  
[1,2,3].forEach(item => {  
  console.log(item);  
  if (item > 1) continue; //Uncaught SyntaxError: Illegal continue statement: no surrounding iteration statement  
  
});
```

희소 배열의 경우 존재하지 않는 요소는 순회 대상에서 제외된다. 배열을 순회하는 map, filter, reduce 메서드 등에서도 마찬가지다.

```javascript
// 희소 배열  
const arr = [1, , 3];  
  
// for 문으로 희소 배열을 순회  
for (let i = 0; i < arr.length; i++) {  
  console.log(arr[i]); // 1, undefined, 3  
}  
  
// forEach 메서드는 희소 배열의 존재하지 않는 요소를 순회 대상에서 제외한다.  
arr.forEach(v => console.log(v)); // 1, 3
```

forEach 메서드는 for 문에 비해 성능이 좋지는 않지만 가독성은 더 좋다. 따라서 요소가 대단히 많은 배열을 순회하거나 시간이 많이 걸리는 복잡한 코드 또는 성능이 필요한 경우가 아니라면 for 문 대신 forEach 메서드를 사용할 것을 권장한다.

---

## 폴리필이란?
> 최신 사양의 기능을 지원하지 않는 브라우저를 위해 누락된 최신 사양의 기능을 구현하여 추가하는 것을 폴리필polyfill이라 한다.
