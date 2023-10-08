ES7에서 도입된 includes 메서드는 배열 내에 특정 요소가 포함되어 있는지 확인하여 true 또는 false를 반환한다. 첫 번째 인수로 검색할 대상을 지정한다.

```javascript
const arr = [1, 2, 3];  
  
// 배열 요소 2가 포함되어 잇는지 확인한다.  
arr.includes(2); // true  
  
// 배열 요소 100이 포함되어 있는지 확인한다.  
arr.includes(100); // false
```

두 번째 인수로 검색을 시작할 인덱스를 전달할 수 있다. 두 번째 인수를 생략할 경우 기본값 0 이 설정된다.
만약 두 번째 인수에 음수를 전달하면 length 프로퍼티 값과 음수 인덱스를 합산하여(length + index) 검색 시작 인덱스를 설정한다.
```javascript
const arr = [1, 2, 3];  
  
// 배열 요소 1이 포함되어 잇는지 인덱스 1부터 확인한다.  
arr.includes(1, 1); // false  
  
// 배열에 요소 3이 포함되어 있는지 인덱스 2(arr.length - 1)부터 확인한다.  
arr.includes(3, -1); // true
```

배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환하는 indexOf 메서드를 사용하여도 배열 내에 특정요소가 포함되어 있는지 확인할 수 있다. 하지만 indexOf 메서드를 사용하면 반환값이 -1인지 확인해 보아야 하고 배열에 `NaN`이 포함되어 있는지 확인할 수 없다는 문제가 잇다.
```javascript
[NaN].indexOf(NaN) !== -1; // false
[NaN].includes(NaN);       // true
```
