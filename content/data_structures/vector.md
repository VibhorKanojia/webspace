+++ 
draft = true
date = 2019-01-20T21:31:55+05:30
title = "Vector"
description = ""
slug = "" 
tags = ["Data Structures"]
+++
<p>Vectors are same as dynamic arrays with the ability to resize themselves automatically when an element is inserted or deleted, with their storage being handled automatically by the container. Vector elements are placed in contiguous storage so that they can be accessed and traversed using iterators in O(1) time.
<!--more-->
<h3> Specifics </h3>
Vector overcomes most of the drawbacks of arrays:
<ol>
    <li>Adding an element at the end can be done in O(1) time</li>
    <li>Removing the last element can also be done in O(1) time</li>
    <li>Inserting or erasing at the beginning or in the middle is linear in time</li>
</ol>

<h3> Implementation </h3>
Below are some of the frequently used member functions of the vector class:
{{< highlight cpp "linenos=table, linenostart=1" >}}
vector<int> A; /*defines a vector*/

vector<int> A(20,0) /* defines a vector of size 20; all elements are initialized to 0 */

vector::size(); /* returns the size of a vector */

vector::empty(); /* returns true if the vector is empty; else false */

vector::erase(); /* erases all the elements from the vector */

vector::push_back(int elem); /* adds elem at the end of the vector; effectively increases the size by 1 */

vector::pop_back(); /* removes the last element from the vector; effectively decreases the size by 1 */

vector::insert(iterator pos, int elem); /* insert elem at position pos; O(N) time complexity; */
{{< / highlight >}}
