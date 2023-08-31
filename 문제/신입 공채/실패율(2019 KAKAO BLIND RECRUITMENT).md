# 실패율(2019 KAKAO BLIND RECRUITMENT)

https://school.programmers.co.kr/learn/courses/30/lessons/42889

## 나의 답

```js
function solution(N, stages) {
  let answer = [];

  for (let i = 1; i < N + 1; i++) {
    const applyPlayers = stages.filter((v) => i <= v);
    const dodalCount = applyPlayers.length;
    const notClearCount = applyPlayers.filter((v) => i >= v).length;
    answer.push({ stage: i, failure: notClearCount / dodalCount });
  }
  answer = answer
    .sort((a, b) => {
      return b.failure - a.failure;
    })
    .map((v) => v.stage);
  return answer;
}
```

생각보다는 가볍게 풀었다.

## 다른 답

```js
function solution(N, stages) {
    let result = [];
    for(let i=1; i<=N; i++){
        let reach = stages.filter((x) => x >= i).length;
        let curr = stages.filter((x) => x === i).length;
        result.push([i, curr/reach]);
    }
    result.sort((a,b) => b[1] - a[1]);
    return result.map((x) => x[0]);
}
```

나랑 완전 똑같네..

다른 답도 비슷.