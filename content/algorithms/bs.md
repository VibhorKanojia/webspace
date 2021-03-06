+++ 
draft = true
date = 2019-01-20T00:36:07+05:30
title = "Binary Search"
slug = ""
tags = ["algorithm"]
+++
Binary Search is a search algorithm that finds the position of a target value within a sorted array. Binary search compares the target value to the middle element of the array; if they are unequal, the half in which the target cannot lie is eliminated and the search continues on the remaining half until it is successful. If the search ends with the remaining half being empty, the target is not in the array.
<!--more-->
<h3> Tutorials </h3>

<table>
  <tr>
    <th>Links</th>
  </tr>
  <tr>
      <td><a href="https://en.wikipedia.org/wiki/Binary_search_algorithm">Wikipedia</a></td>
  </tr>
  <tr>
      <td><a href="https://www.geeksforgeeks.org/binary-search/">GeeksforGeeks</a></td>
  </tr>
</table>


<h3> Complexity </h3>
<table>
  <tr>
    <th>Time Complexity (Worst case)</th>
    <th>Space Compexity (Worst case)</th>
  </tr>
  <tr>
    <td>O(logN)</td>
    <td>O(1)</td>
  </tr>
</table>

<h3> Implementation </h3>

Before moving forward, try to implement it yourself. Both iterative and recursive implementations should not take more than 10 minutes combined.

<h4> Iterative </h4>

{{< highlight cpp "linenos=table, linenostart=1" >}}

bool binarySearch(vector<int> array, int target){
    
    int start = 0;
    int end = array.size();

    while (start < end){
        int mid = start + (end-start)/2;
        if (array[mid] == target) return true;
        if (array[mid] > target) end = mid;
        else start = mid;
    }

    return false;
}

{{< / highlight >}}

<h4> Recursive </h4>
{{< highlight cpp "linenos=table, linenostart=1" >}}
//Note that in the following implementation array is sorted, start is inclusive, end is exclusive.

bool binarySearch(vector<int> array, int start, int end, int target){
    
    if (start >= end) return false;

    int mid = start + (end-start)/2;

    if (array[mid] == target) return true;

    else if (array[mid] > target) return binarySearch(array,start,mid,target);

    else return binarySearch(array,mid,end,target);
}

{{< / highlight >}}

<h3> Quiz </h3>
<ul>
    <li> Why don't we calculate mid as (start+end)/2 ?</li>
    <li> Why is Binary Search preferred over Ternary Search? What are the number of comparisons in both the cases?</li>
    <li> Worst case time complexity to find if the target exits in an array? </li>
    <li> Worst case time complexity to find if the target exists in a sorted array? </li>
    <li> Worst case time complexity to find the indices of the target in a sorted array? </li>
    <li> How would you modify the code to make end inclusive in both the implementations?</li>
</ul>

