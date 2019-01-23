+++ 
draft = true
date = 2019-01-19T00:36:50+05:30
title = "Prime Number Generation / Sieve"
slug = "" 
+++
<p>Sometimes we encounter problems which are mathematical in nature, and involve concepts of number theory. More often than not, solving these problems require us to use prime numbers. Hence, we should know the Sieve (Sieve of Eratosthenes) algorithm to be able to generate prime numbers efficiently.</p>
<!--more-->
<h3> Tutorials </h3>

<table>
  <tr>
    <th>Links</th>
  </tr>
  <tr>
      <td><a href="https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes">Wikipedia</a></td>
  </tr>
  <tr>
      <td><a href="https://www.geeksforgeeks.org/sieve-of-eratosthenes/">GeeksforGeeks</a></td>
  </tr>
</table>

<h3> Complexity </h3>
Sieve will generate all prime numbers less than or equal to a given number N.
<table>
  <tr>
    <th>Time Complexity (Worst case)</th>
    <th>Space Compexity (Worst case)</th>
  </tr>
  <tr>
    <td>O(N*log(log(N)))</td>
    <td>O(N)</td>
  </tr>
</table>

<h3> Specifics </h3>
<p> Sieve of Eratosthenes make use of the fact that prime numbers won't appear in the multiplication table of any number smaller than them (except 1)</p>
<p> Based on this idea, we first mark all numbers as prime and available, and then run a loop where we select the smallest available number and remove all the numbers that appear in the multiplication table of this number, and then move to the next available number</p>
<p> Hence, every time we select an available number, it is guaranteed to be prime as it didn't appear in the multiplication table of any previous number.</p> 

<h3> Implementation </h3>

{{< highlight cpp "linenos=table, linenostart=1" >}}
void Sieve(int N){
    //bool vector which holds all the numbers till N.
    //Initially all numbers are marked as prime.
    vector<bool> numArr(N+1, 1);
    
    //We start the loop from 2 as 0 and 1 are not prime anyway.
    for (int i = 2; i <= N; i++){
        
        //if current number is not prime, move to the next number
        if (!numArr[i]) {
            continue;
        }
        
        //if current number is prime, print it, and mark its multiples as not prime
        else {
            cout<<i<<endl; 
            
            int j = 2;
        
            while (i*j <= N){
                numArr[i*j] = 0;
                j++;
            }
        }
}
{{< / highlight >}}
