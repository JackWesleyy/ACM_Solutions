## D.Tokitsukaze and Concatenate‌ Palindrome

## 题意：

给字符串a，b，可以对a进行打乱，替换字母的操作，然后接上b要求是回文字符串，问最小可以换掉几个字母

## 解析：

**消除重合部分**
由于可以重排 **a**，我们首先统计 **a** 中每个字母的频率，并利用这些字符去“覆盖” **b** 的字符（注意我们从 **b** 的末尾开始考虑，因为回文串中 **b** 处于右半部分，其镜像应该出现在 **a** 的前面）。

- 具体做法：
  - 将 **a** 中各字符的出现次数存入一个 map（或数组）中。
  - 从 **b** 的末尾开始（因为镜像对要求对应）遍历 **b** 中的字符。如果在 **a** 的字符统计中存在该字符，则使用该字符（计数减 1）；否则，说明 **a** 中缺少这个字符，需要后续通过替换来补上，这里用变量 **sum** 记录这种情况的个数。

**处理 a 中剩余字符的奇偶性**
在第一步消除后，map 中剩下的即为 **a** 中没有“匹配”到 **b** 的字符。此时，我们统计剩余字符中出现次数为奇数的种类数，记为 **ans**。

- 如果 **s = a + b** 总长度为偶数，则回文串要求所有字符均出现偶数次，此时只需要对剩余奇数的字符进行调整：每两种奇数只需一次替换就可以让它们成对（即使得它们中少一个字符出现次数变为偶数）。因此，替换次数为 `sum + (ans - sum) / 2`（当 ans > sum 时）；
- 如果 **s** 总长度为奇数，则允许中间有一个字符出现奇数次，多出的奇数仍需要调整；代码中的处理方法也是类似的思想。

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
const int N = 1010;
int n, m;
int x, y;
void solve() {
    int ans = 0, sum = 0;
    map<char, int> s;
    cin >> n >> m;
    string a, b;
    cin >> a >> b;
    if (m >= n)swap(a, b), swap(n, m);//保证 a 比 b 长
    for (int i = 0; i < n; i++)s[a[i]]++;
    for (int i = m - 1; i >= 0; i--)
    {
        if (!s[b[i]])sum++;
        else s[b[i]]--;
    }//消除重合部分
    for (auto i : s)
    {
        if (i.second % 2 == 1)ans++;
    }//处理 a 中剩余字符的奇偶性问题
    if (ans > sum)cout << sum + (ans - sum) / 2 <<endl;
    else cout << sum <<endl;
}
signed main() {    
    ios::sync_with_stdio(false); cin.tie(0), cout.tie(0);
    int T = 1; cin >> T;
    while (T--) {
        solve();
        n = 0, m = 0, x = 0, y = 0;
    }
}
```

