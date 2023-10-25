> [Portal.](https://codeforces.com/contest/1802)

### A. Likes

[Portal.](https://codeforces.com/contest/1802/problem/A)

赛时代码：

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long

const int maxn=1e5+5;
int b[maxn],n,cnt1,cnt2;
bool qwq[maxn];

//b数组无序 

signed main()
{
	int t;cin>>t;
	while(t--)
	{
		cin>>n;
		memset(b,0,sizeof(b));cnt1=0;cnt2=0;
		for(int i=1;i<=n;i++) 
		{
			cin>>b[i];
			if(b[i]>0) cnt1++;
			else cnt2++;
		}
		int tmp=cnt1;
		for(int i=1;i<=n;i++)
		{
			if(i<=cnt1) cout<<i<<' ';
			else tmp--,cout<<tmp<<' '; 
		}
		cout<<endl;
	//	int tmp=abs(cnt1-cnt2);
		for(int i=1;i<=n;i++)
		{
			if(i%2==1&&i<min(cnt1,cnt2)*2) cout<<1<<' ';
			else if(i%2==0&&i<=min(cnt1,cnt2)*2) cout<<0<<' ';
			else cout<<i-min(cnt1,cnt2)*2<<' ';
		}
		cout<<endl;
	}
	return 0;
}
```

### B. Settlement of Guinea Pigs

[Portal.](https://www.luogu.com.cn/problem/CF1802B)

设已知 $x$ 只豚鼠的性别，未知 $y$ 只豚鼠的性别。

- 若 $x=0$，此时所有豚鼠的性别都未知，则需要 $y$ 个笼子。
- 否则，最坏情况是 $1$ 只 A 性别豚鼠，$x-1$ 只 B 性别豚鼠，需要 $1+\lceil \dfrac{x-1}{2}\rceil+y$ 个笼子。

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn=1e5+5;
int b[maxn];

void solve()
{
    int n;cin>>n;
    for(int i=1;i<=n;i++) cin>>b[i];
    int x=0,y=0,ans=0;
    for(int i=1;i<=n;i++)
    {
        if(b[i]==1) y++;
        else x+=y,y=0;
        if(!x) ans=max(ans,y+x);
        else ans=max(ans,y+x/2+1);
    }
    cout<<ans<<endl;
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

