이분탐색 알고리즘
====================

## 이분탐색 알고리즘이란?

UP DOWN 게임 같이 범위를 나눠가면서 찾는 방식

* 정렬된 데이터에서 필요한 값을 찾거나, 혹은 필요한 숫자를 찾을 때 사용
* 개념 자체가 명확하고 직관적인 만큼 코드도 간단합니다. 
* 일단 찍어놓고 그 값이 맞는지 찾아가는 과정

`근데.. 이 문제를 이분탐색으로 풀어야되는 지 어떻게 알아?`

## 무엇을 이분탐색으로 찾을까?
#### 실제 문제에서의 활용

*근데 문제들 보니까 '**최댓값**을 구하시오' 할 때 이분탐색을 많이 활용하는 것 같다...*

*아니 근데 **최솟값** 구하기 할때도 쓰이던데...*

*아니면 숫자 찾기 하거나...*

1. 백준 입국심사 문제 [문제(링크)](https://programmers.co.kr/learn/courses/30/lessons/43238)
********************************
'무엇을 이분탐색을 찾을 것인가?'
* 최종 걸린 시간을 안다면 반대로 몇명이 지나갈 수 있는 지 알 수 있다.
* '심사관들에게 주어지는 시간'
* 어떤 시간이 주어졌을 때 심사관들이 몇 명을 심사할 수 있는지를 계산할 수 있기 때문에 몇 명을 심사할 수 있는 지를 주어진 n과 비교해 n보다 크면 시간을 줄이고, n보다 작으면 시간을 늘이는 식
* 시간을 찾는 방법은 이분탐색

```python
N, M = map(int, input().split())

times = []
for i in range(N):
    time = int(input())
    times.append(time)

left = 1
right = min(times)*M
result  = right
while(left < right):
    mid = (left+right)//2
    people = 0
    for i in range(N):
        people += mid//times[i]

    if people >= M:
        right = mid
    else: 
        left = mid + 1
print(left)
```
시간초과 에러나긴 하는데,,,ㅠㅜ

2. 백준 나무 자르기 문제 [문제(링크)](https://www.acmicpc.net/problem/2805)
*****************************
'문제 푸는 요령'
* 유추한 정답 후보를(mid값) 문제에 대입해서 가장 적당한 정답값을 이끌어내는 방법
* 정답 후보를 유추하는 과정에서 이분탐색을 사용한다.
* 초기 left는 0이고, right는 tree들의 max값
* 이분탐색으로 정답 후보를 뽑고 그 후보로 나무를 잘라서 우리가 필요한 통나무 길이인 M과 비교한다.
* if(mid > M) 이라면, 더 작은 값을 탐색 / if(mid < M) 이라면, 결과값을 저장한 후, 더 큰 값을 탐색한다!