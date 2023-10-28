> [Portal.](https://codeforces.com/contest/1133)

### A. Middle of the Contest

[Portal.](https://www.luogu.com.cn/problem/CF1133A)

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int main()
{
    int h1,h2,m1,m2;
    scanf("%d:%d %d:%d",&h1,&m1,&h2,&m2);
    int tot1=h1*60+m1,tot2=h2*60+m2;
    int tot=(tot2+tot1)/2;
    int h3=tot/60,m3=tot%60;
    if(h3<10) cout<<'0';cout<<h3<<':';
    if(m3<10) cout<<'0';cout<<m3;
    return 0;
}
```



