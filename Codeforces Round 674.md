> [Portal.](https://codeforces.com/contest/1426)

### A. Floor Number

[Portal.](https://www.luogu.com.cn/problem/CF1426A)

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

void solve()
{
    int n,x;cin>>n>>x;
    if(n==1||n==2) cout<<"1\n";
    else n-=2,cout<<(n%x?n/x+1:n/x)+1<<'\n';
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### B. Symmetric Matrix

[Portal.](https://www.luogu.com.cn/problem/CF1426B)

注意“不限数量”。当且仅当 $m$ 为偶数，且至少有一个左下角和右上角相同的矩形，存在满足条件的对称矩阵。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

void solve()
{
    int n,m;cin>>n>>m;
    bool flag=0;
    for(int i=1;i<=n;i++)
    {
        int a1,a2,a3,a4;
        cin>>a1>>a2>>a3>>a4;
        if(a2==a3) flag=1;
    }
    if(!flag||m%2) cout<<"NO\n";
    else cout<<"YES\n";
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### C. Increase and Copy

[Portal.](https://www.luogu.com.cn/problem/CF1426C)

题意可以转化为求满足 $xy\geq n$ 的最小的 $x+y-1$ 的值。假设有 $x-1$ 次翻倍操作使得数到 $x$，再进行 $\lceil\dfrac{n-x}{x}\rceil$ 次操作得到最后的结果，答案为 $x-1+\lceil\dfrac{n-x}{x}\rceil$，即 $x+\lceil\dfrac{n}{x}\rceil-2$，由均值不等式可知 $x=\sqrt n$ 时有最小值，答案即为 $\sqrt n+\lfloor\dfrac{n}{\sqrt n}\rfloor+[\sqrt n|n]-2$。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

void solve()
{
    int n;cin>>n;
    cout<<((int)sqrt(n)+n/(int)sqrt(n)+(n%(int)sqrt(n)>0)-2)<<'\n';
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### D. Non-zero Segments

[Portal.](https://www.luogu.com.cn/problem/CF1426D)

想到了前缀和，找到每一个和为 $0$ 的子段，按左端点排序，假设插入的数是无穷大的“关键数”，即求让每个子段有“关键数”的最优方案，贪心思路是对于每一个不包含“关键数”的区间，把关键数放到其右端点。时间复杂度 $O(n^2)$，无法通过。

考虑如果有前缀和 $sum_j=sum_{i-1}(j>i)$，那么区间 $[i,j]$ 一定是一段和为 $0$ 的子段，此时在区间右端点前插入一个无穷大的数，则后面的前缀和不可能与该前缀和相等。可以用 `map` 维护一个前缀和是否出现过，插入极大值后直接把 `map` 清空，标记当前前缀和，注意还要加入当前点的 $sum_{j-1}$，因为可能这个点会是下一个子段和为 $0$ 的子段的左端点。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

map<ll,bool> mp;

int main()
{
    int n;cin>>n;
    mp[0]=1;
    ll sum=0,ans=0;
    for(int i=1;i<=n;i++)
    {
        int x;cin>>x;
        sum+=x;
        if(mp[sum]) sum=x,ans++,mp.clear(),mp[0]=1;
        mp[sum]=1;
    }
    cout<<ans<<'\n';
    return 0;
}
```

### E. Rock, Paper, Scissors

[Portal.](https://www.luogu.com.cn/problem/CF1426E)

对于 Alice 赢最少的次数，尽量要平局 / 输局，用总局数减去平局数与输局数之和即可。

对于 Alice 赢最多的次数，让 Alice 每一次出手都尽量获胜即可。

```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int n;cin>>n;
    int a1,a2,a3,b1,b2,b3;
    cin>>a1>>a2>>a3>>b1>>b2>>b3;
    cout<<(n-min(a1,b1+b3)-min(a2,b2+b1)-min(a3,b3+b2))<<' '<<(min(a1,b2)+min(a2,b3)+min(a3,b1));
    return 0;
}
```

### F. Number of Subsequences

[Portal.](https://www.luogu.com.cn/problem/CF1426F)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-CF1426F)