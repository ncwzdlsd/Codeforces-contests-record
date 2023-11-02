> [Portal.](https://codeforces.com/contest/10)

### A. Power Consumption Calculation

[Portal.](https://www.luogu.com.cn/problem/CF10A)

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

