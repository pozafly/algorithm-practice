# 백준 JS로 풀기

https://www.acmicpc.net/problem/4344 이쪽 백준 문제로 예시를 든다.

## 배경

`input.txt` 라는 파일이 백준에서 제공이 되며, 이는 Node.js의 `fs` 패키지를 통해 파일을 import(require) 해와야 한다.

> 📌 참고, 백준에 실제로 낼 때는 `fs.readFileSync('/dev/stdin').toString()` 으로 사용해 내야 한다.

```js
/*
  https://www.acmicpc.net/problem/4344

  5
  5 50 50 70 80 100
  7 100 95 90 80 70 60 50
  3 70 90 80
  3 70 90 81
  9 100 99 98 97 96 95 94 93 91
*/

const fs = require('fs');
let input = fs.readFileSync('./input.txt').toString(); // input.txt 파일에서 가져옴.
input = input.split('\n');

console.log(input);
/*
  [
    '5',
    '5 50 50 70 80 100',
    '7 100 95 90 80 70 60 50',
    '3 70 90 80',
    '3 70 90 81',
    '9 100 99 98 97 96 95 94 93 91'
  ]
*/
```

이와 같이 들고옴. split을 사용해 줄을 나눠주었다.

```js
const testCaseNum = input[0];
console.log(testCaseNum); // 5

for (let i = 1; i <= testCaseNum; ++i) { // error
  const arr = input[i].split(' ').map((item) => +item);
  console.log(arr);
}
```

이제 테스트 케이스를 가져오기 위해 `input[0]`을 사용해 첫번째 숫자인 5를 가져왔다. 하지만, `testCaseNum` 변수에 든 것은 string이기 때문에 for문에서 에러가 발생한다.

`const testCaseNum = Number(input[0])` 로 Number를 씌워 주어야 함. 혹은, `+input[0]` 을 사용해 암시적으로 바꿔 주어도 된다.

이렇게, input을 가져오는 과정, 파싱하는 과정을 통해 input을 가져왔다.

## solution

그리고 이제, solution 함수를 만들어야 함.

```js
// C = 5
// testCase = [
//   { N: 5, arr: [50, 50, 70, 80, 100] },
//   { N: 7, arr: [100, 95, 90, 80, 70, 60, 50] },
//   ...
// ]
function solution(C, testCase) {}
```

위에 주석으로 우리가 받고 싶은 인자를 먼저 적어두고 시작하면 좋다.

그러면, 위의 파싱하는 과정을 다시 고쳐보자.

```js
const fs = require('fs');
let input = fs.readFileSync('./input.txt').toString().split('\n');

// C 변수를 위한 변수
const inputC = +input[0];
const inputTestCase = [];

for (let i = 1; i <= inputC; ++i) {
  const arr = input[i].split(' ').map((item) => +item);
  const newArr = [];
  for (let i = 1; i <= arr[0]; ++i) {
    newArr.push(arr[i]);
  }
  // testCase를 위한 변수
  const testCase = {
    N: arr[0],
    arr: newArr,
  };
  inputTestCase.push(testCase);
}
```

이제, solution에 넣어주도록 하자.

```js
function solution(C, testCase) {
  // ...
}

solution(inputC, inputTestCase);
```



