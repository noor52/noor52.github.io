---
layout: post
title: PROBLEM SOLVE Maximum adjacent difference in an array in its sorted form
subtitle: problem solving Maximum adjacent difference in an array in its sorted form
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [problem solbing, Java]
comments: true
mathjax: false
author: Noor
---

#  Solution Guide

## 1. Problem Solving

###  BEE 1004-Simple Product
```html
Fizz Buzz
Last Updated : 07 Feb, 2025
Given an integer n, for every positive integer i <= n, the task is to print,

“FizzBuzz” if i is divisible by 3 and 5,
“Fizz” if i is divisible by 3,
“Buzz” if i is divisible by 5
“i” as a string, if none of the conditions are true.
Examples:

Input: n = 3
Output: [“1”, “2”, “Fizz”]


Input: n = 10
Output: [“1”, “2”, “Fizz”, “4”, “Buzz”, “Fizz”, “7”, “8”, “Fizz”, “Buzz”]


Input: n = 20
Output: [“1”, “2”, “Fizz”, “4”, “Buzz”, “Fizz”, “7”, “8”, “Fizz”, “Buzz”, “11”, “Fizz”, “13”, “14”, “FizzBuzz”, “16”, “17”, “Fizz”, “19”, “Buzz”]


Try it on GfG Practice
redirect icon
Table of Content

[Naive Approach] By checking every integer individually
[Better Approach] By String Concatenation
[Expected Approach] Using Hash Map or Dictionary
[Naive Approach] By checking every integer individually
A very simple approach to solve this problem is that we can start checking each number from 1 to n to see if it’s divisible by 3, 5, or both. Depending on the divisibility:

If a number is divisible by both 3 and 5, append “FizzBuzz” into result.
If it’s only divisible by 3, append “Fizz” into result.
If it’s only divisible by 5, append “Buzz” into result.
Otherwise, append the number itself into result.



// C++ program for Fizz Buzz Problem 
// by checking every integer individually

#include <iostream>
#include <vector>
using namespace std;

vector<string> fizzBuzz(int n){
    vector<string> res;
    for (int i = 1; i <= n; ++i) {

        // Check if i is divisible by both 3 and 5
        if (i % 3 == 0 && i % 5 == 0) {

            // Add "FizzBuzz" to the result vector
            res.push_back("FizzBuzz");
        }

        // Check if i is divisible by 3
        else if (i % 3 == 0) {

            // Add "Fizz" to the result vector
            res.push_back("Fizz");
        }

        // Check if i is divisible by 5
        else if (i % 5 == 0) {

            // Add "Buzz" to the result vector
            res.push_back("Buzz");
        }
        else {

            // Add the current number as a string to the
            // result vector
            res.push_back(to_string(i));
        }
    }

    return res;
}

int main(){
    int n = 20;
    vector<string> res = fizzBuzz(n);
    for (const string& s : res) {
        cout << s << " ";
    }
    return 0;
}

Output
1 2 Fizz 4 Buzz Fizz 7 8 Fizz Buzz 11 Fizz 13 14 FizzBuzz 16 17 Fizz 19 Buzz 
Time Complexity: O(n), since we need to traverse the numbers from 1 to n in any condition.
Auxiliary Space: O(n), for storing the result

[Better Approach] By String Concatenation
While the naive approach works well for the basic FizzBuzz problem, it becomes very complicated if additional mappings comes under picture, such as “Jazz” for multiples of 7. The number of conditions for checking would increases.


Instead of checking every possible combination of divisors, we check each divisor separately and concatenate the corresponding strings if the number is divisible by them.


Step-by-step approach:

For each number i <= n, start with an empty string s.
Check if i is divisible by 3, append “Fizz” into s.
Check if i is divisible by 5, append “Buzz” into s.
If we add “Fizz” and “Buzz“, the string s becomes “FizzBuzz” and we don’t need extra comparisons to check divisibility of both.
If nothing was added, just use the number.
Finally, append this string s into our result array.



// C++ program for Fizz Buzz Problem 
// by checking every integer individually 
// with string concatenation

#include <iostream>
#include <vector>
using namespace std;

vector<string> fizzBuzz(int n) {
    vector<string> res;
    for (int i = 1; i <= n; i++) {
        
        // Initialize an empty string for the current result
        string s = "";

        // Divides by 3, add Fizz
        if (i % 3 == 0)
            s.append("Fizz");

        // Divides by 5, add Buzz
        if (i % 5 == 0)
            s.append("Buzz");

        // Not divisible by 3 or 5, add the number
        if (s.empty())
            s.append(to_string(i));

        // Append the current res to the result vector
        res.push_back(s);
    }

    return res;
}

int main() {

    int n = 20;
    vector<string> res = fizzBuzz(n);

    for (const string &s : res)
        cout << s << " ";

    return 0;
}

Output
1 2 Fizz 4 Buzz Fizz 7 8 Fizz Buzz 11 Fizz 13 14 FizzBuzz 16 17 Fizz 19 Buzz 
Time Complexity: O(n), since we need to traverse the numbers from 1 to n in any condition.
Auxiliary Space: O(n), for storing the result

[Expected Approach] Using Hash Map or Dictionary
When we have many words to add like “Fizz“, “Buzz“, “Jazz” and more, the second method can still get complicated and lengthy. To make things cleaner, we can use something called a hash map. Initially, we can store the divisors and their corresponding words into hash map. 


For this problem, we would map 3 to “Fizz” and 5 to “Buzz” and for each number, checks if it is divisible by 3 or 5, if so, appends the corresponding string from map to the result. If the number is not divisible by either, simply adds the number itself as a string.





// C++ program for Fizz Buzz Problem 
// by checking every integer individually 
// with hashing

#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

vector<string> fizzBuzz(int n) {

    vector<string> res;

    // Hash map to store all fizzbuzz mappings.
    unordered_map<int, string> mp = 
                        {{3, "Fizz"}, {5, "Buzz"}};

    // List of divisors which we will iterate over.
    vector<int> divisors = {3, 5};

    for (int i = 1; i <= n; i++) {
        string s = "";

        for (int d : divisors) {

            // If the i is divisible by d, add the 
              // corresponding string mapped with d
            if (i % d == 0)
                s.append(mp[d]);
        }
       
        // Not divisible by 3 or 5, add the number
        if (s.empty())
            s.append(to_string(i));

        // Append the current answer str to the result vector
        res.push_back(s);
    }

    return res;
}

int main() {
    int n = 20;
    vector<string> res = fizzBuzz(n);

    for (const string &s : res)
        cout << s << " ";

    return 0;
}

Output
1 2 Fizz 4 Buzz Fizz 7 8 Fizz Buzz 11 Fizz 13 14 FizzBuzz 16 17 Fizz 19 Buzz 
Time Complexity: O(n), since we need to traverse the numbers from 1 to n in any condition.
Auxiliary Space: O(n), for storing the result
```

### Solution 




```