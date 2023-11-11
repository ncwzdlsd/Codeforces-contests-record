> [Portal.](https://codeforces.com/contest/5)

### A. Chat Server's Outgoing Traffic

[Portal.](https://www.luogu.com.cn/problem/CF5A)

按题意模拟即可。注意 `find()` 函数能快速查找 `string` 中特定字符的位置。

```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    string s;
    int cnt=0,ans=0;
    while(getline(cin,s))
    {
        if(s[0]=='+') cnt++;
        else if(s[0]=='-') cnt--;
        else
        {
            int p=s.find(':');
            ans+=cnt*(s.length()-p-1);
        }
    }
    cout<<ans;
    return 0;
}
```

### B. Center Alignment

[Portal.](https://www.luogu.com.cn/problem/CF5B)

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn=1005;
char s[maxn][maxn];
int len[maxn];

int main()
{
	int cnt=0,mxlen=0;
	while(gets(s[cnt]))
	{
		len[cnt]=strlen(s[cnt]);
		mxlen=max(mxlen,len[cnt]);
		++cnt;
	}
	--cnt;
	for(int i=1;i<=mxlen+2;i++) cout<<"*";
	cout<<endl;
	bool flag=0;
	for(int i=0;i<=cnt;i++)
	{
		cout<<"*";
		if(!len[i]) for(int j=1;j<=mxlen;j++) cout<<" ";
		else
		{
			int p;
			if((mxlen-len[i])%2)
			{
				if(!flag)
				{
					int p=(mxlen-len[i]-1)/2;
					for(int j=1;j<=p;j++) cout<<" ";
					cout<<s[i];
					for(int j=1;j<=p+1;j++) cout<<" ";
					flag=1;
				}
				else
				{
					int p=(mxlen-len[i]+1)/2;
					for(int j=1;j<=p;j++) cout<<" ";
					cout<<s[i];
					for(int j=1;j<=p-1;j++) cout<<" ";
					flag=0;
				}
			}
			else
			{
				int p=(mxlen-len[i])/2;
				for(int j=1;j<=p;j++) cout<<" ";
				cout<<s[i];
				for(int j=1;j<=p;j++) cout<<" ";
			}
		}
		cout<<"*"<<endl;
	}
	for(int i=1;i<=mxlen+2;i++) cout<<"*";
	return 0;
}
```

### C. Longest Regular Bracket Sequence

[Portal.](https://www.luogu.com.cn/problem/CF5C)

DP。

设 $f_i$ 表示以 $i$ 为结尾的最长括号序列长度。用栈维护括号序列，如果当前元素为 $\texttt{(}$，入栈；否则若栈非空，以当前元素为结尾的最长括号序列长度即为该元素到当前栈顶元素的长度与以栈顶元素的前一个元素为结尾的最长括号序列长度。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int maxn=1e6+5;
int sta[maxn],f[maxn],cnt[maxn],top;
bool vis[maxn];
char s[maxn];

int main()
{
    cin>>(s+1);
    cnt[0]=1;
    for(int i=1;i<=strlen(s+1);i++)
    {
        if(s[i]=='(') sta[++top]=i;
        else if(top) f[i]=i-sta[top]+1+f[sta[top]-1],top--,cnt[f[i]]++;
    }
    for(int i=strlen(s+1);i>=0;i--)
        if(cnt[i]){cout<<i<<' '<<cnt[i]<<'\n';break;}
    return 0;
}
```

