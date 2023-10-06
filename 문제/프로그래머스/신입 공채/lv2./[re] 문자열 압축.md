# 문자열 압축

> https://school.programmers.co.kr/learn/courses/30/lessons/60057

## 나의 답

```js
function solution(s) {
  let result = 0;
  for (let i = 1; i < s.length / 2 + 1; i++) {
    let string = [...s];
    let resultString = '';
    let targetCount = 1;

    for (let j = 0; j < string.length; j++) {
      const target = string.slice(j, j + i).join('');
      let countRound = 0;

      while (countRound++ !== i) {
        const diff = string.slice(j + i, j + i + i).join('');
        if (target === diff) {
          targetCount++;
          console.log('targetCount', targetCount);
        } else {
          if (targetCount > 1) {
            resultString += `${targetCount > 1 ? targetCount : ''}${target}`;
            j += i;
          } else {
            resultString += `${target}`;
            j += i;
          }

          targetCount = 1;
          break;
        }
      }
    }
  }
}
```

틀렸음 풀지 못했다.

## 다른 답

```js
function solution(s) {
  let answers = [];
  for (let i = 1; i <= s.length; i++) {
    answers.push(getAnswer(s, i));
  }
  return Math.min(...answers.map((e) => e.join('').length));
}

function getAnswer(str, unit) {
  let count = 1;
  let answer = [];
  for (let i = 0; i <= str.length / unit; i++) {
    let unitStr = str.slice(unit * i, unit * i + unit);
    if (answer[answer.length - 1] == unitStr) {
      count++;
    } else {
      if (count > 1)
        answer[answer.length - 1] = count + answer[answer.length - 1];
      answer.push(unitStr);
      count = 1;
    }
  }
  return answer;
}
```

그나마 제일 알아보기 쉬었던 답.

나와 접근법은 동일하다.