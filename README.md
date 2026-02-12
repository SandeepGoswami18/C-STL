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
int sum = 0;
vector<int> nums{1, 3, 2, 5};
sum = accumulate(begin(nums), end(nums), 0);

cout << sum; //11

Benefit : You didn't have to write for loop to find the sum

```cpp
accumulate(begin_iterator, end_iterator, initial_value);


---

## 💻 Language

C++
