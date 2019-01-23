+++ 
draft = true
date = 2019-01-19T00:36:50+05:30
title = "Morris Traversal"
slug = "" 
+++
<p>As discussed before, there are various ways to traverse a binary tree. Inorder traversal is very popular as it visits nodes in a sorted manner if the tree is a binary search tree.</p>
<p>The common implementation of inorder traversal is by recursion. But recursive implementation is not considered to be O(1) space solution due to the recursion stack; it is in fact O(logN). Inorder traversal can also be implemented iteratively by using a stack data structure, but even this implementation will have O(N) space complexity. There exists an algorithm called Morris Traversal which guarantees iterative inorder traversal of a binary tree with O(1) space complexity.</p> 
<p> Note that this is a slightly advanced algorithm and should be considered only when the normal recursive implementation results in TLE.</p>
<!--more-->
<h3> Tutorials </h3>

<table>
  <tr>
    <th>Links</th>
  </tr>
  <tr>
      <td><a href="https://en.wikipedia.org/wiki/Threaded_binary_tree">Wikipedia</a></td>
  </tr>
  <tr>
      <td><a href="https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/">GeeksforGeeks</a></td>
  </tr>
</table>

<h3> Complexity </h3>
<table>
  <tr>
    <th>Time Complexity (Worst case)</th>
    <th>Space Compexity (Worst case)</th>
  </tr>
  <tr>
    <td>O(N)</td>
    <td>O(1)</td>
  </tr>
</table>

<h3> Specifics </h3>
<p>Morris traveral works by creating a threaded binary tree where we create a link from one node to its inorder successor. We create links as we move towards the left child, and then remove them as we go towards the right child to restore the original tree.
<p>Morris traversal, by creating extra links, ensures that when we reach a node that doesn't have a right child, we don't have to traverse the tree upwards to know which node to print next.
<h3> Implementation </h3>

{{< highlight cpp "linenos=table, linenostart=1" >}}
struct Node{
    int value;
    Node * left;
    Node * right;
};

/*
      Example Tree:
               1
             /   \
           2      3
         /  \
       4     5


           |           
           V

            1
          /   \ 
        2      3 
      /  \ 
    4     5 
     \     \
      2     1

*/

void MorrisTraversal(Node * root){
    Node * current = root;
    Node * previous = NULL;
    
    while(current != NULL){
        //Most basic condition: If left child doesn't exist, print current node and go to right child.
        if (current->left == NULL){
            cout << current->value <<endl;
            current = current -> right;
        }

        else{
            //previous pointer is used to find the previous node in inorder traversal
            previous = current->left;
            
            while (previous->right !=NULL && previous->right != current){
                previous = previous->right;
            }
            
            
            // previous->right == NULL would mean that we found the previous node in inorder traversal
            // Hence, we will create a link from this previous node to current node, making current node its right child.
            // we then move the current pointer to its left, and start the loop again. Basically, before moving to the left,
            // we had to make sure that we had a way to reach the current node again. That we did by creating a link.
            if (previous->right == NULL){
                previous->right = current;
                current = current->left;
            }


            // previous->right == current would mean that we had already processed the subtree in the left, hence we need to clear
            // the link. As we have processed the left subtree completely, we just have to print the current node, and move to its right.
            else{
                previous->right = NULL;
                cout<<current->value<<endl;
                current = current->right;
            }
        }
    }   
}

{{< / highlight >}}















