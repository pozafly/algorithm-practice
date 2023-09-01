# 올바른 괄호

> https://school.programmers.co.kr/learn/courses/30/lessons/12909?language=javascript

## 나의 답

```js
function solution(s) {
  const arr = [...s];
  const stack = [];
  for (let i = 0; i < arr.length; i++) {
    const value = arr[i];
    if (value === ')' && stack.at(-1) === '(') {
      stack.pop();
      continue;
    }
    stack.push(value);
  }
  return stack.length === 0 ? true : false;
}
```

처음에는 6번째 줄에 `if (stack.at(-1) === '(' && value === ')') {` 이렇게 조건을 적어주었는데, 효율성에서 문제가 생김.

효율성 테스트를 통과하지 못했었다. 하지만, 조건 순서를 바꿔주니 통과 함. `stack.at(-1)` 로 접근하는 것이 속도가 조금 더 오래 걸리는듯?

## 다른 답

```js
function is_pair(s){
  var result = s.match(/(\(|\))/g);
  return result[0] == '(' && result.length % 2 == 0 ? true : false
}
```

역시 정규식을 사용한게 참 빠르구나.