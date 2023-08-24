# 폰켓몬

https://school.programmers.co.kr/learn/courses/30/lessons/1845?language=javascript

## 나의 답

```js
function solution(arr) {
  const myMap = new Map();
  arr.forEach((v) => {
    let count = 1;
    if (myMap.has(v)) {
      count = myMap.get(v) + 1;
    }
    myMap.set(v, count);
  });
  if (myMap.size >= arr.length / 2) {
    return arr.length / 2;
  } else {
    return myMap.size;
  }
}
```

## 다른 답

```js
function solution(nums) {
  const max = nums.length / 2;
  const arr = [...new Set(nums)];

  return arr.length > max ? max : arr.length
}
```

---

숫자가 겹치는 것을 판단하는 문제이기 때문에 Map을 쓸 필요가 없었다. Set을 사용하면 되는 문제였다.