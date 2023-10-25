### A. Love Story

[Portal.](https://codeforces.com/contest/1829/problem/A)

赛时代码：

```cpp
#include <bits/stdc++.h>
using namespace std;

string s="codeforces";
char q[15];

int main()
{
	int t;cin>>t;
	while(t--)
	{
		cin>>q;
		int cnt=0;
		for(int i=0;i<10;i++) if(s[i]!=q[i]) cnt++;
		cout<<cnt<<endl;
	}
	return 0;
}
```

### B. Blank Space

[Portal.](https://codeforces.com/contest/1829/problem/B)

赛时代码：

```cpp
#include <bits/stdc++.h>
using namespace std;

int a[105],cnt[105];

int main()
{
	int t;cin>>t;
	while(t--)
	{
		int n;cin>>n;
		memset(cnt,0,sizeof cnt);
		int ans=0,tmp=1;
		for(int i=1;i<=n;i++)
		{
			cin>>a[i];
			if(!a[i]) cnt[tmp]++;
			else tmp++;
		}
		for(int i=1;i<=tmp;i++) ans=max(ans,cnt[i]);
		cout<<ans<<endl;
	}
	return 0;
}
```

### C. Mr. Perfectly Fine

[Portal.](https://www.luogu.com.cn/problem/CF1829C)

用 $ans_1$ 统计只训练出技能 A 的最少时间，$ans_2$ 统计只训练出技能 B 的最少时间，$ans$ 统计同时训练出两种技能的最少时间。按题意模拟即可。

```cpp
#include <bits/stdc++.h>
using namespace std;

void solve()
{
    int n;cin>>n;
    int ans1=0x3f3f3f,ans2=0x3f3f3f,ans=0x3f3f3f;
    for(int i=1;i<=n;i++)
    {
        int tme;string s;cin>>tme>>s;
        if(s[0]=='1') ans1=min(ans1,tme);
        if(s[1]=='1') ans2=min(ans2,tme);
        if(s[0]=='1'&&s[1]=='1') ans=min(ans,tme);
    }
    if((ans1==0x3f3f3f||ans2==0x3f3f3f)&&ans==0x3f3f3f) cout<<"-1"<<endl;
    else cout<<min(ans,ans1+ans2)<<'\n';
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### D. Gold Rush

[Portal.](https://www.luogu.com.cn/problem/CF1829D)

简单题。

```cpp
#include <bits/stdc++.h>
using namespace std;

int n,m;

bool dfs(int x)
{
    if(x==m) return 1;
    if(x<m) return 0;
    if(x%3) return 0;
    return dfs(x/3)|dfs(x/3*2);    
}

void solve()
{
    cin>>n>>m;
    if(dfs(n)) cout<<"YES"<<endl;
    else cout<<"NO"<<endl;
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### E. The Lakes

[Portal.](https://www.luogu.com.cn/problem/CF1829E)

直接 DFS 统计每个联通块即可。

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn=1005;
int dx[4]={0,1,-1,0},dy[4]={1,0,0,-1},a[maxn][maxn],sum,n,m;
bool vis[maxn][maxn];

void dfs(int x,int y)
{
    sum+=a[x][y];
    for(int i=0;i<4;i++)
    {
        int nx=x+dx[i],ny=y+dy[i];
        if(vis[nx][ny]||nx<1||nx>n||ny<1||ny>m||!a[nx][ny]) continue;
        vis[nx][ny]=1,dfs(nx,ny);
    }
}

void solve()
{
    cin>>n>>m;
    int ans=0;
    for(int i=1;i<=n;i++) for(int j=1;j<=m;j++) cin>>a[i][j],vis[i][j]=0;
    for(int i=1;i<=n;i++)
        for(int j=1;j<=m;j++)
        {
            if(vis[i][j]||!a[i][j]) continue;
            sum=0,vis[i][j]=1;
            dfs(i,j),ans=max(ans,sum);
        }
    cout<<ans<<endl;
}

int main()
{
    ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### F. Forever Winter

[Portal.](https://www.luogu.com.cn/problem/CF1829F)

$dep$ 记录每个结点的层数。

考虑如何找到雪花的根结点，对于每一个点假定为根统计其子节点的层数，如果出现层数大于 $3$ 的情况则一定不是根结点。

找到根结点后，统计层数为 $2$ 和 $3$ 的结点个数 $sum_1,sum_2$，显然 $x=sum_1,y=\dfrac{sum_2}{sum_1}$。

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn=10005;
struct edge{int to,nxt;}e[maxn*2];
int head[maxn],cnt,dep[maxn];

void add(int x,int y){e[++cnt]=(edge){y,head[x]},head[x]=cnt;}

void dfs(int x,int fa)
{
    dep[x]=dep[fa]+1;
    for(int i=head[x];i;i=e[i].nxt)
    {
        if(e[i].to==fa) continue;
        dfs(e[i].to,x);
    }
}

void solve()
{
    int n,m;cin>>n>>m;
    for(int i=1,u,v;i<=m;i++) cin>>u>>v,add(u,v),add(v,u);
    int sum1=0,sum2=0;
    for(int i=1;i<=n;i++)
    {
        bool flag=1;
        sum1=0,sum2=0;
        dfs(i,0);
        for(int j=1;j<=n;j++)
        {
            if(dep[j]==2) sum1++;
            if(dep[j]==3) sum2++;
            if(dep[j]>3){flag=0;break;}
        }
        if(flag) break;
    }
    cout<<sum1<<' '<<sum2/sum1<<endl;
    memset(head,0,sizeof head),memset(e,0,sizeof e),cnt=0;
}

int main()
{
    ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### G. Hits Different

[Portal.](https://www.luogu.com.cn/problem/CF1829G)

x #include <bits/stdc++.h>using namespace std;​const int maxn=505;int f[maxn][maxn],s[maxn][maxn];​int main(){    memset(f,0x3f3f3f,sizeof f);    int n;cin>>n;    for(int i=1;i<=n;i++) cin>>s[i][i],f[i][i]=1;    for(int len=2;len<=n;len++)        for(int i=1;i<=n-len+1;i++)        {            int j=len+i-1;            for(int k=i;k<j;k++)            {                f[i][j]=min(f[i][j],f[i][k]+f[k+1][j]);                if(f[i][k]==1&&f[k+1][j]==1&&s[i][k]==s[k+1][j]) f[i][j]=1,s[i][j]=s[i][k]+1;            }        }    cout<<f[1][n];    return 0;}cpp

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long

const int maxn=2030;
int s[maxn*maxn],a[maxn][maxn],id=1;

void init()
{
    for(int i=1;i<=2023;i++)
        for(int j=1;j<=i;j++)
        {
            if(i==1) za[i][j]=1;
            else a[i][j]=id*id+a[i-1][j]+a[i-1][j-1]-a[i-2][j-1];
            s[id]=a[i][j],id++;
        }
}

signed main()
{
    int t;cin>>t;
    init();    
    while(t--)
    {
        int n;cin>>n;
        cout<<s[n]<<endl;
    }
    return 0;
}
```

### H. Don't Blame Me

[Portal.](https://www.luogu.com.cn/problem/CF1829H)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1829h)
