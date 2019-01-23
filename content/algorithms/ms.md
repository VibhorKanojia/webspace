+++ 
draft = true
date = 2019-01-20T00:36:07+05:30
title = "Merge Sort"
slug = ""
tags = ["algorithm"]
+++
<p>Merge Sort is one of the prime examples of a class of algorithms known as Divide and conquer. The basic idea of such algorithms is to divide the space into two equal halves recursively until they become small enough to be solved directly, then come up with a way to combine the solution of these smaller halves.
<p> Based on this idea, merge sort recursively divides the input array and sort the individual sub arrays. Then later, combine the two sorted halves.
<p> The implementation of this algorithm is very important and often serves as the base to solve a variety of problems. 
<!--more-->
<h3> Tutorials </h3>

<table>
  <tr>
    <th>Links</th>
  </tr>
  <tr>
      <td><a href="https://en.wikipedia.org/wiki/Merge_sort">Wikipedia</a></td>
  </tr>
  <tr>
      <td><a href="https://www.geeksforgeeks.org/merge-sort/">GeeksforGeeks</a></td>
  </tr>
</table>


<h3> Complexity </h3>
<table>
  <tr>
    <th>Time Complexity (Worst case)</th>
    <th>Space Compexity (Worst case)</th>
  </tr>
  <tr>
    <td>O(NlogN)</td>
    <td>O(N)</td>
  </tr>
</table>

<h3> Specifics </h3>
<p> Merge Sort is a comparison-based stable sorting algorithm. A stable sort is the one where the relative order of equal elements is the same in the input and output.

<h3> Implementation </h3>

{{< highlight cpp "linenos=table, linenostart=1" >}}
//Note that in the following implementation both start and end are inclusive.


vector<int> mergeSort(vector<int> & input, int start, int end){
    vector<int> output;
    
    //When there's only one element left, just return a vector with that element in it.
    if (start == end){
        output.push_back(input[start]);
        return output;
    }
    
    //Note that when end = start + 1, mid is equal to start 
    int mid = start + (end-start)/2;
    
    //As mid is equal to start when we have two elements, we will divide
    //the input as (start:mid) and (mid+1:end)
    //For eg., if start = 0 and end = 1, mid will be 0.
    //Hence, we want to divide it as (0:0) and (1:1)
    vector<int> left = mergeSort(input, start, mid);
    vector<int> right = mergeSort(input, mid+1, end);
    
    int i = 0;
    int j = 0;
    
    //This is the main loop which will be modified based on 
    //the requirements of the problem.
    while(i < left.size() && j < right.size()){
        if (left[i] < right[j]){
            output.push_back(left[i]);
            i++;
        }
        else{
            output.push_back(right[j]);
            j++;
        }
    }
    
    //Only one of the following two while loops will run,
    //This is needed as left and right vectors can have different size.
    while (i < left.size()){
        output.push_back(left[i]);
        i++;
    }
    
    while(j < right.size()){
        output.push_back(right[j]);
        j++;
    }
    
    return output;
}


{{< / highlight >}}

