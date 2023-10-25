> [Portal.](https://codeforces.com/contest/1798)

### A. Showstopper

[Portal.](https://codeforces.com/contest/1798/problem/A)

赛时代码：

```cpp
#include <bits/stdc++.h>
using namespace std;
 
const int maxn=105;
int a[maxn],b[maxn];
 
int main()
{
	int t;cin>>t;
	while(t--)
	{
		memset(a,0,sizeof a);
		memset(b,0,sizeof b);
		int n;cin>>n;
		for(int i=1;i<=n;i++)
		// {
			cin>>a[i];
			// if(max2<=a[i])
				// max2=a[i],maxp2=i;
		// }
		for(int i=1;i<=n;i++)
		// {
			cin>>b[i];
			// if(max2<=a[i])
				// max2=a[i],maxp2=i;
		// }
		for(int i=1;i<=n;i++)
			if(a[i]>=b[i])
			{
				int tmp=a[i];
				a[i]=b[i],b[i]=tmp;
			}
		int maxa=0,maxb=0;
		for(int i=1;i<=n;i++) maxa=max(maxa,a[i]),maxb=max(maxb,b[i]);
		if(maxa<=min(a[n],b[n])&&maxb<=max(a[n],b[n])) cout<<"Yes"<<endl;
		else cout<<"No"<<endl;
			
	}
	return 0;
}
```

### B. Three Sevens

[Portal.](https://www.luogu.com.cn/problem/CF1798B)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1798b)

### C. Candy Store

[Portal.](https://www.luogu.com.cn/problem/CF1798C)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1798c)

### D. Shocking Arrangement

[Portal.](https://www.luogu.com.cn/problem/CF1798D)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1798d)
