ES10(ECMAScript 2019)에서 도입된 flatMap 메서드는 map 메서드를 통해 생성된 새로운 배열을 평탄화한다. 즉, map 메서드와 flat 메서드를 순차적으로 실행하는 효과가 있다.

```javascript
const arr = ['hello', 'world'];  
  
// map과 flat을 순차적으로 실행  
arr.map(x => x.split('')).flat();   
// ['h', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd']  
  
arr.flatMap(item => item.split(''));  
// ['h', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd']
```

단, flatMap 메서드는 flat 메서드처럼 인수를 전달하여 평탄화 깊이를 지정할 수는 없고 1단계만 평탄화한다. map 메서드를 통해 생성된 중첩 배열의 평탄화 깊이를 지정해야 하면 flatMap 메서드를 사용하지 말고 map 메서드와 flat메서드를 각각 호출한다.

```javascript
const arr = ['hello', 'world'];  
  
// flatMap은 1단계만 평탄화 한다.  
arr.flatMap((str, index) => [index, [str.length]]);   
// [0, [5], 1, [5]]  
  
// 평탄화 깊이를 지정해야 하면 flatMap 메서드를 사용하지 말고 map 메서드와 flat 메서드를 각각 호출한다.  
arr.map((str, index) => [index, [str, str.length]]).flat(2);  
// [0, 'hello', 5, 1, 'world', 5]
```