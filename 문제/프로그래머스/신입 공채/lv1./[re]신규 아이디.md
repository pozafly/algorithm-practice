# 신규 아이디

> [출처](https://school.programmers.co.kr/learn/courses/30/lessons/72410), [해설](https://bingbingba.tistory.com/19)

## 나의 답

```js
function solution(new_id) {
  let answer = new_id.toLowerCase();
  answer = answer
    .replace(/[`~!@#$%^&*()|+\=?;:'",<>\{\}\[\]\\\/ ]/g, '')
    .replace(/\.+/g, '.');
  answer = answer[0] === '.' ? answer.slice(1) : answer;

  answer =
    answer[answer.length - 1] === '.'
      ? [...answer].filter((v, i) => i < answer.length - 1).join('')
      : answer;
  answer = answer.length === 0 ? 'a' : answer;
  answer =
    answer.length > 15 ? [...answer].filter((v, i) => i < 15).join('') : answer;
  answer =
    answer[answer.length - 1] === '.'
      ? [...answer].filter((v, i) => i < answer.length - 1).join('')
      : answer;
  if (answer.length <= 2) {
    const last = [...answer].at(-1);
    while (answer.length <= 2) {
      answer += last;
    }
  }

  return answer;
}
```

약간 어거지로 푼 감이 있다..

