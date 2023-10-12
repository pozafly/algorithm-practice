# 괄호 반환

> https://school.programmers.co.kr/learn/courses/30/lessons/60058

## 나의 답

틀림

```js
const dividRightString = (string) => {
  string = [...string];
  let left = 0;
  let right = 0;

  for (let i = 0; i < string.length; i += 1) {
    if (left !== 0 && left === right) break;
    if (string[i] === '(') left++;
    if (string[i] === ')') right++;
  }

  return {
    u: string.splice(0, left * 2).join(''),
    v: string.join(''),
  };
};

const isCorrectString = (string) => {
  const stack = [];
  [...string].forEach((v) => {
    if (stack.at(-1) === '(' && v === ')') stack.pop();
    else stack.push(v);
  });
  return stack.length === 0 ? true : false;
};

function solution(s, result = '') {
  const { u, v } = dividRightString(s);
  if (!v) return u;

  if (isCorrectString(u)) {
    result += u;
    return solution(v, result);
  } else {
    const middle = [...u].splice(1);
    middle.pop();
    let string = `(${middle.reverse().join('')})`;
    string += solution(v);
    result += string;
  }
  return result;
}

// console.log(solution('()))((()'));
console.log(solution('(()())()'));
// console.log(solution(')))(((()(())))))((()'));

```

---

## 다른 답

```js
const solution = (p) => {
  return executeAsTheProblemDemands(p);  
};

const executeAsTheProblemDemands = (p) => {  
  // 1. 입력이 빈 문자열일 경우, 빈 문자열을 반환합니다.
  if (p.length === 0) {
    return "";
  }

  // 2. 문자열 w를 두 "균형잡힌 괄호 문자열" u, v로 분리합니다.
  // 단, u는 "균형잡힌 괄호 문자열"로 더 이상 분리할 수 없어야 하며,
  // v는 빈 문자열이 될 수 있습니다. 
  let openCount = 0;
  let closeCount = 0;
  let v = p.split("")
  let u = [];
  while(true) {
    let current = v.shift();

    if (current === "(") {
      u.push(current);
      openCount += 1;
    } else {
      u.push(current);
      closeCount += 1;
    }

    if (openCount > 0 && closeCount > 0 && openCount === closeCount) {
      u = u.join("");
      v = v.join("");
      break;
    }
  }

  // 3. 문자열 u가 "올바른 괄호 문자열" 이라면 문자열 v에 대해 1단계부터 다시 수행합니다. 
  // 3-1. 수행한 결과 문자열을 u에 이어 붙인 후 반환합니다. 
  if (u.charAt(0) === "(") {
    return u + executeAsTheProblemDemands(v);
  }

  // 4. 문자열 u가 "올바른 괄호 문자열"이 아니라면 아래 과정을 수행합니다. 
  // 4-1. 빈 문자열에 첫 번째 문자로 '('를 붙입니다. 
  // 4-2. 문자열 v에 대해 1단계부터 재귀적으로 수행한 결과 문자열을 이어 붙입니다. 
  // 4-3. ')'를 다시 붙입니다. 
  return "(" + executeAsTheProblemDemands(v) + ")" + transformU(u);
}

const transformU = (u) => {
  // 4-4. u의 첫 번째와 마지막 문자를 제거하고, 나머지 문자열의 괄호 방향을 뒤집어서 뒤에 붙입니다. 
  // 4-5. 생성된 문자열을 반환합니다.
  const str1 = u.substring(1, u.length - 1);
  const str2 = str1.replace(/\(/g, "!");
  const str3 = str2.replace(/\)/g, "(");
  const str4 = str3.replace(/\!/g, ")");

  return str4;
}
```

- 나랑 거의 동일하게 풀었다. 다만, while 문을 썼으며, while문의 break 까지 걸려 있었기 때문에 잘 통과 될 수 있었음. 위와 같은 식으로 해야 한다.