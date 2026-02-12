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

## 📝 std::accumulate(begin_iterator, end_iterator, initial_sum)

---

### 🔹 Basic Usage

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int sum = 0;
    vector<int> nums{1, 3, 2, 5};

    sum = accumulate(begin(nums), end(nums), 0);

    cout << sum; // 11
}
```

### ✅ Benefit

- No need to write a for loop
- Cleaner and shorter code
- Very useful in competitive programming

---

## 📝 std::accumulate(begin_iterator, end_iterator, initial_sum, lambda)

### 🔹 Lambda Version Syntax

```cpp
accumulate(begin_iterator, end_iterator, initial_value, lambda);
```

🔹 **Lambda Explanation**

Lambda is a binary operation:
- First parameter → accumulated value
- Second parameter → current element
- Must return updated accumulated value

---

### 🔹 Example 1: Sum of Squares

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {

    auto lambda = [&](int s, long n) {
        return s + n * n;   // sums square of numbers
    };

    int sum = 0;
    vector<int> nums{1, 3, 2, 5};

    sum = accumulate(begin(nums), end(nums), 0, lambda);

    cout << sum; // 39
}
```

---

### 🔹 Example 2: Handling 2D Matrix

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {

    vector<vector<int>> matrix{
        {1, 2},
        {3, 4}
    };

    auto lambda = [&](int sum, vector<int> vec) {
        return sum + accumulate(begin(vec), end(vec), 0);
    };

    int result = accumulate(matrix.begin(), matrix.end(), 0, lambda);

    cout << result; // 10
}
```

---

### 🔥 Beautiful Example Usage

- LeetCode 1572 (Matrix Diagonal Sum)
- LeetCode 1577
