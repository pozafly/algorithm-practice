# 후보키

> https://school.programmers.co.kr/learn/courses/30/lessons/42890

## 나의 답

```js
// 배열의 index로 진행한다.
// 순서대로, 중복이 있는지 체크한다.
// set을 사용하여 값을 넣고, length 비교한다.
// 만약 중복되는 값이 있다면, 그 다음 index와 함께 묶어 비교한다.

function solution(relation) {
  let answer = 0;
  const candidateLength = relation[0].length;

  for (let i = 0; i < candidateLength; i++) {
    const set = new Set();
    for (let j = 0; j < relation.length; j++) {
      set.add(relation[j][i]);
    }

    if (set.size === relation.length) {
      answer++;
    } else {
      const anotherSet = new Set();
      for (let j = 0; j < relation.length; j++) {
        anotherSet.add(`${relation[j][i]}${relation[j][i + 1]}`);
      }

      if (anotherSet.size === relation.length) {
        answer++;
      }
    }
  }

  return answer;
}
```

예제는 만족하지만, 답은 틀렸음.

재귀를 사용할까 했는데, 재귀 사용법이 미숙하다.

## 다른 답

```js
function solution(relation) {
    let column = relation[0].length;
    let row = relation.length;
    let count = 0;
    let bitMaskList = [];
    for(let i = 1; i < (1 << column); ++i) {
        let keySet = new Set();
        for(let j = 0; j < row; ++j) {
            let key = "";
            for(let k = 0; k < column; ++k) {
                if((i & (1 << k)) != 0) key += relation[j][k];
            }
            keySet.add(key);
        }
        if(keySet.size == row && duplcateCheck(bitMaskList, i)) ++count;
    }

    return count;
}

function duplcateCheck(list, key) {
    let size = list.length;
    for(let i=0; i<size; ++i) {
        if((list[i] & key) == list[i]) return false;
    }
    list.push(key);
    return true;
}
```

다들 `<<` left shift를 사용해서 어떤 경우에 사용하는지 잘 모르겠다.

```js
function solution(relation) {
    const colLen = relation[0].length

    const candidates = []

    combi(range(colLen)).forEach(cols => {
        if(hasParentCols(cols)) return
        const set = new Set()
        relation.map(r => cols.map(c => r[c]).join(',')).forEach(hash => set.add(hash))
        if(relation.length === set.size) candidates.push(cols)
    })

    return candidates.length;

    function hasParentCols(cols){
        return candidates.some(candidate => candidate.every(col => cols.includes(col)))
    }
}

function combi(set) {
  return (function acc(xs, set) {
    var x = xs[0];
    if(typeof x === "undefined")
      return set;
    for(var i = 0, l = set.length; i < l; ++i)
      set.push(set[i].concat(x));
    return acc(xs.slice(1), set);
  })(set, [[]]).slice(1);
}

function range(n){
    return [...Array(n).keys()]
}
```

그나마 제일 알아보기 쉬운 코드임.