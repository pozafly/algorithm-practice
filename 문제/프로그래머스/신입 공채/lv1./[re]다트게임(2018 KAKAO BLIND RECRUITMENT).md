# 다트게임(2018 KAKAO BLIND RECRUITMENT)

> https://school.programmers.co.kr/learn/courses/30/lessons/17682

## 나의 답

```js
function solution(dartResult) {
  const answer = [];
  let temp = 0;

  for (let i = 0; i < dartResult.length; i++) {
    const target = dartResult[i];
    if (target >= 0 && target <= 9) {
      if (target == 1 && dartResult[i + 1] == 0) {
        temp = 10;
        i++;
      } else {
        temp = target;
      }
    } else if (target === 'S') {
      answer.push(temp);
    } else if (target === 'D') {
      answer.push(Math.pow(temp, 2));
    } else if (target === 'T') {
      answer.push(Math.pow(temp, 3));
    } else if (target === '*') {
      answer[answer.length - 1] *= 2;
      answer[answer.length - 2] *= 2;
    } else if (target === '#') {
      answer[answer.length - 1] *= -1;
    }
  }
  return answer.reduce((acc, cur) => acc + Number(cur), 0);
}
```

