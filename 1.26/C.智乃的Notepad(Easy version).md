## C.智乃的Notepad(Easy version)

## 题意：

给n个单词，键盘上只能输入字母和退格，问最少敲击多少次键盘可以表示出所有字母

## 解析：

### 题目分析

题目结果应该为2*(字符串总长度)-2*（总公共前缀长度）-最长字符串

#### 贪心

- 要最小化公式，就需要最大化字符串之间的公共前缀总和
- 字典序排序可以让相邻的字符串的公共前缀尽可能大

#### 排序

- 将所有字符串按字典序排序：
  - 若长度相等，则直接按字典序比较
  - 若长度不等，则长度短的排在前面
- 排序后的字符串排列能够保证公共前缀长度的和尽可能大

#### 计算

- 遍历排序后的字符串数组，计算：
  - 总长度：每个字符串的长度 |Si|
  - 总公共前缀长度：相邻字符串的最长公共前缀 lcp(Si,Si−1)
- 最后减去最长字符串的长度即可

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
const int N = 100010;
int s[N];
int n, m;
int x, y;
int sum;
int lcp(const string& a, const string& b) {
	int i = 0;
	while (i < a.size() && i < b.size() && a[i] == b[i]) ++i;
	return i;
}
int mina(vector<string>& words) {
	sort(words.begin(), words.end());
	int sum = 0, max_len = 0;
	for (int i = 0; i < words.size(); ++i) {
		sum += words[i].size() * 2;
		if (i > 0) sum -= lcp(words[i], words[i - 1]) * 2;
		max_len = max(max_len, (int)words[i].size());
	}
	return sum - max_len;
}
void solve() {
	cin >> n >> m;
	vector<string> words(n);
	for (int i = 0; i < n; i++) {
		cin >> words[i];
	}
	cout << mina(words) << endl;
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

