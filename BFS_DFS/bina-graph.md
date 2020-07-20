### 判断二分图

![](/images/785.png)

#### DFS

```java
class Solution {
    private static final int UNCOLORED = 0;
    private static final int RED = 1;
    private static final int GREEN = 2;
    private int[] color;
    private boolean valid;

    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        valid = true;
        color = new int[n];
        Arrays.fill(color, UNCOLORED);
        for (int i = 0; i < n && valid; ++i) {
            if (color[i] == UNCOLORED) {
				//任选一个节点开始染成红色
                dfs(i, RED, graph);
            }
        }
        return valid;
    }

    public void dfs(int node, int c, int[][] graph) {
        color[node] = c;
		//获取相邻节点需要染成的颜色
        int cNei = c == RED ? GREEN : RED;
		//将当前节点的所有邻节点染色
        for (int neighbor : graph[node]) {
            if (color[neighbor] == UNCOLORED) {
                dfs(neighbor, cNei, graph);

                if (!valid) {
                    return;
                }
            } else if (color[neighbor] != cNei) {
				//只要遇到无法染色成功的情况就返回false
                valid = false;
                return;
            }
        }
    }
}
```
