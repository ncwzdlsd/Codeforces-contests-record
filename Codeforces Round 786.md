> [Portal.](https://codeforces.com/contest/1674)

### A. Number Transformation

[Portal.](https://www.luogu.com.cn/problem/CF1674A)

一个构造技巧：令指数为 $1$。

```cpp
#include <bits/stdc++.h>
using namespace std;

void solve()
{
    int x,y;cin>>x>>y;
    if(y%x){cout<<"0 0"<<'\n';return;}
    else cout<<"1 "<<y/x<<'\n';
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### B. Dictionary

[Portal.](https://www.luogu.com.cn/problem/CF1674B)

```cpp
#include <bits/stdc++.h>
using namespace std;

void solve()
{
    char a,b;cin>>a>>b;
    int ans=(a-'a')*25;
    if(b>a) ans+=b-'a',cout<<ans<<'\n';
    else ans+=b-'a'+1,cout<<ans<<'\n';
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### C. Infinite Replacement

[Portal.](https://www.luogu.com.cn/problem/CF1674C)

分情况讨论：

- $t=\texttt{a}$，则替换是无效的，只有一种可能。

- $\texttt{a}\in t$ ，则可以无限替换。
- 其他情况，$s$ 中的每一项都可以选择换 / 不换，共有 $2^{\operatorname{len}(s)}$ 种可能。

```cpp
#include <bits/stdc++.h>
using namespace std;

void solve()
{
    string s,t;cin>>s>>t;
    if(t=="a"){cout<<"1\n";return;}
    for(int i=0;i<t.length();i++) if(t[i]=='a'){cout<<"-1\n";return;}
    cout<<(long long)pow(2,s.length())<<endl; 
}

int main()
{
    int t;cin>>t;
    while(t--) solve();
    return 0;
}
```

### E. Breaking the Wall

[Portal.](https://www.luogu.com.cn/problem/CF1674E)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-CF1674E)

### G. Remove Directed Edges

[Portal.](https://www.luogu.com.cn/problem/CF1066F)

[sol.](https://www.luogu.com.cn/blog/ncwzdlsd/solution-cf1674g)