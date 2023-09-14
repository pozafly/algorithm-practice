# 신고 결과 받기[2022 KAKAO BLIND RECRUITMENT]

https://school.programmers.co.kr/learn/courses/30/lessons/92334

## 나의 답

```js
function solution(id_list, report, k) {
  const table = id_list.map((v) => {
    return { id: v, reportId: new Set() };
  });

  report.forEach((v) => {
    const [id, reporter] = v.split(' ');
    const target = table.find((obj) => obj.id === id);
    target.reportId.add(reporter);
  });

  const result = new Map();
  table.forEach((v) => {
    v.reportId.forEach((id) => {
      result.get(id) ? result.set(id, result.get(id) + 1) : result.set(id, 1);
    });
  });

  const target = [...result].filter((v) => v[1] >= k).map((v) => v[0]);

  return table.reduce((acc, cur) => {
    let count = 0;
    target.forEach((v) => {
      if (cur.reportId.has(v)) count++;
    });
    return [...acc, count];
  }, []);
}
```

꽤 오래 걸렸고, 생각보다 복잡하게 풀었다..

## 다른 답

```js
function solution(id_list, report, k) {
    let reports = [...new Set(report)].map(a=>{return a.split(' ')});
    let counts = new Map();
    for (const bad of reports){
        counts.set(bad[1],counts.get(bad[1])+1||1)
    }
    let good = new Map();
    for(const report of reports){
        if(counts.get(report[1])>=k){
            good.set(report[0],good.get(report[0])+1||1)
        }
    }
    let answer = id_list.map(a=>good.get(a)||0)
    return answer;
}
```

- `[...new Set(report)]` 이것으로 애초부터 걸러냈고, map으로 이어서 바로 가공했다.
- 나머지는 비슷.