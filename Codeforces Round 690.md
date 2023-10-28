> [Portal.](https://codeforces.com/contest/1462)

### A. Favorite Sequence

[Portal.](https://www.luogu.com.cn/problem/CF1462A)

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn=305;
int b[maxn];

void solve()
{
    int n;cin>>n;
    for(int i=1;i<=n;i++) cin>>b[i];
    for(int i=1;i<=n/2;i++) cout<<b[i]<<' '<<b[n-i+1]<<' ';
    if(n%2) cout<<b[n/2+1];
    cout<<"\n";
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### B. Last Year's Substring

[Portal.](https://www.luogu.com.cn/problem/CF1462B)

分情况讨论即可。

```cpp
#include <bits/stdc++.h>
using namespace std;

void solve()
{
    int n;string s;
	cin>>n>>s;
	if(s[0]=='2'&&s[1]=='0'&&s[2]=='2'&&s[3]=='0') return cout<<"YES"<<"\n",void();
	if(s[0]=='2'&&s[1]=='0'&&s[2]=='2'&&s[n-1]=='0') return cout<<"YES"<<"\n",void();
	if(s[0]=='2'&&s[1]=='0'&&s[n-2]=='2'&&s[n-1]=='0') return cout<<"YES"<<"\n",void();
	if(s[0]=='2'&&s[n-3]=='0'&&s[n-2]=='2'&&s[n-1]=='0') return cout<<"YES"<<"\n",void();
	if(s[n-4]=='2'&&s[n-3]=='0'&&s[n-2]=='2'&&s[n-1]=='0') return cout<<"YES"<<"\n",void();
	cout<<"NO"<<"\n";
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### C. Unique Number

因为只有 $9$ 个数，所以 $x>45$ 时无解。

贪心思路是优先把大的数往低位填。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int a[10];

void solve()
{
    int x;cin>>x;
    if(x>45) return cout<<"-1\n",void();
    int tot=0;
    for(int i=9;i>=0;i--)
    {
        if(i>x) continue;
        x-=i,a[++tot]=i;
        if(!x) break;
    }
    for(int i=tot;i;i--) cout<<a[i];
    cout<<"\n";
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### D. Add to Neighbour and Remove

[Portal.](https://www.luogu.com.cn/problem/CF1462D)

由于 $n\leq 3000$，可以考虑 $O(n^2)$ 的暴力。

观察到所谓的合并元素其实就是区间加和。第一个区间的左端点显然为 $1$，暴力枚举第一个区间的右端点，然后统计后面的每个段能否和它区间和相等即可。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int maxn=3005;
int a[maxn];

void solve()
{
    int n;cin>>n;
    for(int i=1;i<=n;i++) cin>>a[i];
    int res=0,acnt=0,sum=0,ans=0x3f3f3f;
    for(int i=1;i<=n;i++)
    {
        if(i>1) ++acnt;
        res=acnt,sum+=a[i];
        int tmp=0;
        bool flag=1;
        for(int j=i+1;j<=n;j++)
        {
            if(tmp) ++res;
            tmp+=a[j];
            if(tmp==sum) tmp=0;
            else if(tmp>sum) {flag=0,tmp=0;break;}
        }
        if(flag&&(!tmp)) ans=min(ans,res); 
    }
    cout<<ans<<"\n";
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### E1. Close Tuples (easy version)

[Portal.](https://www.luogu.com.cn/problem/CF1462E1)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1462e1)

### E2. Close Tuples (hard version)

[Portal.](https://www.luogu.com.cn/problem/CF1462E2)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1462e2)
