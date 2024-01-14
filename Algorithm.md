# 并查集

## acwing836

~~~c++
#include <bits/stdc++.h>

using namespace std;

typedef long long LL;

const int N = 1000010;
char w;
int n, m, x, y;
int a[N], p[N];

int find(int x)
{
    if(p[x] != x) p[x] = find(p[x]);
    return p[x];
}

int main()
{
    ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);

    cin >> n >> m;
    for (int i = 1; i <= n; i ++ ) p[i] = i;

    while(m -- )
    {
        cin >> w >> x >> y;
        int pa = find(x), pb = find(y);
        if(w == 'M')
        {
            //加到以x当中
            if(pa != pb) p[pb] = pa;
        }
        else
        {
            if(pa == pb) cout <<"Yes" << endl;
            else cout << "No" << endl;
        }
    }
    return 0;
}
~~~

## acwing837

~~~c++
//若要统计有多少个块 检查p[x] = x
#include <bits/stdc++.h>

using namespace std;

typedef long long LL;

const int N = 1000010;
string w;
int n, m, x, y;
int a[N], p[N], cnt[N];

int find(int x)
{
    if(p[x] != x) p[x] = find(p[x]);
    return p[x];
}

int main()
{
    ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);
    cin >> n >> m;
    for (int i = 1; i <= n; i ++ )
    {
        p[i] = i, cnt[i] = 1;
    }

    while(m -- )
    {
        cin >> w >> x;
        if(w == "C")
        {
            cin >> y;
            int pa = find(x), pb = find(y);
            if(pa == pb) continue;
            p[pb] = pa;
            cnt[pa] += cnt[pb];            
        }
        else if(w == "Q1")
        {
            cin >> y;
            int pa = find(x), pb = find(y);
            if(pa == pb) cout << "Yes" << endl;
            else cout << "No" << endl;
        }
        else 
        {
            cout << cnt[find(x)] << endl;
        }
    }
    return 0;
}
~~~

