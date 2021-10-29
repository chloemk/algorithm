# Programmers 실패율

## 문제 이해

- 게임의 실패율을 구하는 문제이다.
- 실패율은 스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수 / 스테이지에 도달한 플레이어 수 이다.
- 만약 실패율이 같은 스테이지가 있다면 작은 번호의 스테이지가 먼저 오도록 한다.
- 스테이지에 도달한 유저가 없으면 해당 스테이지의 실패율은 0이다.

## 계획

- 스테이지 개수인 N만큼의 길이의 배열을 만든다.
- map 함수를 이용해 생성한 배열에 요소들을 채운다.
- 현재 스테이지에 도전했던 사람들의 수 stages.length를 구해준다.
- 현재 스테이지보다 +1보다 큰 요소들만 filter 함수로 걸러준다.
- 그러면 현재 스테이지를 성공한 사람들만 배열에 남게된다.
- (현재 스테이지에 도전했던 사람들의 수 - 현재 스테이지를 성공한 사람의 수) = (현재 스테이지를 클리어하지 못하고 다음 스테이지로 넘어가지 못한 사람)
- (현재 스테이지를 클리어하지 못하고 다음 스테이지로 넘어가지 못한 사람) / (현재 스테이지에 도전했던 사람들의 수) = (실패율)
- 실패율을 구한 후, 각 스테이지와 실패율을 배열안 객체로 만든다.
- 실패율이 높은 스테이지부터 내림차순으로 만든다.
- 실패율이 같은 경우에는 작은 번호의 스테이지가 먼저 오도록 한다.
- 정렬된 배열 객체들을 map 함수를 사용해 스테이지 넘버만 리턴한다.

## 느낀점

- 초기화 된 객체 만드는 2가지 방법

```js
let obj = {};
let numArr = Array.from({ length: N }, (v, i) => i + 1);
for (const key of numArr) {
	obj[key] = 0;
} //{1: 0, 2: 0, 3: 0, 4: 0, 5: 0}
```

```js
let obj = {};
for (let i = 1; i <= N; i++) {
	obj[i] = 0;
}
```

- 첫 시도 해본 코드. 실패했다.

```js
function solution(N, stages) {
	let result = [];

	let obj = {};
	let numArr = Array.from({ length: N }, (v, i) => i + 1);
	for (const key of numArr) {
		obj[key] = 0;
	} //{1: 0, 2: 0, 3: 0, 4: 0, 5: 0}

	stages = stages.sort((a, b) => a - b);

	//stages 배열이 비워질 때까지 순회
	while (!stages.length) {
		if (stages.includes(N + 1)) {
		}
		//1, 2, 3, 4, 5
		for (const key of obj) {
			//스테이지에는 키를 가지고 있나?
			if (stages.includes(key)) {
				//있으면 value에 1을 더해주고
				obj[key] += 1;
				//스테이지에서 그 요소를 제거해준다
				stages.shift();
			}
		}
	}
}
```