# [3차] 방금그곡

> https://school.programmers.co.kr/learn/courses/30/lessons/17683

## 나의 답

```js
function convertProcess(value) {
  value = [...value];
  let result = [];
  for (let i = 0; i < value.length; i++) {
    if (value[i + 1] === '#') {
      result.push(`${value[i]}#`);
      value.splice(i + 1, 1);
    } else {
      result.push(value[i]);
    }
  }
  return result;
}

function getDifferenceTime(startTime, endTime) {
  const [startHour, startMinute] = startTime.split(':');
  const [endHour, endMinute] = endTime.split(':');
  return (endHour - startHour) * 60 + (endMinute - startMinute);
}

function solution(m, musicinfos) {
  m = convertProcess(m);
  const songs = [];
  musicinfos.forEach((musicinfo) => {
    let [start, end, title, process] = musicinfo.split(',');
    const runTime = getDifferenceTime(start, end);
    process = convertProcess(process);

    let curcular = runTime;
    const realProcess = [];
    for (let i = 0; i < curcular; i++) {
      const index = process.length <= i ? i % process.length : i;
      realProcess.push(process[index]);
    }

    songs.push({
      title,
      runTime,
      process: realProcess,
    });
  });

  const resultArr = songs
    .sort((a, b) => {
      if (a.runTime === b.runTime) {
        return 0;
      }
      return b.runTime - a.runTime;
    })
    .filter((song) => {
      for (let i = 0; i < song.process.length; i++) {
        if (m[0] === song.process[i]) {
          let temp = true;
          for (let j = 1; j < m.length; j++) {
            if (m[j] !== song.process[i + j]) {
              temp = false;
              break;
            }
          }
          return temp;
        }
      }
    });

  return resultArr.length > 0 ? resultArr[0].title : '(None)';
}

// console.log(
//   solution('ABC', ['12:00,12:14,HELLO,C#DEFGAB', '13:00,13:05,WORLD,ABCDEF'])
// );
// console.log(
//   solution('ABCDEFG', ['11:50,12:04,HELLO,CDEFGAB', '12:57,13:11,BYE,CDEFGAB'])
// );
console.log(solution('A#', ['13:00,13:02,HAPPY,B#A#']));
// console.log(
//   solution('CC#BCC#BCC#BCC#B', [
//     '03:00,03:30,FOO,CC#B',
//     '04:00,04:08,BAR,CC#BCC#BCC#B',
//   ])
// );
```

틀렸다.

## 다른 답

```js
function solution(m, musicinfos) {
    m = m.replace(/(C|D|F|G|A)#/g, (_, a) => a.toLowerCase());
    musicinfos = musicinfos
        .map((music) => {
            let [start, end, title, melody] = music.split(',');
            let h = end.slice(0, 2) - start.slice(0, 2);
            let m = end.slice(3) - start.slice(3);
            const time = h * 60 + m;
            melody = melody.replace(/(C|D|F|G|A)#/g, (_, a) => a.toLowerCase());
            return [time, title, melody.padEnd(time, melody).slice(0, time)];
        })
        .filter(([_, $, melody]) => melody.indexOf(m) >= 0)
        .sort(([a], [b]) => b - a);
    return musicinfos[0]?.[1] || '(None)';
}
```

너무 간단하잖아. 도대체..

- `C#` 같은 것을 #을 떼어내고 소문자로 바꾼다.
- 시간을 구한다.
- `padEnd` 메서드를 사용해 melody를 채워주고, 잘라준다.
- 멜로디를 m과 비교해 필터링한다.
- 소팅한다.