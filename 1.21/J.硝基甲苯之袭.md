## J.硝基甲苯之袭

## 题目描述             

给定一个数组，问有多少对元素满足它们的gcd等于xor

### 解析：

- 对于每个数 x，我们可以枚举它的每一个因子 p，假设 p 是 x 和另一个数的最大gcd，接着，我们检查这个因子 p 是否真的符合 gcd 的定义，也就是验证 p 是否等于gcd(x,x^p)
- 如果验证通过，说明 p 确实是 gcd。这时，我们可以用一个映射（map 或数组）统计 x^p 出现的次数，然后用这些统计结果计算最终的答案。

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
	map<int, int> ma;
	cin >> n;
	for (int i = 1; i <= n; i++) {
		int k; cin >> k;
		ma[k]++;
	}
	int res = 0;
	for (int i = 1; i <= N; i++) {
		for (int j = i; j <= N; j += i) {
			if (i == __gcd(j, j ^ i) && j <= N)res += 1ll * ma[j] * ma[j ^ i];
		}
	}
	cout << res / 2;
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

