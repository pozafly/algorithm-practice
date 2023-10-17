# 두 큐 합 같게 만들기

> https://school.programmers.co.kr/learn/courses/30/lessons/118667

## 나의 답

```js
// sum 모든 합친 값 /2 를 해 각 큐를 더했을 경우 나와야 하는 수를 뽑는다.
// 1번 큐의 합을 다시 구해서 sum /2에서 값을 빼본다.
// 만약 - 일경우, 넘친다는 뜻으로 2번 큐에 넣어주어야 한다.
// + 일 경우, 부족하다는 뜻이므로, 2번 큐의 값을 가져와야 한다.
// 부족한 값이 채워지는지 확인한다.
// 두 수의 총 합이 홀수라면 서로의 값이 같아질 수 없다.
function sumArr(arr) {
  return arr.reduce((acc, cur) => acc + cur, 0);
}

function solution(queue1, queue2) {
  let queue1Sum = sumArr(queue1);
  let queue2Sum = sumArr(queue2);

  const sum = queue1Sum + queue2Sum;
  if (sum % 2 !== 0) return -1;
  const targetSum = sum / 2;

  let count = 0;
  while (true) {
    queue1Sum = sumArr(queue1);
    queue2Sum = sumArr(queue2);
    if (queue1Sum < queue2Sum) {
      queue1.unshift(queue2.pop());
    } else if (queue1Sum > queue2Sum) {
      queue2.unshift(queue1.pop());
    } else {
      return count;
    }
    count += 2;
  }
  // return -1;
}

console.log(solution([1, 2, 1, 2], [1, 10, 1, 2]));
```

틀림.

큐의 합을 계산하고, 합이 큰 부분의 원소를 빼 작은 부분에 추가하는 식으로 구현한다.

## 다른 답

![image](https://github.com/pozafly/algorithm-practice/assets/59427983/4be17c68-46bd-45bc-ba20-22afc669c5fe)

[출처](https://koguri.tistory.com/108)

- half를 뽑아내는 과정까지는 동일.
- `q` 는 큐1, 큐2 원소를 풀어 하나로 합친것과 동일하다. 그럼 위의 경우와 같이 포인터를 옮겨가며 대상을 판단할 수 있다.
- 단, for 문에서 왜 length * 3을 하는지는 이해가 가지 않는다. qPointer2는 len 부터 len * 2 까지 갈 수 있으므로 최대 len * 3 만큼 간다는게..

```js
const solution = (queue1, queue2) => {
  let sum1 = queue1.reduce((prev, cur) => prev + cur, 0);
  let sum2 = queue2.reduce((prev, cur) => prev + cur, 0);
  const half = (sum1 + sum2) / 2;
  const q = [...queue1, ...queue2];
  let q1Pointer = 0;
  let q2Pointer = queue1.length;

  for (let cnt = 0; cnt < queue1.length * 3; cnt++) {
    if (sum1 === half) {
      return cnt;
    }
    sum1 =
      sum1 > half
        ? sum1 - q[q1Pointer++ % q.length]
        : sum1 + q[q2Pointer++ % q.length];
  }

  return -1;
};
```

