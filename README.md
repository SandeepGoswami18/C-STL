# 🚀 C++ STL Quick Help (Interview + Leetcode Ready)

This repository contains **most used + important STL utilities** with clean syntax and simple examples.  
All examples use basic data types like `int`, `string` for clarity.

---

# 🗻 priority_queue (Heap)

## ✅ Max Heap (Default)

```cpp
priority_queue<int> pq;
priority_queue<int, vector<int>> pq;
```

## ✅ Min Heap (Using Inbuilt Comparator)

```cpp
priority_queue<int, vector<int>, greater<int>> pq;

priority_queue<pair<int,int>,
               vector<pair<int,int>>,
               greater<pair<int,int>>> pq;
```

## ✅ Custom Comparator (Struct)

```cpp
struct comp {
    bool operator()(int &a, int &b) {
        return a > b; // Min Heap
    }
};

priority_queue<int, vector<int>, comp> pq;
```

## ✅ Lambda Comparator

```cpp
auto comp = [](int &a, int &b) {
    return a > b; // Min Heap
};

priority_queue<int, vector<int>, decltype(comp)> pq(comp);
```

📌 Common Use Cases:
- Top K Elements
- Kth Largest Element
- Merge K Sorted Lists  
LC: 215, 347, 703

---

# 🔁 std::move()

Transfers ownership of resources (avoids copying).

```cpp
string s = "Hello";
string t = move(s);
```

After move:
```
s becomes empty
t gets data
```

Example with vector:

```cpp
vector<int> temp{1,2,3};
vector<vector<int>> result;

result.push_back(move(temp));
```

📌 Use when pushing large vectors/strings.

---

# ➕ std::accumulate()

## Sum of vector

```cpp
vector<int> v{1,2,3,4};
int sum = accumulate(begin(v), end(v), 0);
```

## With Lambda

```cpp
int sum = accumulate(begin(v), end(v), 0,
    [](int s, int n) {
        return s + n*n;
    });
```

LC: 1572, 1577

---

# 🔍 min_element / max_element / minmax_element

```cpp
vector<int> v{1,3,2,5};

int mn = *min_element(begin(v), end(v));
int mx = *max_element(begin(v), end(v));
```

OR

```cpp
auto p = minmax_element(begin(v), end(v));
int mn = *p.first;
int mx = *p.second;
```

---

# 📤 upper_bound / lower_bound

⚠ Works only on sorted data.

## Vector

```cpp
vector<int> v{1,2,3,4,5};

auto it1 = lower_bound(begin(v), end(v), 3);
auto it2 = upper_bound(begin(v), end(v), 3);
```

## Map / Set

```cpp
mp.lower_bound(key);
mp.upper_bound(key);
```

LC: 729, 981, 744

---

# 🌀 std::rotate()

```cpp
vector<int> v{1,2,3,4};
rotate(v.begin(), v.begin()+2, v.end()); // Left rotate
```

Right rotate:

```cpp
rotate(v.begin(), v.end()-k, v.end());
```

---

# 🔁 Check String Rotation

```cpp
string s = "abcde";
string t = "cdeab";

if(s.size() == t.size() && (s+s).find(t) != string::npos)
    cout << "Yes";
```

---

# ➡️ next_permutation()

```cpp
vector<int> v{1,2,3};

next_permutation(begin(v), end(v));
```

LC: 31

---

# ⏩ stringstream

## String → Integer

```cpp
string s = "123";
stringstream ss(s);

int x;
ss >> x;
```

## Count Words

```cpp
stringstream ss("hello world here");
string word;
int count = 0;

while(ss >> word)
    count++;
```

LC: 151, 165, 537

---

# 🤖 std::transform()

## Lowercase

```cpp
transform(begin(s), end(s), begin(s), ::tolower);
```

## Uppercase

```cpp
transform(begin(s), end(s), begin(s), ::toupper);
```

---

# 📟 std::regex_replace()

## Remove vowels

```cpp
regex rgx("[aeiouAEIOU]");
string result = regex_replace(s, rgx, "");
```

## Replace '.' with [.]

```cpp
regex rgx("\\.");
regex_replace(s, rgx, "[.]");
```

LC: 1108, 1119

---

# 🔢 std::count_if()

```cpp
vector<int> v{1,2,0,4,0};

int cnt = count_if(begin(v), end(v),
    [](int x){
        return x == 0;
    });
```

---

# 🔢 std::copy_if()

```cpp
vector<int> from{1,2,3,4,5};
vector<int> to;

copy_if(begin(from), end(from),
        back_inserter(to),
        [](int x){
            return x % 2 == 0;
        });
```

---

# 🔢 upper_bound with custom comparator

```cpp
vector<pair<int,string>> v;

auto lambda = [](const pair<int,string>& a,
                 const pair<int,string>& b) {
    return a.first < b.first;
};

pair<int,string> ref = {timestamp, ""};

auto it = upper_bound(begin(v), end(v), ref, lambda);
```

LC: 981

---

# 🔢 Lambda in unordered_map

```cpp
unordered_map<string, function<int(int,int)>> mp = {
    {"+", [](int a, int b){ return a+b; }},
    {"-", [](int a, int b){ return a-b; }},
    {"*", [](int a, int b){ return a*b; }},
    {"/", [](int a, int b){ return a/b; }}
};

int result = mp["+"](1,2);
```

LC: 150

---

# 🔢 set_difference()

```cpp
set<int> s1{1,2,3};
set<int> s2{2,3};

vector<int> result;

set_difference(begin(s1), end(s1),
               begin(s2), end(s2),
               back_inserter(result));
```

LC: 2215

---

# 📐 std::hypot()

## 2D Distance

```cpp
double dist = hypot(x2-x1, y2-y1);
```

## 3D (C++17)

```cpp
double dist = hypot(x, y, z);
```

LC: 812

---

# 🎯 Final Notes

✔ STL reduces code size  
✔ STL improves readability  
✔ Focus on when to use it  
✔ Practice using these in real problems  

Happy Coding 🚀
