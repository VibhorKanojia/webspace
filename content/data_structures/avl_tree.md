+++ 
draft = true
date = 2019-01-20T21:28:50+05:30
title = "AVL Tree"
description = ""
slug = "" 
tags = ["Data Structures"]
+++
<p>Binary Trees provide O(logN) average case time complexity for insert, delete, and search operations. But depending upon the order of insert, we might form an unbalanced tree which makes the time complexity linear. AVL Trees are self-balancing binary trees that can guarantee O(logN) time complexity even in the worst case. The only drawback is that the structure of the tree changes as we add more and more nodes. </p> 
<!--more-->

<h3> Specifics </h3>

<p>An AVL tree has all the properties of a normal binary tree. But in order to keep the tree balanced, an AVL tree has the following extra properties:</p>
<ol>
    <li> The sub-trees of every node differ in height by at most one </li>
    <li> Every sub-tree is an AVL tree </li>
</ol>

Every time the insertion or deletion of a node violates these properties, it changes the structure to make itself balanced.

<h3> Complexities </h3>
<table>
  <tr>
    <th> Operation </th>
    <th>Time Complexity (Average Case)</th>
    <th>Time Complexity (Worst case)</th>
  </tr>
  <tr>
    <td> Insertion</td>
    <td>O(logN)</td>
    <td>O(logN)</td>
  </tr>
  <tr>
    <td> Deletion</td>
    <td>O(logN)</td>
    <td>O(logN)</td>
  </tr>
  <tr>
    <td> Search</td>
    <td>O(logN)</td>
    <td>O(logN)</td>
  </tr>
</table>

<h3> Implementation </h3>
<p>w -> Last node that was inserted.<br>
z -> Starting from w and going up, the first node that is unbalanced.<br>
y -> Child of z which is in the direction of w.<br>
x -> Child of y which is in the direction of w.</p>

<p>While performing a standard BST insertion of w, we can encounter four cases that violate the properties of an AVL tree:</p>


{{< highlight cpp "linenos=table, linenostart=1" >}}
struct Node{
    int key;
    int height;
    Node * left;
    Node * right;
    
    Node(int key){
        this->key = key;
        this->height= 0;
        left = NULL;
        right = NULL;
    }
};


int getHeight(Node * root){
    if (root == NULL) return -1;
    else return root->height;
}

void rotateRight(Node * z){
    Node * y = z->left;
    z->left = y->right;
    y->right = z;

    z->height = max(getHeight(z->left), getHeight(z->right)) +1;
    y->height = max(getHeight(y->left), getHeight(y->right)) +1;
    return y;
}



void rotateLeft(Node * z){
    Node * y = z->right;
    z->right = y->left;
    y->left = z;

    z->height = max(getHeight(z->left), getHeight(z->right)) +1;
    y->height = max(getHeight(y->left), getHeight(y->right)) +1;
    return y;
}


Node * insert(Node * root, int val){

    if (root == NULL) return new Node(val);

    if (root->key >= val) root->left = insert(root->left, val, root);

    else root->right = insert(root->right, val, root);

    root->height = max(getHeight(root->left), getHeight(root->right)) + 1;

    int difference = getHeight(root->left) - getHeight(root->right);

    //LL case
    if (difference > 1 && val <= (root->left)->key){
        root = rotateRight(root);
    }

    //LR case
    else if (difference > 1 && val > (root->left)->key){
        root->left = rotateLeft(root->left);
        root = rotateRight(root);
    }

    //RR case
    else if (difference < -1 && val > (root->right)->key){
        root= rotateLeft(root);
    }

    //RL case
    else if (difference < -1 && val <= (root->right)->key){
        root->right = rotateRight(root->right);
        root = rotateLeft(root);
    }

    return root;
}

Node * search(Node * root, int val){
    if (root == NULL) return NULL;
    
    if (root->key == val) return root;
    
    else if (root->key > val) return search(root->left, val);
    
    else return search(root->right, val);
}
{{< / highlight >}}
