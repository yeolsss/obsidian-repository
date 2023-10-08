map 메서드는 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다. 그리고 **콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다**. 이때 원본 배열은 변경되지 않는다.

```javascript
const numbers = [1, 4, 9];  
  
// map 메서드는 numbers 배열의 모든 요소를 순회하면서 콜백 함수를 반복 호출한다.  
// 그리고 콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다.  
const roots = numbers.map(item => Math.sqrt(item));  
// 위 코드는 다음과 같다.  
// const roots = numbers.map(Math.sqrt);  
  
// map 메서드는 새로운 배열을 반환한다.  
console.log(roots); // [1, 2, 3]  
// map 메서드는 원본 배열을 변경하지 않는다.  
console.log(numbers); // [1, 4, 9]
```

forEach 메서드와 map 메서드의 공통점은 자신을 호출한 배열의 모든 요소를 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다는 것이다. 하지만 forEach 메서드는 언제나 undefined를 반환하고, map 메서드는 콜백 함수의 반환값들로 구성된 새로운 배열을 반환하는 차이가 있다. 즉, forEach 메서드는 단순히 반복문을 대체하기 위한 고차 함수이고, map 메서드는 요소값을 다른 값으로 매핑한 새로운 배열을 생성하기 위한 고차 함수다.

**map 메서드가 생성하여 반환하는 새로운 배열의 length 프로퍼티 값은 map 메서드를 호출한 배열의 length프로퍼티 값과 반드시 일치한다. 즉, map 메서드를 호출한 배열과 map 메서드가 생성하여 반환한 배열은 1:1 매핑한다.**

![[Screen Shot 2023-09-20 at 3.35.17 PM.png]]

forEach 메서드와 마찬가지로 map 메서드의 콜백 함수는 map 메서드를 호출한 배열의 요소값과 인덱스, map 메서드를 호출한 배열 자체, 즉 this를 순차적으로 전달받을 수 있다. 다시 말해, map 메서드는 콜백 함수를 호출할 때 3개의 인수, 즉 map 메서드를 호출한 배열과 요소값 인덱스 그리고 map 메서드를 호출한 배열(this)을 순차적으로 전달한다.

```javascript
[1,2,3].map((item, index, arr) =>{  
  console.log(`요소값: ${item}, 인덱스: ${index}, this: ${arr}`);  
  return item;  
})  
  
/*  
요소값: 1, 인덱스: 0, this: 1,2,3  
요소값: 2, 인덱스: 1, this: 1,2,3  
요소값: 3, 인덱스: 2, this: 1,2,3  
*/
```

forEach 메서드와 마찬가지로 map 메서드의 두 번째 인수로 map 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달할 수 있다.

```javascript
class Prefixer {  
  constructor(prefix) {  
    this.prefix = prefix;  
  }  
  
  add(arr) {  
    return arr.map(function (item){  
      // 외부에서 this를 전달하지 않으면 this는 undefined를 가리킨다.  
      return this.prefix + item;   
    }, this); // map 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달   
}  
}  
  
const prefixer = new Prefixer('-webkit-');  
console.log(prefixer.add(['transition', 'user-select']));  
// ['-webkit-transition', '-webkit-user-select']
```

더 나은 방법은 ES6의 화살표 함수를 사용하는 것이다. 화살표 함수는 함수 자체의 this 바인딩을 갖지 않는다. 따라서 화살표 함수 내부에서 this를 참조하면 상위 스코프, 즉 add 메서드 내부의 this를 그대로 참조한다.

```javascript
class Prefixer {  
  constructor(prefix) {  
    this.prefix = prefix;  
  }  
  
  add(arr) {  
    return arr.map((item) => {  
      // 외부에서 this를 전달하지 않으면 this는 undefined를 가리킨다.  
      return this.prefix + item;  
    }); // map 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달  
  }  
}  
  
const prefixer = new Prefixer('-webkit-');  
console.log(prefixer.add(['transition', 'user-select']));  
// ['-webkit-transition', '-webkit-user-select']
```