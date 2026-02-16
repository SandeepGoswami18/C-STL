C++ STL Quick Help
It contains C++ STLs usage and quick help with easy to understand comments and examples (copy+paste to use). I learned these while solving different kinds of Leetcode Questions.
I will be using "int, string etc" for ease and not complex entities like pairs, structs etc 😉. You can replace it with any data structure If you are confused with the syntax or description, see the example. I am sure that will clear things BECAUSE I have specifically chosen
🔎 "EASY + IMPORTANT + MOST USED" examples. Last but not least, I have added Leetcode Qns also which can be easily solved using STLs

📝Different ways of using priority_queue (i.e. heap) 🗻
Default declarations
priority_queue<int> pq;                            //creates max-heap
priority_queue<int, vector<int>> pq;               //creates max-heap

writing comparator function for priority_queue
1. Using in-built comparator provided by C++ : 

priority_queue<int, vector<int>, greater<int>> pq;  //creates min-heap
priority_queue< pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>> > pq; //min_heap of pairs
priority_queue< pair<int, int>, vector<pair<int, int>>, greater<> > pq;               //min_heap of pairs
2. Using user defined comparator as a structure

struct comp {
    bool operator()(int &a, int &b) {
        return a<b; //max-heap
        return a>b; //min-heap
    }
};

priority_queue<int, vector<int>, comp> pq;  //usage
3. Using user defined comparator as a function

static bool comp(int &a, int &b) {
    return a<b; //max-heap
    return a>b; //min-heap
}

priority_queue<int, vector<int>, function<bool(int&, int&)> > pq(comp);   //usage
4. Using lambda function

auto comp = [](int &a, int &b) {
    return a<b; //max-heap
    return a>b; //min-heap 
};

priority_queue<int, vector<int>, decltype(comp) > pq(comp);   //usage

NOTE :
You can receive parameters inside [] as well i.e. auto comp = [some_parameters]
Ex : You want to access a map inside this lambda function
unordered_map<int, int> mp;

auto comp = [&mp](int &a, int &b) {
    return mp[a] < mp[b]; //etc.
};

📝 When and why to use std::move() ⬅️
/*
    To efficiently transfer the resources from source to target.
    By efficient, I mean no usage of extra space and time for creating copy.
*/
Examples :
    string source = "MIK";
    string target = "";
    target = std::move(source);
    cout << " source = " << source << endl;
    cout << "target = "  << target << endl;
    /*
        output :
        source = 
        target = "MIK"
    */
    
    vector<string> v;
    string str = "example";
    v.push_back(std::move(str));
    /*
    After this, str becomes empty i.e. ""
    And while moving str inside v, no extra copy of str was done implicitly.
    */

    vector<int> temp{1, 2, 3};
    vector<vector<int>> result;
    result.push_back(std::move(temp));
    /*
    This allows no copy of "temp" being created.
    It ensures that the contents of "temp"
    will be moved into the "result".  This is less
    expensive, also means temp will now be empty.
    */

📝 std::accumulate(begin_iterator, end_iterator, initial_sum) ➕
int sum = 0;
vector<int> nums{1, 3, 2, 5};
sum = accumulate(begin(nums), end(nums), 0);

cout << sum; //11

📝 std::accumulate(begin_iterator, end_iterator, initial_sum, lambda) ➕
Example-1 : 

auto lambda = [&](int s, long n) {
    return s + n*n;
};

int sum = 0;
vector<int> nums{1, 3, 2, 5};
sum = accumulate(begin(nums), end(nums), 0, lambda);

cout << sum; //39

Example-2 : Handling 2-D matrix
auto lambda = [&](int sum, vector<int> vec) {
    sum = sum + accumulate(begin(vec), end(vec), 0);
    return sum;
};

int result =  accumulate(matrix.begin(), matrix.end(), 0, lambda);

📝 min_element(begin_iterator, end_iterator), max_element(begin_iterator, end_iterator), minmax_element(begin_iterator, end_iterator) 😲
vector<int> nums{1, 3, 2, 5};

int minimumValue = *min_element(begin(nums), end(nums));
int maximumValue = *max_element(begin(nums), end(nums));

auto itr  = minmax_element(begin(nums), end(nums));
int minimumValue2  = *itr.first;
int maximumValue2  = *itr.second;

📝 upper_bound(), lower_bound() in sorted vector, ordered set, ordered map 📤
vector<int> vec{10,20,30,30,20,10,10,20};

vector<int>::iterator up  = upper_bound(begin(vec), end(vec), 35);
vector<int>::iterator low = lower_bound(begin(vec), end(vec), 35);

st.upper_bound(35);
st.lower_bound(35);

mp.upper_bound(35);
mp.lower_bound(35);

📝 std::rotate 🌀
vector<int> vec{1, 2, 3, 4};
int n = vec.size();
int k = 2;

rotate(vec.begin(), vec.begin()+k, vec.end());
rotate(vec.begin(), vec.begin()+n-k, vec.end());

📝 To check if some rotation of string s can become string t 🌀
string s = "abcde";
string t = "cdeab";

cout << (s.length() == t.length() && (s+s).find(t) != string::npos) << endl;

📝 std::next_permutation ➡️
vector<int> vec{1, 2, 3, 4};
    
if(next_permutation(begin(vec), end(vec)))
    cout << "Next permutation available" << endl;

for(int &x : vec)
    cout << x << " ";

📝 std::stringstream ⏩
string s = "12345";
stringstream ss(s);
int x = 0;
ss >> x;
cout << x;

📝 std::transform 🤖
string line = "Hello world, this is MIK";
transform(begin(line), end(line), begin(line), ::tolower);
transform(begin(line), end(line), begin(line), ::toupper);

📝 std::regex_replace 📟
string s2 = "mika";
auto rgx = regex("[aeiouAEIOU]");
cout << regex_replace(s2, rgx, "");

📝 std::count_if 🔢
vector<int> vec2{1, 3, 2, 0, 5, 0};
auto lambda2 = [&](const auto& i) {
    return i == 0;
};
cout << count_if(begin(vec2), end(vec2), lambda2);

📝 std::copy_if 🔢
vector<int> from_vec = {1,2,3,4,5,6,7,8,9,10};
vector<int> to_vec;
copy_if(from_vec.begin(), from_vec.end(), back_inserter(to_vec),[](int n){return n%2==0;});

📝 std::set_difference and std::back_inserter 🔢
set<int> st1, st2;
vector<int> v1;
set_difference(begin(st1), end(st1), begin(st2), end(st2), back_inserter(v1));

📝 std::hypot 📐
double x1 = 1, y1 = 2;
double x2 = 4, y2 = 6;
double dist = std::hypot(x2 - x1, y2 - y1);
cout << dist;
