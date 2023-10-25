> [Portal.](https://codeforces.com/contest/1312)

### A. Two Regular Polygons

[Portal.](https://www.luogu.com.cn/problem/CF1312A)

正 $n$ 边形中心角为 $\dfrac{360^\circ}{n}$，正 $m$ 边形中心角为 $\dfrac{360^\circ}{m}$，若能包含显然要 $(\dfrac{360^\circ}{m})|(\dfrac{360^\circ}{n})$，则需要 $m|n$。

> 正多边形的中心角：每一条边所对的外接圆的圆心角。

```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int t;cin>>t;
    while(t--)
    {
        int n,m;cin>>n>>m;
        if(n%m) cout<<"NO"<<endl;
        else cout<<"YES"<<endl;
    }
    return 0;
}
```

### B. Bogosort

[Portal.](https://www.luogu.com.cn/problem/CF1312B)

第一反应是移项，把限制条件转化为 $j-i\neq a_j-a_i$。

由于 $i<j$，左边一定大于 $0$，所以只需要右边小于等于 $0$ 即可。即 $a_j-a_i\leq 0$，由此可知 $a_i\geq a_j$。将原序列降序排序即可。

```cpp
#include <bits/stdc++.h>
using namespace std;

int a[105];

void solve()
{
    int n;cin>>n;
    for(int i=1;i<=n;i++) cin>>a[i];
    sort(a+1,a+n+1);
    for(int i=n;i;i--) cout<<a[i]<<' ';
    cout<<endl;
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### C. Adding Powers

[Portal.](https://www.luogu.com.cn/problem/CF1312C)

对 $a_i$ 做 $k$ 进制拆解。统计 $a$ 数组中每一位 $k$ 进制下是否有值，若有值将该位的 $cnt_i$ 累加。最后统计是否有 $cnt_i>1$ 的情况。若有，则不存在方案。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

ll cnt[105];

void solve()
{
    int n,k;cin>>n>>k;
    memset(cnt,0,sizeof cnt);
    int mxlen=0,len;
    for(int i=1;i<=n;i++)
    {
        ll a;cin>>a,len=1;
        while(a) cnt[len]+=a%k,a/=k,mxlen=max(mxlen,++len);
    }    
    for(int i=1;i<=mxlen;i++) if(cnt[i]>1){cout<<"NO"<<endl;return;}
    cout<<"YES"<<endl;
}

int main()
{
    int T;cin>>T;
    while(T--) solve();
    return 0;
}
```

### D. Count the Arrays

[Portal.](https://www.luogu.com.cn/problem/CF1312D)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-CF1312D)

### E. Array Shrinking

[Portal.](https://www.luogu.com.cn/problem/CF1312E)

区间 DP。

设计状态 $f(l,r)$ 表示区间 $[l,r]$ 合并之后的最小长度，用 $s_{l,r}$ 表示区间 $[l,r]$ 合并之后的新数的值。

显然有转移：
$$
f(l,r)=\min_{k\in[l,r]}(f(l,k)+f(k+1,r))
$$
对于可以合并的两个元素，有：
$$
f(l,r)=1,s_{l,r}=s_{l,k}+1
$$

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn=505;
int f[maxn][maxn],s[maxn][maxn];

int main()
{
    memset(f,0x3f3f3f,sizeof f);
    int n;cin>>n;
    for(int i=1;i<=n;i++) cin>>s[i][i],f[i][i]=1;
    for(int len=2;len<=n;len++)
        for(int i=1;i<=n-len+1;i++)
        {
            int j=len+i-1;
            for(int k=i;k<j;k++)
            {
                f[i][j]=min(f[i][j],f[i][k]+f[k+1][j]);
                if(f[i][k]==1&&f[k+1][j]==1&&s[i][k]==s[k+1][j]) f[i][j]=1,s[i][j]=s[i][k]+1;
            }
        }
    cout<<f[1][n];
    return 0;
}
```
