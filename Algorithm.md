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







# LeetCode

寻找某一个数字 x，当我们将豆子数量小于 x 的袋子清空，并将豆子数量大于 x 的袋中豆子数量变为 x 时，拿出的豆子数量最少。

~~~java
/*
	我们可以将 beans从小到大排序后，枚举最终非空袋子中魔法豆的数目记为x，将小于x的魔法豆全部清空，大于x的魔法豆减少至x，这样所有非空袋子中的魔法豆就都相等了。
由于拿出魔法豆 + 剩余魔法豆 = 初始魔法豆之和，我们可以考虑最多能剩下多少个魔法豆，从而计算出最少能拿出多少个魔法豆。

*/

public class Solution {
    public long minimumRemoval(int[] beans) {
        Arrays.sort(beans);
        long sum = 0, mx = 0;
        int n = beans.length;
        for (int i = 0; i < n; i++) {
            sum += beans[i];
            mx = Math.max(mx, (long) (n - i) * beans[i]);
        }
        return sum - mx;
    }
}

~~~

