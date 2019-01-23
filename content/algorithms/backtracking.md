+++     
draft = true
date = 2019-01-20T00:36:07+05:30
title = "Backtracking"
slug = ""
tags = ["algorithm"]
+++
<p>Sometimes, none of the faster algorithms seem to work on some problems. In such scenarios, one should check the possible input size and if it seems small enough, the problem can be solved by using a brute force approach where we consider all the possibilities, also known as backtracking. A lot of NP hard problems like solving a sudoku, N-queens problem, etc can not be solved in polynomial time. Hence, we use backtracking, which usually has exponential complexity, to solve such problems.
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
      <td><a href="https://www.geeksforgeeks.org/backtracking-algorithms/">GeeksforGeeks</a></td>
  </tr>
</table>


<h3> Complexity </h3>
<p> Backtracking is a class or algorithms, or rather, an approach. So the complexity varies depending upon the question.
Mostly it is non-polynomial in nature.

<h3> Specifics </h3>
<p> In backtracking, we use brute force recursion to generate all possible outcomes, and put those which satify the constraint/criteria, into an output vector.
<p> As the name suggests, we go in-depth to find a solution, and if we don't find one we backtrack to the state where we have some alternative path to consider.

<h3> Implementation </h3>
<p> Since it's more of an approach than an algorithm, I'll use a sample problem to share the thought process and code flow when solving a problem with backtracking.


<p><b>Problem Statement:</b> Subset sum problem is to find subset of elements that are selected from a given set whose sum adds up to a given number K. We are considering the set contains non-negative values. It is assumed that the input set is unique (no duplicates are presented).

{{< highlight cpp "linenos=table, linenostart=1" >}}

void backtrack(
    vector<int> & input,            // input array
    int K,                          // target sum
    int cur_sum,                    // sum of elements currently being considered
    int start,                      // start index, all the elements before this index are already considered
    vector<int> solution,           // vector of elements currently being considered. Not passed by reference,
    vector<vector<int>> & result    // vector which holds all the solution vectors that satisfy the constraint/criteria. Passed by reference
){ 
    
    //We found the solution, no need to process further as we have only non-negative numbers in the array. So the sum will only increase further.
    //Add the current solution vector to the results.
    if (cur_sum == K){             
        result.push_back(solution);
        return;
    }
    
    //If we have considered all the elements, or if the sum of elements currently being considered is already greater than K, return.
    //We don't add the solution vector to the results here as it doesn't meet the required condition.
    if (start >= input.size() || cur_sum > K){
        return;
    }
    
    //Main loop; note that we start considering elements from start index.
    for (int i = start; i < input.size(); i++){
        //take current element and make the next call recursively by updating cur_sum and start index.
        solution.push_back(input[i]);
        backtrack(input, K, cur_sum+input[i], i+1, solution, result);
    
        /*After generating all possible outcomes that contain the current element, pop it from the solution,
        to generate those outcomes which don't have this element in them. */
        solution.pop_back();
    }
    
    return;
}

{{< / highlight >}}

