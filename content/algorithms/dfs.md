+++ 
draft = true
date = 2019-01-20T00:35:46+05:30
title = "Depth First Search"
slug = ""
tags = ["algorithm"] 
+++
Depth-first search (DFS) is an algorithm for traversing or searching tree or graph data structures. One starts at the root (selecting some arbitrary node as the root in the case of a graph) and explores as far as possible along each branch before backtracking.

<!--more-->

<h3> Tutorials </h3>

<table>
  <tr>
    <th>Links</th>
  </tr>
  <tr>
      <td><a href="https://en.wikipedia.org/wiki/Depth-first_search">Wikipedia</a></td>
  </tr>
  <tr>
      <td><a href="https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/">GeeksforGeeks</a></td>
  </tr>
</table>


<h3> Complexity </h3>
<table>
  <tr>
    <th>Time Complexity (Worst case)</th>
    <th>Space Compexity (Worst case)</th>
  </tr>
  <tr>
    <td>O(V+E)</td>
    <td>O(V)</td>
  </tr>
</table>

<h3> Implementation </h3>

Before moving forward, try to implement it yourself. Both iterative and recursive implementations should not take more than 10 minutes combined.

<h4> Iterative </h4>


{{< highlight cpp "linenos=table, linenostart=1" >}}
struct Node{
    int id;                     //Unique ID for each node
    vector<Node *> neighbors;   //List of neighbor nodes
    bool visited;               //boolean status for each node
    Node(int id){
        this->id = id;
        this->visited = false;
    }
};

void dfs(Node * root){

    if (root == NULL) return;
    
    stack<Node *> buffer;
    buffer.push(root);
    
    while (!buffer.empty()){
        
        Node * cur_node = buffer.top();
        
        cout<<cur_node->id<<endl;

        cur_node->visited = true;
        buffer.pop();
        
        for (auto it = (cur_node->neighbors).begin(); it != (cur_node->neighbors).end(); it++){
            if (!it->visited) buffer.push(it);
        }
    }

    return;
}
{{< / highlight >}}

<h4> Recursive </h4>

{{< highlight cpp "linenos=table, linenostart=1" >}}
struct Node{
    int id;                     //Unique ID for each node
    vector<Node *> neighbors;   //List of neighbor nodes
    bool visited;               //boolean status for each node
    Node(int id){
        this->id = id;
        this->visited = false;
    }
};

void dfs(Node * root){
    if (root->visited) return;

    cout<< root->id <<endl;             
    cur_node->visited = true;

    for (auto it = (cur_node->neighbors).begin(); it != (cur_node->neighbors).end(); it++){
        dfs(it);
    }

    return;
}
{{< / highlight >}}


Note that we don't need a stack for the recursive implementation. Function stack acts as the stack data structure in this case. Again, recursive function is not tail recursive.

<h3> Quiz </h3>

<ul>
    <li> How do we handle disconnected graph for the DFS traversal? </li>
    <li> Can DFS be used to print all the paths from root to leaves? </li>
    <li> How many recursive calls does each call of DFS function makes? Is there an upper bound on the total number of recursive calls made?</li>
    <li> Can a DFS algorithm be used to detect cycles in an undirected graph? In a directed graph?</li>
    <li> What is the time and space complexity of DFS if we use adjacency matrix instead of adjacency list to represent the graph?</li>
    <li> How would you modify the code to store path information as well?</li>

</ul>

