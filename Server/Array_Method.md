# Array_Method 
- 공부하다 이해가 잘 안되는 부분은 _ 를 앞에 쳐 놓고 누구한테나 물어본 뒤 보충한다.
## POP
- 배열 뒷 부분의 값을 삭제한다.
```.js
var arr = [ 1, 2, 3, 4 ];
arr.pop();
console.log(arr); // [ 1, 2, 3 ]
```

### PUSH
- 배열 뒷부분에 값을 삽입
```.js
var arr = [ 1, 2, 3, 4 ];
arr.pop( 5 );
console.log(arr); // [ 1, 2, 3 , 4, 5]
```

### UNSHIFT
- 배열 앞 부분에 값을 삽입
```.js
var arr = [ 1, 2, 3, 4 ];
arr.pop( 5 );
console.log(arr); // [ 5, 1, 2, 3 , 4]
```

### SHIFT
- 배열의 앞 부분의 값을 삭제
```.js
var arr = [ 1, 2, 3, 4 ];
arr.shift();
console.log( arr ); // [2, 3, 4]
```

### SPLICE
- 배열의 특정 위치에 요소를 추가하거나 삭제
- splice(index, 제거할 요소 개수, 배열에 추가될 요소)
```.js
var arr = [ 1, 2, 3, 4, 5, 6, 7];
arr.aplice( 3, 2 );
console.log( arr ); //[1,2,3,6,7] // 3 번째 인덱스에서부터 2개 제거

var arr = [ 1, 2, 3, 4, 5, 6, 7 ];
arr.aplice( 2, 1, "a", "b");
console.log( arr ); // [1, 2, "a", "b", 4, 5, 6, 7] // 2번째 인덱스에서 1개 제거 후 "a" 와 "b" 를 추가
```

### _SLICE (startindex, endindex)
- 배열의 시작 인덱스부터 끝 인덱스까지 (시작 인덱스 이상 끝 인덱스 미만 느낌) shallow copy 를 새로운 배열 객체로 반환
```.js
var arr = [ 1, 2, 3, 4, 5, 6, 7 ];
var newArr = arr.slice( 3, 6 );
console.log( 'slice' , newArr); // [4, 5, 6]
```

### CONCAT
- 다수의 배열을 합치고 병합된 배열의 사본을 반환
```
var arr1 = [ 1 , 2, 3 ];
var arr2 = [ 4, 5, 6];
var arr3 = arr2.concat( arr1 ); //arr2 뒤에다가 arr1 을 병합하고 그 값을 arr3로
console.log (arr3); //[4,5,6,1,2,3]
```

### EVERY
- 배열의 모든 요소가 제공한 함수로 구현된 테스트를 통과하는지를 테스트
```.js
var arr =[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
var isEven = fuction (value) {
  // value 가 2의 배수면 true 를 반환한다.
  return value % 2 == 0;
};
console.log( arr.every( isEven) ); // false 모든 요소가 true면 true를 return 하고 그렇지 않으면 false
```

### SOME
- 지정된 함수의 결과가 true일 때까지 배열의 각 원소를 반복
```.js
var arr = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var isEven = function(value) {
  // value가 2의 배수이면 true를 반환한다.
  return value % 2 == 0;
};
console.log( arr.some( isEven ) ); // true 하나라도 true 이면 true를 반환.
```

### _forEach
- 배열의 각 원소별로 지정된 함수를 실행한다.
```.js
var arr = [ 1,2 ,3];
arr.forEach (function (value) ) {
  console.log(value); // 1 2 3
  });

```

### map 
- 배열의 각 원소별로 지정된 함수를 실행한 결과로 구성된 새로운 배열을 반환한다.
```.js
var arr =[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
var isEven = function( value ) {
  return value % 2 === 0;
};
var newArr = arr.map( isEven );
console.log( newArr ); // [ false, true, false, true, false, true, false, true, false, true ]


```

### filter
- 지정된 함수의 결과 값을 true로 만드는 원소들로만 구성된 별도의 배열을 반환한다.
```.js
var arr = [ 1, 2, 3, 4, 5, 6, 7, 8,9, 10];
var isEven = function(value){
  return value % 2 == 0;
};
var newArr = arr.filter( isEven );
console.log(newArr); // [2, 4, 6, , 10]
```

### reduce
- 누산기 및 배열의 각 값에 대해 한 값으로 줄도록 함수를 적용
```.js
var arr =[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
var value = arr.reduce( function( previousValue, currentValue, index ) {
  return previousValue + currentValue;
});
console.log( value ); // 55
```

### reserve
- 배열의 원소 순서를 거꾸로 바꾸다.
```.js
var arr =[ 1, 2, 3, 4 ];
arr.reverse();
console.log( arr ); // [ 4, 3, 2, 1 ]
```

### _sort
- 배열의 원소를 알파벳, 지정된 함수에 따른 순서로 정렬. 모든 원소를 문자열로 취급 -> 사전적으로 정렬
```.js
var arr = [ 13, 12, 11, 10, 5, 3, 2, 1 ];
arr.sort();
console.log( arr ); // [ 1, 10, 11, 12, 13, 2, 3, 5 ];

// sort에 함수로 정렬
var arr = [ 13, 12, 11, 10, 5, 3, 2, 1 ];
arr.sort( function( a, b ) {
  return a - b;
})
console.log( arr ); // [ 1, 2, 3, 5, 10, 11, 12, 13 ]
```

### toString
- 배열 -> 문자열
```.js
var arr =[ 1, 2, 3, 4 ];
console.log( arr.toString() ); // 1, 2, 3, 4
```
### valueOf
- toString 과 비슷, 그러나 배열을 반환
```.js
var arr =[ 1, 2, 3, 4 ];
console.log( arr.valueOf() ); // [ 1, 2, 3, 4 ]
```

### join
- 배열 원소 전부를 하나의 문자열로 합친다.
```.js
var arr =[ 1, 2, 3, 4 ];
console.log( arr.join() );      // 1,2,3,4
console.log( arr.join( '-' ) ); // 1-2-3-4
```
