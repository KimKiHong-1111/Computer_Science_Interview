알고리즘

DFS, BFS
쉽게 개념을 알기위해서 비유를 하면,
어떤 드라마를 볼 때, 한 드라마를 끝까지 보는 스타일은 DFS,
여러 드라마를 한 편씩 보는 스타일은 BFS라고 할 수 있다.

깊이 우선 탐색 (DFS, Depth-First Search)
깊이 우선 탐색은 그래프나 트리에서 특정 노드에서 시작하여, 그 노드의 자식 노드를 먼저 탐색하는 방식의 알고리즘입니다. 이 방식은 한 방향으로 가능한 한 깊이 탐색한 후, 더 이상 진행할 수 없으면 이전 노드로 돌아와 다른 방향으로 탐색을 계속합니다.

주요 특징
구현 방법: DFS는 주로 재귀 함수 또는 스택을 이용해 구현됩니다. 재귀 함수는 코드가 간결하지만, 스택 오버플로우 위험이 있습니다. 스택을 사용하면 명시적으로 노드를 관리할 수 있습니다.

시간 복잡도: 인접 리스트를 사용하면 시간 복잡도가 O(V + E)입니다. 여기서 V는 노드의 개수, E는 간선의 개수입니다. 인접 행렬을 사용하면 O(V²)입니다.

장점:

메모리 효율성: 현재 경로상의 노드만 기억하면 되므로 메모리 사용량이 적습니다.

구현의 간결성: 재귀 함수로 구현할 경우 코드가 간결합니다.

깊은 경로 탐색: 목표 노드가 깊은 단계에 있을 경우 빠르게 발견할 수 있습니다.

단점:

최단 경로 보장 없음: 탐색 중에 발견한 경로가 최단 경로가 아닐 수 있습니다.

무한 루프 위험: 방문 여부를 체크하지 않으면 무한 루프에 빠질 수 있습니다.

활용 사례
경로의 특징 저장: 각 노드에 특정 조건이 있을 때, 경로 상의 노드를 기억해야 하는 문제에 적합합니다.

깊은 경로 탐색: 목표 노드가 깊은 단계에 있을 경우 빠르게 탐색할 수 있습니다.

백준 문제 중 n과m 구현을 예시로 넣었습니다.
```aiignore
public class Main {

    public static int[] arr;
    public static boolean[] visited;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int m = sc.nextInt();

        arr = new int[m];
        visited = new boolean[n];
        dfs(n,m,0);
    }

    public static void dfs(int n, int m , int depth) {
        if(depth == m) {
            for (int val : arr) {
                System.out.print(val + " ");
            }
            System.out.println();
            return;
        }

        for (int i = 0; i < n; i++) {
            if(!visited[i]) {
                visited[i] = true;
                arr[depth] = i + 1;
                dfs(n, m, depth + 1);
                visited[i] = false;
            }
        }
    }
}

```