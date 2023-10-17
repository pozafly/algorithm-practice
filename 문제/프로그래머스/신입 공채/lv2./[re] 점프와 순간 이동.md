# 점프와 순간 이동

> https://school.programmers.co.kr/learn/courses/30/lessons/12980

## 나의 답

```js
function solution(n) {
  let result = [];
  let energy = 0;

  for (let i = 1; i <= Math.floor(n / 2); i += 1) {
    let move = i;
    energy = i;
    while (true) {
      move = move * 2;
      if (move > n) {
        move -= move / 2;
        break;
      }
    }
    result.push(energy + n - move);
  }
  return Math.min(...result);
}
```

틀렸다.. 이런 쉬운 문제를 풀지 못하다니..

## 다른 답

```js
function solution(n) {
  let answer = 0;
  while (n !== 0) {
    if (n % 2 === 0) {
      n /= 2;
    } else {
      n--;
      answer++;
    }
  }
  return answer;
}
```

- 짝수일 경우는 단지 2로 나누어 주는 것만한다.
- 홀수일 경우에만 에너지를 소모하기 때문이다.

[참고](https://school.programmers.co.kr/questions/51643)