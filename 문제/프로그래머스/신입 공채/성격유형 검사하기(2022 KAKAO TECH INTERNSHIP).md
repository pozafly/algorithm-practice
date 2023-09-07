# 성격유형 검사하기(2022 KAKAO TECH INTERNSHIP)

https://school.programmers.co.kr/learn/courses/30/lessons/118666

## 나의 답

```javascript
const SURVEYS = [
  { R: 0, T: 0 },
  { C: 0, F: 0 },
  { J: 0, M: 0 },
  { A: 0, N: 0 },
];

function solution(survey, choices) {
  let answer;
  let temp = [];

  for (let i = 0; i < survey.length; i++) {
    const score = choices[i];
    const target = [...survey[i]];
    if (score >= 1 && score <= 3) {
      temp.push({ [target[0]]: score === 1 ? 3 : score === 3 ? 1 : score });
    } else if (score >= 5) {
      temp.push({ [target[1]]: score - 4 });
    }
  }

  temp.forEach((v) => {
    const key = Object.keys(v)[0];
    const findIndex = SURVEYS.findIndex((v) => Object.hasOwn(v, key));
    SURVEYS[findIndex][key] += v[key];
  });

  answer = SURVEYS.reduce((acc, cur) => {
    if (cur[Object.keys(cur)[0]] >= cur[Object.keys(cur)[1]]) {
      cur = Object.keys(cur)[0];
    } else {
      cur = Object.keys(cur)[1];
    }
    return acc + cur;
  }, '');

  return answer;
}
```

아래와 같은 형태로 만들어서 풀었다.

- temp : `[ { N: 1 }, { C: 1 }, { M: 2 }, { T: 3 }, { A: 1 } ]`
- SURVEYS : `[ { R: 0, T: 3 }, { C: 1, F: 0 }, { J: 0, M: 2 }, { A: 1, N: 1 } ]`

## 다른 답

```js
function solution(survey, choices) {
    const MBTI = {};
    const types = ["RT","CF","JM","AN"];
  
    types.forEach((type) =>
        type.split('').forEach((char) => MBTI[char] = 0)
    )

    choices.forEach((choice, index) => {
        const [disagree, agree] = survey[index];
        MBTI[choice > 4 ? agree : disagree] += Math.abs(choice - 4);
    });
    return types.map(([a, b]) => MBTI[b] > MBTI[a] ? b : a).join("");
}
```

- `Math.abs` : 절대 값을 이용해서 풀었다. 절대 값을 이용하면, `score` 조건문이 붙지 않아도 된다.
- map을 이용해서 가공했다. 굳이 reduce를 사용하지 않아도 된다.

```js
function solution(survey, choices) {
    const data = { R: 0, T: 0, C: 0, F: 0, J: 0, M: 0, A: 0, N: 0 }

    for (let i = 0; i < survey.length; i++) {
        const score = choices[i] - 4
        let type = survey[i].split('')[score < 0 ? 0 : 1] 
        data[type] += Math.abs(score)
    }

    const { R, T, C, F, J, M, A, N } = data
    return `${R >= T ? 'R' : 'T'}${C >= F ? 'C' : 'F'}${J >= M ? 'J' : 'M'}${A >= N ? 'A' : 'N'}`
}
```

- data는 나와 똑같이 만들었다. 이 분도 Math.abs 사용함.

```js
function solution(survey, choices) {
    var answer = '';
    let indi = new Map();
    ['R','T', 'C','F', 'J','M', 'A', 'N'].forEach(item => indi.set(item, 0));

    choices.forEach((item,index) => {
        let [A, B] = survey[index].split('');
        if(item > 4) indi.set(B, indi.get(B)+item-4);
        else if(item < 4) indi.set(A, indi.get(A)+4-item);
    })
    answer += indi.get('R') >= indi.get('T') ? 'R' : 'T';
    answer += indi.get('C') >= indi.get('F') ? 'C' : 'F';
    answer += indi.get('J') >= indi.get('M') ? 'J' : 'M';
    answer += indi.get('A') >= indi.get('N') ? 'A' : 'N';
    return answer;
}
```

Map 을 이용한 방법도 있다. Map이 보기에 가장 깔끔해보인다.