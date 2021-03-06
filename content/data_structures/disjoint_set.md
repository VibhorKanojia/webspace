+++ 
draft = true
date = 2019-01-20T21:19:06+05:30
title = "Disjoint Set"
description = ""
slug = "" 
tags = ["Data Structures"]
+++
<p>Facebook has more than 2 billion users and, very often, given two users A and B, Facebook needs to find if A and B are connected. Such information can be really useful in features like friend suggestions, privacy protections, and various data analysis tasks.</p>
<p>One way to approach this problem is by doing a BFS, starting with A as source node and expanding the graph by visiting A's friends and stopping the search when we reach B. This approach will work for small datasets, but when you consider over 2 billion users each having around 500 friends, BFS ends up using a lot of space, and unnecessary expansion of graph leads to performance degradation. For example, imagine a scenario where A is infact not connnected to B! </p>
<p>One can think of various optimizations to improve the performance, and develop better heuristics to guide the graph expansion (A* algorithm), but it still won't give the satisfactory results. Keep in mind that the graph is not static, and the graph may have new connections over time.</p>
<p> What if we could answer this query in O(logN) time? Even better, what if we could answer this query in O(1) time?</p>
<p><i>Disjoint Sets to the rescue</i></p>
<!--more-->

<h3> Specifics </h3>
<p>Let's consider a graph of N nodes, where each node is isolated initially. We need to implement 2 functions:</p>
<ol>
    <li><b>Connect(node A, node B):</b> Connects nodes A and B; as a result, all connections of B are also connected to A and vice-versa</li>
    <li><b>Find(node A, node B):</b> Finds out if nodes A and B are connected</li>
</ol>
<p>Disjoint Set data structure assigns a root node for each group of connected nodes. To connect nodes A and B, we merge the two groups and assign a root node to the new group. To check if node A is connected to node B, we see if the root of A is the same as the root of B (because this will imply that nodes A and B are in the same group).</p>

<h3> Implementation </h3>
<p>Disjoint Set data structure maintains a vector of size N to store the root of each group. Initially we have N isolated groups with each node being the root of its group. We just change the root nodes accordingly when we connect two nodes.</p>
{{< highlight cpp "linenos=table, linenostart=1" >}}

/* O(N) time complexity in the worst case */
int getRoot(int A, vector<int> & DS){
    
    while (DS[A] != A) A = DS[A];  /* Keep moving up until we reach the root. */
    
    return A;
}


void Connect(int A, int B, vector<int> & DS){
    
    int rootA = getRoot(A,DS);
    
    int rootB = getRoot(B,DS);

    DS[rootB] = rootA;        /*Change the root of the rootB to the root of the rootA, effectively merging the groups together */
}


void Find(int A, int B){
    
    int rootA = getRoot(A,DS);

    int rootB = getRoot(A,DS);

    return (rootA == rootB);
}
{{< / highlight >}}

<p>The above code is the basic implementation of disjoint set data structure and algorithm. But as you can notice, getRoot function has worst case time complexity of O(N). And hence, both Connect and Find functions also become O(N) in the worst case. We can improve this by using two heuristics, union by rank and path compression.</p>

<h5> Union by Rank </h5>
<p>The idea in the first heuristic, union by rank, is to make the root of the tree with fewer nodes point to the root of the tree with more nodes. To implement this, we need to maintain the rank of each group in another vector. With each node x, we keep the integer value rank[x], which is bigger than or equal to the number of edges in the longest path between node x and a sub-leaf. In other words, rank[x] is an upper bound on the height of the node x. This will make sure that the tree formed is balanced, thereby, reducing the complexity of getRoot function to O(logN) in the worst case.</p>

<h5> Path Compression </h5>
<p>The idea of path compression is to flatten the structure everytime we traverse the tree. This is done by making each node point to root directly. This reduces the complexity of getRoot function to O(log*N).</p>
<p>O(log*N) is the number of log functions needed to make N equal to 1. log*(2<sup>65536</sup>) = 5. Therefore, for every practical purpose, O(log*N) ~ O(1).</p>
<p>Note that this step doesn't change the rank of a node.</p>

<p>The code below uses both of these heuristics to significantly improve the performance of the disjoint set data structure. Rank of each group is set to 0 initially.</p>

{{< highlight cpp "linenos=table, linenostart=1" >}}

/* O(log*N) time complexity in the worst case */
int getRoot(int A, vector<int> & DS){
    
    if (DS[A] != A) DS[A] = getRoot(DS[A], DS); /* Path compression */

    return DS[A];
 
}


void Connect(int A, int B, vector<int> & DS, vector<int> & rank){
    
    int rootA = getRoot(A,DS);
    
    int rootB = getRoot(B,DS);
    
    /* Union by rank */
    if (rank[A] < rank[B]) DS[rootA] = rootB;
    
    else if (rank[B} < rank[A]) DS[rootB] = rootA;
    
    /* Ranks only change when both groups were of same rank before merging */
    else {
        DS[rootA] = rootB;
        rank[rootB] += 1;
    }

    return;
}


void Find(int A, int B){
    
    int rootA = getRoot(A,DS);

    int rootB = getRoot(A,DS);

    return (rootA == rootB);
}
{{< / highlight >}}


<h3> External Tutorials </h3>

<table>
  <tr>
    <th>Links</th>
  </tr>
  <tr>
      <td><a href="https://www.topcoder.com/community/data-science/data-science-tutorials/disjoint-set-data-structures/">Topcoder</a></td>
  </tr>
  <tr>
      <td><a href="https://www.geeksforgeeks.org/union-find/">GeeksforGeeks</a></td>
  </tr>
</table>
