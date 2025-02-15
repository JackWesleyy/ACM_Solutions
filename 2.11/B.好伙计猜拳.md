## B.好伙计猜拳

## 题意：

根据给定的比赛记录序列和操作代价，找到使得比赛记录合法的最小代价。合法的比赛记录要求后续的得分序列不能低于前面的得分,对于每一条记录 (ai, bi) 和 (ai+1, bi+1)：ai+1>=ai,bi+1>=bi

## 解析：

**状态转移：** 对于每一条比赛记录 `(ai, bi)`，要判断当前记录是否可以合法地和前面的记录连接（无论是交换了分数还是没有交换）。如果可以合法连接：

如果不交换当前记录，前面的状态 `dp[j][0]` 继续推进，且删除所有记录的代价为 `(i - j - 1) * c1`。

如果交换当前记录，前面的状态 `dp[j][1]` 继续推进，并且需要考虑交换的代价 `c2`。

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
int n, m;
int x, y;
int sum;
const int N = 2e5+10;
int a[N], b[N];
int dp[N][2]; 
void solve() {
    int c1, c2; 
    cin >> n >> c1 >> c2;
    for (int i = 1; i <= n; i++) cin >> a[i] >> b[i];
    int ans = 1e12;
    for (int i = 1; i <= n; i++) {
        dp[i][0] = dp[i][1] = 1e12; 
        for (int j = 0; j < i; j++) {
            if (a[i] >= a[j] && b[i] >= b[j]) {
                dp[i][0] = min(dp[i][0], dp[j][0] + (i - j - 1) * c1);
                dp[i][1] = min(dp[i][1], dp[j][1] + (i - j - 1) * c1 + c2);
            }
            if (a[i] >= b[j] && b[i] >= a[j]) {
                dp[i][0] = min(dp[i][0], dp[j][1] + (i - j - 1) * c1);
                dp[i][1] = min(dp[i][1], dp[j][0] + (i - j - 1) * c1 + c2);
            } 
        }
        ans = min({ ans,(n - i) * c1 + dp[i][0],(n - i) * c1 + dp[i][1] });
    }
    cout << ans <<endl;
}

signed main() {
    ios::sync_with_stdio(false); cin.tie(0), cout.tie(0);
    int T = 1; cin >> T;
    while (T--) {
        solve();
        n = 0, m = 0, x = 0, y = 0, sum = 0;
    }
}
```

