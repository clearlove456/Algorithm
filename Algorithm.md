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



给你一个字符串数组 `words` 和一个字符 `separator` ，请你按 `separator` 拆分 `words` 中的每个字符串。

返回一个由拆分后的新字符串组成的字符串数组，**不包括空字符串** 。

~~~java
/*
	复习了String和StringBuilder的区别
	String（不可变）：String 类是不可变的。一旦创建了一个 String 对象，它的值就不能被修改。任何对字符串的操作，比如连接、替换等，都会创建一个新的字符串对象。String的创建方式有两种 一种是字符变量直接赋值，这种使用到了java中的字符串常量池，在字符串常量池中创建一个对象。 另一种是使用new String("...")这种方法会创建对象还会在字符串常量池中创建对象。（都是在字符串常量池没有重复值的情况下）
	StringBuilder（可变）：StringBuilder 类是可变的，允许在已有对象的基础上进行修改，而不是创建新的对象。这使得在频繁修改字符串时，StringBuilder 比 String 具有更好的性能。
	
	String 类的常用方法：
        charAt(int index): 返回指定索引位置的字符。
        length(): 返回字符串的长度。
        substring(int beginIndex): 返回从指定索引开始到字符串末尾的子字符串。
        substring(int beginIndex, int endIndex): 返回从指定开始索引到结束索引的子字符串。
        equals(Object anObject): 比较字符串是否相等。
        equalsIgnoreCase(String anotherString): 比较字符串是否相等，忽略大小写。
        indexOf(String str): 返回指定子字符串在字符串中第一次出现的位置。
        lastIndexOf(String str): 返回指定子字符串在字符串中最后一次出现的位置。
        startsWith(String prefix): 判断字符串是否以指定的前缀开始。
        endsWith(String suffix): 判断字符串是否以指定的后缀结束。
        toUpperCase(): 将字符串转换为大写。
        toLowerCase(): 将字符串转换为小写。
        trim(): 去除字符串两端的空白字符。
        
    StringBuilder 类的常用方法：
        append(String str): 在字符串末尾追加指定的字符串。
        insert(int offset, String str): 在指定位置插入字符串。
        delete(int start, int end): 删除指定范围内的字符。
        deleteCharAt(int index): 删除指定位置的字符。
        reverse(): 反转字符串。
        length(): 返回字符串的长度。
        charAt(int index): 返回指定索引位置的字符。
        substring(int start): 返回从指定索引开始到字符串末尾的子字符串。
        substring(int start, int end): 返回从指定开始索引到结束索引的子字符串。
        indexOf(String str): 返回指定子字符串在字符串中第一次出现的位置。
        lastIndexOf(String str): 返回指定子字符串在字符串中最后一次出现的位置.
        replace(int start, int end, String str): 用指定字符串替换指定范围内的字符。
        
        
        StringBuilder s = "a";
        StringBuilder转化为String的方法:s.toString();
*/
class Solution {
    public List<String> splitWordsBySeparator(List<String> words, char separator) {

        List<String> list = new ArrayList<String>();
        
        for (String word : words){
            StringBuilder s = new StringBuilder();
            int length = word.length();
            for (int i = 0; i < length; i ++ ){
                char c = word.charAt(i);
                if(c == separator){
                    if(s.length() > 0){
                        list.add(s.toString());
                        s.setLength(0);
                    }
                }else{
                    s.append(c);
                }
            }
            if(s.length() > 0){
                list.add(s.toString());
            }
        }
        return list;
    }
}

~~~



给你一个下标从 **0** 开始的整数数组 `nums` 。如果 `nums` 中长度为 `m` 的子数组 `s` 满足以下条件，我们称它是一个 **交替子数组** ：

- `m` 大于 `1` 。
- `s1 = s0 + 1` 。
- 下标从 **0** 开始的子数组 `s` 与数组 `[s0, s1, s0, s1,...,s(m-1) % 2]` 一样。也就是说，`s1 - s0 = 1` ，`s2 - s1 = -1` ，`s3 - s2 = 1` ，`s4 - s3 = -1` ，以此类推，直到 `s[m - 1] - s[m - 2] = (-1)m` 。

请你返回 `nums` 中所有 **交替** 子数组中，最长的长度，如果不存在交替子数组，请你返回 `-1` 。

~~~java
/*
	分组循环的一般模板
	n = len(nums)
i = 0
while i < n:
    start = i
    while i < n and ...:
        i += 1
    # 从 start 到 i-1 是一组
    # 下一组从 i 开始，无需 i += 1
*/


class Solution {
    public int alternatingSubarray(int[] nums) {
        int ans = -1;
        int i = 0, n = nums.length;
        while (i < n - 1) {
            if (nums[i + 1] - nums[i] != 1) {
                i++; // 直接跳过
                continue;
            }
            int i0 = i; // 记录这一组的开始位置
            i += 2; // i 和 i+1 已经满足要求，从 i+2 开始判断
            while (i < n && nums[i] == nums[i - 2]) {
                i++;
            }
            // 从 i0 到 i-1 是满足题目要求的（并且无法再延长的）子数组
            ans = Math.max(ans, i - i0);
            i--;
        }
        return ans;
    }
}


~~~



