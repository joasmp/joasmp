import java.util.Arrays;

public class HamiltonianCycle {

    private static final int V = 9;

    private static boolean isValid(int v, boolean[] visited) {
        return !visited[v];
    }

    private static void hamiltonianCycleUtil(int[][] graph, boolean[] visited, int[] path) {
        int v = 0;
        for (int i = 0; i < V; i++) {
            if (isValid(i, visited)) {
                v = i;
                break;
            }
        }

        int pos = 0;
        path[pos++] = v;

        visited[v] = true;

        for (int i = 0; i < V; i++) {
            if (graph[v][i] == 1 && isValid(i, visited)) {
                path[pos++] = i;
                visited[i] = true;
                v = i;
                break;
            }
        }

        boolean done = false;
        for (int i = 0; i < V; i++) {
            if (graph[v][i] == 1 && isValid(i, visited)) {
                int nextVertex = i;
                int nextIndex = Arrays.binarySearch(path, 0, pos, nextVertex);
                if (nextIndex < 0) {
                    hamiltonianCycleUtil(graph, visited, path);
                    done = true;
                    break;
                }
            }
        }

        if (!done) {
            if (path[pos - 1] == path[0]) {
                for (int i = 0; i < pos; i++) {
                    System.out.print(path[i] + " ");
                }
                System.out.println();
            } else {
                System.out.println("Solution does not exist");
            }
        }
    }

    public static void main(String[] args) {
        int[][] graph = {
                {0, 1, 1, 1, 0, 0, 0, 0, 0},
                {1, 0, 1, 0, 0, 0, 0, 0, 0},
                {1, 1, 0, 1, 0, 0, 0, 0, 0},
                {1, 0, 1, 0, 0, 0, 0, 0, 0},
                {0, 0, 0, 0, 0, 1, 1, 1, 0},
                {0, 0, 0, 0, 1, 0, 1, 0, 0},
                {0, 0, 0, 0, 1, 1, 0, 1, 0},
                {0, 0, 0, 0, 1, 0, 1, 0, 0},
                {0, 0, 0, 0, 0, 0, 0, 0, 0}
        };

        boolean[] visited = new boolean[V];
        int[] path = new int[V];

        hamiltonianCycleUtil(graph, visited, path);
    }
}
