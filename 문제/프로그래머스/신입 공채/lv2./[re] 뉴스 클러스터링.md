# 뉴스 클러스터링

https://school.programmers.co.kr/learn/courses/30/lessons/17677

## 나의 답

```js
const convertStringToArr = (value) => {
  const arr = [];
  convertArr = [...value];

  for (let i = 0; i < convertArr.length - 1; i++) {
    const current = convertArr[i];
    const next = convertArr[i + 1];
    if (current.match(/[A-Z]/g) && next.match(/[A-Z]/g)) {
      arr.push(`${current}${next}`);
    }
  }
  return arr.sort();
};

function solution(str1, str2) {
  str1 = str1.toUpperCase();
  str2 = str2.toUpperCase();
  if (str1 === str2) return 65536;

  str1 = convertStringToArr(str1);
  str2 = convertStringToArr(str2);

  let 교집합 = 0;
  let 합집합 = 0;

  for (let i = 0; i < str1.length; i++) {
    if (str2.includes(str1[i])) {
      교집합++;
      str2.splice(str2.indexOf(str1[i]), 1);
    }
    합집합++;
  }
  합집합 += str2.length;
  if (합집합 === 0) return 65536;
  return Math.floor((교집합 / 합집합) * 65536);
}
```

맞추긴 얼추 맞추었는데, 교집합, 합집합을 구하지 못했다. 다시 해야한다.

## 다른 답

```js
function solution(str1, str2) {
    const strArr1 = []
    const strArr2 = []
    let intersection = 0;  //교집합 원소 개수
    let union = 0;  //합집합 원소 개수
    const check = new RegExp(/[a-z]{2}/);
    for (let i=0; i<str1.length-1; i++){
        const str = str1.slice(i,i+2).toLowerCase()
        if(check.test(str)) {
            strArr1.push(str)
        }
    }
    for (let i=0; i<str2.length-1; i++){
    const str = str2.slice(i,i+2).toLowerCase()
    if(check.test(str)) {
            strArr2.push(str)
        }
    }
    strArr1.sort()
    strArr2.sort()
    for (let i=0; i<strArr1.length; i++) {
        if(strArr2.indexOf(strArr1[i]) >= 0){
            intersection++
            strArr2.splice(strArr2.indexOf(strArr1[i]),1)
        }
        union++
    }
    union += strArr2.length
    if (union === 0) return 65536
     return Math.floor((intersection / union) * 65536)
}
```

아래 부분을 참고 했다.,

```js
function solution (str1, str2) {

  function explode(text) {
    const result = [];
    for (let i = 0; i < text.length - 1; i++) {
      const node = text.substr(i, 2);
      if (node.match(/[A-Za-z]{2}/)) {
        result.push(node.toLowerCase());
      }
    }
    return result;
  }

  const arr1 = explode(str1);
  const arr2 = explode(str2);
  const set = new Set([...arr1, ...arr2]);
  let union = 0;
  let intersection = 0;

  set.forEach(item => {
    const has1 = arr1.filter(x => x === item).length;
    const has2 = arr2.filter(x => x === item).length;
    union += Math.max(has1, has2);
    intersection += Math.min(has1, has2);
  })
  return union === 0 ? 65536 : Math.floor(intersection / union * 65536);
}
```

- 이분이 정석일 듯.