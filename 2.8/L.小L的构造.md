## L.小L的构造

## 题意：

输入n，求1~n里面每个数用一次，最多可以构造多少满足xy,xz,yz三对数里面恰有两对互质的三元组

## 解析：

1. 当n<=3时，直接输出 0。

2. n>3时分类讨论：

   (1)如果n%6<=2,那么就用连续6个一组进行构造

   (2)如果n>=9,则首先用固定的9个数构造三元组，然后继续用以上方法构造

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
    cin >> n;
    if (n <= 3){
        cout << 0 << endl;
        return;
    }
    if (n >= 4 && n <= 5){
        cout << 1 << endl << 2 << " " << 3 << " " << 4 << endl; 
        return;
    }
    cout << n / 3 << endl;
    if (n % 6 <= 2) {
        for (int i = 1; i + 5 <= n; i += 6){
            cout << i << " " << i + 1 << " " << i + 3 << endl;
            cout << i + 2 << " " << i + 4 << " " << i + 5 << endl;
        }
        return;
    }
    int i = 1;
    while (i + 5 <= n - 9){
        cout << i << " " << i + 1 << " " << i + 3 << endl;
        cout << i + 2 << " " << i + 4 << " " << i + 5 << endl;
        i += 6;
    }
    cout << i << " " << i + 1 << " " << i + 3 << "\n";
    cout << i + 2 << " " << i + 4 << " " << i + 8 << "\n";
    cout << i + 5 << " " << i + 6 << " " << i + 7 << "\n";
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

