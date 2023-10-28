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

### C. Load Balancing

[Portal.](https://www.luogu.com.cn/problem/CF609C)

显然最平均的情况即为 $tot\bmod n$ 台服务器处理 $\dfrac{tot}{n}+1$ 个任务，其余的服务器处理 $\dfrac{tot}{n}$ 台任务。

一个贪心思路，为了让减少操作少一点，我们让任务多的服务器分配到 $\dfrac{tot}{n}+1$ 个任务。

由于一次移动产生的贡献是 $2$，所以答案要除以 $2$。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int maxn=1e5+5;
int m[maxn];

int main()
{
	int n;cin>>n;
	ll tot=0;
	for(int i=1;i<=n;i++) cin>>m[i],tot+=m[i];
	sort(m+1,m+n+1);
	ll tmp=0;
	for(int i=1;i<=(n-tot%n);i++) tmp+=abs(m[i]-tot/n);
	for(int i=n-tot%n+1;i<=n;i++) tmp+=abs(m[i]-tot/n-1);
	cout<<tmp/2;
	return 0;
}
```

### D. Gadgets for dollars and pounds

[Portal.](https://www.luogu.com.cn/problem/CF609D)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf609d)

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
#define int long long

const int maxn=2e5+5;
int a[maxn],b[maxn],s,m,n,k;
struct node{int t/*type*/,c/*cost*/,id;ll v;}p[maxn];
struct nod{int d,q;}out[maxn];

bool cmp(node a,node b){return a.v<b.v;}

bool check(int x)
{
	int mina=INT_MAX,minb=INT_MAX,d1=1,d2=1;
	for(int i=1;i<=x;i++)
	{
		if(a[i]<mina) mina=a[i],d1=i;
		if(b[i]<minb) minb=b[i],d2=i;
	}
	for(int i=1;i<=m;i++) 
	{
		if(p[i].t==1) p[i].v=p[i].c*mina;
		else p[i].v=p[i].c*minb;
	}
	sort(p+1,p+m+1,cmp);
	ll sum=0;
	for(int i=1;i<=k;i++) sum+=p[i].v;
	if(sum>s) return 0;
	for(int i=1;i<=k;i++)
	{
		out[i].q=p[i].id;
		if(p[i].t==1) out[i].d=d1;
		else out[i].d=d2;
	}
	return 1;
}

signed main()
{
	cin>>n>>m>>k>>s;
	for(int i=1;i<=n;i++) cin>>a[i];
	for(int i=1;i<=n;i++) cin>>b[i];
	for(int i=1;i<=m;i++) cin>>p[i].t>>p[i].c,p[i].id=i;
	int l=0,r=n,ans=0;
	while(l<=r)
	{
		int mid=(l+r)/2;
		if(check(mid)) ans=mid,r=mid-1;
		else l=mid+1;
	}
	if(ans) 
	{
		cout<<ans<<'\n';
		for(int i=1;i<=k;i++) cout<<out[i].q<<' '<<out[i].d<<'\n';
	}
	else cout<<"-1";
	return 0;
}
```

### E. Minimum spanning tree for each edge

[Portal.](https://www.luogu.com.cn/problem/CF609E)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long

const int maxn=4e5+5;
int m,n,cnt,head[maxn],fa[maxn],to[maxn],nxt[maxn],v[maxn],f[maxn][25],res,w[maxn][25],dep[maxn];
bool vis[maxn];

void add(int x,int y,int z)
{
	to[++cnt]=y;
	v[cnt]=z;
	nxt[cnt]=head[x];
	head[x]=cnt;
}

struct node{int from,to,vv,id;}gg[maxn];

int find(int x)
{
	if(x!=fa[x]) return fa[x]=find(fa[x]);
	return fa[x];
}

bool cmp1(node a,node b){return a.vv<b.vv;}

bool cmp2(node a,node b){return a.id<b.id;}

void kruskal()
{
	sort(gg+1,gg+m+1,cmp1);
	for(int i=1;i<=n;i++) fa[i]=i;
	int tmp=0;
	for(int i=1;i<=m&&tmp<n;i++)
	{
		int uuu=find(gg[i].from),vvv=find(gg[i].to);
		if(uuu!=vvv)
		{
			fa[uuu]=vvv;
			add(uuu,vvv,gg[i].vv);
			add(vvv,uuu,gg[i].vv);
			res+=gg[i].vv;
			tmp++;
		}
	}
}

void dfs(int x)
{
	vis[x]=1;
	for(int i=1;i<=20;i++)
		f[x][i]=f[f[x][i-1]][i-1],w[x][i]=max(w[x][i-1],w[f[x][i-1]][i-1]);
	for(int i=head[x];i;i=nxt[i])
	{
		if(vis[to[i]]) continue;
		dep[to[i]]=dep[x]+1;
		f[to[i]][0]=x;
		w[to[i]][0]=v[i];
		dfs(to[i]);
	}
}

int lca(int x,int y)
{
	int ans=0;
	if(dep[x]<dep[y]) swap(x,y);
	for(int i=20;i>=0;i--)
		if(dep[f[x][i]]>=dep[y])
			ans=max(ans,w[x][i]),x=f[x][i];
	if(x==y) return ans;
	for(int i=20;i>=0;i--)
		if(f[x][i]!=f[y][i])
			ans=max(ans,max(w[x][i],w[y][i])),x=f[x][i],y=f[y][i];
	return max(ans,max(w[x][0],w[y][0]));
}

signed main()
{
	cin>>n>>m;
	for(int i=1;i<=m;i++) cin>>gg[i].from>>gg[i].to>>gg[i].vv,gg[i].id=i;
	kruskal();
	dfs(1);
	sort(gg+1,gg+m+1,cmp2);
	int lans;
	for(int i=1;i<=m;i++)
		lans=res+gg[i].vv-lca(gg[i].from,gg[i].to),cout<<lans<<endl;
	return 0;
}
```

