## M.数值膨胀之美

## 题目描述             

给定一个数组，可以选择一个区间将所有元素乘2，问操作后的最小极差

### 解析：

极差最小化，优先考虑增大最小值，扩大区间时，尽量只在包含最小值和次小值的范围里面操作

1.对数组按值排序，这样方便找到当前最小值以及次小值。

2.使用两个指针维护当前区间的范围l,r，动态计算区间内的最大值。

3.对于每一个当前最小值 a[i]，尝试更新区间范围并计算可能的极差，记录最优解。

时间复杂度是 O(nlog⁡n)

```c++
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define endl '\n'
#define PII pair<int,int>
#define fi first
#define se second
#define MAX 1e9
#define itn int
#define bce(x) x.begin(),x.end()
const double PI = acos(-1);
const int mod = 1e9 + 7;
const int N = 200010;
int s[N];
int n, m;
int x, y;
int sum;
bool static cmp(PII a, PII b) {
	//if (a.first == b.fi)return a.second < b.second;else return a.fi < b.fi;
	return a.se < b.se;
}
void solve() {
	vector<PII> a;
	vector<int> b;
	cin >> n;
	a.push_back({ 0,0 });//占位置，不用
	b.push_back(0);//占位置,不用
	for (int i = 1; i <=n; i++) {
		int k, p;
		cin >> k;
		p = i;
		a.push_back({ k,p });
		b.push_back(a[i].first);
	}
    
	a.push_back({ INT_MAX,n+1 });// 添加一个无穷大位，方便处理边界问题
	sort(bce(a));
	int l = a[1].second, r = a[1].second;// 初始化双指针区间 [l, r]，初始只包含最小值的索引
	int ma = max(a[1].first * 2, a[n].fi);// 初始最大值，考虑当前最小值翻倍后的情况
	int res = ma - min(a[1].first * 2, a[2].fi);// 初始极差
	for (int i = 2; i <=n; i++) {
		while (a[i].second < l)
			l--, ma = max(ma, b[l] * 2);// 更新左指针和最大值
		while (a[i].second > r)
			r++, ma = max(ma, b[r] * 2);// 更新右指针和最大值
		res = min(res, ma - min(a[1].first * 2, a[i + 1].fi));// 更新最小极差
	}
	cout << res;
}

signed main() {
	ios::sync_with_stdio(false); cin.tie(0), cout.tie(0);
	int T = 1;//cin>>T;
	while (T--) {
		solve();
		n = 0, m = 0, x = 0, y = 0, sum = 0;
	}
}	
```

