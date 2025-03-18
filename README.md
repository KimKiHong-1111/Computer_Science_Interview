# Computer_Science_Interview
[면접 대비] 컴퓨터 공학 지식을 기록하는 공간입니다.

# 알고리즘
코딩 테스트에서는 잘 사용해도 정의에 대해 설명을 professional하게 하지 못하는 경우를 방지하기 위해 각 알고리즘의 정의를 기록 동빈나님의 알고리즘 강의 및 구글링 참조

## 깊이 우선 탐색(DFS, Depth-First Search)
- 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘

- 탐색 시작 노드에서 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방식

- 스택 자료구조 or 재귀 함수를 사용하며 구체적인 동작은 아래와 같음

- 탐색 시작 노드를 스택에 삽입하고 방문 처리

- 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리
방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼냄

- 더 이상 2번 과정을 수행할 수 없을 때까지 반복

