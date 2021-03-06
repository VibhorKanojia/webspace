+++ 
draft = true
date = 2019-01-20T17:18:39+05:30
title = "Binary Tree"
description = ""
slug = "" 
tags = ["Data Structures"]
+++
<p>Unlike Arrays, Linked Lists, Stacks and Queues, which are linear data structures, trees are hierarchical data structures. Many real world datasets are hierarchical by nature and it makes more sense to store them in a tree data structure. I'll be discussing a special type of trees, Binary Trees.</p> 
<!--more-->
<h3> Types </h3>
Binary Trees have only one root node, and each node has at most two children nodes. Following are common types of Binary Trees:
<ul>
    <li><b>Full Binary Tree:</b> A Binary Tree is full if every node has zero or two children. In such a tree, #Leaves = #InternalNodes + 1</li>
    <li><b>Complete Binary Tree:</b> A Binary Tree is complete Binary Tree if all levels are completely filled except possibly the last level and the last level has all keys as left as possible</li>
    <li><b>Perfect Binary Tree:</b> A Binary tree is Perfect Binary Tree in which all internal nodes have two children and all leaves are at same level. Such a tree has 2<sup>h</sup>-1 nodes, where h is the height of the tree</li>
    <li><b>Degenerate Tree:</b> A Tree where every internal node has one child. Such trees are performance-wise same as linked list</li>
</ul>    

<h3> Binary Search Trees </h3>
<p>A Binary Search Tree additionally satisfies the binary search property, which states that the key in each node must be greater than or equal to any key stored in the left sub-tree, and less than or equal to any key stored in the right sub-tree. This property really improves the average case time complexity for inserting, deleting, searching a node in the data structure. However, the complexity doesn't change in the worst case scenario where the tree is a Degenerate tree.</p>

<table>
  <tr>
    <th> Operation </th>
    <th>Time Complexity (Average Case)</th>
    <th>Time Complexity (Worst case)</th>
  </tr>
  <tr>
    <td> Insertion</td>
    <td>O(logN)</td>
    <td>O(N)</td>
  </tr>
  <tr>
    <td> Deletion</td>
    <td>O(logN)</td>
    <td>O(N)</td>
  </tr>
  <tr>
    <td> Search</td>
    <td>O(logN)</td>
    <td>O(N)</td>
  </tr>
</table>

<h3> Implementation </h3>
Implementation of the above three operations should not take more than 10 minutes.

{{< highlight cpp "linenos=table, linenostart=1" >}}

struct Node{
    int key;
    Node * left;
    Node * right;
    Node * parent;
    Node(int key, Node * parent){
        this->key = key;
        left = NULL;
        right = NULL;
        this->parent = parent;
    }
};

Node * insert(Node * root, int val, Node * parent){
    if (root == NULL) return new Node(val, parent);

    if (root->key >= val) root->left = insert(root->left, val, root);

    else root->right = insert(root->right, val, root);

    return root;
}

Node * search(Node * root, int val){
    if (root == NULL) return NULL;
    
    if (root->key == val) return root;
    
    else if (root->key > val) return search(root->left, val);
    
    else return search(root->right, val);
}

/* This function finds the biggest node in the subtree rooted at this node */
Node * findMax(Node * node){
   Node * cur_node = node;
   
   while (cur_node->right != NULL) cur_node = cur_node->right;
   
   return cur_node;
}

void swap(Node * n1, Node * n2){
    int temp = n1->key;
    n1->key = n2->key;
    n2->key = temp;
}

/* This function deletes the node and returns the new node that takes its place */
Node * delete(Node * node){
    if (node == NULL) return NULL;
    
    if (node->left == NULL) return node->right;
    
    if (node->right == NULL) return node->left;
    
    Node * new_root = findMax(node->left);
    
    swap(new_root, node);
    
    (new_root->parent)->right = delete(new_root);
    
    return node;
}

{{< / highlight >}}

<h3> Tree Traversal </h3>
There are various ways to traverse a binary tree. Following are the most important traversal techniques:
<h4> In-order traversal </h4>
<i>Traverse the left-subtree, visit the current node, traverse the right subtree.</i>
<p>In-order traversal is really useful when traversing a binary search tree, as the nodes are visited in a sorted manner.</p>
{{< highlight cpp "linenos=table, linenostart=1" >}}

/* Prints the in-order traversal of a binary tree */
void inorder(Node * node){
    if (node == NULL) return;

    inorder(node->left);

    cout<<node->key<<endl;

    inorder(node->right);

    return;
}
{{< / highlight >}}


<h4> Pre-order traversal </h4>
<i>Visit the current node, traverse the left subtree, traverse the right subtree.</i>
<p>Pre-order traversal is used when you want to make changes to a tree recursively starting at the parent, and moving towards the children. It can be seen as a top-down recursive approach</p>
{{< highlight cpp "linenos=table, linenostart=1" >}}

/* Prints the pre-order traversal of a binary tree */
void preorder(Node * node){
    if (node == NULL) return;

    cout<<node->key<<endl;
    
    preorder(node->left);

    preorder(node->right);

    return;
}
{{< / highlight >}}

<h4> Post-order traversal </h4>
<i>Traverse the left subtree, traverse the right subtree, visit the current node.</i>
<p>Post-order traversal is used when you want to make changes to a tree recursively starting at the children, and moving towards the parent. It can be seen as a bottom-up recursive approach</p>

{{< highlight cpp "linenos=table, linenostart=1" >}}
/* Prints the post-order traversal of a binary tree */
void postorder(Node * node){
    if (node == NULL) return;

    postorder(node->left);

    postorder(node->right);

    cout<<node->key<<endl;
    
    return;
}
{{< / highlight >}}

<h4> Level-order traversal </h4>
<i>Traverse the tree one level at a time..</i>
<p>Level-order traversal is used when you want to visit all the nodes at height i before moving towards height i-1. Leaves have height = 0. General implementation is covered in the Breadth First Search algorithm. </p>

<h3> Quiz </h3>
<ul>
    <li> In a full binary tree, all nodes except leaves have two children. True or False? </li>
    <li> Every complete binary tree is a full binary tree and vice-versa? Tree or False? </li>
    <li> If we reverse the order of nodes in pre-order traversal, we get post-order traversal. True or False? </li>
    <li> In the delete function, instead of selecting the biggest node in the left sub-tree, we can also select the smallest node in the right sub-tree. True or False?</li>
    <li> How would you implement the delete function if you cannot store the parent information?</li>
    <li> If the Node struct has height variable, how would you update it while inserting or deleting a node? </li>
</ul>
