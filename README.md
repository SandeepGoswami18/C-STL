# 🚀 C++ STL Quick Help

It contains C++ STL usage and quick help with easy to understand comments and examples (copy + paste to use).  
I learned these while solving different kinds of problems.

I am using simple types like `int`, `string` etc for clarity.  
You can replace them with any data structure as needed.

🔎 EASY + IMPORTANT + MOST USED examples  

I have also added Leetcode question numbers where these STLs are useful.

---

# 📝 Different ways of using **priority_queue (Heap)** 🗻

## **Default Declarations (Max Heap)**

```cpp
priority_queue<int> pq;                          
priority_queue<int, vector<int>> pq;             
```

---

## **Using In-built Comparator (Min Heap)**

```cpp
priority_queue<int, vector<int>, greater<int>> pq;

priority_queue<pair<int, int>,
               vector<pair<int, int>>,
               greater<pair<int, int>>> pq;

priority_queue<pair<int, int>,
               vector<pair<int, int>>,
               greater<>> pq;
```

---

## **User Defined Comparator (Struct)**

```cpp
struct comp {
    bool operator()(int &a, int &b) {
        return a > b; // Min Heap
    }
};

priority_queue<int, vector<int>, comp> pq;
```

---

## **User Defined Comparator (Function)**

```cpp
static bool comp(int &a, int &b) {
    return a > b; // Min Heap
}

priority_queue<int,
               vector<int>,
               function<bool(int&, int&)>> pq(comp);
```

---

## **Using Lambda Function**

```cpp
auto comp = [](int &a, int &b) {
    return a > b; // Min Heap 
};

priority_queue<int,
               vector<int>,
               decltype(comp)> pq(comp);
```

### **Capturing External Variables**

```cpp
unordered_map<int, int> mp;

auto comp = [&mp](int &a, int &b) {
    return mp[a] < mp[b];
};
```

LC: 215, 347, 703

---

# 📝 When and Why to use **std::move()** ⬅️

Transfers resources efficiently without copying.

```cpp
string source = "MIK";
string target = move(source);

cout << source; // empty
cout << target; // MIK
```

### Example with vector

```cpp
vector<int> temp{1, 2, 3};
vector<vector<int>> result;

result.push_back(move(temp));
```

After moving, `temp` becomes empty.

---

# 📝 **std::accumulate()** ➕

## Basic Usage

```cpp
vector<int> nums{1, 3, 2, 5};
int sum = accumulate(begin(nums), end(nums), 0);

cout << sum; // 11
```

---

## With Lambda (Custom Logic)

```cpp
int sum = accumulate(begin(nums), end(nums), 0,
    [](int s, int n) {
        return s + n*n;
    });

cout << sum; // 39
```

---

## Handling 2D Matrix

```cpp
int result = accumulate(matrix.begin(), matrix.end(), 0,
    [](int sum, vector<int> row) {
        return sum + accumulate(begin(row), end(row), 0);
    });
```

LC: 1577, 1572

---

# 📝 **min_element / max_element / minmax_element** 😲

```cpp
vector<int> nums{1, 3, 2, 5};

int minimumValue = *min_element(begin(nums), end(nums));
int maximumValue = *max_element(begin(nums), end(nums));
```

OR

```cpp
auto itr  = minmax_element(begin(nums), end(nums));

int minimumValue  = *itr.first;  
int maximumValue  = *itr.second;
```

---

# 📝 **upper_bound() / lower_bound()** 📤

⚠ Works on sorted containers

```cpp
vector<int> vec{10,20,30,40};

auto up  = upper_bound(begin(vec), end(vec), 35);
auto low = lower_bound(begin(vec), end(vec), 35);
```

For set:

```cpp
st.upper_bound(35);
st.lower_bound(35);
```

For map:

```cpp
mp.upper_bound(35);
mp.lower_bound(35);
```

LC: 729, 981, 744, 1351

---

# 📝 **std::rotate()** 🌀

```cpp
vector<int> vec{1, 2, 3, 4};

rotate(vec.begin(), vec.begin()+2, vec.end());   
rotate(vec.begin(), vec.end()-2, vec.end());     
```

---

# 📝 Check if String Rotation Possible 🌀

```cpp
string s = "abcde";
string t = "cdeab";

bool ans = (s.length() == t.length() &&
           (s+s).find(t) != string::npos);
```

---

# 📝 **std::next_permutation()** ➡️

```cpp
vector<int> vec{1, 2, 3};

if(next_permutation(begin(vec), end(vec))){
    // next permutation generated
}
```

LC: 31

---

# 📝 **std::stringstream** ⏩

## Convert String to Number

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

while (ss >> word)
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

LC: 151, 165, 537, 1108

---

# 📝 **std::transform()** 🤖

```cpp
transform(begin(s), end(s), begin(s), ::tolower);
transform(begin(s), end(s), begin(s), ::toupper);
```

---

# 📝 **std::regex_replace()** 📟

```cpp
regex rgx("[aeiouAEIOU]");
string result = regex_replace(s, rgx, "");
```

```cpp
regex rgx("\\.");
string result = regex_replace(s, rgx, "[.]");
```

LC: 1108, 1119

---

# 📝 **std::count_if()** 🔢

```cpp
vector<int> vec{1, 3, 2, 0, 5, 0};

int count = count_if(begin(vec), end(vec),
    [](int x){
        return x == 0;
    });
```

LC: 1773

---

# 📝 **std::copy_if()** 🔢

```cpp
vector<int> from_vec{1,2,3,4,5,6};
vector<int> to_vec;

copy_if(from_vec.begin(), from_vec.end(),
        back_inserter(to_vec),
        [](int n){ return n%2==0; });
```

LC: 1796

---

# 📝 **set_difference() & back_inserter()** 🔢

```cpp
set<int> st1{1,2,3};
set<int> st2{2,3};

vector<int> v1;

set_difference(begin(st1), end(st1),
               begin(st2), end(st2),
               back_inserter(v1));
```

LC: 2215

---

# 📝 **std::hypot()** 📐

## 2D Distance

```cpp
double result = hypot(3.0, 4.0);
cout << result; // 5.0
```

## 3D Distance (C++17)

```cpp
double dist3D = hypot(1.0, 2.0, 2.0);
```

✔ Numerically stable  
✔ Cleaner than sqrt(x*x + y*y)

LC: 812

---

# 🎯 Final Notes

✔ STL reduces code size  
✔ STL improves readability  
✔ Learn when to use it  
✔ Practice using real problems  

Happy Coding 🚀
