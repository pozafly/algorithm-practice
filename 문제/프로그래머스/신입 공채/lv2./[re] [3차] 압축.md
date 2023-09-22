# [3차] 압축

> https://school.programmers.co.kr/learn/courses/30/lessons/17684

## 나의 답 (틀림)

```js
function solution(msg) {
  msg = [...msg];
  const dic = [...'ABCDEFGHIJKLMNOPQRSTUVWXYZ'];
  const answer = [];
  let prev = '';
  let next = '';

  for (let i = 0; i < msg.length; i++) {
    if (prev.length === 0) {
      prev = msg[i];
      next = msg[i + prev.length];
    }

    if (!dic.includes(prev + next)) {
      answer.push(dic.findIndex((v) => v === prev) + 1);
      dic.push(prev + next);
      prev = '';
      next = '';
    } else {
      // 존재한다.
      answer.push(dic.findIndex((v) => v === prev + next) + 1);
      next = msg[i + prev.length];
      prev = msg[i + prev.length + 1];
      i++;
    }
  }
  return answer;
}

console.log(solution('TOBEORNOTTOBEORTOBEORNOT'));
```



## 다른 답

```js
function solution(msg) {
    const dict = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split('').reduce((dict, c, i) => {
        dict[c] = i+1;
        return dict;
    }, {});
    dict.nextId = 27;
    const ans = [];
    for(let i = 0, j = 0; i < msg.length; i = j){
        j = msg.length;
        let longest = '';
        while(dict[(longest = msg.substring(i, j))] === undefined) --j;
        ans.push(dict[longest]);
        dict[longest + msg[j]] = dict.nextId++;
    }

    return ans;
}
```

