## D.字符串里串

## 题意：

给个字符串，求一个连续子串跟一个不连续子串的最大相同长度k

## 解析：

最开始我的做法是，先统计所有字母的出现次数，然后对于每个出现次数大于一次的字母，找到他倒数第二次出现的位置，然后从最开始到倒数第二次出现的位置就是最长的，但是少考虑了从最后开始往前数。

正确做法是：既要考虑第一段包含一个字母，也要考虑第二段包含一个字母。

```c++
#include<bits/stdc++.h>
#include<unordered_map>
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
const int N = 100010;
int s[N];
int n, m;
int x, y;
int sum;
bool static cmp(PII a, PII b) {
	//if (a.first == b.fi)return a.second < b.second;else return a.fi < b.fi;
	return a.se < b.se;
}
void solve() {
	string s;
	cin >> n >> s;
	s = "#" + s;//防止边界问题
	int ans = 0;
	for (int ch = 'a'; ch <='z'; ch++) {
		int a = 0, b = 0; 
		for (int i = 1; i <= n; i++) {
			if (s[i] != ch) continue;
			if (a != 0) 
				ans = max(ans, n-i + 1);
			a = i;
		}
		for (int i = n; i >= 1; i--) {
			if (s[i]!= ch) continue;
			if (b != 0)
				ans = max(ans, i);
			b = i;
		}
	}
	if (ans == 1)cout << 0;
	else cout << ans;
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

