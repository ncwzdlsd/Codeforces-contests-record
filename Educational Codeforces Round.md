> [Portal.](https://codeforces.com/contest/609)

### A. USB Flash Drives

[Portal.](https://www.luogu.com.cn/problem/CF609A)

```cpp
#include <bits/stdc++.h>
using namespace std;

int a[105];

int main()
{
	int n,m;cin>>n>>m;
	for(int i=1;i<=n;i++) cin>>a[i];
	int ans=0;
    sort(a+1,a+1+n);
    for(int i=n;i;i--)
    {
        m-=a[i],ans++;
        if(m<=0) cout<<ans,exit(0);
    }
    return 0;
}
```

### B. The Best Gift

[Portal.](https://www.luogu.com.cn/problem/CF609B)

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int maxn=2e5+5;
int a[maxn],cnt[15];

int main()
{
	int n,m;cin>>n>>m;
	for(int i=1;i<=n;i++) cin>>a[i],cnt[a[i]]++;
	ll ans=0;
	for(int i=1;i<=m;i++)
		for(int j=i+1;j<=m;j++) ans+=cnt[i]*cnt[j];
	cout<<ans;
	return 0;
}
```

