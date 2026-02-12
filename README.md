# C-STL
# 🚀 C++ STL Quick Help

This repository contains quick notes and examples of C++ STL for fast revision.

---

## 📚 Topics Covered

- Vector
- Pair
- Map
- Unordered Map
- Set
- Multiset
- Stack
- Queue
- Priority Queue
- Algorithms (sort, accumulate, etc.)

---

## 🎯 Purpose

- Quick revision before contest
- Clean STL syntax examples
- Beginner friendly explanations

- ---

# 📝 std::accumulate(begin_iterator, end_iterator, initial_sum)

### 🔹 Syntax
```cpp
int sum = 0;
vector<int> nums{1, 3, 2, 5};
sum = accumulate(begin(nums), end(nums), 0);

cout << sum; //11

Benefit : You didn't have to write for loop to find the sum
accumulate(begin_iterator, end_iterator, initial_value);
---
📝 std::accumulate(begin_iterator, end_iterator, initial_sum, lambda) ➕
```cpp
lambda : Binary operation taking an element of type <initial_sum> as first argument and an
            element in the range as second, and which returns a value that can be assigned to type T.

Example-1 : 

auto lambda = [&](int s, long n) {
    return s + n*n; //sums the square of numbers
    //You can call any other function inside as well
};

int sum = 0;
vector<int> nums{1, 3, 2, 5};
sum = accumulate(begin(nums), end(nums), 0, lambda);

cout << sum; //39

Example-2 : Handling 2-D matrix
//Summming all elements row by row
auto lambda = [&](int sum, vector<int> vec) {
    sum = sum + accumulate(begin(vec), end(vec), 0);
    return sum;
};

int result =  accumulate(matrix.begin(), matrix.end(), 0, lambda);


Beautiful example and usage :
Leetcode-1577 
Leetcode-1572 
---
