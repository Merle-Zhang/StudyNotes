# LeetCode

### 733. Flood Fill

https://leetcode.com/problems/flood-fill/

Java DFS loop:

```java
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        if (image[sr][sc] != newColor) dfs(image, new Pair(sr, sc), newColor);
        return image;
    }
    
    public void dfs(int[][] image, Pair<Integer, Integer> start, int newColor) {
        int oldColor = image[start.getKey()][start.getValue()];
        Stack<Pair<Integer, Integer>> stack = new Stack<>();
        boolean[][] isVisited = new boolean[image.length][image[0].length];
        stack.push(start);
        while(!stack.isEmpty()) {
            Pair<Integer, Integer> current = stack.pop();
            isVisited[current.getKey()][current.getValue()] = true;
            visit(current, image, newColor);
            for (Pair<Integer, Integer> dest : getAdj(current, image, oldColor)) {
                if (!isVisited[dest.getKey()][dest.getValue()]) {
                    stack.push(dest);
                }
            }
        }
    }
    
    private void visit(Pair<Integer, Integer> current, int[][] image, int newColor) {
        image[current.getKey()][current.getValue()] = newColor;
    }
        
    private List<Pair<Integer, Integer>> getAdj(Pair<Integer, Integer> current, int[][] image, int oldColor) {
        int i = current.getKey();
        int j = current.getValue();
        List<Pair<Integer, Integer>> adj = new ArrayList<>();
        
        if (i+1 < image.length && image[i+1][j] == oldColor) {
            adj.add(new Pair(i+1, j));
        }
        if (i-1 >= 0 && image[i-1][j] == oldColor) {
            adj.add(new Pair(i-1, j));
        }
        if (j+1 < image[0].length && image[i][j+1] == oldColor) {
            adj.add(new Pair(i, j+1));
        }
        if (j-1 >= 0 && image[i][j-1] == oldColor) {
            adj.add(new Pair(i, j-1));
        }
        return adj;
    }
}
```

* Graph DFS with Recursion

  * ```java
    public void dfs(int start) {
        boolean[] isVisited = new boolean[adjVertices.size()];
        dfsRecursive(start, isVisited);
    }
     
    private void dfsRecursive(int current, boolean[] isVisited) {
        isVisited[current] = true;
        visit(current);
        for (int dest : adjVertices.get(current)) {
            if (!isVisited[dest])
                dfsRecursive(dest, isVisited);
        }
    }
    ```

* Graph DFS Without Recursion

  * ```java
    public void dfsWithoutRecursion(int start) {
        Stack<Integer> stack = new Stack<Integer>();
        boolean[] isVisited = new boolean[adjVertices.size()];
        stack.push(start);
        while (!stack.isEmpty()) {
            int current = stack.pop();
            isVisited[current] = true;
            visit(current);
            for (int dest : adjVertices.get(current)) {
                if (!isVisited[dest])
                    stack.push(dest);
            }
        }
    }
    ```

