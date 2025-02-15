## J.铁刀磨成针

## 题意：

在给定的回合数、初始攻击力和磨刀石数量下，最大化刀造成的伤害，每回合可以选择磨刀（提升攻击力）或攻击（造成伤害并减少攻击力），磨刀石用完后只能攻击，且攻击力降为零时刀损坏

## 解析：

1. **磨刀阶段策略：** 磨刀是一个固定的策略，因为磨刀在任何时候都不会吃亏，所以从第一回合开始连续磨刀，直到磨刀石用完或回合结束。

1. **砍的策略：** 砍的时机要从某一回合开始持续砍下去。关键在于找到一个最优的开始砍的时机。枚举能砍的回合


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
const int N = 1e6 + 5;
void solve() {
	cin >> n >> x >> y;
    int ans  = 0;
    for(int i = 1;i <= y;i ++){
        if(i > n) break;
        int a = min(n, y) - i;
        int b = min(x + i, n - min(n, y) + 1);
        ans = max(ans, a * (x + i) + (x +i + x + i - b + 1) * b / 2);
    }
    cout << ans << endl;
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

