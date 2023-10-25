> [Portal.](https://codeforces.com/contest/1066)

### C. Books Queries

[Portal.](https://www.luogu.com.cn/problem/CF1066C)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-CF1066C)

### D. Boxes Packing

[Portal.](https://www.luogu.com.cn/problem/CF1066D)

把从左至右删物品转化为从右至左加物品。模拟即可。

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn=2e5+5;
int a[maxn];

int main()
{
    int n,m,k;cin>>n>>m>>k;
    for(int i=1;i<=n;i++) cin>>a[i];
    int cnt=m,res=0;
    for(int i=n;i;i--)
    {
        if(res+a[i]<=k) res+=a[i];
        else cnt--,res=a[i];
        if(!cnt) cout<<(n-i),exit(0);  
    }
    cout<<n;
    return 0;
}
```

### F. Yet another 2D Walking

[Portal.](https://www.luogu.com.cn/problem/CF1066F)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1066f)

