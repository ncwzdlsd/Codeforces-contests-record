> [Portal.](https://codeforces.com/contest/10)

### A. Power Consumption Calculation

[Portal.](https://www.luogu.com.cn/problem/CF10A)

```cpp
#include <bits/stdc++.h>
using namespace std;

int l[105],r[105];

int main()
{
    int n,P1,P2,P3,T1,T2;cin>>n>>P1>>P2>>P3>>T1>>T2;
    int ans=0;
    for(int i=1;i<=n;i++) cin>>l[i]>>r[i],ans+=(r[i]-l[i])*P1;
    for(int i=1;i<=n;i++)
    {
        if(i==1) continue;
        if(l[i]-r[i-1]<=T1) ans+=(l[i]-r[i-1])*P1;
        else if(l[i]-r[i-1]>T1&&l[i]-r[i-1]<=T1+T2) ans+=T1*P1+(l[i]-r[i-1]-T1)*P2;
        else ans+=T1*P1+T2*P2+(l[i]-r[i-1]-T1-T2)*P3;
    }
    cout<<ans;
    return 0;
}
```

### B. Cinema Cashier

[Portal.](https://www.luogu.com.cn/problem/CF10B)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf10b)

### C. Digital Root

[Portal.](https://www.luogu.com.cn/problem/CF10C)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-CF10C)

### E. Greedy Change

[Portal.](https://www.luogu.com.cn/problem/CF10E)

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn=405;
int n,a[maxn],ans=3e9;

signed main()
{
	cin>>n;
	for(int i=1;i<=n;i++) cin>>a[i];
	bool flag=false;//判断能否以最优方式求出和
	for(int i=2;i<=n;i++)
		for(int j=i;j<=n;j++)
		{
			int sum=0,dp=0/*最优解*/,now=a[i-1]-1;
			for(int k=1;k<=j;k++)
				sum+=now/a[k],now%=a[k];
			int tmp=now=a[i-1]-1-now+a[j];
			for(int k=i;k<=j;k++)
				dp+=now/a[k],now%=a[k];
			sum=0;now=tmp;
			for(int k=1;k<=n;k++)
				sum+=now/a[k],now%=a[k];
			if(dp<sum) ans=min(ans,tmp),flag=true;
		}
	if(flag) cout<<ans,exit(0);
	cout<<-1;
	return 0;
}
```
