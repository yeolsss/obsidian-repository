some 메서드는 자신을 호출한 배열의 요소를 순회하면서 인수로 전달된 콜백 함수를 호출한다. 이때 some 메서드는 콜백 함수의 반환값이 단 한번이라도 참이면 true, 모두 거짓이면 false를 반환한다. 즉, 배열의 요소 중에 콜백 함수를 통해 정의한 조건을 만족하는 요소가 1개 이상 존재하는지 확인하여 그 결과를 Boolean타입으로 반환한다. 단, some 메서드를 호출한 배열이 빈 배열인 경우 언제나 false를 반환하므로 주의하자.

forEach, map, filter 메서드와 마찬가지로 some 메서드의 콜백 함수는 some 메서드를 호출한 요소값과 인덱스, some 메서드를 호출한 배열 자체, 즉 this를 순차적으로 전달받을 수 있다.

```javascript
// 배열의 요소 중 10보다 큰 요소가 1개 이상 존재하는지 확인  
[5, 10, 15].some(item => item > 10);//true  
  
// 배열의 요소 중 0보다 작은 요소가 1개 이상 존재하는지 확인  
[5, 10, 15].some(item => item < 0); //false  
  
// 배열 요소 중 'banana'가 1개 이상 존재하는지 확인  
['apple', 'banana', 'mango'].some(item => item === 'banana');//true  
  
// some 메서드를 호출한 배열이 빈 배열인 경우 언제나 false를 반환한다.  
[].some(item => item > 3); //false
```

forEach, map, filter 메서드와 마찬가지로 some 메서드의 두 번째 인수로 some 메서드의 콜백 함수 내부에서 this로 사용할 객체를 전달할 수 있다. 더 나은 방법은 화살표 함수를 사용하는 것이다.
