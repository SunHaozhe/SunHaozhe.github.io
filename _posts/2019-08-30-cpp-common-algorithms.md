---
title: C++ code common algorithms
description: >
  C++
---

# Dijkstra

Assume `N` nodes, source node is indexed by `root`, using adjacency list

```
#include<climits> // INT_MAX
#include<vector>
#include<queue> // priority_queue
#include<<utility>> // pair
typedef pair<int, int> pii; // weight goes first 

vector<int> dist(N, INT_MAX);
dist[root] = 0;
priority_queue<pii, vector<pii>, greater<pii>> q;
q.push(make_pair(0, root));
while(!q.empty()){
  pii current = q.top();
  q.pop();
  for(pii neighbor : adj[current.second]){
    if(dist[neighbor.second] > dist[current.second] + neighbor.first){
      dist[neighbor.second] = dist[current.second] + neighbor.first;
      q.push(make_pair(dist[neighbor.second], neighbor.second));
    }
}
```

# Union Find



# Catalan number


# Fibonacci number 



# KMP  







