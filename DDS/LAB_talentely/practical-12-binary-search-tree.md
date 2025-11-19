Practical: 12 - Implement Graph with BFS and DFS Traversals
```
#include <bits/stdc++.h>
using namespace std;

class Graph {
    int n; // number of vertices
    vector<vector<int>> adjList;   // adjacency list
    vector<vector<int>> adjMatrix; // adjacency matrix

public:
    Graph(int n) {
        this->n = n;
        adjList.resize(n + 1);
        adjMatrix.assign(n + 1, vector<int>(n + 1, 0));
    }

    void addEdge(int u, int v) {
        // For adjacency list
        adjList[u].push_back(v);
        adjList[v].push_back(u); // undirected

        // For adjacency matrix
        adjMatrix[u][v] = 1;
        adjMatrix[v][u] = 1;
    }

    void printAdjList() {
        cout << "Adjacency List:\n";
        for (int i = 1; i <= n; i++) {
            cout << i << " -> ";
            for (int v : adjList[i]) {
                cout << v << " ";
            }
            cout << "\n";
        }
        cout << "\n";
    }

    void printAdjMatrix() {
        cout << "Adjacency Matrix:\n";
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {
                cout << adjMatrix[i][j] << " ";
            }
            cout << "\n";
        }
        cout << "\n";
    }

    void BFS(int start) {
        vector<bool> visited(n + 1, false);
        queue<int> q;

        cout << "BFS: ";
        visited[start] = true;
        q.push(start);

        while (!q.empty()) {
            int u = q.front();
            q.pop();
            cout << u << " ";

            for (int v : adjList[u]) {
                if (!visited[v]) {
                    visited[v] = true;
                    q.push(v);
                }
            }
        }
        cout << "\n";
    }

    void DFSUtil(int u, vector<bool> &visited) {
        visited[u] = true;
        cout << u << " ";
        for (int v : adjList[u]) {
            if (!visited[v]) {
                DFSUtil(v, visited);
            }
        }
    }

    void DFS(int start) {
        vector<bool> visited(n + 1, false);
        cout << "DFS: ";
        DFSUtil(start, visited);
        cout << "\n";
    }
};

int main() {
    int n, m;
    cin >> n >> m;

    Graph g(n);

    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        g.addEdge(u, v);
    }

    int start;
    cin >> start;

    g.printAdjList();
    g.printAdjMatrix();
    g.BFS(start);
    g.DFS(start);

    return 0;
}
```
