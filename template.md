## 基础模板
```cpp
#include<bits/stdc++.h>
#define endl '\n'
#define int long long
using namespace std;

const int N = 1e5 + 10;

void solve()
{

}

signed main()
{
    ios::sync_with_stdio(0),cin.tie(0),cout.tie(0);
    int _ = 1;
    //cin >> _;
    while(_--) solve();
    return 0;
}
```

## 高精度

### I/O
```cpp
void solve()
{

}
```

### BI + BI
```cpp
void solve()
{

}
```

### BI - BI
```cpp
void solve()
{

}
```

### BI * BI
```cpp
void solve()
{

}
```

### BI / BI
```cpp
void solve()
{

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
//滑动窗口类
void solve()
{
    //输入
    for(int i = 0; i < len; i++) cin >> ary[i];
    deque<int> dq;//存放下标,队首为最优值对应下标
    for(int i = 0; i < len; i++){//以i为右端点，大小为k的窗口
        while(dq.size() && dq.front() <= i-k) dq.pop_front();//保证队首合法（在窗口内）
        while(dq.size() && ary[dq.back()] ___ ary[i]) dq.pop_back();//保证队尾比新元素更优越
        dq.push_back(i);
        //输出或其他处理
    }

    dq = deque<int>();//清空（可选）
    while(dq.size()) dq.pop_back();//另一种清空方式
} 
```

### 数组写法
```cpp
void solve()
{
    //输入
    for(int i = 0; i < len; i++) cin >> ary[i];
    int dq[N],hh,tt;//hh表示窗口左端，tt表示窗口右端
    for(int i = 0; i < len; i++){
        while(hh <= tt && dq[hh] <= i-k) hh++;
        while(hh <= tt && ary[dq[tt]] ___ ary[i]) tt--;
        dq[++tt] = i;
        //输出或其他处理
    }
    //清空
    hh = 1, tt = 0;
}
```