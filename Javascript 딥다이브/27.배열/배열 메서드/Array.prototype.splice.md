push, pop, unshift, shift 메서드는 모두 원본 배열을 직접 변경하는 메서드이며 원본 배열의 처음이나 마지막에 요소를 추가하거나 제거한다.
원본 배열의 중간에 요소를 추가하거나 중간에 있는 요소를 제거하는 경우 splice 메서드를 사용한다.
splice 메서드는 3개의 매개변수가 있으며 원본 배열을 직접 변경한다.

- start: 원본 배열의 요소를 제거하기 시작할 인덱스다. start만 지정하면 원본 배열의 start부터 모든 요소를 제거한다. start가 음수인 경우 배열의 끝에서 인덱스를 나타낸다. 만약 start가 -1이면 마지막 요소를 가리키고 -n이면 마지막에서 n번째 요소를 가르킨다.
- deleteCount: 원본 배열의 요소를 제거하기 시작할 인덱스인 start부터 제거할 요소의 개수다. deleteCount가 0인 경우 아무런 요소도 제거되지 않는다. (옵션)
- items: 제거한 위치에 삽입할 요소들의 목록이다. 생략할 경우 원본 배열에서 요소들을 제거하기만 한다.(옵션)

```javascript
const arr = [1, 2, 3, 4];

// 원본 배열의 인덱스 1부터 2개의 요소를 제거하고 그 자리에 새로운 요소 20, 30을 삽입힌다.
const result = arr.splice(1, 2, 20, 30);

// 제거한 요소가 배열로 반환된다.
console.log(result); // [2, 3]
// splice 메서드는 원본 배열을 직접 변경한다.
console.log(arr); // [1, 20, 30, 4]

```

splice 메서드에 3개의 인수를 빠짐없이 전달하면 첫 번째 인수, 즉 시작 인덱스부터 두 번째 인수, 즉 제거 할 요소의 개수만큼 원본 배열에서 요소를 제거한다. 그리고 세 번째 인수, 즉 제거한 위치에 삽입할 요소들을 원본 배열에 삽입힌다.
splice 메서드의 두 번째 인수, 즉 제거할 요소의 개수를 0으로 지정하면 아무런 요소도 제거하지 않고 새로운 요소들을 삽입힌다.

```javascript
const arr = [1, 2, 3, 4];

// 원본 배열의 인덱스 1부터 0개의 요소를 제거하고 그 자리에 새로운 요소 100을 삽입한다.
const result = arr.splice(1, 0, 100);

// 원본 배열이 변경된다.
console.log(arr); // [1, 100, 2, 3, 4]
// 제거한 요소가 뱅열로 반환된다.
console.log(result); // []
```

splice 메서드의 세 번째 인수, 즉 제거한 위치에 추가할 요소들의 목록을 전달하지 않으면 원본 배열에서 지정된 요소를 제거하기만 한다.

```javascript
const arr = [1, 2, 3, 4];

// 원본 배열의 인덱스 1부터 2개의 요소를 제거한다.
const result = arr.splice(1, 2);

// 원본 배열이 변경된다.
console.log(arr); //[1, 4]
// 제거한 요소가 배열로 반환된다.
console.log(result); //[2, 3]
```

splice 메서드의 두 번째 인수, 즉 제거할 요소의 개수를 생략하면 첫 번째 인수로 전달된 시작 인덱스부터 모든 요소를 제거한다.

```javascript
const arr = [1, 2, 3, 4];

// 원본 배열의 인덱스 1부터 모든 요소를 제거한다.
const result = arr.splice(1);

// 원본 배열이 변경된다.
console.log(arr); // [1]
// 제거한 요소가 배열로 반환된다.
console.log(result); // [2, 3, 4]
```

배열에서 특정 요소를 제거하려면 indexOf 메서드를 통해 특정 요소의 인덱스를 취득한 다음 splice 메서드를 사용한다.

```javascript
const arr = [1, 2, 3, 1, 2];  
  
// 배열 array에서 item 요소를 제거한다. item 요소가 여러 개 존재하면 첫 번째 요소만 제거한다.  
function remove(array, item) {  
  //제거할 item 요소의 인덱스를 취득한다.  
  const index = array.indexOf(item);  
  
  // 제거할 item 요소가 있다면 제거한다.  
  if (index !== -1) array.splice(index, 1);  
  return array;  
}  
  
console.log(remove(arr, 2));  //[1, 3, 1, 2]
console.log(remove(arr, 10)); //[1, 3, 1, 2]
```

filter 메서드를 사용하여 특정 요소를 제거할 수도 있다. 하지만 특정 요소가 중복된 경우 모두 제거된다.

```javascript
const arr = [1, 2, 3, 1, 2];  
  
// 배열 array에서 모든 item 요소를 제거한다.  
const removeAll = (array, item ) => {  
  return array.filter(v => v !== item);  
}  
  
console.log(removeAll(arr, 2)); // [1, 3, 1]
```
