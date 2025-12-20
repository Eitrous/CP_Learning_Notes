## 三分屏配置
- 在文件夹下新建三个文件：`solution.cpp`，`input.txt`，`output.txt`
- 在 VS Code 中同时打开它们
- 调整布局：
  - 把 `solution.cpp` 放在左边
  - 把 `input.txt` 拖动到右上角
  - 把 `output.txt` 拖动到右下角
- 代码重定向：
```cpp
#ifndef ONLINE_JUDGE
freopen("input.txt", "r", stdin);
freopen("output.txt", "w", stdout);
#endif
```
- 输出调试信息：
```cpp
#ifndef ONLINE_JUDGE
    cerr << "Debug: 当前变量 x 的值是 " << x << endl;
#endif
```

## 基础模板
```cpp
#include<bits/stdc++.h>
#define endl '\n'
#define int long long
using namespace std;

//const int N = 1e5 + 10;

void solve()
{

}

signed main()
{
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int _ = 1;
    //cin >> _;
    while (_--)
        solve();
    return 0;
}
```

## 高精度

### I/O
```cpp
void solve()
{
    string a;
    vector<int> A;

    //输入
    cin >> a;
    for (int i = a.size()-1; i >= 0; i--)
        A.push_back(a[i] - '0');

    //输出
    for (int i = A.size()-1; i >= 0; i--)
        cout << A[i];

}
```

### BI + BI
```cpp
vector<int> add(vector<int> &A, vector<int> &B)
{
	if (B.size() > A.size())
        return add(B,A);

	vector<int> C;
	int t = 0;
	for (int i = 0; i < A.size(); i++){
		t += A[i];
		if(i < B.size()) t+= B[i];
		C.push_back(t % 10);
		t = t > 9 ? 1 : 0;
	}
	if (t)
        C.push_back(1);
	return C;
}
```

### BI - BI
```cpp
vector<int> sub(vector<int> &A, vector<int> &B)
{
	vector<int> C;
	int t = 0;
	for (int i = 0; i < A.size(); i++){
		t = A[i] - t;
		if(i < B.size()) t -= B[i];
		C.push_back((t+10) % 10);
		t = t < 0 ? 1 : 0;
	}
	while (C.size() > 1 && C.back() == 0)
        C.pop_back();
	return C;
}

bool cmp(vector<int> &A, vector<int> &B) // 若A>=B返回true，否则返回false
{
	if (A.size() != B.size())
        return A.size() > B.size();
	for (int i = A.size()-1; i >= 0; i--){
		if(A[i] != B[i])
            return A[i] > B[i];
	}
	return true;
}

void solve()
{
    vector<int> C;
    if(cmp(A, B))
        C = sub(A, B);
    else
        C = sub(B, A); // 这种情况输出为负值
}
```

### BI * I
```cpp
vector<int> mul(vector<int> &A, int b)
{
	vector<int> C;
	int t = 0;
	for (int i = 0; i < A.size() || t; i++){
		if(i < A.size()) t += A[i] * b;
		C.push_back(t % 10);
		t /= 10;
	}
	while (C.size() > 1 && C.back() == 0)
        C.pop_back();
	return C;
}
```

### BI / I
```cpp
vector<int> div(vector<int> &A, int b, int &r)
{
	vector<int> C;
	r = 0;
	for (int i = A.size()-1; i >= 0; i--){
		r = r*10 + A[i];
		C.push_back(r/b);
		r %= b;
	}
	reverse(C.begin(),C.end());
	while (C.size() > 1 && C.back() == 0)
        C.pop_back();
	return C;
}
```

## 排序

## 二分         

## 前缀和

### 一维
```cpp
void solve()
{

}
```

### 二维
```cpp
void solve()
{

}
```

## 差分

### 一维
```cpp
void solve()
{

}
```

### 二维
```cpp
void solve()
{

}
```

## DFS
```cpp
void solve()
{

}
```

## BFS
```cpp
void solve()
{

}
```



## 单调栈
```cpp
void solve()
{

}
```

## 单调队列

### STL写法
```cpp
// 滑动窗口类
void solve()
{
    // 输入
    for (int i = 0; i < len; i++)
        cin >> ary[i];
    deque<int> dq;// 存放下标,队首为最优值对应下标
    for (int i = 0; i < len; i++){// 以i为右端点，大小为k的窗口
        while (dq.size() && dq.front() <= i-k)
            dq.pop_front();// 保证队首合法（在窗口内）
        while (dq.size() && ary[dq.back()] ___ ary[i])
            dq.pop_back();// 保证队尾比新元素更优越
        dq.push_back(i);
        // 输出或其他处理
    }

    dq = deque<int>();// 清空（可选）
    while (dq.size())
        dq.pop_back();// 另一种清空方式
} 
```

### 数组写法
```cpp
void solve()
{
    // 输入
    for (int i = 0; i < len; i++)
        cin >> ary[i];
    int dq[N],hh,tt;// hh表示窗口左端，tt表示窗口右端
    for (int i = 0; i < len; i++){
        while (hh <= tt && dq[hh] <= i-k)
            hh++;
        while (hh <= tt && ary[dq[tt]] ___ ary[i])
            tt--;
        dq[++tt] = i;
        // 输出或其他处理
    }
    // 清空
    hh = 1, tt = 0;
}
```

## 树状数组

### 单点修改

```cpp
int ft[MAXN];

// 查询(0,pos]的区间和
int query(int pos)
{
    int ans = 0;
    for (int i = pos; i; i -= i & -i)
        ans += ft[i];
    return ans;
}

// 查询[l,r]的区间和
inline int query(int l, int r)
{
    return query(r) - query(l-1);
}

// 第pos位加上val
void update(int pos, int val)
{
    for (int i = pos; i <= n; i += i & -i) // n为数组大小
        ft[i] += val;
}

```

### 区间修改（也可单点修改）

```cpp
int t[MAXN],ti[MAXN];

void update(int pos, int val)
{
    for (int i = pos; i <= n; i += i & -i) // n为数组大小
        t[i] += val, ti[i] += pos * val;
}

// 区间[l,r]加上val
inline void update(int l, int r, int val)
{
    update(l, val), update(r + 1, -val);
}

// 查询(0,pos]的区间和
int query(int pos)
{
    int ans = 0;
    for (int i = pos; i > 0; i -= i & -i)
        ans += (pos+1) * t[i] - ti[i];
    return ans;
}

// 查询[l,r]的区间和
inline int query(int l, int r)
{
    return query(r) - query(l-1);
}
```