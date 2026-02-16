# 🚀 C++ STL Quick Help (With Explanation + Examples)

This file contains **most used + important STL utilities**  
with explanation of:

✔ What it does  
✔ When to use it  
✔ Small example  
✔ Leetcode number tags  

All examples use simple types (`int`, `string`) for clarity.

---

# 🗻 priority_queue (Heap)

## 🔹 What?
Stores elements in heap order.

Default → **Max Heap**

---

## ✅ Max Heap (Default)

```cpp
priority_queue<int> pq;

pq.push(10);
pq.push(5);
pq.push(20);

cout << pq.top(); // 20 (largest element)
```

### 📌 When to use?
- Find K largest elements
- Maintain running maximum
- Scheduling problems

LC: 215, 703

---

## ✅ Min Heap

```cpp
priority_queue<int, vector<int>, greater<int>> pq;

pq.push(10);
pq.push(5);
pq.push(20);

cout << pq.top(); // 5 (smallest element)
```

### 📌 When to use?
- K smallest elements
- Dijkstra algorithm
- Merge K sorted lists

LC: 347

---

# ⬅️ std::move()

## 🔹 What?
Transfers ownership of data (avoids copying).

---

```cpp
string a = "Hello";
string b = move(a);

cout << a; // empty
cout << b; // Hello
```

### 📌 When to use?
- Passing large vectors
- Returning large objects
- Avoiding copy overhead

---

# ➕ std::accumulate()

## 🔹 What?
Used to sum or combine elements.

---

## Basic Sum

```cpp
vector<int> v{1,2,3,4};
int sum = accumulate(v.begin(), v.end(), 0);
cout << sum; // 10
```

---

## Custom Logic (Sum of Squares)

```cpp
int sum = accumulate(v.begin(), v.end(), 0,
    [](int s, int x){
        return s + x*x;
    });

cout << sum; // 30
```

### 📌 When to use?
- Prefix logic
- Matrix sum
- Custom reduction

LC: 1572

---

# 😲 min_element / max_element

## 🔹 What?
Find smallest or largest element.

```cpp
vector<int> v{5,1,9,3};

int mn = *min_element(v.begin(), v.end());
int mx = *max_element(v.begin(), v.end());

cout << mn; // 1
cout << mx; // 9
```

### 📌 When to use?
- Find max/min in array quickly
- Avoid manual loop

---

# 📤 lower_bound / upper_bound

⚠ Works only on sorted array

```cpp
vector<int> v{1,2,4,4,5};

auto it = lower_bound(v.begin(), v.end(), 4);
cout << (it - v.begin()); // index of first 4
```

### 📌 Difference:
- lower_bound → first ≥ value
- upper_bound → first > value

### 📌 When to use?
- Binary search
- First/last occurrence problems
- Range queries

LC: 744, 981

---

# 🌀 std::rotate()

## 🔹 Left Rotate

```cpp
vector<int> v{1,2,3,4};

rotate(v.begin(), v.begin()+1, v.end());
// Result: 2 3 4 1
```

### 📌 When to use?
- Array rotation problems

---

# 🔁 Check String Rotation

```cpp
string s = "abcde";
string t = "cdeab";

bool ans = (s.size()==t.size() &&
           (s+s).find(t)!=string::npos);
```

### 📌 When to use?
- Rotation validation problems

---

# ➡️ next_permutation()

```cpp
vector<int> v{1,2,3};

next_permutation(v.begin(), v.end());

// v becomes 1 3 2
```

### 📌 When to use?
- Generate permutations
- Next lexicographic arrangement

LC: 31

---

# ⏩ stringstream

## Convert String to Integer

```cpp
string s = "123";
stringstream ss(s);

int x;
ss >> x;

cout << x; // 123
```

---

## Count Words

```cpp
stringstream ss("hello world");
string word;
int count=0;

while(ss >> word)
    count++;

cout << count; // 2
```

### 📌 When to use?
- Parsing input
- Reverse words problems

LC: 151, 165

---

# 🤖 std::transform()

## Lowercase

```cpp
string s = "HELLO";

transform(s.begin(), s.end(), s.begin(), ::tolower);

cout << s; // hello
```

### 📌 When to use?
- String manipulation
- Case conversion problems

---

# 📟 std::regex_replace()

## Remove vowels

```cpp
string s = "mika";
regex rgx("[aeiouAEIOU]");

string result = regex_replace(s, rgx, "");
cout << result; // mk
```

### 📌 When to use?
- Pattern based replacement
- String cleanup problems

LC: 1108

---

# 🔢 std::count_if()

```cpp
vector<int> v{1,0,3,0,5};

int cnt = count_if(v.begin(), v.end(),
    [](int x){
        return x==0;
    });

cout << cnt; // 2
```

### 📌 When to use?
- Count elements with condition

LC: 1773

---

# 🔢 std::copy_if()

```cpp
vector<int> from{1,2,3,4,5};
vector<int> to;

copy_if(from.begin(), from.end(),
        back_inserter(to),
        [](int x){
            return x%2==0;
        });

// to = {2,4}
```

### 📌 When to use?
- Filtering data

---

# 🔢 set_difference()

```cpp
set<int> s1{1,2,3};
set<int> s2{2,3};

vector<int> result;

set_difference(s1.begin(), s1.end(),
               s2.begin(), s2.end(),
               back_inserter(result));

// result = {1}
```

### 📌 When to use?
- Find unique elements between sets

LC: 2215

---

# 📐 std::hypot()

```cpp
double dist = hypot(3.0,4.0);
cout << dist; // 5
```

### 📌 When to use?
- Distance calculation
- Geometry problems

LC: 812

---

# 🎯 Final Advice

✔ STL reduces code length  
✔ STL improves readability  
✔ Know when to use it  
✔ Practice in real problems  

Happy Coding 🚀
