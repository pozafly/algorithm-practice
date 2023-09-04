# [1차] 비밀지도(2018 KAKAO BLIND RECRUITMENT)

https://school.programmers.co.kr/learn/courses/30/lessons/17681

## 나의 답

```js
const convertMap = (arr) => {
  const result = [];
  arr.forEach((v) => {
    let 진수2 = [...v.toString(2)];
    while (진수2.length < arr.length) {
      진수2.unshift('0');
    }
    result.push(진수2);
  });
  return result;
};

function solution(n, arr1, arr2) {
  const answer = [];
  arr1 = convertMap(arr1);
  arr2 = convertMap(arr2);

  for (let i = 0; i < n; i++) {
    const result = [];
    for (let j = 0; j < n; j++) {
      if (arr1[i][j] === '0' && arr2[i][j] === '0') {
        result.push(' ');
      } else {
        result.push('#');
      }
    }
    answer.push(result.join(''));
  }

  return answer;
}
```

## 다른 답

```js
function solution(n, arr1, arr2) {
  return arr1.map((v, i) =>
    addZero(n, (v | arr2[i]).toString(2)).replace(/1|0/g, (a) =>
      +a ? '#' : ' '
    )
  );
}

const addZero = (n, s) => {
  return '0'.repeat(n - s.length) + s;
};
```

현타오네.. 이렇게 쉽게 풀 수 있는거였다니..

- 우선 addZero 같은 경우는, `repeat`를 사용했다. 길이 만큼 빼주고 남는 수를 0으로 채우는 것.
- 그리고, arr1, arr2를 **비트 연산자** `|`로 비교했다. 비교하는 비트 중 하나라도 1이면 1을 반환하는 연산자가 `|` 이다.
- arr1을 map 형태로 넣어주었다. 정규 표현식을 사용해 2진수로 변환된 값을 #, ' ' 로 다시 replace 해줌.

replace, repeat를 적절한 상황에서 잘 써야겠다..