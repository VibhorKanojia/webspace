+++     
draft = true
date = 2019-01-20T00:36:07+05:30
title = "Quick Sort/Select"
slug = ""
tags = ["algorithm"]
+++
<p>Quick Sort is an incredibly interesting sorting algorithm. The worst case time complexity of this algorithm is O(N<sup>2</sup>), but when implemented well, it can be about two or three times faster than its main competitors, merge sort and heap sort. Another good thing is that quick sort is an in-place sorting algorithm.
<p>The only drawback is that the efficient implementations of this algorithm are not stable in nature, i.e., it doesn't preserve the relative order of equal elements in the output.
<!--more-->
<h3> Tutorials </h3>

<table>
  <tr>
    <th>Links</th>
  </tr>
  <tr>
      <td><a href="https://en.wikipedia.org/wiki/Quicksort">Wikipedia</a></td>
  </tr>
  <tr>
      <td><a href="https://www.geeksforgeeks.org/quick-sort/">GeeksforGeeks</a></td>
  </tr>
</table>


<h3> Complexity </h3>
<table>
  <tr>
    <th>Time Complexity (Average case)</th>
    <th>Space Compexity (Average case)</th>
    <th>Time Complexity (Worst case)</th>
    <th>Space Compexity (Worst case)</th>
  </tr>
  <tr>
    <td>O(NlogN)</td>
    <td>O(logN)</td>
    <td>O(N<sup>2</sup>)</td>
    <td>O(N) / O(logN)</td>
  </tr>
</table>

<h3> Specifics </h3>
<p> Quick sort works by selecting a pivot element in each step, and putting it on its correct place, such that, all the elements smaller than the pivot are on one side and all the elements greater than the pivot on the other. This step takes O(N) operations. The same step is repeated on the two smaller halves.
<p> In this implementation, selection of pivot is the most important step, ideally we would want the pivot to roughly divide the input space into two equal halves, which would result in O(NlogN) complexity. However, in the worst case, we could select the maximum/minimum element as pivot and end up putting all the elements on the same side of the pivot. This would lead to a time complexity of O(N<sup>2</sup>)

<h3> Implementation </h3>
<p>We'll be discussing the recursive implementations of quick sort. Note that it can also be implemented iteratively by using auxillary stack
to mimic the function stack.

<p><b>Basic Implementation:</b> uses O(N) space in the worst case 
{{< highlight cpp "linenos=table, linenostart=1" >}}


void swap(vector<int> & input, int i1, int i2){
    int temp = input[i1];
    input[i1] = input[i2];
    input[i2] = temp;
}


/* This function takes last element as pivot, places
   the pivot element at its correct position in sorted
   array, and places all smaller (smaller than pivot)
   to left of pivot and all greater elements to right
   of pivot. At the end, it returns the position where 
   the pivot was placed. */

int partition(vector<int> & input, int start, int end){ 
    //We are selecting the last element as our pivot in each step
    int pivot = end;
    
    //index stores the position where the next smaller element will go
    int index = start;

    for(int i = start; i <=end; i++){
        if (input[i] < array[pivot]){
            swap(input, i, index);
            index++;
        }
    }
    //once we put all the smaller elements in the beginning of the array,
    //we put the pivot element in its correct position
    swap(input, pivot, index);
    return index;
}

//Note that both start and end are inclusive in this implementation
void quickSort(vector<int> & input, int start, int end){
    //Just return if there's zero on one element
    if (start >= end) return;
    
    int p_index = partition(input, start, end);

    //recursively call the same function on the left and right halves
    quickSort(input, start, p_index-1);
    quickSort(input, p_index+1, end);
    return;
}

{{< / highlight >}}

<p>Note that, in the worst case, we can have N recursive calls which would result in O(N) function stack space usage.
We can optimize the above code to make only one recursive call instead of two, and as the recursive call is being made
at the end of the function, modern compiler can use tail call optimization.

<p><b>Optimized Version:</b> uses O(logN) space in the worst case

{{< highlight cpp "linenos=table, linenostart=1" >}}


void swap(vector<int> & input, int i1, int i2){
    int temp = input[i1];
    input[i1] = input[i2];
    input[i2] = temp;
}

int partition(vector<int> & input, int start, int end){ 
    int pivot = end;
    
    int index = start;

    for(int i = start; i <=end; i++){
        if (input[i] < array[pivot]){
            swap(input, i, index);
            index++;
        }
    }
    swap(input, pivot, index);
    return index;
}

//Note that both start and end are inclusive in this implementation
void quickSort(vector<int> & input, int start, int end){
    //Just return if there's zero on one element
    if (start >= end) return;
    
    while (start < end){
        int p_index = partition(input, start, end);

        //recursively call the same function on the smaller half
        if (p_index - start < end - p_index){  //left half is smaller
            quickSort(input, start, p_index-1);
            start = p_index+1;    //change start so that next loop sorts the right half
        }
        else{  //right half is smaller
            quickSort(input, p_index+1, end);  
            end = p_index-1;     //change end so that next loop sorts the left half
        }
    }
}

{{< / highlight >}}

