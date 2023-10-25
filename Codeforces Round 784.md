> [Portal.](https://codeforces.com/contest/1669)

### A. Division?

[Portal.](https://www.luogu.com.cn/problem/CF1669A)

```cpp
#include<bits/stdc++.h>
using namespace std;

int main()
{
	int t;cin>>t;
	while(t--)
	{
		int x;cin>>x;
		if(x<1400) cout<<"Division 4"<<endl;
		else if(x<1600) cout<<"Division 3"<<endl;
		else if(x<1900) cout<<"Division 2"<<endl;
		else cout<<"Division 1"<<endl;
	}
	return 0;
} 
```

### B. Triple

[Portal.](https://www.luogu.com.cn/problem/CF1669B)

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn=2e5+5;
int cnt[maxn],a[maxn];

void solve()
{
    int n;cin>>n;
    for(int i=1;i<=n;i++) cin>>a[i],cnt[i]=0;
    for(int i=1;i<=n;i++) cnt[a[i]]++;
    for(int i=1;i<=n;i++) if(cnt[i]>=3) return cout<<i<<'\n',void();
    cout<<"-1"<<'\n';
}

int main()
{
    ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### C. Odd/Even Increments

[Portal.](https://www.luogu.com.cn/problem/CF1669C)

若开始时下标为奇数 / 偶数的元素奇偶性不同，则不存在可能的操作。否则存在。

```cpp
#include <bits/stdc++.h>
using namespace std;

int a[55];

void solve()
{
    int n;cin>>n;
    bool flag=1;
    for(int i=1;i<=n;i++)
    {
        cin>>a[i];
        if(i%2){if((a[i]%2)!=(a[1]%2)) flag=0;}
        else{if((a[i]%2)!=(a[2]%2)) flag=0;}
    }
    if(!flag) cout<<"NO"<<endl;
    else cout<<"YES"<<endl;
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### E. 2-Letter Strings

输入时记录每个字符组的出现次数，统计和该字符组一个字符相同一个字符不同的字符组数量累加。

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long

int cnt[30][30];

void solve()
{
    int n;cin>>n;
    memset(cnt,0,sizeof cnt);
    int ans=0;
    for(int i=1;i<=n;i++)
    {
        char a,b;cin>>a>>b;
        cnt[a-'a'][b-'a']++;
        for(int j=0;j<11;j++)
        {
            if(cnt[a-'a'][j]&&j!=b-'a') ans+=cnt[a-'a'][j];
            if(cnt[j][b-'a']&&j!=a-'a') ans+=cnt[j][b-'a'];
        }
    }
    cout<<ans<<'\n';
}

signed main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### H. Maximal AND

[Portal.](https://www.luogu.com.cn/problem/CF1669H)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1669h)