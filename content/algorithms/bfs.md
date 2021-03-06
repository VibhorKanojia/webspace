+++ 
draft = true
date = 2019-01-20T00:35:46+05:30
title = "Breadth First Search"
slug = "" 
+++
Breadth-first search (BFS) is an algorithm for traversing or searching tree or graph data structures. It starts at the tree root (or some arbitrary node of a graph) and explores the neighbor nodes first, before moving to the next level neighbors.
<!--more-->
<h3> Tutorials </h3>

<table>
  <tr>
    <th>Links</th>
  </tr>
  <tr>
      <td><a href="https://en.wikipedia.org/wiki/Breadth-first_search">Wikipedia</a></td>
  </tr>
  <tr>
      <td><a href="https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/">GeeksforGeeks</a></td>
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

void bfs(Node * root){

    if (root == NULL) return;
    
    queue<Node *> buffer;
    buffer.push(root);
    
    while (!buffer.empty()){
        
        Node * cur_node = buffer.front();
        
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


//NOTE: buffer will initially contain the root/source node

void bfs(queue<Node *> & buffer){
    
    Node * cur_node = buffer.front();

    cout<<it->id<<endl;

    buffer.pop();               
    cur_node->visited = true;

    for (auto it = (cur_node->neighbors).begin(); it != (cur_node->neighbors).end(); it++){
        if (!it->visited) buffer.push(it);
    }

    if (!buffer.empty()) bfs(buffer);
    return;
}

{{< / highlight >}}

Note that the recursive implementation is linearly recursive and, in the worst case, will fill the stack with recursive calls, greatly affecting the time and space complexities.

<h3> Quiz </h3>

<ul>
    <li> Why do we need to store which nodes are visited? </li>
    <li> Can BFS be used to print level-order traversal of a tree? Without using extra space or modifying the Node struct? </li>
    <li> Can the recursive implementation modified to be tail recursive? What changes need to be made? </li>
    <li> Can a BFS algorithm be used to detect cycles in an undirected graph? In a directed graph?</li>
    <li> What is the time and space complexity of BFS if we use adjacency matrix instead of adjacency list to represent the graph?</li>
</ul>

<h4> Questions </h4>


<table>
  <tr>
    <th>Title</th>
    <th>LeetCode</th>
    <th>C++ Solution</th>
  </tr>
  {% for post in site.tags.BFS %}
  <tr>
      <td>{{post.title}}</td>
      <td><a href={{post.leetcode}}>Link</a></td>
      <td><a href={{post.solution}}>Link</a></td>
  </tr>  
  {% endfor %}
</table>
