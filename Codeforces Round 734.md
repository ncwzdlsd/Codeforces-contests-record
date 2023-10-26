> [Portal.](https://codeforces.com/contest/1551)

### B1. Wonderful Coloring - 1

[Portal.](https://www.luogu.com.cn/problem/CF1551B1)

记 $cnt_i$ 代表第 $i$ 种字母在 $s$ 中的出现次数，有两种情况：

1. 若 $cnt_i>1$，此时对于这种字母，我们将它出现的某次染成红色，某次染成绿色，其他的出现情况不染色
2. 若 $cnt_i=1$，此时需要和另一个 $cnt_j=1$ 的字母配对染成一红一绿。

```cpp
#include <bits/stdc++.h>
using namespace std;

int cnt[30];

void solve()
{
    string s;cin>>s;
    memset(cnt,0,sizeof cnt);
    for(int i=0;i<s.length();i++) cnt[s[i]-'a']++;
    int cnt1=0,cnt2=0;
    for(int i=0;i<26;i++) 
    {
        if(cnt[i]==1) cnt1++;
        else if(cnt[i]>1) cnt2++;
    }
    cout<<(cnt1/2+cnt2)<<'\n';
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### B2. Wonderful Coloring - 2

[Portal.](https://www.luogu.com.cn/problem/CF1551B2)

和 B1 相似的思路，统计每种字母出现的次数，出现次数大于 $k$ 的填成 $k$ 种颜色，否则就都可以填色。

由于需要输出方案数，按照序列中数的大小排序，保证一样的数排在一起，记录原 id 按序输出即可。

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn=2e5+5;
int cnt[maxn],ans[maxn],ct[maxn];
struct node{int id,v;}a[maxn],b[maxn];

bool cmp(node a,node b)
{return a.v<b.v;}

void solve()
{
    int n,k;cin>>n>>k;
    for(int i=0;i<=n;i++) cnt[i]=0,ans[i]=0,ct[i]=0;
    for(int i=1;i<=n;i++) cin>>a[i].v,cnt[a[i].v]++,a[i].id=i;
    int tmp=0;
    for(int i=1;i<=n;i++) 
    {
        if(cnt[a[i].v]<k) b[++tmp]=a[i];
        else if(cnt[a[i].v]>=k&&ct[a[i].v]<k) ct[a[i].v]++,ans[a[i].id]=ct[a[i].v];
    }
    sort(b+1,b+tmp+1,cmp);
    int tp=1,tot=tmp/k*k;
    for(int i=1;i<=tot;i++)
    {
        ans[b[i].id]=tp,tp++;
        if(tp>k) tp=1;
    }
    for(int i=1;i<=n;i++) cout<<ans[i]<<' ';
    cout<<'\n';
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### C. Interesting Story

[Portal.](https://www.luogu.com.cn/problem/CF1551C)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1551c)

### D1. Domino (easy version)

[Portal.](https://www.luogu.com.cn/problem/CF1551D1)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-CF1551D1)

### D2. Domino (hard version)

[Portal.](https://www.luogu.com.cn/problem/CF1551D2)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1551d2)

### E. Fixed Points

设计状态 $f(i,j)$ 表示对于前 $i$ 个数，删去 $j$ 个数后，满足 $b_i=i$ 的条件个数。 

对于第 $i$ 个位置，考虑删 / 不删，转移如下：
$$
f(i,j)=\max(f(i-1,j-1),f(i-1,j)+[a_i=i-j])
$$
答案即为满足 $f(n,i)\geq k$ 的最小的 $i$。

```cpp
#include <bits/stdc++.h>
using namespace std;

int a[2005],f[2005][2005];

void solve()
{
    int n,k;cin>>n>>k;
    for(int i=0;i<=n;i++) for(int j=0;j<=n;j++) f[i][j]=0;
    for(int i=1;i<=n;i++) cin>>a[i],f[i][0]=f[i-1][0]+(a[i]==i);
    for(int i=1;i<=n;i++)
        for(int j=1;j<=n;j++) f[i][j]=max(f[i-1][j-1],f[i-1][j]+(a[i]==i-j));
    for(int i=0;i<=n;i++) if(f[n][i]>=k) return cout<<i<<'\n',void();
    cout<<"-1\n";
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### F. Equidistant Vertices

[Portal.](https://www.luogu.com.cn/problem/CF1551F)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1551f)
