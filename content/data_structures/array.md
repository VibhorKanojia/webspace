+++ 
draft = true
date = 2019-01-20T17:09:12+05:30
title = "Array"
description = ""
slug = "" 
tags = ["Data Structures"]
+++
<p>In C++, arrays can be used to store a collection of elements having the same type, where each element is uniquely identified by an index. Elements in an array are stored consecutively, and hence, given the address of the first element, the address of each element can be calculated using a mathematical formula. This provides O(1) access to each element of the array.</p>
<p>The size of an array means the number of elements it can hold.</p>
<!--more-->

<h3> Specifics </h3>
In order to have O(1) access, we need to allocate a continuous block of memory to hold all the elements of an array. This constraint has a few drawbacks:
<ol>
    <li>User must specify the array size (number of elements) initially while defining the array</li>
    <li>User cannot resize the array</li>
    <li>Deleting an element has O(N) time complexity, as we will have to move all the elements after it by one position</li>
</ol>

<h3> Implementation </h3>
{{< highlight cpp "linenos=table, linenostart=1" >}}
int A[20]; /*defines an array of size 20*/
{{< / highlight >}}

Note that this command will allocate a block of 20*4 bytes of memory to the array A. The memory is allocated in the function stack.
Here A is an integer pointer which points to the first element of the array.

{{< highlight cpp "linenos=table, linenostart=1" >}}
cout << A[i] <<endl; /*prints the ith element of the array*/
cout << *(A+i) <<endl; /*alternative way to print the ith element of the array*/
cout << sizeof(A)/sizeof(int) <<endl; /*prints the size of the array*/
{{< / highlight >}}

Arrays defined using the above method have their scope limited to the function stack. In order to access an array across various functions without making copies of the array, we need to allocate the memory in heap. In c++, this is done via the new commmand.

{{< highlight cpp "linenos=table, linenostart=1" >}}

int * A = new int[20]
{{< / highlight >}}


Arrays don't have to be one dimensional. One can also define multi-dimensional arrays.
The following code defines a 2D array having 20 rows and 10 columns.

{{< highlight cpp "linenos=table, linenostart=1" >}}

int A[20][10]; /*memory is allocated in stack*/

int ** A = new int*[20];   /*memory is allocated in heap*/
for (int i = 0 ; i < 20; i++){
    A[i] = new int[10];
}

cout<< A[i][j] <<endl; /*prints the element at indices i:j*/
{{< / highlight >}}

<h3> Problems </h3>

</body>
</html>
