> [Portal.](https://codeforces.com/contest/148)

### A. Insomnia cure

[Portal.](https://www.luogu.com.cn/problem/CF148A)

求 $[1,d]$ 中能被 $k,l,m,n$ 中的任意一个数整除的数的数量。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int main()
{
    int k,l,m,n,d;cin>>k>>l>>m>>n>>d;
    int ans=0;
    for(int i=1;i<=d;i++)
        if(i%k==0||i%l==0||i%m==0||i%n==0) ans++;
    cout<<ans;
    return 0;
}
```

### B. Escape

[Portal.](https://www.luogu.com.cn/problem/CF148B)