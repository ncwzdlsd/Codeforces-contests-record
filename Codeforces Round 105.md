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

追及问题。

考虑每一次追上的时间 $t$，如果此时公主还未到达终点，则必须花费一个珠宝让龙回去。不断重复这个过程知道公主的行走距离大于 $c$。

注意特判 $v_p\geq v_d$ 的情况，此时龙永远追不上公主。

```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int vp,vd,f,c;double t;cin>>vp>>vd>>t>>f>>c;
    if(vp>=vd) cout<<0,exit(0);
    double s1=vp*t,s2=0;
    int ans=0;
    while(s1<c)
    {
        t+=(double)(s1-s2)/(vd-vp);
        s1=s2=vp*t;
        if(s1>=c) break;
        t+=s2/vd+f,s1=vp*t,s2=0,ans++;
    }
    cout<<ans;
    return 0;
}
```

### C. Terse princess

[Portal.](https://www.luogu.com.cn/problem/CF148C)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf148c)

### E. Porcelain

$f(i,j)$ 表示在第 $i$ 行选择了 $j$ 个数的最大价值、