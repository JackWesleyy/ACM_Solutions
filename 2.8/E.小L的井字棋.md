## E.小L的井字棋

## 题意：

下井字棋，小L可以走两步，判断是否必胜

## 解析：

1. **棋子数较少时（cnt ≤ 4）**：
   - 棋盘空位较多，小L有足够空间通过两次连续落子构造必胜局面
2. **棋子数较多时（cnt > 4）**：
   - 检查是否存在某行、列或对角线满足条件：仅包含X和空位（G），且无O，如果存在，小L可以直接获胜，若不存在则不行

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
string s[4] = {};
bool check(char a, char b, char c) {
    int x = 0, o = 0, g = 0;
    for (auto i : { a,b,c }) {
        if (i == 'X')x++;
        else if (i == 'O')o++;
        else g++;
    }
    if (!o && x) {
        return 1;
    }
    return 0;
}
void solve() {
    int cnt = 0;
    for (int i = 1; i <= 3; i++) {
        cin >> s[i];
        s[i] = "G" + s[i];
        for (auto j : s[i]) {
            if (j != 'G')cnt++;
        }
    }
    if (cnt <= 4) {
        cout << "Yes" << endl;
        return;
    }
    for (int i = 1; i <= 3; i++) {
        if (check(s[i][1], s[i][2], s[i][3])) { cout << "Yes" << endl; return; }
        if (check(s[1][i], s[2][i], s[3][i])) { cout << "Yes" << endl; return; }
    }
    if (check(s[1][1], s[2][2], s[3][3])) { cout << "Yes" << endl; return; }
    if (check(s[3][1], s[2][2], s[1][3])) { cout << "Yes" << endl; return; }
    cout << "No" << endl;
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

