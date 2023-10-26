> [Portal.](https://codeforces.com/contest/1811)

### A. Insert Digit

[Portal.](https://codeforces.com/contest/1811/problem/A)

赛时代码：

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn=2e5+5;
string b;

int main()
{
	int t;cin>>t;
	while(t--)
	{
		int n,d;cin>>n>>d;
		cin>>b;
		// string res=b;
		// for(int i=0;i<n;i++) 
			// if(b[i]-'0'<d) 
			// {
	            // res.insert(i,1,d+'0');
				// break;
			// }
		// cout<<res<<endl;
		int i=0;
        while(i<n&&b[i]-'0'>=d) ++i;
        if(i==n) cout<< b + to_string(d)<<endl;
        else cout<<b.substr(0, i) + to_string(d) + b.substr(i)<<endl;
		// for(int i=1;i<=n+1;i++) a[i]=0;
		// for(int i=n;i;i--) 
		// {
			// char ch;cin>>ch;
			// a[i]=ch-'0';
		// }
		// int pos=n;
		// for(int i=n;i;i--)
			// if(a[i]<=d) {pos=i;break;}
		// if(d&&pos!=n)
		// {
			// for(int i=n;i>pos;i--) ans[i]=a[i];
			// ans[pos]=d;
			// for(int i=pos;i;i--) ans[i]=a[i];
			// for(int i=n;i;i--) cout<<ans[i];
			// cout<<endl;
		// }
		// else if(pos==n)
		// {
			// cout<<d;
			// for(int i=n;i;i--) cout<<a[i];
			// cout<<endl;
		// }
		// else
		// {
			// for(int i=n;i;i--) cout<<a[i];
			// cout<<0<<endl;
		// }
	}
	return 0;
}
```

### B. Conveyor Belts

[Portal.](https://www.luogu.com.cn/problem/CF1811B)

发现层与层之间可以直接转移，分别计算出两个点的层数作差即可。

这里的层数由外而内递增，易得 $id=\min(x,y,n-x+1.n-y+1)$。

```cpp
#include <bits/stdc++.h>
using namespace std;
#define x1 x11
#define x2 x22
#define y1 y11
#define y2 y22

void solve()
{
	int n,x1,x2,y1,y2;cin>>n>>x1>>y1>>x2>>y2;
	int id1=min(min(x1,y1),min(n-x1+1,n-y1+1)),id2=min(min(x2,y2),min(n-x2+1,n-y2+1));
	cout<<abs(id1-id2)<<endl;
}

int main()
{
	int t;cin>>t;
	while(t--) solve();
	return 0;
}
```

### C. Restore the Array

[Portal.](https://www.luogu.com.cn/problem/CF1811C)

$b_i=\max(a_i,a_{i+1}),b_{i-1}=\max(a_i,a_{i-1})$，所以有 $a_i\leq\min(b_i,b_{i-1})$。

注意特判边界的 $a_1$ 和 $a_n$。

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn=2e5+5;
int a[maxn],b[maxn];

void solve()
{
	int n;cin>>n;
	for(int i=1;i<n;i++) cin>>b[i];
	b[0]=1e9,a[n]=b[n-1];
	for(int i=1;i<n;i++) a[i]=min(b[i],b[i-1]);
	for(int i=1;i<=n;i++) cout<<a[i]<<' ';
	cout<<endl;
}

int main()
{
	int t;cin>>t;
	while(t--) solve();
	return 0;
}
```

### D. Umka and a Long Flight

[Portal.](https://www.luogu.com.cn/problem/CF1811D)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1811d)

### E. Living Sequence

[Portal.](https://www.luogu.com.cn/problem/CF1811E)

很巧妙的一道题。把不含 $4$ 的数转化为不含 $9$ 的数，则题目要求的序列就等价于一个九进制数表。把 $k$ 转化为九进制，但是把九进制下的 $[4,8]$ 映射为 $[5,9]$ 即可。‘

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long

int a[10]={0,1,2,3,5,6,7,8,9};

void solve()
{
	int k;cin>>k;
	int cnt=1,ans=0;
	while(k)
		ans+=a[k%9]*cnt,cnt*=10,k/=9;
	cout<<ans<<'\n';
}

signed main()
{
	int t;cin>>t;
	while(t--) solve();
	return 0;
}
```

### F. Is It Flower?

[Portal.](https://www.luogu.com.cn/problem/CF1811F)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1811f)

### G1. Vlad and the Nice Paths (easy version)

### G2. Vlad and the Nice Paths (hard version)

[Portal.](https://www.luogu.com.cn/problem/CF1811G2)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1811g2)
