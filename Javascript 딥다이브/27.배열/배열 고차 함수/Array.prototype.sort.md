sort 메서드는 배열의 요소를 정렬한다. 원본 배열을 직접 변경하며 정렬된 배열을 반환한다.
sort 메서드는 기본적으로 오름차순으로 요소를 정렬한다.

```javascript
const fruits = ['Banana', 'Orange', 'Apple'];  
  
// 오름차순(ascending) 정렬  
fruits.sort(); 
  
// sort 메서드는 원본 배열을 직접 변경한다.  
console.log(fruits); // ['Apple', 'Banana', 'Orange']
```

한글 문자열인 요소도 오름차순으로 정렬된다.

```javascript
const fruits = ['바나나', '오렌지', '사과'];  
  
// 오름차순(ascending) 정렬  
fruits.sort(); 
  
// sort 메서드는 원본 배열을 직접 변경한다.  
console.log(fruits); // ['바나나', '사과', '오렌지']
```

sort 메서드는 기본적으로 오름차순으로 정렬한다. 따라서 내림차순으로 요소를 정렬하려면 sort 메서드를 사용하여 오름차순으로 정렬한 후 reverse 메서드를 사용하여 요소의 순서를 뒤집는다.

```javascript
const fruits = ['Banana', 'Orange', 'Apple'];  
  
// 오름차순(ascending) 정렬  
fruits.sort();   
  
// sort 메서드는 원본 배열을 직접 변경한다.  
console.log(fruits); // ['Apple', 'Banana', 'Orange']  
  
// 내림차순(descending) 정렬  
fruits.reverse();  
  
// reverse 메서드도 원본 배열을 직접 변경한다.  
console.log(fruits); // ['Orange', 'Banana', 'Apple']
```

문자열 요소로 이루어진 배열의 정렬은 아무런 문제가 없다. 하지만 숫자 요소로 이루어진 배열을 정렬할 때는 주의가 필요하다.

```javascript
const points = [40, 100, 1, 5, 2, 25, 10];  
  
points.sort();  
  
// 숫자 요소들로 이루어진 배열은 의도한 대로 정렬되지 않는다.  
console.log(points); //[1, 10, 100, 2, 25, 40, 5]
```

sort 메서드의 기본 정렬 순서는 유니코드 코드 포인트의 순서를 따른다. 배열의 요소가 숫자 타입이라 할지라도 배열의 요소를 일시적으로 문자열로 변환 후 유니코드 코드 포인트의 순서를 기준으로 정렬한다.

문자열 '1'의 유니코드 코드 포인트는 U_0031, 문자열 '2'의 유니코드 코드 포인트는 U+0032다. 
이처럼 문자열 '1'의 유니코드 코드 포인트 순서가 문자열 '2'의 유니코드 코드 포인터 순서보다 앞서므로 문자열 배열`['2', '1']`을 sort 메서드로 정렬하면 `['1', '2']`로 정렬된다. sort 메서드는 배열의 요소를 일시적으로 문자열로 변환한 후 정렬하므로 숫자 배열 `[2, 1]`을 sort 메서드로 정렬해도 `[1, 2]`로 정렬된다.

```javascript 
['2', '1'].sort(); // ['1', '2']
[2, 1].sort(); // [1, 2]
```

하지만 문자열 '10'의 유니코드 코드 포인트는 U+0031U+0030이다. 따라서 문자열 배열 `[2, 10]`을 sort메서드로 정렬하면 문자열 '10'의 유니코드 코드 포인트 U+0031U+0030이 문자열 '2'의 유니코드 코드 포인트 U+0032보다 앞서므로 `['10', '2']`로 정렬된다. sort 메서드는 배열의 요소를 일시적으로 문자열로 변환한 후 정렬하므로 숫자 배열`[2, 10]`을 sort 메서드로 정렬해도 `[10, 2]`로 정렬된다.

```javascript
['2', '10'].sort(); // ['10', '2']  
[2, 10].sort(); // [10, 2]
```

따라서 숫자 요소를 정렬 할때는 sort 메서드에 **정렬 순서를 정의하는 비교 함수를 인수로 전달**해야한다. 비교 함수는 양수나 음수 또는 0을 반환해야 한다. 비교 함수의 반환값이 0보다 작으면 비교 함수의 첫 번째 인수를 우선하여 정렬하고, 0이면 정렬하지 않으며, 0보다 크면 두 번째 인수를 우선하여 정렬한다.

```javascript
const points = [40, 100, 1, 5, 2, 25, 10];  
  
// 숫자 배열의 오름차순 정렬. 비교 함수의 반환값이 0보다 작으면 a를 우선하여 정렬한다.  
points.sort((a, b) => a - b);  
console.log(points); // [1, 2, 4, 10, 25, 40, 100]  
  
// 숫자 배열에서 최소/최댓감 취득  
console.log(points[0], points[points.length - 1]); // 1 100  
  
// 숫자 배열의 내림차순 정렬. 비교 함수의 반환값이 0보다 작으면 b를 우선하여 정렬한다.  
points.sort((a, b) => b - a);  
console.log(points); // [100, 40, 25, 10, 5, 2, 1]  
  
// 숫자 배열에서 최소/최댓값 취득  
console.log(points[points.length - 1], points[0]); // 1 100
```

객체를 요소로 갖는 배열을 정렬하는 예제는 다음과 같다.

```javascript
const todos = [  
  {id: 4, content: 'Javascript'},  
  {id: 1, content: 'HTML'},  
  {id: 2, content: 'CSS'}  
];  
  
// 비교 함수. 매개변수 key는 프로퍼티 키  
const compare = (key) =>{  
  // 프로퍼티 값이 문자열인 경우 - 산술 연산으로 비교하면 NaN이 나오므로 비교 연산을 사용한다.  
  // 비교 함수는 양수/음수/0을 반환하면 되므로 - 산술 연산 대신 비교 연산을 사용할 수 있다.  
  return (a, b) => (a[key] > b[key] ? 1 : (a[key] < b[key] ? -1 : 0));  
}  
  
// id를 기준으로 오름차순 정렬  
todos.sort(compare('id'));  
console.log(todos)  
/*  
[  
  {id: 1, content: 'HTML'},  {id: 2, content: 'CSS'},  {id: 4, content: 'Javascript'}]  
*/  
  
// content를 기준으로 오름차순 정렬  
todos.sort(compare('content'));  
console.log(todos);  
/*  
[  
  {id: 2, content: 'CSS'},  {id: 1, content: 'HTML'},  {id: 4, content: 'Javascript'}]  
*/
```

> ### sort 메서드의 정렬 알고리즘
> sort 메서드는 quicksort 알고리즘을 사용했었다. quicksort 알고리즘은 동일한 값의 요소가 중복되어 있을 때 초기 순서와 변경 될 수 있는 불안정한 정렬 알고리즘으로 알려져 있다. ECMAScript 2019(ES10)에서는 timsort 알고리즘을 사용하도록 바뀌었다.

[QuickSort](https://ko.wikipedia.org/wiki/%ED%80%B5_%EC%A0%95%EB%A0%AC)
[TimSort](https://en.wikipedia.org/wiki/Timsort)