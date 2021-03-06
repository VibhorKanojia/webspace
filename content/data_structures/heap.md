+++ 
draft = true
date = 2019-01-20T21:31:44+05:30
title = "Heap"
description = ""
slug = "" 
tags = ["Data Structures"]
+++
<p>Many a times we need a data structure which can be used to access elements based on certain criteria, for e.g., from smallest to largest element. A Heap or A Priority Queue is a data structure which stores elements in an orderly fashion, such that the element with highest priority is at the top of the heap.</p> 
<!--more-->

<h3> Specifics </h3>
<p>Heaps are implemented using an array/vector with the root node at index 0. Any node at index i has children at indices 2*i+1 and 2*i+2 in the array. All nodes follow the constraint that a parent has more priority than its children. While adding a node, we add it at the end of the array and then move it upwards while the constraint is violated.</p>

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
    <td> Get Top Element</td>
    <td>O(logN)</td>
    <td>O(logN)</td>
  </tr>
</table>

<h3> Implementation </h3>
<p>Implementation of the min/max heaps should not take more than 10 minutes. Below is the implementation of a min heap, i.e., a priority queue where priority is given to smaller elements.</p>

{{< highlight cpp "linenos=table, linenostart=1" >}}
/* Function to swap the two elements at given indices */
void swap(vector<int> & heap, int index1, int index2){
    
    int temp = heap[index1];

    heap[index1] = heap[index2];

    heap[index2] = temp;

    return;

}

/* Shifting upwards the element at the given index until it satifies the constraint */
void shiftUp(vector<int> & heap, int index){

    int par_index = (index -1)/2;

    if (par_index >= 0){

        if (heap[par_index] > heap[index]){

            swap(heap, par_index, index);

            shiftUp(heap, par_index);

        }
    }

    return;
}

/*Shifting downwards the element at the given index until it satisfies the constraint */
void shiftDown(vector<int> & heap, int index){
    
    int child1 = 2*index+1;
    int child2 = 2*index+2;
    int min_child = -1;

    if (child2 < heap.size()){
            min_child = (heap[child1] < heap[child2])? child1 : child2;
    }

    else if (child1 < heap.size()){
        min_child = child1;
    }

    if (min_child == -1 || heap[index] <= heap[min_child]) return;
    
    swap(heap, index, min_child);

    shiftDown(heap, min_child);

    return;
}

/* Function to convert an array to a heap */
/* Heapify method appears to have O(NlogN) complexity but it is actually O(N) */
void heapify(vector<int> & heap){
    int N = heap.size();

    for (int i = N/2; i >=0 ; i--){
        shiftDown(heap, i);
    }

    return;
}

/* Function to add an element into the heap */
void add(vector<int> & heap, int elem){
  
    heap.push_back(elem);

    shiftUp(heap, heap.size()-1);

    return;
}

/* Function to accesss & remove the smallest element from the heap */
int getMin(vector<int> & heap){ 
    
    int min_elem = heap[0];
    
    int last_index = heap.size() -1;

    heap[0] = heap[last_index];

    heap.pop_back();

    if (!heap.empty()) shiftDown(heap, 0);

    return min_elem;
}
{{< / highlight >}}

<h5> Heapify </h5>
<p>To heapify an array means to convert an array into a heap. To do this, we start at the bottom ignoring all the leaves, and call shiftDown function on all the non-leaf nodes. But looking at the recursive call one may mistakenly assume it to be a O(NlogN) complexity method. But there is an upper bound on the number of steps a node can move downwards which makes this function have O(N) complexity.</p>

<i>N: Number of nodes in the heap</i><br>
<i>H: Height of the heap</i><br>
<i>2<sup>i</sup> -> Nodes at level i (root is at level 0)</i><br>
<br>
<i>Therefore, number of operations involved are:</i><br>

<i>#O = 1*2<sup>H-1</sup> + 2*2<sup>H-2</sup> + 3*2<sup>H-3</sup> ... H*2<sup>0</sup>.</i><br>
<i>#O = 2<sup>H</sup>* i/2<sup>i</sup>  (i = [1,H]).</i><br>
<i>Now,</i><br>
<i>i/2<sup>i</sup>  (i = [1,H])  <  i/2<sup>i</sup>  (i = [1,inf]). </i><br>
<i>Right hand side is an AGP which sums up to 1. </i><br>
<i>Hence,</i><br>
<i>i/2<sup>i</sup>  (i = [1,H]) < 1.</i> <br>
<i>#O = 2<sup>H</sup></i><br>
<i>#O = O(N) (H = log(N)/log(2)) </i><br>





<h3> C++ STL Library </h3>
<p>C++ has its own STL library implementation of priority queues which can be used directly without implementing your own methods.
Below is an example where we want to access an employee database starting from the youngest employees.</p>

{{< highlight cpp "linenos=table, linenostart=1" >}}
#include <priority_queue>


/* Struct which stores the employees' information */
struct Person{
    string name;
    int age;
    Person(string name, int age){
        this->name = name;
        this->age = age;
    }
};


/* Class function to decide the priority order */
class Compare{
public:
    bool operator()(Person * a, Person * b){
        return (a->age > b->age);
    }
};


int main(){
    
    int N;
    cin >> N;   //Number of employees


    /*<datatype, container, comparator function>*/
    priority_queue<Person *, vector<Person *>, Compare> heap;
    
    for (int i =0 ; i < N ; i++){
    
        string name;
        int age;

        cin >> name;
        cin >> age;

        Person * p = new Person(name, age);

        heap.push(p);
    }


    while (!heap.empty()){
        Person * p = heap.top();
        
        cout<< p->name <<" "<< p->age<<endl;

        heap.pop();
    }
    
    return 0;
}
{{< / highlight >}}
