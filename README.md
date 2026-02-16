# 🚀 C++ STL Quick Help

It contains C++ STL usage and quick help with easy-to-understand comments and examples (copy + paste ready).

I learned these while solving different types of problems.

For simplicity, I am using basic types like `int`, `string`, etc.
You can replace them with any data structure as needed.

If you are confused about syntax or description, see the example carefully.
I have specifically chosen:

🔎 EASY + IMPORTANT + MOST USED examples

I have also added Leetcode question numbers where these STLs are very useful.

---

# 🗻 Different Ways of Using priority_queue (Heap)

## ✅ Default Declaration (Max Heap)

```cpp
priority_queue<int> pq;  
priority_queue<int, vector<int>> pq;
```

---

## ✅ Using In-built Comparator (Min Heap)

```cpp
priority_queue<int, vector<int>, greater<int>> pq;

priority_queue<pair<int,int>,
               vector<pair<int,int>>,
               greater<pair<int,int>>> pq;

priority_queue<pair<int,int>,
               vector<pair<int,int>>,
               greater<>> pq;
```

---

## ✅ User Defined Comparator (Struct)

```cpp
struct comp {
    bool operator()(int &a, int &b) {
        return a > b; // Min Heap
    }
};

priority_queue<int, vector<int>, comp> pq;
```

---

## ✅ User Defined Comparator (Function)

```cpp
static bool comp(int &a, int &b) {
    return a > b; // Min Heap
}

priority_queue<int,
               vector<int>,
               function<bool(int&, int&)>> pq(comp);
```

---

## ✅ Lambda Comparator

```cpp
auto comp = [](int &a, int &b) {
    return a > b; // Min Heap
};

priority_queue<int,
               vector<int>,
               decltype(comp)> pq(comp);
```

### Capturing External Variables

```cpp
unordered_map<int,int> mp;

auto comp = [&mp](int &a, int &b) {
    return mp[a] < mp[b];
};
```

📌 Useful in:
LC: 215, 347, 703

---

# ⬅️ std::move()

Used to transfer resources efficiently (avoids copying).

```cpp
string source = "MIK";
string target = move(source);
```

After move:
```
source becomes empty
target contains "MIK"
```

### Example with vector

```cpp
vector<int> temp{1,2,3};
vector<vector<int>> result;

result.push_back(move(temp));
```

📌 Efficient for large objects.

---

# ➕ std::accumulate()

## Basic Sum

```cpp
vector<int> nums{1,3,2,5};
int sum = accumulate(begin(nums), end(nums), 0);
```

---

## With Lambda (Custom Logic)

```cpp
int sum = accumulate(begin(nums), end(nums), 0,
    [](int s, int n){
        return s + n*n;
    });
```

---

## 2D Matrix Sum

```cpp
int result = accumulate(matrix.begin(), matrix.end(), 0,
    [](int sum, vector<int> row){
        return sum + accumulate(begin(row), end(row), 0);
    });
```

📌 Useful in:
LC: 1572, 1577

---

# 😲 min_element / max_element / minmax_element

```cpp
vector<int> nums{1,3,2,5};

int mn = *min_element(begin(nums), end(nums));
int mx = *max_element(begin(nums), end(nums));
```

OR

```cpp
auto p = minmax_element(begin(nums), end(nums));
int mn = *p.first;
int mx = *p.second;
```

---

# 📤 upper_bound / lower_bound

⚠ Works on sorted containers

## Vector

```cpp
vector<int> vec{10,20,30,40};

auto low = lower_bound(begin(vec), end(vec), 30);
auto up  = upper_bound(begin(vec), end(vec), 30);
```

## Set / Map

```cpp
st.lower_bound(key);
st.upper_bound(key);

mp.lower_bound(key);
mp.upper_bound(key);
```

📌 Useful in:
LC: 729, 981, 744, 1351

---

# 🌀 std::rotate()

```cpp
vector<int> vec{1,2,3,4};
rotate(vec.begin(), vec.begin()+2, vec.end()); // Left rotate
```

Right rotate:

```cpp
rotate(vec.begin(), vec.end()-k, vec.end());
```

---

# 🔁 Check String Rotation

```cpp
string s = "abcde";
string t = "cdeab";

bool ans = (s.length()==t.length() &&
           (s+s).find(t)!=string::npos);
```

---

# ➡️ std::next_permutation()

```cpp
vector<int> vec{1,2,3};

if(next_permutation(begin(vec), end(vec))){
    // next permutation generated
}
```

📌 LC: 31

---

# ⏩ stringstream

## String → Integer

```cpp
string s = "12345";
stringstream ss(s);

int x;
ss >> x;
```

---

## Count Words

```cpp
stringstream ss("hello world here");
string word;
int count = 0;

while(ss >> word)
    count++;
```

---

## Extract Numbers from String

```cpp
string complex = "1+1i";
stringstream ss(complex);

char skip;
int real, imag;

ss >> real >> skip >> imag >> skip;
```

📌 Useful in:
LC: 151, 165, 537, 1108

---

# 🤖 std::transform()

```cpp
transform(begin(s), end(s), begin(s), ::tolower);
transform(begin(s), end(s), begin(s), ::toupper);
```

---

# 📟 std::regex_replace()

## Remove Vowels

```cpp
regex rgx("[aeiouAEIOU]");
string result = regex_replace(s, rgx, "");
```

## Replace '.' with "[.]"

```cpp
regex rgx("\\.");
string result = regex_replace(s, rgx, "[.]");
```

📌 LC: 1108, 1119

---

# 🔢 std::count_if()

```cpp
vector<int> vec{1,3,2,0,5,0};

int cnt = count_if(begin(vec), end(vec),
    [](int x){
        return x == 0;
    });
```

📌 LC: 1773

---

# 🔢 std::copy_if()

```cpp
vector<int> from{1,2,3,4,5,6};
vector<int> to;

copy_if(begin(from), end(from),
        back_inserter(to),
        [](int n){
            return n%2==0;
        });
```

📌 LC: 1796

---

# 🔢 upper_bound with Custom Comparator

```cpp
vector<pair<int,string>> v;

auto lambda = [](const pair<int,string>& a,
                 const pair<int,string>& b){
    return a.first < b.first;
};

pair<int,string> ref = {timestamp, ""};

auto it = upper_bound(begin(v), end(v), ref, lambda);
```

📌 LC: 981

---

# 🔢 Lambda in unordered_map

```cpp
unordered_map<string,
    function<int(int,int)>> mp = {
    {"+", [](int a,int b){return a+b;}},
    {"-", [](int a,int b){return a-b;}},
    {"*", [](int a,int b){return a*b;}},
    {"/", [](int a,int b){return a/b;}}
};

int result = mp["+"](1,2);
```

📌 LC: 150

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

📌 LC: 2215

---

# 📐 std::hypot()

## 2D Distance

```cpp
double dist = hypot(x2-x1, y2-y1);
```

## 3D Distance (C++17)

```cpp
double dist = hypot(x,y,z);
```

📌 Safer than sqrt(x*x + y*y)

📌 LC: 812

---

# 🎯 Final Notes

✔ STL reduces code size  
✔ STL improves readability  
✔ Know when to use it  
✔ Practice applying in problems  

Happy Coding 🚀
