## 三分屏配置
> Gemini倾情贡献
- 在文件夹下新建三个文件：`solution.cpp`，`input.in`，`output.out`
- 在 VS Code 中同时打开它们
- 调整布局：
  - 把 `solution.cpp` 放在左边
  - 把 `input.in` 拖动到右上角
  - 把 `output.out` 拖动到右下角
- 代码重定向：
```cpp
#ifndef ONLINE_JUDGE
freopen("input.in", "r", stdin);
freopen("output.out", "w", stdout);
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
    #ifndef ONLINE_JUDGE
    freopen("input.txt", "r", stdin);
    freopen("output.txt", "w", stdout);
    #endif
    
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

### BI * BI
```cpp

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

<font color = red> 蓝大人给的，直接抄下来了 </font>
<font color = red> 记得修改！！！ </font>
<font color = red> 记得修改！！！ </font>
<font color = red> 记得修改！！！ </font>

```cpp
void solve()
{
    #include <iostream>
#include <queue>
#include <cstring> // 用于memset

using namespace std;

// 定义最大范围，别到时候RE了哭着来找我
const int MAXN = 1005;
const int INF = 0x3f3f3f3f;

// 地图与距离数组
int mp[MAXN][MAXN]; // 存图，0空地，1障碍
int dist[MAXN][MAXN]; // 存起点到(x,y)的最短距离
int n, m; // 行数，列数

// 方向数组！这点小技巧都不会的话就趁早退役吧
// 对应：上、下、左、右
int dx[] = {-1, 1, 0, 0};
int dy[] = {0, 0, -1, 1};

struct Node {
    int x, y;
};

void bfs(int sx, int sy, int ex, int ey) {
    // 1. 初始化
    // 把距离数组初始化为无穷大，表示未访问
    memset(dist, -1, sizeof(dist)); 
    
    queue<Node> q;
    
    // 2. 起点入队
    q.push({sx, sy});
    dist[sx][sy] = 0; // 起点距离为0
    
    while (!q.empty()) {
        // 3. 取出队首
        Node cur = q.front();
        q.pop();
        
        // 这里的 cur.x, cur.y 就是当前层级的节点
        // 如果题目要求到达终点立刻停止，可以在这里判断
        if (cur.x == ex && cur.y == ey) {
            cout << dist[cur.x][cur.y] << endl;
            return;
        }
        
        // 4. 扩展节点（向四个方向）
        for (int i = 0; i < 4; i++) {
            int nx = cur.x + dx[i];
            int ny = cur.y + dy[i];
            
            // 5. 合法性判断（这是重点！别写漏了！）
            // 越界了吗？是障碍物吗？是不是已经访问过了（dist != -1）？
            if (nx >= 1 && nx <= n && ny >= 1 && ny <= m && 
                mp[nx][ny] == 0 && dist[nx][ny] == -1) {
                
                // 更新距离并入队
                dist[nx][ny] = dist[cur.x][cur.y] + 1;
                q.push({nx, ny});
            }
        }
    }
    
    cout << "No Solution! 笨蛋！" << endl;
}

int main() {
    // 这种IO优化还需要我提醒你吗？
    ios::sync_with_stdio(false);
    cin.tie(0);
    
    cin >> n >> m;
    for(int i=1; i<=n; ++i)
        for(int j=1; j<=m; ++j)
            cin >> mp[i][j];
            
    // 假设从(1,1)走到(n,m)
    bfs(1, 1, n, m);
    
    return 0;
}
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