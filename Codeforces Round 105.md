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

[Portal.](https://www.luogu.com.cn/problem/CF148E)

因为每一层都是从最左端或最右端开始维护，考虑用前缀和维护。$s_{i,j}$ 表示 第 $i$ 行前 $j$ 个数的价值，$num_i$ 表示第 $i$ 行的物品数。

考虑把每一层的所有取的情况当成一组处理，这个东西要预处理出来。设 $g(i,j)$ 表示第 $i$ 层取了 $j$ 个物品的最大价值。状态转移 $g(i,j)=\max(g(i,j),s_{i,l}+s_{i,num_i}-s_{i,num_i-(j-l)})$。

处理完这部分之后可以考虑最后的 DP 转移。设 $f(i,j)$ 表示考虑前 $i$ 行，选了 $j$ 个数的最小花费。有 $f(i,j)=\max(f(i,j),f(i-1,j-k)+g(i,k))$。

时间复杂度 $O(n^3)$。

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long

const int maxn=105,maxm=1e4+5;
int g[maxn][maxn],f[maxn][maxm],s[maxn][maxn],num[maxn];

signed main()
{
    int n,m;cin>>n>>m;
    for(int i=1;i<=n;i++)
    {
        cin>>num[i];
        for(int j=1,a;j<=num[i];j++) cin>>a,s[i][j]=s[i][j-1]+a;
    }
    for(int i=1;i<=n;i++)
        for(int j=1;j<=num[i];j++)
            for(int l=0;l<=j;l++) g[i][j]=max(g[i][j],s[i][l]+s[i][num[i]]-s[i][num[i]-(j-l)]);
    for(int i=1;i<=n;i++)
        for(int j=1;j<=m;j++)
            for(int k=0;k<=min(j,num[i]);k++) f[i][j]=max(f[i][j],f[i-1][j-k]+g[i][k]);
    cout<<f[n][m];
    return 0;
}
```

