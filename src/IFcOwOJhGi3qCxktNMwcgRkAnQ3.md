---
title: 算法备忘录
slug: IFcOwOJhGi3qCxktNMwcgRkAnQ3
sidebar_position: 2
---


# 算法备忘录

# ACM输入输出

## <b>单组输入</b>

单组输入比较简单

数量固定的话，就直接先读数量，然后再读数据

数量不固定的话，方法很多，常见的就是while(cin)，getline(cin)

## <b>多组输入</b>

多组输入，一般题目都是多组输入，所以我们需要练习这一块的内容

其中根据多组数量，和单组数量，是否固定，我将牛客的acm模式练习分类进行了总结

https://ac.nowcoder.com/acm/contest/5652/

### <b>多组数量固定-单组数量固定</b>

[A+B(2)](https://ac.nowcoder.com/acm/contest/5652/B)

```cpp
#include <iostream>

using namespace std;

int main() {
    int t;
    cin >> t;
    
    int a, b;
    while (t--) {
        cin >> a >> b;
        cout << a + b << endl;
    }
    return 0;
}
```

[A+B(5)](https://ac.nowcoder.com/acm/contest/5652/E)

```cpp
#include <iostream>

using namespace std;

int main() {
    int t;
    cin >> t;
    
    while (t --) {
        int n;
        cin >> n;
        
        int x, sum = 0;
        while (n --) cin >> x, sum += x;
            
        cout << sum << endl;
    }
    
    return 0;
}
```

### <b>多组数量不固定-单组数量固定</b>

[A+B(1)](https://ac.nowcoder.com/acm/contest/5652/A)

```cpp
#include <iostream>

using namespace std;

int main() {
    int a, b;
    while (cin >> a >> b) {
        cout << a + b << endl;
    }    
    return 0;
}
```

[A+B(3)](https://ac.nowcoder.com/acm/contest/5652/C)

```cpp
#include <iostream>

using namespace std;

int main() {
    int a, b;
    while (cin >> a >> b, a || b) {
        cout << a + b << endl;    
    }
    return 0;
}
```

[A+B(4)](https://ac.nowcoder.com/acm/contest/5652/D)

```cpp
#include <iostream>

using namespace std;

int main()
{
    int n;    
    while(cin >> n, n)
    {
        int x, sum = 0;

        while(n--) cin >> x, sum += x;
        cout << sum << endl;
    }

    return 0;
}
```

[A+B(6)](https://ac.nowcoder.com/acm/contest/5652/F)

```cpp
#include <iostream>

using namespace std;

int main() {
    int n;
    while (cin >> n) {
        int sum = 0, x;
        
        while (n --) cin >> x, sum += x;
        cout << sum << endl;
    }
    
    return 0;
}
```

### <b>多组数量不固定-单组数量不固定</b>

[A+B(7)](https://ac.nowcoder.com/acm/contest/5652/G)

```cpp
#include <iostream>
#include <string>
#include <sstream>

using namespace std;

int main() {
    string s;
    while (getline(cin, s)) {
        stringstream line(s);
        int sum = 0, x;
        while (line >> x) sum += x;
        cout << sum << endl;
    }
    return 0;
}
```

[字符串排序(2)](https://ac.nowcoder.com/acm/contest/5652/I)

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
#include <sstream>

using namespace std;

int main() {
    string s;
    while (getline(cin, s)) {
        stringstream line(s);
        
        vector<string> res;
        string x;
        
        while (line >> x) res.push_back(x);
        sort(res.begin(), res.end());
        
        for (auto &s: res) cout << s << " ";
        cout << endl;
    }
    return 0; 
}
```

[字符串排序(3)](https://ac.nowcoder.com/acm/contest/5652/J)

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <sstream>
#include <algorithm>

using namespace std;

int main() {
    string s;
    while (getline(cin, s)) {
        stringstream line(s);
        
        string x;
        vector<string> res;
        while (getline(line, x, ',')) res.push_back(x);
        sort(res.begin(), res.end());
        
        for (int i = 0; i < res.size(); i ++ ) {
            if (i == res.size() - 1) cout << res[i] << endl;
            else cout << res[i] << ",";
        }
    }
    return 0;
}
```

# <b>双指针</b>

双指针是一个很经典的算法，常见的模型有定长同向双指针，不定长同向双指针，相向双指针，多指针匹配

其中同向双指针我们又叫做滑动窗口

## 不定长同向双指针

场景：
暴力枚举发现单调性，利用双指针算法优化

固定一个指针，另一个指针往一个方向移动，一定满足性质；发现单调性，利用双指针算法优化 

满足某种条件的子数组/子串问题，满足单调性；最常见的场景


方法：
枚举右端点，然后根据题目找最大的左端点或者是最小的左端点（枚举右端点可以避免边界判断）


如果是最大的左端点，说明该端点在满足条件的最后一个位置，
所以可以利用while（满足条件）的最后一次循环到达这个位置，while循环内部更新结果


如果是最小的左端点，说明该端点在满足条件的第一个位置，
所以可以利用whie（不满足条件）跳出后到达这个位置，之后更新结果


该思路参考了y神，灵神，以及b站up主的思路，综合转化为自己的思路和模板
<u>https://www.bilibili.com/video/BV1V44y1s7zJ/?spm_id_from=333.788&vd_source=cb02f779bd17a3aad9801e0c4464dfc9</u><u>
</u>

技巧：

同向双指针，需要维护窗口

维护窗口，我们一般关注两点，窗口维护什么，窗口用什么去维护

窗口维护什么看题目限制；窗口用什么维护根据个人需求，更新窗口，就是更新窗口维护的变量

eg:

乘积小于k的子数组数目，窗口维护乘积小于k，窗口使用乘积去维护，每次更新乘积

无重复最长子串，窗口维护无重复，窗口使用哈希表统计字符出现次数去维护，每次更新哈希表

定长子串中元音的最大数目，窗口维护元音数目，窗口使用cnt统计数目维护，每次更新cnt

模板：

```cpp
模板题
lc_209. 长度最小的子数组 #求最小，找最大的j
for (int i = 0, j = 0; i < n; i ++ ) {
    右端点i进入更新窗口
    while (满足) {
        更新res
        左端点j移出更新窗口
        左端点j移出
    }
}
// 特判res一直没有更新，res应该=0

lc_03. 无重复字符的最长子串 #求最大，找最小的j
for (int i = 0, j = 0; i < n; i ++ ) {
    右端点i进入更新窗口
    while (不满足) {
        左端点j移出更新窗口
        左端点j移出
    }
    更新res
}
// 特判res一直没有更新，res应该=0，但是这里发现一直没有更新，res本来就是0，所以省略
```

#### [LeetCode 209. 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/)

> 模板题

AC，思路：求最小，找最大，所以while满足；然后注意最后特判res没有更新，res = 0；

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int n = nums.size();
        
        int res = n + 1, sum = 0;
        for (int i = 0, j = 0; i < n; i ++) {
            sum += nums[i];
            while (sum >= target) {
                res = min(res, i - j + 1);
                sum -= nums[j];
                j ++;
            }
        }

        return res == n + 1 ? 0 : res;
    }
};
```

#### [LeetCode 3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

> 模板题, leetcode hot100

AC，思路：最长字串，考虑滑动窗口来做，然后发现满足单调性；求最长，找最小的左端点，while不满足；由于while之前一定是满足，所以不满足肯定是因为新加入的字符造成的，所以while里的条件可以确定了；然后滑动窗口都需要特判，res一直没有更新时res = 0，这里求最长本身res初始化为0，所以可以省略特判；

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.size();

        unordered_map<int, int> map;
        int res = 0;
        for (int i = 0, j = 0; i < n; i ++) {
            map[s[i]] ++;
            while (map[s[i]] > 1) {
                map[s[j]]--;
                j ++;
            }
            res = max(res, i - j + 1);           
        }
        return res;
    }
};
```

#### [76. 最小覆盖子串](https://leetcode.cn/problems/minimum-window-substring/)

> Leetcode hot100

AC，思路：首先发现是不定长滑动窗口，然后关键在于覆盖子串怎么判断，当该子串和目标串的每个字符的出现次数相同时说明该串是覆盖子串；其中统计子串和目标串的每个字符出现次数相同，看438题，可以通过hash表记录每个字符的出现次数之差；最后有两个易错点，首先不要再while里直接记录答案，极端情况下会超时；然后就是注意特判窗口没有滑动的情况

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        int k = t.size(), n = s.size();
        if (k > n) return "";

        unordered_map<int, int> hash;
        for (auto c: t) hash[c]++;
        int cnt = hash.size();

        int min_len = n + 1, start = 0;
        for (int i = 0, j = 0, ok = 0; i < n; i ++) {
            // 右端点滑入
            hash[s[i]] --;
            if (hash[s[i]] == 0) ok ++;

            // 最小，求最大的j，while满足
            while (ok == cnt){
                if (i - j + 1 < min_len) {
                    // res = s.substr(j, i - j + 1);  这样写某些极端情况会反复统计超时
                    start = j;
                    min_len = i - j + 1;
                }
                if (hash[s[j]] == 0) ok --;
                hash[s[j]]++;
                j ++;
            }
        }
        return min_len == n + 1 ? "": s.substr(start, min_len);
    }
};
```

#### <b>LeetCode 1493. 删掉一个元素以后全为 1 的最长子数组</b>

> 笔试题单

AC，思路：求删除一个后只包含1的子数组最大长度；转为 最多包含一个0的子数组的最大长度；窗口满足条件时，左端点移动还是满足，满足单调性；不定长滑动窗口，窗口维护最多包含一个0，也就是维护0的个数；然后模板求最长，最小的j；

```cpp
class Solution {
public:
    int longestSubarray(vector<int>& nums) {
        // 满足单调性 当前窗口只包含1 j移动还是只包含1

        int n = nums.size();
        int ans = 0;
        int cnt = 0;   //窗口维护最多只有一个0, 维护0的个数
        for (int i = 0, j = 0; i < n; i ++) {
            if (nums[i] == 0) cnt ++;
            // 找最长， 最小的j
            while (j <= i && cnt > 1) {
                if (nums[j] == 0) cnt --;
                j ++;
            }
            ans = max(ans, i - j);
            // printf("cnt: %d, ans: %d\n", cnt, ans);
        }

        return ans;
    }
};
```

#### <b>LeetCode 904. 水果成篮</b>

> 笔试题单

AC, 思路：主要就是题意转化 转化模型 子数组 满足只能由两种水果 求最大长度；所以不定长滑动窗口，窗口维护 不同元素数目 &lt;= 2，所以维护不同元素数目；注意这里要用map，而不是set；具体原因前面有提过；

```cpp
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        // 转化模型 子数组 满足只能由两种水果 求最大长度

        int n = fruits.size();
        int ans = 0;
        // 窗口维护 不同元素只能有两个；
        unordered_map<int, int> map;
        for (int i = 0, j = 0; i < n; i ++) {
            map[fruits[i]]++;

            while (j <= i && map.size() > 2) {
                map[fruits[j]]--;
                if (map[fruits[j]] == 0) map.erase(fruits[j]);
                j ++;
            }
            ans = max(ans, i - j + 1);
        }

        return ans;
    }
};
```

#### <b>2023 华为 od- k 优雅阈值</b>

> 笔试题单

NOT AC，思路：分析后发现满足单调性；也是不定长滑动窗口，然后窗口维护出现次数最多的元素的出现次数 &gt; x; 但是维护的内容我不会处理，卡住了；这里是统计子数组数目，跟之前的模板不太一样；暂时还没有理非常好的思路，下次回过头看；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 10001;

int n, x;
int a[N];

int main() {
    
    cin  n  x;
    for (int i = 0; i < n; i ++) cin >> a[i];

    unordered_map<int, int map;
    int ans = 0;
    for (int i = 0, j = 0; i < n; i ++ ) {
        map[a[i]] ++;

        while (map[a[i]] = x) {
            ans += n - i;
            map[a[j]] --;
            j ++;
        }
    }

    cout << ans << endl;

    return 0;

}
```

#### <b>2023 字节-牧羊人塔子</b>

> 笔试题单

NOT AC，思路：只能感觉是子数组模型，无法确定滑动窗口需要维护什么；窗口维护连续有羊的羊圈个数 &lt;= n，我们总共才n个有羊圈，所以不满足跳过；然后满足条件后就统计答案，转换次数 = n - (区间目前的有羊的羊圈数）；不是所有的不定长滑动窗口都是运用模板，这两道笔试题都是要自己分析；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5 + 10;
int n;
int a[N];

int main() {
    cin >> n;
    for (int i = 0; i < n; i ++) cin >> a[i];


    
    // 窗口维护 连续有羊的羊圈个数 <= n
    sort(a, a + n);
    int res = 1e9;
    for (int i = 0, j = 0; i < n; i ++) {
        while (j <= i && a[i] - a[j] + 1 > n) j ++;   // 不满足跳过
        int cnt = n - (i - j+ 1);
        res = min(res, cnt); 
    }
    cout << res << endl;
    return 0;
}
```

## 定长同向双指针

场景：

需要枚举每一个定长窗口

方法：

直接枚举每一个窗口，需要注意的是窗口的性质，有些时候通过上一个窗口递推来求，而不是直接求

技巧：

跟同向双指针的技巧一样，都是看窗口维护什么，用什么维护

模板：

两种模板写法，第一种是把初始窗口也放入了循环内，第二种需要先初始化初始窗口，然后移动；

所以很显然，第一种写法，更容易写出错率低

```cpp
lc_1456. 定长子串中元音的最大数目

写法1： 不定长通用写法 本质是 while(满足长度) 然后因为while每个i只循环一次，所以if（满足长度）
窗口长度为k
for (int i = 0, j = 0; i < n; i ++ ) {
    右端点i进入更新窗口
    if (i - j + 1 == k) {
        更新res
        左端点j移出更新窗口
        左端点j移出
    }
}

写法2：枚举每一个窗口
初始化第一个窗口,更新答案
for (int i = k; i < n; i ++ ) {
    右端点i入，更新窗口
    左端点i - k出，更新窗口
    更新res
}
```

#### <b>LeetCode 1456. 定长子串中元音的最大数目</b>

> 模板题

AC，思路：枚举所有定长子串，很明显定长滑动窗口；窗口维护元音数目；窗口使用cnt维护；

```cpp
class Solution {
public:
    int maxVowels(string s, int k) {
        int n = s.size();

        unordered_set<char> set {'a', 'i', 'o', 'e', 'u'};
        int cnt = 0, res = 0;
        for (int i = 0, j = 0; i < n; i ++) {
            if (set.count(s[i])) cnt ++;
            if (i - j + 1 == k) {
                res = max(res, cnt);
                if (set.count(s[j])) cnt --;
                j ++;
            }
        }

        return res;
    }
};
```

#### [438. 找到字符串中所有字母异位词](https://leetcode.cn/problems/find-all-anagrams-in-a-string/)

> Leetcode hot100

NOT AC，思路：在s中找p的异位词子串，可以固定长度的滑动窗口来做，然后每次判断s和p是否为异位词；那么如何判断呢，就是它们的每个字母的出现次数要相同；所以你可以使用两个数组各自统计窗口和p的字符出现次数；但是这样的比较显然不是最高效的；我们可以使用diff数组直接统计每个字母的出现次数之差，当差为0，说明有一种字符满足了，当所有的字符都满足，说明两个数组为异位词了，具体看代码

```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        if (p.size() > s.size()) return {};     // p比s大，不可能是异位词
        
        // 哈希表统计，p和s每个字符的出现次数差
        unordered_map<char, int> hash;
        for (auto c: p) hash[c] ++;
        vector<int> res;

        // cnt代表字符种数，ok代表满足的字符总数
        int cnt = hash.size();
        for (int i = 0, j = 0, ok = 0; i < s.size(); i ++ ) {
            // 右端点滑入，出现次数差减小
            hash[s[i]]--;
            if (hash[s[i]] == 0) ok ++;  // 如果减完是0，说明当前字符满足要求了，ok++

            // 窗口满足长度了
            if (i - j + 1 == p.size()) {
                if (ok == cnt) res.push_back(j);
                if (hash[s[j]] == 0) ok--;   // 如果当前是0，说明左端点滑出后不满足要求了，ok--;
                hash[s[j]]++;
                j++;
            }
        }

        return res;
    }
};
```

#### [239. 滑动窗口最大值](https://leetcode.cn/problems/sliding-window-maximum/)

> Leetcode hot100

NOT AC，思路：难点在于如何判断窗口的最大值，多次判断窗口内的最大值

堆：用堆去维护窗口遍历过的元素，如果最大值出现在窗口左侧，就把该值pop出去，直到最大值出现在窗口内部，我们不需要关心堆中的元素数量和窗口的元素数量相等，我们只需要关心堆中的最大元素是窗口中的最大元素即可；

```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> ans;
        // 堆中的元素需要维护下标，这样才能判断是否在窗口中
        priority_queue<pair<int, int>> heap;
        for (int i = 0; i < n; i ++) {
            heap.emplace(nums[i], i);
            if (i >= k - 1) {  // 第一个窗口的右端
                // 不断地移除堆顶的元素，直到其确实出现在滑动窗口中 
                while (heap.top().second <= i - k) heap.pop();
                ans.push_back(heap.top().first);
            }
        }
        return ans;
    }
};
```

单调队列：todo

#### <b>LeetCode 2841. 几乎唯一子数组的最大和</b>

> 笔试题单

AC, 思路：定长滑动窗口，但是这里窗口维护的是不同元素数目；不能使用set维护，因为set只能维护不同元素，无法维护数目；所以这里要用map维护；要注意int爆栈，需要使用long long；map里value = 0的元素要自己清除；这是一道代码细节很多的题目；

```cpp
class Solution {
public:
    long long maxSum(vector<int>& nums, int m, int k) {
        int n = nums.size();
        
        unordered_map<int, int> hash_map; //窗口维护不同元素数目
        long long sum = 0;           //窗口维护数组和

        long long ans = 0;
        for (int i = 0, j = 0; i < n; i ++) {
            hash_map[nums[i]]++;
            sum += nums[i];

            if (i - j + 1 == k) {
                if (hash_map.size() >= m) ans = max(ans, sum);
                // printf("sum : %ld, size: %ld, ans; %ld\n", sum, hash_map.size(), ans);
                hash_map[nums[j]]--;
                if (hash_map[nums[j]] == 0) hash_map.erase(nums[j]);
                sum -= nums[j];
                j ++; 
            }
        }

        return ans;
    }
};
```

#### <b>2023 阿里-加一减一</b>

> 笔试题单

NOT AC，思路：我的想法是枚举所有长度为k的子串，然后统计最小次数；所以定长滑动窗口，窗口维护最小次数；然后维护最小次数这里，我没写出来，我的思路是贪心地发现如果要最小次数，那么目标是平均值，然后统计最小次数；最后发现平均值贪心是错的，所以还是老老实实枚举目标值；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 10e5 + 10;

int n, k;
int a[N];

int main() {
    cin  n;
    cin  k;

    for (int i = 0; i < n; i ++) cin >> a[i];

    long long ans = 0x3f3f3f3f;

    for (int x = 0; x < 10; x ++) {
        // 窗口维护 最小操作次数
        long long cost = 0;
        for (int i = 0, j = 0; i < n; i ++) {
            cost += abs(a[i] - x);

            if (i - j + 1 == k) {
                ans = min(ans, cost);
                cost -= abs(a[j] - x);
                j ++;
            }

        }
    }

    if (ans == 0x3f3f3f3f) cout << 0 << endl;
    else cout << ans;
}
```

#### <b>LeetCode 2134. 最少交换次数来组合所有的 1 II</b>

> 笔试题单

NOT AC, 思路：自己完全没有思路；首先思考聚集1的数组，其实长度是固定的就是1的个数；所以我们枚举这个长度的子数组去统计答案；定长滑动窗口，窗口维护最小交换次数；然后由于是环形数组，我们滑动窗口长度肯定不会超过原数组长度，所以直接破环成链，再末端添加原数组；

```cpp
class Solution {
public:
    int minSwaps(vector<int>& nums) {
        int n = nums.size(), ones = 0;
        for (int i = 0; i < n; i ++) {
            if (nums[i] == 1) ones++;
            nums.push_back(nums[i]);
        }


        int k = ones;
        int cost = 0;// 窗口维护最少交换次数 = 0的个数

        int ans = 1e9;
        for (int i = 0, j = 0; i < 2*n; i ++) {
            if (nums[i] == 0) cost ++;

            if (i - j + 1 == k) {
                ans = min(ans, cost);
                if (nums[j] == 0) cost --;
                j ++;
            }
        }

        return ans == 1e9 ? 0 : ans;
    }
};
```

## 相向双指针

场景：

暴力枚举，发现指针之间有单调性，可以通过双指针优化

直接先让右指针向右移动一位，然后看左指针是否一定会向左移动一位，如果是的话，那就代表存在单调性，可以使用相向双指针算法

方法：

首先定义左右指针，放在首尾两侧，然后通过比较current和target，移动左右指针

 

技巧：

模板：

```cpp
模板题
- lc_167. 两数之和 II - 输入有序数组
int l = 0, r = n - 1;
while (l < r) {
    calc cur
    if (cur == target) 更新res
    else 移动l or r
}
```

#### [LeetCode 167. 两数之和 II - 输入有序数组](https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted/)

> 模板题

AC，思路：首先暴力枚举可以做，然后尝试双指针优化，假设lr满足target，然后r右移，如果需要满足target，l必须左移，发现相向单调性，相向双指针优化；注意索引从1开始

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int n = numbers.size();

        int l = 0, r = n - 1;
        while (l < r) {
            int sum = numbers[l] + numbers[r];
            if (sum == target) return {l + 1, r + 1};
            else if (sum > target) r --;
            else l ++;
        }

        return {};
    }
};
```

#### [LeetCode 15. 三数之和](https://leetcode.cn/problems/3sum/)

> 模板题, leetcode hot100

NOT AC，思路：首先暴力枚举三个指针，然后里面两个指针尝试使用双指针优化，只要我们先对原数组排序，就可以满足单调性；然后注意去重，对每一个数去重，第一个数去重就在循环开头，如果和上一个数一样，说明情况已经考虑过了，所以跳过；后两个数，在满足条件后去重，如果满足条件，那么我们就先跳到下一位，如果和之前的数相同，说明已经添加过了，跳过；

为什么不能把后两个数的去重逻辑放在 sum != target的时候，很简单，我们去重是对满足条件的答案去重，sum == target时满足条件，我们才去重

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        vector<vector<int>> ans;
        
        for (int i = 0; i < n - 2; i ++) {
            // 第一个数去重
            if (i >= 1 && nums[i] == nums[i - 1]) continue;
            
            int l = i + 1, r = n - 1;
            while (l < r) {
                int sum = nums[i] + nums[l] + nums[r];
                if (sum == 0) {
                    ans.push_back({nums[i], nums[l], nums[r]});
                    // 后两个数去重  先跳一步，然后判断后一步和前一步是否相同
                    do r--; while (r > l && nums[r] == nums[r + 1]);
                    do l ++;  while (l < r && nums[l] == nums[l - 1]);
                }
                else if (sum > 0) r --; 
                else l ++; 
            }
        }

        return ans;
    }
};
```

#### [11. 盛最多水的容器](https://leetcode.cn/problems/container-with-most-water/)

> Leetcode hot100

AC，思路：相向双指针模板题，首先找到单调性发现可以双向双指针，最后再根据木桶原理，只能移动短板

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int n = height.size();
        int l = 0, r = n - 1;
        
        int ans = 0;
        while (l < r) {
            int w = r - l, h = min(height[l], height[r]);
            int area = w * h;
            ans = max(ans, area);
            // 移动长板没有意义面积绝对会变小，移动短板面积才有增大的可能性
            if (height[l] < height[r]) l++;
            else r --; 
        }
        return ans;
    }
};
```

#### [42. 接雨水](https://leetcode.cn/problems/trapping-rain-water/)

> Leetcode hot100

NOT AC，思路：

前后缀分解：首先图中的每个位置，我们看作是一个宽度为1的桶，首先我们要统计每个桶的容量，那就是要算出木桶的高，木桶的左板高度其实就是左边的最大值，我们可以利用前缀最大值O(1)计算，木桶的右板高度就是右边的最大值，我们可以利用后缀最大值O(1)计算，这样我们的木桶容量就得出来了，也就是min(左板高度，右板高度）* 宽度1；但是我们实际接雨水的容量需要减去原本的体积，所以每个木桶接雨水的容量 = min(左板高度，右板高度）* 1 - height * 1;

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
        
        // 数组从1开始，方便构造前后缀数组;
        vector<int> pre_max(n + 1);
        for (int i = 1; i <= n; i ++) pre_max[i] = max(pre_max[i - 1], height[i - 1]);
    
        vector<int> suf_max(n + 2);
        for (int i = n; i >= 1; i --) suf_max[i] = max(suf_max[i + 1], height[i - 1]);
        
        int ans = 0;
        // 遍历数组 1~n
        for (int i = 1; i <= n; i ++) {
            ans += min(pre_max[i], suf_max[i]) - height[i - 1];
        }
        return ans;
    }
};
```

#### 
## 多指针匹配

场景：

这类题型一般是有多个数组或者字符串，然后多个指针指向不同的数组或者字符串，这类题型<b>最经典的问题</b>就是<b>判断子序列问题</b>，很多题目都可以抽象成这样一个问题

方法：

声明多个指针，指向不同序列的头

#### <b>LeetCode 392.判断子序列</b>

> 模板题

AC，思路：双指针i, j指向s，t首位，然后如果匹配成功，一起后移 i++，j++;

如果匹配不成功，j向后移动一位，继续匹配；如果j遍历完了，i也遍历完了那就是true，否则false;

```cpp
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int i = 0, j = 0, m = s.size(), n = t.size();

        while (i < m && j < n) {
            // 匹配成功
            if (s[i] == t[j]) i ++, j ++;
            // 匹配不成功
            else j ++;
        }
        return i == m;
    }
};
```

#### [283. 移动零](https://leetcode.cn/problems/move-zeroes/)

> Leetcode hot100

AC，思路：很多种做法，最简单的想法就是先把非0元素放入数组，然后再把0元素放入数组

放入新数组：遍历原数组，非零元素放入新数组，同时统计0元素个数，然后0元素放入新数组，原数组 = 新数组

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int cnt = 0;
        vector<int> nums1;
        for (int num: nums) {
            if (num != 0) nums1.push_back(num);
            else cnt ++;
        }
        while(cnt --) nums1.push_back(0);
        nums = nums1; 
    }
};
```

覆盖原数组：遍历原数组，非0元素覆盖原数组，同时统计当前的非0元素的index，最后index - end覆盖成0元素

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        int idx = 0;   // 非零元素的遍历index
        for (int i = 0; i < n; i ++) {
            if (nums[i] != 0) {
                nums[idx++] = nums[i];
            }
        }

        // 现在idx为第一个0元素的位置，补齐0即可
        for (int i = idx; i < n; i ++) {
            nums[i] = 0;
        }
    }
};
```

#### <b>LeetCode 2410. 运动员和训练师的最大匹配数</b>

> 笔试题单

AC, 思路：还是贪心匹配，匹配比他的数值大，且尽可能接近他的训练师trainers[i]；所以我们先排序，之后就是多指针匹配问题模板；

```cpp
class Solution {
public:
    int matchPlayersAndTrainers(vector<int& players, vector<int& trainers) {
        // 贪心匹配
        int i = 0, j = 0, m = players.size(), n = trainers.size();
        int ans = 0;
        
        sort(players.begin(), players.end()); sort(trainers.begin(), trainers.end());
        while (i < m && j < n) {
            if (players[i] <= trainers[j]) {
                i ++, j ++, ans ++;
            }
            else j ++;
        }

        return ans;
    }
};
```

#### <b>2023 米哈游-子序列</b>

> 笔试题单

AC, 思路：增删一个子序列可以变成t；那么说明s可能是t的子序列或者t可能是s的子序列；只要满足其中一个条件就可以转化成功；

```cpp
#include <bits/stdc++.h>

using namespace std;

int q; 
string s, t;


bool check(string a, string b) {
    int i = 0, j = 0, m = a.size(), n = b.size();

    while (i < m && j < n) {
        if (a[i] == b[j]) {
            i ++ , j ++;
        }
        else j ++;
    }

    return i == m;
}

int main() {
    cin  q;
    while (q --) {
        cin  s;
        cin  t;

        if (check(s, t) || check(t, s)) cout << "Yes" << endl;
        else cout << "No" << endl;
    }


    return 0;
}
```

# 模拟

模拟 顾名思义 其实就是按照题目的要求，使用代码进行模拟求解；

其实这一类题目很能锻炼代码功底，其实日常工作和学习，我们写的代码大部分就是模拟，按照需求写出对应的代码；

常见模拟：

(1) 数组/矩阵 的 移动/变换模拟

#### [56. 合并区间](https://leetcode.cn/problems/merge-intervals/)

> Leetcode hot100

NOT AC，思路：合并区间是一个很巧妙的题，关键就在于记住要左端点排序，然后l &gt; mr和l &lt;= mr的情况，这里给出两种不同的板子；

yxc的板子：

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());  // 按照左端点从小到大排序
        
        vector<vector<int>> ans;
        int l = intervals[0][0], r = intervals[0][1];  // 第一个区间
        for (int i = 1; i < intervals.size(); i ++) {
            if (intervals[i][0] > r) {      // 当前区间和上一个区间不相交
                ans.push_back({l, r});      // 将上一个区间加入到答案
                l = intervals[i][0], r = intervals[i][1];  // 更新上一个区间为当前区间
            }
            else {  // 当前区间和上一个区间相交
                r = max(r, intervals[i][1]);   // 上一个区间的l不会变，r有可能变大
            }
        }
        ans.push_back({l, r});   // 加入最后一段区间
        return ans;
    }
};
```

灵神的板子：看灵神题解很容易分析的[56. 合并区间 - 力扣（LeetCode）](https://leetcode.cn/problems/merge-intervals/solutions/2798138/jian-dan-zuo-fa-yi-ji-wei-shi-yao-yao-zh-f2b3/?envType=study-plan-v2&envId=top-100-liked)

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());  // 按照左端点从小到大排序
        vector<vector<int>> ans;
        for (auto p: intervals) {
            int l = p[0], r = p[1];
            if (!ans.size() || l > ans.back()[1]) {  // 当前区间和上一个区间不相交，无法合并
                // 加入当前区间，左端点是确定下来了，右端点有可能更新
                ans.push_back({l, r});   
            }
            // 当前区间和上一个区间相交，可以合并，更新上一个区间的右端点
            else ans.back()[1] = max(ans.back()[1], r);
        }
        return ans;
    }
};
```

#### [189. 轮转数组](https://leetcode.cn/problems/rotate-array/)

> Leetcode hot100

AC，思路：比较简单的下标转换问题

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> tmp(n);
        
        // 遍历原数组
        for (int i = 0; i < n; i ++) {
            // 新位置 (i + k) % n, 老位置 i
            tmp[(i + k) % n] = nums[i];
        }
        nums = tmp;
    }
};
```

#### [73. 矩阵置零](https://leetcode.cn/problems/set-matrix-zeroes/)

> Leetcode hot100

AC，思路：开始犯了个错误，我想试图边找到0的位置，然后同时置0操作，这样做会有逻辑的错误，因为置0的位置有可能在后期被当作找到的0来操作，但题目的要求显然是我们只把初始为0的位置进行置0操作；所以如果非要这么写，那么我们就需要在置0操作的时候去区分初始0和后期置0；这样的话代码会复杂很多；

所以干脆直接 先找到初始0的位置，然后直接对初始0的位置进行置0操作；代码也简洁可读性高

以下代码可以空间进一步优化，把state优化成row，col两个数组，同时判断

```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        vector<vector<int>> state(m, vector<int>(n, 0));

        // 找到初始0的地方
        for (int i = 0; i < m; i ++) 
            for (int j = 0; j < n; j ++) 
                if (matrix[i][j] == 0) state[i][j] = 1;

        // 置0
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                if (state[i][j] == 1) {
                    // 行置0
                    for (int k = 0; k < n; k ++) matrix[i][k] = 0;
                    // 列置0
                    for (int k = 0; k < m; k ++) matrix[k][j] = 0;
                }
            }
        }
    }
};
```

#### [54. 螺旋矩阵](https://leetcode.cn/problems/spiral-matrix/)

> Leetcode hot100

NOT AC，思路：很经典的题目；属于网格图的范畴，一般要使用方向数组，但是螺旋矩阵这里，我们需要按照螺旋的方向去定义方向数组，然后就是确定遍历多少次，这里有m*n个数，所以遍历m*n次；然后初始化螺旋矩阵的起点和起点方向，之后就是正常网格图解法

[756. 蛇形矩阵 - AcWing题库](https://www.acwing.com/problem/content/description/758/) acm模式练习

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        // 方向数组，按照螺旋矩阵的顺序，右下左上
        int dx[4] = {0, 1, 0, -1}, dy[4] = {1, 0, -1, 0};
        
        // 螺旋矩阵起点 x,y 起点方向d, i是ans的索引，总共有m * n个数
        int x = 0, y = 0, d = 0;
        vector<int> ans(m * n);
        for (int i = 0; i < m * n; i ++) {
            ans[i] = matrix[x][y];
            matrix[x][y] = 101;  // 网格图技巧，可以省略vis数组
            int a = x + dx[d], b = y + dy[d];  // a，b新坐标
            // 出界，或者碰到已经遍历过的数
            if (a < 0 || a > m - 1 || b < 0 || b > n - 1 || matrix[a][b] == 101) {
                d = (d + 1) % 4;  // 改变方向
                a = x + dx[d], b = y + dy[d];
            }
            // 新坐标设为当前坐标
            x = a, y = b;
        }
        return ans;
    }
};
```

#### [48. 旋转图像](https://leetcode.cn/problems/rotate-image/)

> Leetcode hot100

NOT AC，矩阵相关的题目，这题是顺时针旋转90度；通过这题我们要快速复习，矩阵变换，主要掌握不同变换，矩阵坐标怎么变，代码怎么写！

方法1：顺时针旋转90度后，找规律发现，原来的(i, j)元素 转移到 倒数第i列的第j个位置，根据这个规律，利用辅助数组达到新矩阵；

技巧：坐标的计算主要看起点和偏移量，之前是0，偏移量i - 0，反转后起点n - 1，偏移量不变 =&gt; n - 1 - i；

如果是1为起点，之前是1，偏移量i - 1，反转后起点n，偏移量i - 1 =&gt; n - (i - 1) = n - i + 1

正数第i个位置，起点0，偏移量i - 1 =&gt; i - 1

倒数第i个位置，起点n - 1，偏移量i - 1 =&gt; n - 1 - (i - 1) = n - i;

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        auto tmp = matrix;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < n; j ++) {
                // 对于矩阵中第 i 行的第 j 个元素，在旋转后，它出现在倒数第 i 列的第 j 个位置
                tmp[j][n - i - 1] = matrix[i][j];
            }
        }
        matrix = tmp;
    }
};
```

方法2：方法1使用了额外的数组，不使用额外数组的话；我们就考虑 [i][j] =&gt; [j][n - i - 1]，怎么要经过多次操作得到；可以结合线性代数的矩阵变换来想；变换方法有很多种，这里提供两种思路；

首先对角线翻转[i][j] = &gt; [j][i]，然后左右翻转[j][i] = &gt; [j][n - 1 - i];

首先上下翻转[i][j] = &gt;[n - 1 - i][j]，然后对角线翻转[n - 1 - 1][j] =&gt; [j][n - i - 1];

首先副对角线翻转[i][j] = [n - j - 1][n - i - 1]，然后上下翻转[n - j - 1][n - i - 1] =&gt; [j][n - i - 1]

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        // 对角线翻转
        for (int i = 0; i < n; i ++) 
            for (int j = 0; j < i; j ++)
                swap(matrix[i][j], matrix[j][i]);
        
        // 左右翻转
        for (int i = 0; i < n; i ++) 
            for (int j = 0; j < n / 2; j ++)
                swap(matrix[i][j], matrix[i][n - j - 1]);
    }
};


class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        // 上下翻转
        for (int i = 0; i < n / 2; i ++) 
            for (int j = 0; j < n; j ++)
                swap(matrix[i][j], matrix[n - i - 1][j]);
        
        // 对角线翻转
        for (int i = 0; i < n; i ++) 
            for (int j = 0; j < i; j ++)
                swap(matrix[i][j], matrix[j][i]);
    }
};

class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        // 副对角线翻转
        for (int i = 0; i < n; i ++) 
            for (int j = 0; i + j < n - 1; j ++)
                swap(matrix[i][j], matrix[n - 1 - j][n - 1 - i]);
        
        // 上下翻转
        for (int i = 0; i < n / 2; i ++) 
            for (int j = 0; j < n; j ++)
                swap(matrix[i][j], matrix[n - i - 1][j]);
        
    }
};
```

#### 
# <b>数据结构</b>

## <b>哈希表</b>

#### <b>LeetCode 1. 两数之和</b>

> 模板题，leetcode hot100  

AC，思路：暴力枚举肯定是可以过的；优化考虑，枚举一个数，在一些数里找另一些数，用哈希表来查找；那么是枚举右端点好，还是左端点好呢；如果是枚举左端点，那么我们就要先把所有的元素放入哈希表，然后枚举逐渐缩小哈希表，其中哈希表的消除操作较为复杂；如果枚举右端点，逐渐扩大哈希表，不会有消除操作，比较方便；然后就是我们用map还是set，这里我们的key肯定是元素值，我们发现要统计索引并且key可以重复，所以用map，key是元素值，value是索引；所以我们可以发现即使知道要用哈希表还是有不少细节；

1. 哈希表逐渐扩大 要比 哈希表逐渐缩小 好维护；
2. 哈希表是否有重复元素，如果有就只能用map或者multiset；
3. 哈希表除了key是否需要其他信息，例如出现次数，索引等；如果有只能用map；
4. 删除操作是否合法，如果涉及到重复元素的哈希表，使用删除会破坏哈希表，一般不用；除非可以通过出现次数，进行判断删除；

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        vector<int> ans;
        
        unordered_map<int, int> hash;
        for (int i = 0; i < n; i ++) hash[nums[i]] = i;

        for (int i = 0; i < n; i ++) {
            int x = target - nums[i];
            if (hash[x] > i) {
                return {i, hash[x]};
            }
        }

        return {};
    }
};
```

#### [49. 字母异位词分组](https://leetcode.cn/problems/group-anagrams/)

> Leetcode hot100

NOT AC，思路：将字符串分组放入哈希表中，哈希表中key是分组，value是分组中的字符串集；所以核心问题在于，哈希表的key是什么，我们要想办法找到一个分组中的字符串的共同特征；这里有一个技巧，异位词分组的每种字母出现次数都相同；所以对于key，我们最直接的设计思路就是这些字符串排序都是相同的，所以直接将排序后的字符串作为key；

另一种思路就是将每个出现次数大于 0 的字母和出现次数按顺序拼接成字符串，作为key;

排序字符串作为key

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> hash;
        vector<vector<string>> ans;

        for (const auto& str: strs) {
            string key = str;
            sort(key.begin(), key.end());
            hash[key].push_back(str);
        }

        for (auto& [k, v]: hash) {
            ans.push_back(v);
        }
        return ans;
    }
};
```

#### [128. 最长连续序列](https://leetcode.cn/problems/longest-consecutive-sequence/)

> Leetcode hot100

AC，思路：注意这里的序列不是子序列，当前的序列是可以随意取数组成序列；

暴力的做法，就是先排序，然后找每段连续数组（注意这里的连续数组可以包含相同的元素，计算长度的时候不包括它们即可）时间复杂度由排序决定了，O(nlogn)

哈希表：枚举当前的数，判断是否是连续序列起点（如果num - 1不存在，那么就是起点），如果是就判断后面num + 1, num + 2..是否存在，统计当前数作为起点的最大长度；遍历所有的起点，得到最大长度；其中判断是否存在，使用哈希表复杂度减小到O(1)，时间复杂度降低到O(n）

暴力做法：O(nlogn)

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());

        int ans = 0;
        for (int i = 0; i < n; i ++) {
            int len = 1;
            while (i + 1 < n && (nums[i + 1] == nums[i] + 1 || nums[i + 1] == nums[i])) {
                if (nums[i + 1] == nums[i]) i ++;
                else i ++, len ++;
            }
            ans = max(ans, len);
        }
        return ans;
        
    }
};
```

哈希表：O(n)

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> hash;
        for (auto num: nums) {
            hash.insert(num);
        }
        
        int ans = 0;
        for (auto num: nums) {
            int len = 1;
            if (!hash.count(num - 1)) {
                int cur = num + 1;
                while (hash.count(cur)) cur ++, len ++; 
            }
            ans = max(ans, len);
        }
        return ans;  
    }
};
```

#### [41. 缺失的第一个正数](https://leetcode.cn/problems/first-missing-positive/)

> Leetcode hot100

AC，思路：我自己的屎山代码过了，核心思路就是我们的答案范围只能是 1 ~ n + 1，其中如果在数组里缺失就是1 ~n, 数组里都满足就是n + 1; 这里把简单做法和原地哈希做法都写一下

排序：

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int ans = 1;
        // 先找1，1找到了再用剩下的数去找2，遍历完后当前还未找到的数就是答案
        for (int i = 0; i< nums.size();i++) {
            if (nums[i] == ans) {
                ans++;
            }
        }
        return ans;
    }
};
```

哈希表：在数组里依次寻找可能的res，没有找到就是第一个缺失的正数

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();
        unordered_set<int> hash;
        for (int x: nums) hash.insert(x);

        int res = 1;
        while (hash.count(res)) res ++;
        return res;
    }
};
```

原地哈希：遍历每一个数，然后我们想让每个数都放在它应在的下标处（原地哈希），例如1就应该放在index 0处，2就应该放在index 1处；所以index i上正确存放的元素是i + 1 =&gt; nums[i] = i + 1;如果遍历的时候nums[i] = i + 1说明已经放置正确的元素，如果不是i + 1，那我们就需要把nums[i]放在它应该在的下标处，应在的下标是nums[i] - 1；同时为了不覆盖数组中原有的值，所以我们使用swap；所以是把下标i和下标nums[i] - 1这两处的数值交换；完成后，再次遍历数组，第一个不满足的下标，对应的正确放置元素的值就是答案

[LeetCode 41. 缺失的第一个正数---java版、修改数组模拟哈希set、完整注释 - AcWing](https://www.acwing.com/solution/content/94283/)

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();
        for (int i = 0; i < n; i ++) {
            // 数组中<1的数和>n的数不需要找到哈希index
            // nums[i] = i + 1, 当前的index已经放了应有的元素
            // 如果该元素不是正确元素，nums[i]的哈希index = nums[i - 1], nums[i]放入index nums[i - 1]处
            // 放入前要注意 index处的值是否一样，如果一样就不需要swap，否则会值重复死循环
            while(nums[i] >= 1 && nums[i] <= n && nums[i] != i + 1 && nums[nums[i] - 1] != nums[i]) {
                swap(nums[i], nums[nums[i] - 1]);
            }
        }

        for (int i = 0; i < n; i ++) {
            if (nums[i] != i + 1) return i + 1;
        }
        return n + 1;
    }
};
```

#### <b>2022华为-排队报数</b>

> 笔试题单

AC, 思路：很明显后面集合查找数，使用哈希表，之前是查找一个数，现在是查找满足条件的数，满足条件的数区间很小，可以直接枚举；然后我们查到数以后要统计个数，所以用map，key是元素值，value是出现次数；

```cpp
// 缩小哈希表 维护
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5 + 10;

int n;
int a[N];
int res[N];

int main() {
    cin >> n;
    for (int i = 0; i < n; i ++) cin >> a[i];
    
    unordered_map<int, int> map;
    for (int i = 0; i < n; i ++) map[a[i]]++;

    for (int i = 0; i < n; i ++) {
        int cnt = 0;
        map[a[i]]--;
        if (map[a[i]] == 0) map.erase(a[i]);
        for (int x = a[i] - 1; x >= 40; x --) {
            if (map.count(x)) cnt += map[x];
        }
        res[i] = cnt;
    }

    for (int i = 0; i < n; i ++) cout << res[i] << " ";
    return 0;
}


// 扩大哈希表 维护
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5 + 10;

int n;
int a[N];
int res[N];

int main() {
    cin >> n;
    for (int i = 0; i < n; i ++) cin >> a[i];
    
    unordered_map<int, int> map;

    for (int i = n - 1; i >= 0; i --) {
        int cnt = 0;
        for (int x = 40; x < a[i]; x ++) {
            if (map.count(x)) cnt += map[x];
        }
        res[i] = cnt;
        map[a[i]]++;
    }

    for (int i = 0; i < n; i ++) cout << res[i] << " ";
    return 0;
}
```

#### 
## 链表

#### [160. 相交链表](https://leetcode.cn/problems/intersection-of-two-linked-lists/)

> Leetcode hot100

NOT AC，思路：这一题是典型的利用链表指针相遇去找交点。

这里是两个指针指向两个链表的头，同时往后走，走完以后就移动到另一个链表的头继续往后走；这样第一次相遇的地方就是他们的第一个交点。

技巧：链表中涉及到找目标点的问题，大部分都是利用指针相遇找目标点；

具体：构造确定点到目标点的距离关系，如果找到距离关系，我们就将指针放在确定点上，控制每次移动的步数，让他们相遇，此时相遇点就是目标点。

当然我们需要证明指针一定会在目标点相遇：证明很简单，我们得到确定点到目标点的距离，只要找到距离关系，然后根据速度关系，就可以证明相遇了。

证明：目标点是第一个相交点。链表头A到交点的距离是a，交点后面的距离是c，链表头B到交点的距离是b，后面由于是交点距离一样也是c；第一个指针到交点移动a + c + b，第二个指针到交点移动b + c + a，距离一样；两个指针每次都只移动一步，必然会在交点处相遇；

```cpp
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        auto pa = headA, pb = headB;
        while (pa != pb) {
            pa = pa ? pa->next : headB;
            pb = pb ? pb->next : headA;
        }
        return pa;
    }
};
```

当然也有暴力做法，直接把其中一个链表放入哈希表中，然后另一个链表从头开始遍历，第一个在哈希表中找到的节点就是答案

```cpp
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        unordered_set<ListNode*> hash;
        for (auto p = headA; p; p = p->next) {
            hash.insert(p);
        }

        for (auto p = headB; p; p = p->next) {
            if (hash.count(p)) return p;
        }
        return nullptr;
    }
};
```

#### [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

> 反转系列 Leetcode hot100

AC，思路：一开始认为头节点变化，就自己加了dummy节点，后来发现加完后，反转会多一个节点；所以不能加dummy；

反转链表的要点：

1. 逐个反转，我们需要两个指针，一个指向前一个指向后，然后把后面节点的next指针指向前一个节点，所以需要两个指针遍历；
2. 拿到尾节点，遍历cur指针，cur到达end，pre会到达尾节点；
3. pre节点的初始化，我们最后希望原来的头节点指向空，所以pre = nullptr

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* pre = nullptr, *cur = head;
        while(cur) {
            auto tmp = cur->next;
            cur->next = pre;
            pre = cur;
            cur = tmp;
        }
        return pre;
    }
};
```

```cpp
// 错误写法，这里会造成dummy指向head，head指向dummy，这样会死循环
// 链表题报错 一般要么就是nullptr调用了next成员，要么就是两个节点相互指死循环
// 从这一题的报错中，我们需要吸取教训
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        auto dummy = new ListNode(5001); dummy->next = head;
        auto pre = dummy, cur = head;
        while(cur) {
            auto tmp = cur->next;
            cur->next = pre;
            pre = cur;
            cur = tmp;
        }
        return pre;
    }
};
```

#### [LeetCode 92. 反转链表 II](https://leetcode.cn/problems/reverse-linked-list-ii/description/)

> 反转系列

AC，思路：对于链表的题目，分析我们要做的步骤；第一步，我们想要反转left + 1，right这一部分，然后我们想让left - 1节点next指向改变，指向right；然后让left的节点next指向改变，指向right + 1；所以牢牢按照这些步骤即可；

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        ListNode *dummy = new ListNode(-501);
        dummy->next = head;

        ListNode *p1 = dummy, *p2 = head;
        for (int i = 0; i < left - 1 ; i ++) p1 = p1->next, p2 = p2->next;
        // printf("p1: %d, p2: %d", p1->val, p2->val);

        auto pre = p1->next, cur = p2->next;
        for (int i = left + 1; i < right + 1; i ++) {
            auto tmp = cur->next;
            cur->next = pre;
            pre = cur;
            cur = tmp;
        }

        p1->next = pre;
        p2->next = cur;

        return dummy->next;
    }
};
```

刷leetcode hot100的时候，重做了一遍

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        // 涉及到使用头节点前面点的操作，使用哨兵节点
        auto dummy = new ListNode(0); dummy->next = head;

        auto p0 = dummy;
        // 0到left - 1，需要跳left - 1次
        for (int i = 0; i < left - 1; i ++) p0 = p0->next;

        // left - right共有right - left + 1个节点，反转right - left + 1次
        ListNode* pre = nullptr, *cur = p0->next;
        for (int i = 0; i < right - left + 1; i ++) {
            auto tmp = cur->next;
            cur->next = pre;
            pre = cur;
            cur = tmp;
        }

        auto p1 = p0->next;
        p0->next = pre;
        p1->next = cur;

        return dummy->next;
    }
};
```

#### [234. 回文链表](https://leetcode.cn/problems/palindrome-linked-list/)

> Leetcode hot100

AC，思路：如果不考虑空间复杂度，直接将链表的元素放入数组中，然后判断回文串即可；

思考如何直接在链表中判断：较为复杂，首先得反转后半部分链表，然后就比较两段是否相等来判断回文

其中反转后半部分链表，需要两个操作：

1. 得到后半部分链表的两个端点，通过快慢指针就可以拿到这两个端点
2. 反转链表

```cpp
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        vector<int> list;
        for (auto p = head; p; p = p->next) list.push_back(p->val);

        int l = 0, r = list.size() - 1;
        while (l < r) {
            if (list[l++] != list[r--]) return false;
        }
        return true;
    }
};
```

#### [141. 环形链表](https://leetcode.cn/problems/linked-list-cycle/)

> Leetcode hot100

AC，思路：环形链表可以使用快慢指针来做，如果指针相遇那么就是有环；这里重点谈一下证明；快指针每次两步，慢指针每次一步，所以快指针的相对速度是1步，所以如果有环的话，快指针一定会和慢指针相遇，因为相对速度是1步，所以不可能跳过！！！

```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode* slow = head, *fast = head;
        while (fast && fast->next) {  // fast都不为空，slow肯定也不为空
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) return true;
        } 
        return false;
    }
};
```

#### [142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/)

> Leetcode hot100

NOT AC，思路：最暴力做法，遍历链表的时候放入哈希表中，如果遍历的节点在哈希表中出现过，说明这是环的起点，这个思路非常的暴力直观；

数学做法：假设快慢指针在环某处相遇，然后设置起点到环入口的距离为a，入口到相遇的距离为b，相遇到入口的距离为c；首先证明慢指针在环中走的距离绝对不超过一个环长，因为考虑最坏情况，slow指针在入口的时候，fast指针刚好在前面一步，那么此时相对速度1步，所以fast指针需要走环长 - 1次，此时慢指针也走环长-1次，每次一步，没有走完一个环长；

考虑到fast指针走的距离是slow指针的两倍，2(a + b) = a + b + k(b + c) = &gt;a = (k - 1)(b + c) + c；这个等式意味着head到入口的距离 = 相遇点到入口到距离 + 环长的倍数；距离相等，只要两个指针同时从head和相遇点出发，每次走1步，必然会相遇，相遇点就是入口！

总结：

(1) 先找环形链表快慢指针的相遇点，找相遇点，直接就利用环形链表的特征，快慢指针必然会相遇；

(2) 利用相遇点的等式关系，得到信息 相遇点到入口的距离 = 链表头到入口的距离

(3) 找目标点（入口），得到等式关系，将指针放在确定点移动，相遇在目标点；

tips：

找相遇点，不需要证明会在相遇点相遇，就不需要构造距离关系了。

找目标点，利用指针相遇找目标点，需要证明会在目标点相遇，需要构造距离关系。

```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* slow = head, *fast = head;
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            if (fast == slow) {
                // a = (k - 1)(b + c) + c
                // slow到入口的距离和head到入口的距离相等，所以同时走相遇的点就是入口
                while (slow != head) {
                    slow = slow->next;
                    head = head->next;
                }
                return slow;
            }
        }
        return nullptr;
    }
};
```

#### [21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)

> Leetcode hot100

AC，思路：二路归并，只是这里用在链表；我的写法是答案链表使用的是新节点，也就是我自己new出来的；但是其实这里可以直接使用原链表的节点；节省空间！

new:

```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        // 涉及到头节点插入，使用dummy方便头插
        ListNode* dummy = new ListNode(0);
        auto tail = dummy;

        // 二路归并
        while(list1 && list2) {
            if (list1->val < list2->val) {
                tail = tail->next = new ListNode(list1->val);
                list1 = list1->next;
            }          
            else {
                tail = tail->next = new ListNode(list2->val);
                list2 = list2->next;
            }
        }
        while (list1) tail = tail->next = new ListNode(list1->val), list1 = list1->next;
        while (list2) tail = tail->next = new ListNode(list2->val), list2 = list2->next;

        return dummy->next;
    }
};
```

空间优化：

```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        // 涉及到头节点插入，使用dummy方便头插
        ListNode* dummy = new ListNode(0);
        auto tail = dummy;

        // 二路归并
        while(list1 && list2) {
            if (list1->val < list2->val) {
                tail = tail->next = list1;
                list1 = list1->next;
            }          
            else {
                tail = tail->next = list2;
                list2 = list2->next;
            }
        }
        tail->next = list1 ? list1 : list2;
        return dummy->next;
    }
};
```

#### [2. 两数相加](https://leetcode.cn/problems/add-two-numbers/)

> Leetcode hot100

AC，思路：其实就是高精度加法模板题；注意进位的用法；然后就是新链表的依次插入，一般要用到dummy和tail，dummy用来方便插入头节点和最后的返回头节点，tail用来方便尾插新节点；

```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        auto dummy = new ListNode(0);
        auto tail = dummy;

        int t = 0;
        while (l1 || l2 || t) {
            if (l1) t += l1->val, l1 = l1->next;
            if (l2) t += l2->val, l2 = l2->next;
            tail = tail->next = new ListNode(t % 10);
            t = t / 10;
        }
        return dummy->next;
    }
};
```

#### [19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

> Leetcode hot100

AC，思路：核心思路很简单，就是要找到倒数第n个节点的前一个节点（目标点）；两种做法，其实就是找目标点的方式不同

方法1：求出链表的总节点数，然后得到目标点的位置，之后指针移动到这个位置

方法2：使用前后指针，让后指针指向尾节点的时候，前指针指向目标点，我们计算一个它们两个之间的偏移量是n；所以先让前指针走n步；然后再让前后指针同时移动，后指针到尾节点的时候停止，这个时候前指针指向目标点；

tips：涉及到头节点的增删，常用哨兵节点方便操作

方法1

```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        // 可能会删除头节点，所以加入哨兵节点
        auto dummy = new ListNode(0); dummy->next = head;

        // 计算链表总节点数
        int cnt = 0;
        auto p = head;
        while (p) p = p->next, cnt ++;

        // 得到删除点的前一个点的位置
        int pos = cnt - n; ListNode* p1 = dummy;
        for (int i = 0; i < pos; i ++) p1 = p1->next;

        p1->next = p1->next->next;
        return dummy->next;
    }
};
```

方法2

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        auto dummy = new ListNode(0); dummy->next = head;

        auto l = dummy, r = dummy;
        while (n --) r = r->next;   // 右指针先向右走 n 步

        while (r->next) {
            r = r->next;
            l = l->next;   // 左右指针一起走
        }

        // 此时左指针 指向 删除点的前一个节点
        l->next = l->next->next;
        return dummy->next;
    }
};
```

#### [24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)

> Leetcode hot100

AC，思路：链表的题目，总体来说分析我们需要几个指针，然后就是调整步骤，最后注重以下while遍历的条件；

我们这里每次两两交换节点，需要4个指针，分别指向1，2，3，4这4个点；然后因为涉及到头节点更换，我们可以使用哨兵节点，所以我们定义p,a,b,c4个指针，p指向b，b指向a，a指向c就达到了效果

while遍历的时候，条件怎么确定呢，两种方法

1. 看开始的时候最少要有几个点，这里要交换最少要有2个点（反转链表那个题目最少是0个点），因为有哨兵节点的存在，p一定存在，所以就是判断p-&gt;next和p-&gt;next-&gt;next存在，注意一定要先判断p-&gt;next再判断p-&gt;next-&gt;next，直接判断p-&gt;next-&gt;next会报错的，因为有可能p-&gt;next已经为空指针了；
2. 看需要多少指针，然后只有最后一个指针可以指向空（因为前面的指针指向空，就拿不到后面的指针了），所以前面的指针必须都要存在，这里c可以指向空，前面的p，a，b，c必须存在；p开始的时候指向dummy必然存在，之后又移动到b也是必然存在，所以条件就是a和b要存在 =&gt; p-&gt;next && p-&gt;next-&gt;next;

```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if (!head || !head->next) return head; // 空和1个节点的特判，分析之后，其实可以省略
        auto dummy = new ListNode(0); dummy->next = head;

        auto p = dummy;
        // 至少有两个节点，注意写法一定要先p->next存在后，再判断p->next存在
        while (p->next && p->next->next) {  
            auto a = p->next, b = a->next, c = b->next;
            p->next = b;
            b->next = a;
            a->next = c;

            p = p->next->next;
        }
        return dummy->next;
    }
};
```

#### [25. K 个一组翻转链表](https://leetcode.cn/problems/reverse-nodes-in-k-group/)

> Leetcode hot100

NOT AC，k个一组翻转，前置知识是反转链表1和2；反转链表1是反转所有节点，需要两个指针pre和cur；反转链表2是反转一段节点，需要三个指针p0, pre, cur，为什么2需要三个指针呢，因为每次反转完以后，我们还需要把反转后的节点部分拼接到原链表去，需要用到反转之前的开始位置前面的节点，我们使用p0指向；k个一组反转就是多加了一个剩余节点数判断，每次反转k个就行；

```cpp
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        // 统计节点个数
        int n = 0; auto p = head;
        while (p) p = p->next, n ++;

        // 添加哨兵节点，方便反转
        auto dummy = new ListNode(-1); dummy->next = head;

        // 反转一段链表，需要这三个指针！
        ListNode* p0 = dummy, *pre = nullptr, *cur = p0->next;
        while (n >= k) {  // 剩余节点数 >= k，可以继续反转
            // k个节点反转，反转k次；每次就是反转链表2
            for (int i = 0; i < k; i ++) {
                auto tmp = cur->next; 
                cur->next = pre;
                pre = cur;
                cur = tmp;
            }

            auto p1 = p0->next;
            p0->next = pre;
            p1->next = cur;
            p0 = p1;

            // 更新剩余节点数
            n -= k;
        }
        return dummy->next;
    }
};
```

#### [138. 随机链表的复制](https://leetcode.cn/problems/copy-list-with-random-pointer/)

> Leetcode hot100

NOT AC，思路：首先思考复制一个只有next指针的链表还是挺容易的；在之前的链表题目里我们已经总结出了一套，构建新链表的写法，哨兵 + 尾插；但是现在我们还需要复制random指针，所以我们此时可以考虑建立一个原节点 -&gt; 新节点的映射，此时新节点的random指向就可以从原节点的random的映射拿到了；

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {
        // 构建新链表的基本操作，哨兵 + 尾插
        auto dummy = new Node(0), tail = dummy;
        
        // 构建原节点 -> 新节点的映射
        unordered_map<Node*, Node*> map;
        auto p = head;
        while (p) {
            map[p] = new Node(p->val);
            p = p->next;
        }

        // 新链表中插入新节点，然后初始化新节点的next和ranodom
        p = head;
        while (p) {
            tail = tail->next = map[p];      // 新链表中插入新节点（这种插入方式已经将前一个节点的next初始化了）
            // tail->next = map[p->next];    // 初始化新节点的next （可以省略，因为下次循环的时候，该节点next会初始化）
                                             // 最后一个节点的next如果不写上一句就没有在循环中初始化，默认为null
            tail->random = map[p->random];   // 初始化新节点的random
            p = p->next;
        }

        return dummy->next;
    }   
};
```

上述做法空间复杂度O(n)，可以继续优化成O(1)

Todo:

#### [148. 排序链表](https://leetcode.cn/problems/sort-list/)

> Leetcode hot100

AC，思路：时间复杂度最优的做法自然是直接转化为数组排序

```cpp
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        vector<pair<int, ListNode*>> nums;
        auto p = head;
        while (p) {
            nums.push_back({p->val, p});
            p = p->next;
        }
        sort(nums.begin(), nums.end());

        auto dummy = new ListNode(0), tail = dummy;
        for (int i = 0; i < nums.size(); i ++) {
            cout << nums[i].first << " ";
            tail = tail->next = nums[i].second;
        }
        tail->next = nullptr;   
        // 注意：新链表的节点不是new出来的，tail指向的最后一个节点使用的是原来的节点，原来的节点的next不为空，会导致有环
        return dummy->next;
    }
};
```

#### [23. 合并 K 个升序链表](https://leetcode.cn/problems/merge-k-sorted-lists/)

> Leetcode hot100

NOT AC，思路：这题有很多种解法，最应该掌握的就是小根堆和最小堆解法，其中最小堆是小根堆的优化

小根堆：把所有节点放入小根堆中维护，每次弹出最小节点；时间复杂度O(n*log(n))，空间复杂度O(n);

```cpp
class Solution {
public:
    ListNode *mergeKLists(vector<ListNode *> &lists) {
        // 维护一个小根堆，元素是listnode类指针
        auto cmp = [](const ListNode *a, const ListNode *b) {
            return a->val > b->val; // 最小堆
        };
        priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> pq;
        for (auto head: lists) {
            // 把当前链表的所有节点放入小根堆中
            auto p = head;
            while (p) {
                pq.push(p);
                p = p->next;
            }
        }

        // 构建答案链表
        auto dummy = new ListNode(0), tail = dummy;
        while (!pq.empty()) { // 循环直到堆为空
            // 每次拿到最小节点
            auto node = pq.top();
            pq.pop();
            // 添加到新链表
            tail = tail->next = node;
        }
        // 这里不能省略，因为如果最大节点val和前面节点的val相等，不能保证最后pop出的节点是链表中末尾节点
        tail->next = nullptr;    
        return dummy->next;
    }
};
```

最小堆：之前的小根堆解法中，我们直接把所有节点放进去，然后每次取堆顶（最小节点）；我们尝试去将小根堆优化成最小堆，最小堆中维护可能是最小节点的集合；因为给出的k个链表是有序的，所以初始情况下最小节点只可能是每个链表的头节点，之后拿到这个最小节点后，新的最小节点只可能是弹出最小节点的链表的下一个节点或者其他链表的头节点，所以我们每次弹出一个节点后，就将这个节点所在链表的下一个节点放入最小堆中；这样最小堆中最多只有k个元素，时间复杂度优化成O(n*log(k))，空间复杂度优化成O(k);

```cpp
class Solution {
public:
    ListNode *mergeKLists(vector<ListNode *> &lists) {
        // 维护一个最小堆，元素是listnode类指针
        auto cmp = [](const ListNode *a, const ListNode *b) {
            return a->val > b->val; // 最小堆
        };
        priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> pq;
        for (auto head: lists) {
            if (head) {
                pq.push(head);
            }
        }

        // 构建答案链表
        auto dummy = new ListNode(0), tail = dummy;
        while (!pq.empty()) { // 循环直到堆为空
            // 拿到最小节点
            auto node = pq.top();
            pq.pop();
            if (node->next) { // 下一个节点不为空
                pq.push(node->next); // 下一个节点有可能是最小节点，入最小堆
            }
            // 添加到新链表
            tail = tail->next = node;
        }
        // 这里可以省略，因为即使出现相同的最大节点，最小堆中可以保证最后的最大节点最后加入
        // 最大的节点肯定是其中一个链表的末尾节点， 它的next已经指向空
        // tail->next = nullptr;    
        return dummy->next;
    }
};
```

#### [146. LRU 缓存](https://leetcode.cn/problems/lru-cache/)

> Leetcode hot100

NOT AC，思路：我自己的思路首先实现增查改，我们可以使用哈希表，然后删的时候，发现需要维护一个队列，每次使用队列中的元素时，需要把这个元素移动到开头或者末尾；如果使用数组来维护这个队列肯定超过O(1)，使用链表维护这个队列，把元素移动到开头或者结尾，就是删除这个元素，然后新的位置添加元素，链表的增删是O(1)的所以可以达到这个要求；但是删除节点需要先找到这个节点，所以我们利用哈希表存储 key和节点（C++中存储节点这种类对象，一般使用节点类指针），我自己卡在这了；

但是现在我们删除需要的是该节点前面的节点，这个时候单向链表无法拿到前面的节点，所以这里可以使用双向链表，这样就可以拿到前面的节点了；总结：使用哈希表 + 双向链表

这里给出两种实现：

1. 直接使用std::unordered_map和std::list作为哈希表和双向链表

上述说的节点类指针，其实就是std::list中的元素指针，stl容器中的元素指针我们一般使用迭代器代替，这样的话就可以使用容器内部的一些函数方便操作；所以哈希表存储的是&lt;key, list容器的迭代器&gt;，然后list存储的是key value对，使用pair就行；具体实现看代码

```cpp
// 分析后需要使用 哈希表 + 双向链表（模拟队列）
// 使用stl容器 std::unordered_map, std::list

class LRUCache {
public:
    LRUCache(int capacity) {
        size_ = capacity;
    }
    
    int get(int key) {
        auto it = hash.find(key);
        if (it == hash.end()) return -1;
        else {
            cache.splice(cache.begin(), cache, hash[key]);  // 把当前元素放入链表头部
            return hash[key]->second;
        }
    }
    
    void put(int key, int value) {
        if (get(key) != -1) {  //key存在,调用get时已将缓存移到头部，再更新hash
            hash[key]->second = value; 
        }
        else {
            if (cache.size() == size_) {   // 超过容量了，删除链表尾部元素，删除map中的对应元素
                auto delKey = cache.back().first;
                cache.pop_back();
                hash.erase(delKey);
            }
            // 没有超过容量，链表中头插新元素，map中添加新元素
            cache.push_front({key, value});
            hash[key] = cache.begin();
        }
    }

private:
    list<pair<int, int>> cache;
    unordered_map<int, list<pair<int, int>>::iterator> hash;
    int size_;
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```

#### [LeetCode LCR 026. 重排链表](https://leetcode.cn/problems/LGjMqU/description/)

AC，思路：这道题首先考虑简单做法，把链表里的节点存储到数组里进行重排；重排有两种方式，直接重排值然后导入新链表，也可以改变节点的next指向，直接重排节点；这里可以直接重排节点；注意最后一个节点的next指向空；

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    void reorderList(ListNode* head) {
        if (head == nullptr || head->next == nullptr) return;

        vector<ListNode *> a;
        while (head) {
            a.push_back(head);
            head = head->next;
        }

        for (int i = 0; i < a.size(); i ++) cout << a[i]->val << " ";

        int l = 0, r = a.size() - 1, idx = 0;
        while (l < r) {
            a[l]->next = a[r];
            a[r]->next = a[l + 1];
            l ++, r --;
        }
        a[l]->next = nullptr;
        head = a[0];
    }
};
```

拓展：如果要排序列表，怎么做

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    void reorderList(ListNode* head) {
        if (head == nullptr || head->next == nullptr) return;

        vector<ListNode *> a;
        while (head) {
            a.push_back(head);
            head = head->next;
        }

        // for (int i = 0; i < a.size(); i ++) cout << a[i]->val << " ";

        sort(a.begin(), a.end(), [](ListNode *p1, ListNode *p2) -> bool {
            return p1->val < p2->val;
        });

        for (int i = 0; i < a.size(); i ++) cout << a[i]->val << " ";

        ListNode *dummy = new ListNode(0);
        auto p = dummy;
        for (int i = 0; i < a.size(); i ++) p->next = a[i], p = a[i];
        p->next = nullptr;

        head = dummy->next; 
    }
};
```

#### [LeetCode LCR 136. 删除链表的节点](https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/description/)

AC，删除节点顾名思义是要找删除节点的前一个节点，所以使用p-&gt;next遍历；

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* deleteNode(ListNode* head, int val) {
        auto dummy = new ListNode(-100); dummy->next = head;
        auto p = dummy;
        while (p->next) {
            if (p->next->val == val) {
                p->next = p->next->next;
                break;
            }
            p = p->next; 
        }

        return dummy->next;
    }
};
```

#### [LeetCode 237. 删除链表中的节点](https://leetcode.cn/problems/delete-node-in-a-linked-list/)

AC，很经典的题目；思路：让删除的点变成后一个节点；注意内存泄露问题；

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    void deleteNode(ListNode* node) {
        auto tmp = node->next;
        node->val = node->next->val;
        node->next = node->next->next;
        
        // 只能用 delete 不能用 free(tmp);
        delete(tmp);
    }
};
```

## 二叉树

## 栈

讲解：

<img src="/assets/LHhDbK6O3oV9hDxLev2ccnFonvD.png" src-width="1191" src-height="610" align="center"/>

<img src="/assets/C54JbpOlroN0zqx2sfscU6uYnOc.png" src-width="1191" src-height="613" align="center"/>

<img src="/assets/Uc9DbYdMqoSW7Vx1cxlcvygFnAc.png" src-width="1195" src-height="643" align="center"/>

<img src="/assets/WhRebt1RqoVCCXx81bccTriDnUg.png" src-width="1175" src-height="652" align="center"/>

总结：循环不变量：[1, top]存放栈元素，top = 0时栈为空

```cpp
栈 后入先出的数据结构
两大元素：栈大小（size), 栈顶指针（top)
三大操作：push（入栈），pop（出栈），access top（访问栈顶）

一般用数组模拟栈

initial：我是用1-base
1-base：[1, top]存放栈元素，初始时栈为空top = 0，栈中最多元素[1, size], 初始化stk[size + 1]
0-base：[0, top]存放栈元素，初始时栈为空top = -1，栈中最多元素[0, size - 1]，初始化stk[size]

push:
stk[++top] = x;

pop:
if (top == 0) error
--top;

access top:
stk[top]

isempty:   // 使用1-base
top > 0 栈不为空
top == 0 栈为空

query k: (查询从上往下第k个元素）
stk[top + 1 - k]  // 起点是top，偏移量 （倒数第一到倒数第k，k - 1) top - (k - 1)
```

常见问题：

(1) 序列多次匹配字符串：当我们要在一个序列多次匹配一个字符串，我们可以用栈来维护；我们把字符依次放入栈中，然后当栈里出现匹配字符了，就弹出；最后如果栈是空的，就说明序列都是由匹配字符串组成的；

(2) 

#### [828. 模拟栈](https://www.acwing.com/problem/content/830/)

AC，思路：数组实现栈，需要非常熟悉

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5;

// 数组模拟栈
int stk[N + 1];
int top = 0;

int main()
{
    int m;
    cin >> m;
    while (m --) {
        string op;
        cin >> op;
        
        if (op == "push") {
            int x; cin >> x;
            stk[++top] = x;
        }
        else if (op == "pop") {
            --top;
        }
        else if (op == "empty") {
            if (top == 0) cout << "YES" << endl;
            else cout << "NO" << endl;
        }
        else if (op == "query") {
            if (top > 0) cout << stk[top] << endl;
        }
    }
    return 0;
}
```

## 队列

讲解：

普通队列：

<img src="/assets/StVrb3Q8YoUF8Sx4PQTcpLSanJd.png" src-width="1156" src-height="632" align="center"/>

<img src="/assets/Jws0bGUTBoWnKUxnPtmcBL60nsd.png" src-width="1159" src-height="632" align="center"/>

<img src="/assets/HkOVbeRU8o2D77xZwHIcBIqLnXc.png" src-width="1154" src-height="613" align="center"/>

<img src="/assets/EayLb79ICoFjY7xT7POcyn47nce.png" src-width="1166" src-height="641" align="center"/>

总结：

普通队列：循环不变量：[front, rear]存放队列元素，front &lt;= rear队列不为空

```cpp
队列 先入先出的数据结构
   队列增长方向-->
front -----------rear

三大元素：front（队头）rear（队尾） size（大小）
三大操作：push（入队), pop（出队), access(访问）

一般用数组模拟队列

普通队列：
1-base，初始时front = 1；rear = 0（为空），队列区间[1, rear]；q[size + 1]
0-base，初始时front = 0；rear = -1（为空），队列区间[0, rear]；q[size]

push: 入队
q[++rear] = x;

pop: 出队
front ++;

access: 非空访问
q[rear] 队尾
q[front] 队头

isempty:
front <= rear 非空
front > rear 空

query k: (从队头第k个元素）
q[front + k - 1];
```

循环队列：

<img src="/assets/OryqbJ9Svo5krTxuw2dc6I7Hnhf.png" src-width="1173" src-height="582" align="center"/>

循环队列用来处理，入队操作次数非常多，但是队列中元素最多数量其实比较小的情况，可以极大节省空间；

循环队列相对于普通队列，要多注意两点

(1) 循环队列一般使用0-base，可以更好的去找到当前位置指定偏移量后的位置

(2) 循环队列中，队列最大长度size一定要比队列最多元素数量N 要大，这样才可以区分队满和队空的情况；

具体实现可以看leetcode 622. 设计循环队列

```cpp
循环队列：
采用0-base: 更方便拿到当前位置的指定偏移量后的位置 
队列区间[front, rear] or [front, size - 1] + [0, rear]
初始 front = 0, rear = -1为空，元素0 ~ size - 1，初始化q[size]
队列最大长度size一定要比队列最多元素数量n大(否则无法区分刚好装满和空); size = n + 1;


push:
rear = (rear + 1) % size;
q[rear] = x;

pop:
front = (front + 1) % size;

access:
q[rear], q[front]

isempty:
(rear + 1) % size == front      // 隔一位为空

isfull:
(rear + 2) % size == front     // 隔两位为满

query k:
q[(front + k - 1) % size]
```

#### [829. 模拟队列](https://www.acwing.com/problem/content/831/)

AC，普通队列的数组模拟，一定要滚瓜烂熟

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5;

// 数组模拟队列
int q[N + 1];
int front = 1, rear = 0;

int main()
{
    int m;
    cin >> m;
    while (m --) {
        string op;
        cin >> op;
        
        if (op == "push") {
            int x; cin >> x;
            q[++rear] = x;
        }
        else if (op == "pop") {
            ++front;
        }
        else if (op == "empty") {
            if (front <= rear) cout << "NO" << endl;
            else cout << "YES" << endl;
        }
        else if (op == "query") {
            if (front <= rear) cout << q[front] << endl;
        }
    }
    return 0;
}
```

#### [循环队列练习](http://oj.daimayuan.top/course/7/problem/417)

AC，循环队列模拟题，这里第一次见到卡C++的cin和cout的，甚至连关闭cin cout同步流 + tie(0)都过不了，最后是用的C的输入输出才过的；

```cpp
#include <b><</b>bits<b>/</b>stdc<b>++.</b>h<b>></b>

<b>using</b> <b>namespace</b> <b>std;</b>

<b>const</b> <b>int</b> N <b>=</b> 1000<b>;</b>

<em>//</em> <em>循环队列</em>
<b>const</b> <b>int</b> size_ <b>=</b> N <b>+</b> 1<b>;</b>
<b>int</b> q<b>[</b>size_<b>];</b>  <em>//</em> <em>0-base</em>
<b>int</b> front <b>=</b> 0<b>,</b> rear <b>=</b> <b>-</b>1<b>;</b>

<b>int</b> main<b>()</b>
<b> {</b>
    <b>int</b> m<b>;</b>
    cin <b>>></b> m<b>;</b>
    <b>while</b> <b>(</b>m<b>--)</b> <b>{</b>
        <b>char</b> op<b>[</b>10<b>];</b>
        scanf<b>("%s",</b> op<b>);</b>
        
         <b>if</b> <b>(</b>op<b>[</b>2<b>]</b> <b>==</b> 's'<b>)</b> <b>{</b>
            <b>int</b> x<b>;</b>
            scanf<b>("%d",</b> <b>&</b>x<b>);</b>
            
             rear <b>=</b> <b>(</b>rear <b>+</b> 1<b>)</b> <b>%</b> size_<b>;</b>
            q<b>[</b>rear<b>]</b> <b>=</b> x<b>;</b>
        <b>}</b>
        <b>else</b> <b>if</b> <b>(</b>op<b>[</b>1<b>]</b> <b>==</b> 'o'<b>)</b> <b>{</b>
            front <b>=</b> <b>(</b>front <b>+</b> 1<b>)</b> <b>%</b> size_<b>;</b>
        <b>}</b>
        <b>else</b> <b>{</b>
            <b>int</b> k<b>;</b> scanf<b>("%d",</b> <b>&</b>k<b>);</b>
            printf<b>("%d</b>\n<b>",</b> q<b>[(</b>front <b>+</b> k <b>-</b> 1<b>)</b> <b>%</b> size_<b>]);</b>
        <b>}</b>
    <b>}</b>
    <b>return</b> 0<b>;</b>
<b> }</b>
```

#### [约瑟夫问题](http://oj.daimayuan.top/course/7/problem/46)

NOT AC，约瑟夫问题，非常的经典；这里由于m &lt;= n，所以我们可以使用较为经典的队列做法；

总共要选出n个人，每次选出一个人，需要m次操作（一次操作O(1)），时间复杂度是O(n * m)；

队列最大容量就看初始大小和最多push多少次，初始大小是n，每选一个人，需要先push m - 1个人到队列末尾，才能选到这一个人；所以队列最大是 n + n * (m - 1) = n * m;

```cpp
#include <b><</b>bits<b>/</b>stdc<b>++.</b>h<b>></b>

<b>using</b> <b>namespace</b> <b>std;</b>

<b>const</b> <b>int</b> N <b>=</b> 10000<b>;</b>

<em>//</em> <em>队列</em>
<b>int</b> q<b>[</b>N <b>+</b> 1<b>];</b>
<b>int</b> front <b>=</b> 1<b>,</b> rear <b>=</b> 0<b>;</b>

<b>int</b> main<b>()</b>
<b> {</b>
    <b>int</b> n<b>,</b> m<b>;</b>
    cin <b>>></b> n <b>>></b> m<b>;</b>
    
     <em>//</em> <em>先把全部元素入队</em>
    <b>for</b> <b>(int</b> i <b>=</b> 1<b>;</b> i <b><=</b> n<b>;</b> i <b>++)</b> q<b>[++</b>rear<b>]</b> <b>=</b> i<b>;</b>  
     
     <b>int</b> cnt <b>=</b> 0<b>;</b>  <em>//</em> <em>计数</em> <em>cnt表示当前是第几个</em>
    <b>while</b> <b>(</b>front <b><=</b> rear<b>)</b> <b>{</b>
        <b>++</b> cnt<b>;</b>
        <b>if</b> <b>(</b>cnt <b>==</b> m<b>)</b> <b>{</b>  <em>//</em> <em>第m个出队，重新数</em>
            cout <b><<</b> q<b>[</b>front<b>]</b> <b><<</b> <b>"</b> <b>";</b>
            <b>++</b>front<b>;</b>
            cnt <b>=</b> 0<b>;</b>
        <b>}</b>
        <b>else</b> <b>{</b> <em>//</em> <em>不是第m个，说明实际上没有出队，pop后依次加到队尾，之后还是要遍历的</em>
            q<b>[++</b>rear<b>]</b> <b>=</b> q<b>[</b>front<b>];</b>
            <b>++</b>front<b>;</b>
        <b>}</b> 
     <b>}</b>
    
     <b>return</b> 0<b>;</b>
<b> }</b>
```

#### [622. 设计循环队列](https://leetcode.cn/problems/design-circular-queue/)

AC，循环队列模板题；这里很好的练习了一下，循环队列要注意几个点

(1) 首先一定要使用0-base，这样我们可以方便的找到当前位置指定偏移量的位置；

(2) 区分队空和队满，队列最大长度size 一定要比队列最多元素数量n大；举个例子，如果size == n；找出一种队满的情况，front = 0， rear = n - 1 = size - 1，此时在循环队列中隔一位；找出一种队空的情况，front = 0， rear = -1，此时在循环队列中也隔一位；所以如果size = n，我们无法区分队空和队满；但如果size = n + 1，此时队空还是front = 0， rear = -1；但是队满 front = 0，rear = n - 1 = size - 2; 此时我们发现队空隔一位，队满隔两位，两者区分开来了； 

0-base 写法推荐

```cpp
class MyCircularQueue {
public:
    MyCircularQueue(int k) {
        // 队列最大长度size_ 一定要比队列最多元素数量k大！
        // 这样才可以区分队空 和 队满 如果size_ = k,那么队空和队满都是front和rear隔一位
        size_ = k + 1;   // 队列最大长度 比 最多元素数量 大一位，那么队列满的时候front和rear此时隔两位
        q.resize(size_);  // 0-base，所以是[0, size - 1]，初始化[size_]
    }
    
    bool enQueue(int value) {
        if (isFull()) return false;
        rear = (rear + 1) % size_;
        q[rear] = value;
        return true;
    }
    
    bool deQueue() {
        if (isEmpty()) return false;
        front = (front + 1) % size_;
        return true;
    }
    
    int Front() {
        if (isEmpty()) return -1;
        return q[front];
    }
    
    int Rear() {
        if (isEmpty()) return -1;
        return q[rear];
    }
    
    bool isEmpty() {
        return (rear + 1) % size_ == front;  // 空的时候隔一位
    }
    
    bool isFull() {
        return (rear + 2) % size_ == front;  // 满的时候隔两位
    }

    // 成员变量 队列相关
    
    // 循环队列推荐使用0-base，因为0-base的话，可以更容易得到当前位置偏移k位的位置，(i + k) % n
    // 在判断空和满，以及当前元素 左/右 k位元素的时候 都非常方便
    vector<int> q;
    int front = 0, rear = -1;
    int size_;  // 队列最大长度
};
```

1-base写法，判断空和满的时候都需要分类讨论，而且找当前位置的指定偏移量位置会很麻烦

```cpp
class MyCircularQueue {
public:
    MyCircularQueue(int k) {
        size_ = k + 1;
        q.resize(size_ + 1);
    }
    
    bool enQueue(int value) {
        if (isFull()) return false;
        rear = rear % size_ + 1;
        q[rear] = value;
        return true;
    }
    
    bool deQueue() {
        if (isEmpty()) return false;
        front = front % size_ + 1;
        return true;
    }
    
    int Front() {
        if (isEmpty()) return -1;
        return q[front];
    }
    
    int Rear() {
        if (isEmpty()) return -1;
        return q[rear];
    }
    
    bool isEmpty() {
        return rear % size_ + 1 == front;
    }
    
    bool isFull() {
        if (front <= rear) return rear - front + 1 == size_ - 1;
        else return rear + 2 == front;
    }

    vector<int> q;
    int front = 1, rear = 0;
    int size_;
};
```

## 堆

#### [239. 滑动窗口最大值](https://leetcode.cn/problems/sliding-window-maximum/)

> Leetcode hot100

NOT AC，思路：难点在于如何判断窗口的最大值，多次判断窗口内的最大值

堆：用堆去维护窗口遍历过的元素，如果最大值出现在窗口左侧，就把该值pop出去，直到最大值出现在窗口内部，我们不需要关心堆中的元素数量和窗口的元素数量相等，我们只需要关心堆中的最大元素是窗口中的最大元素即可；

```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> ans;
        // 堆中的元素需要维护下标，这样才能判断是否在窗口中
        priority_queue<pair<int, int>> heap;
        for (int i = 0; i < n; i ++) {
            heap.emplace(nums[i], i);
            if (i >= k - 1) {  // 第一个窗口的右端
                // 不断地移除堆顶的元素，直到其确实出现在滑动窗口中 
                while (heap.top().second <= i - k) heap.pop();
                ans.push_back(heap.top().first);
            }
        }
        return ans;
    }
};
```

单调队列：todo

## 单调栈，单调队列

单调栈：

讲解：

<img src="/assets/XCs2bsFrvoEUkYxgyBHc7PFanOe.png" src-width="1163" src-height="606" align="center"/>

<img src="/assets/HxWRblnCwoLijuxDRYgc44AvnUb.png" src-width="1166" src-height="600" align="center"/>

要点：

1. 求更大使用单调递减栈，求更小使用单调递增栈，然后上一个/下一个 更大/更小 都有从左到右和从右到左两种写法，每种都要熟练掌握；一般来说 求下一个使用从右到左，求上一个使用从左到右，这样加入答案时是ans[i] = stk.top；这样的话栈里不仅可以存下标也可以存数；但是如果使用另一个写法，那么加入答案时就是ans[stk.top] = i; 这样的话stk.top只能是下标，所以栈里只能存下标，有的时候写起来不是很方便；
2. 想要理解记忆每种情况的从左到右和从右到左的写法，就需要把下面的图分析模式熟练掌握
3. 条件是否加等号，拿下一个更大举例分析；从左到右，要求下一更大，所以必须是严格大于，a[i] &gt; stk.top，所以不能加等号，加了等号就有可能是等于不是下一个更大了；而从右到左，如果不加等号，相等的时候栈顶就无法弹出了，此时下一个元素(栈顶）和a[i]相等不是答案，我们想要的实际上是图中指向的位置，所以等于的时候必须被弹出，所以此时要加等号；所以判断是否加等号我们自己可以脑海里想象下面的图，可以很容易分析得到

<img src="/assets/DWtvbsgojof8Rxx91nscmAvbnVb.jpeg" src-width="1901" src-height="1080" align="center"/>

#### [739. 每日温度](https://leetcode.cn/problems/daily-temperatures/)

AC，模板题，求下一个更大，练习一下从左到右和从右到左的写法;

从左到右:

```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int> &temperatures) {
        int n = temperatures.size();
        vector<int> ans(n);
        stack<int> stk;
        for (int i = 0; i < n; i++) {
            while (!stk.empty() && temperatures[i] > temperatures[stk.top()]) {
                int j = stk.top();
                stk.pop();
                ans[j] = i - j;
            }
            stk.push(i);
        }
        return ans;
    }
};
```

从右到左:

```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int> &temperatures) {
        int n = temperatures.size();
        vector<int> ans(n);
        stack<int> stk;
        for (int i = n - 1; i >= 0; i --) {
            while (!stk.empty() && temperatures[i] >= temperatures[stk.top()]) {
                stk.pop();
            }
            if (stk.empty()) ans[i] = 0;
            else {
                int j = stk.top();
                ans[i] = j - i;
            }
            stk.push(i);
        }
        return ans;
    }
};
```

#### 830. 单调栈

AC，求上一个最小，使用单调递增栈，这里给出从左到右和从右到左两种写法;

从左到右，此时加入答案 ans[i] = stk.top，所以根据题目要求，我们栈里可以直接存数，而且ans的每一个元素都会去计算答案；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5;
int a[N], ans[N];
stack<int> stk;

int main()
{
    
    int n;
    cin >> n;
    
    for (int i = 0; i < n; i ++) cin >> a[i];

    for (int i = 0; i < n; i ++) {
        while (stk.size() && a[i] <= stk.top()) {
            stk.pop();
        }
        if (stk.empty()) ans[i] = -1;
        else ans[i] = stk.top();
        
        stk.push(a[i]);
    }
    
    for (int i = 0; i < n; i ++) cout << ans[i] << " ";
    return 0;
}
```

从右到左，此时加入答案是ans[stk.top] = i；stk.top必须是下标，所以栈里只能存下标，然后ans中只有找到的元素才会计算答案，所以我们需要先初始化ans数组为-1，代表初始都没找到；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5;
int a[N], ans[N];
stack<int> stk;

int main()
{
    
    int n;
    cin >> n;
    
    for (int i = 0; i < n; i ++) cin >> a[i];
    for (int i = 0; i < n; i ++) ans[i] = -1;
    
    for (int i = n - 1; i >= 0; i --) {
        while (stk.size() && a[i] < a[stk.top()]) {
            ans[stk.top()] = i;
            stk.pop();
        }
        stk.push(i);
    }
    
    for (int i = 0; i < n; i ++) {
        ans[i] == - 1 ? cout << -1 << " " : cout << a[ans[i]] << " ";
    }
    return 0;
}
```

## 并查集

讲解：

<img src="/assets/KD8zbL6owoXjsHx1jzHcV9frnJi.png" src-width="1170" src-height="580" align="center"/>

<img src="/assets/HfGNb6tpbooaPnxkT1GcfCMnnqh.png" src-width="1172" src-height="594" align="center"/>

<img src="/assets/XVnCb1KFuoBHVdxecUGcjFounxc.png" src-width="1170" src-height="587" align="center"/>

<img src="/assets/X2ZrbQOlQoFz5rx6iQscFdYmnxb.png" src-width="1179" src-height="621" align="center"/>

<img src="/assets/Cdo7b9BIEoRpeTxtcTyc3es5n9c.png" src-width="1176" src-height="609" align="center"/>

<img src="/assets/RDtHbOThOo2qoFxtpVncogmwnUh.png" src-width="1173" src-height="575" align="center"/>

<img src="/assets/ScgzbwfwaoRXodxVqAHctq3Intc.png" src-width="758" src-height="392"/>

并查集模板：

```cpp
// find 就是找x所在集合的代表 <=> 找x所在树的根节点
int find(x) {
    if (fa[x] == x) return x;   // 如果是根节点
    return fa[x] = find(fa[x]); // 路径压缩，返回根节点
}

// merge 合并x和y所在的集合
void merge(int x, int y) {
    int fx = find(x), fy = find(y);
    if (fx == fy) return;
    fa[x] = fy;
}
```

参考资料：

1. [代码源-并查集](https://pan.baidu.com/pfile/video?path=%2F2023_job%2F%E7%AE%97%E6%B3%95%2F%E4%BB%A3%E7%A0%81%E6%BA%90%2F%E2%97%8F%E2%97%8F%E2%97%8F01.%E3%80%90%E4%BB%A3%E7%A0%81%E6%BA%90%E7%BC%96%E7%A8%8B%E3%80%91%E4%BB%A3%E7%A0%81%E6%BA%90%E5%88%9D%E7%BA%A7%E8%AF%BE%E2%97%8F%E2%97%8F%E2%97%8F%2F03.%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E5%88%9D%E7%BA%A7%2F%E7%AC%AC%E5%8D%81%E4%B8%80%E8%8A%82%EF%BC%9A%E5%B9%B6%E6%9F%A5%E9%9B%86(2022-03-28%2001-41-38).mp4&theme=light&from=home)
2. [lyd-并查集](https://pan.baidu.com/pfile/video?path=%2F2023_job%2F%E7%AE%97%E6%B3%95%2F%E7%AE%97%E6%B3%95%E8%AE%AD%E7%BB%83%E8%90%A52021%E7%89%88%E7%AC%AC0%E6%9C%9F%E3%80%90%E5%AE%8C%E7%BB%93%E3%80%91%2F%E7%AE%97%E6%B3%95%E8%AE%AD%E7%BB%83%E8%90%A52021%E7%89%88%E7%AC%AC0%E6%9C%9F%2F16--%E7%AC%AC7%E5%91%A8%20%20%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%EF%BC%88%E4%B8%89%EF%BC%89%EF%BC%8C%E5%AD%97%E5%85%B8%E6%A0%91%E3%80%81%E5%B9%B6%E6%9F%A5%E9%9B%86%2F2--%E7%AC%AC14%E8%AF%BE%20%20%E5%AD%97%E5%85%B8%E6%A0%91%E3%80%81%E5%B9%B6%E6%9F%A5%E9%9B%86%2F%E7%AC%AC14%E8%AF%BE%20%20%E5%AD%97%E5%85%B8%E6%A0%91%E3%80%81%E5%B9%B6%E6%9F%A5%E9%9B%86.mp4&theme=light&from=home)
3. [yxc-并查集](https://www.acwing.com/activity/content/problem/content/885/)
4. [github.com](https://github.com/upupming/algorithm/blob/master/template.md#%E5%B9%B6%E6%9F%A5%E9%9B%86)

#### <b>AcWing 836. 合并集合</b>

AC，思路：并查集模板题，主要就是考察并查集的两个操作：1. 两个集合合并； 2. 询问两个元素是否在一个集合当中

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5;

int fa[N + 1];

int find(int x)
{
    if (fa[x] == x) return x;
    return fa[x] = find(fa[x]);
}

void merge(int x, int y) {
    int fx = find(x), fy = find(y);
    if (fx == fy) return;
    fa[fx] = fy;
}

int main()
{
    int n, m;
    cin >> n >> m;
    
    // 初始化集合
    for (int i = 1; i <= n; i ++ ) fa[i] = i;

    while (m --)
    {
        string op;
        int a, b;
        cin >> op >> a >> b;
        if (op == "M") merge(a, b);
        else
        {
            if (find(a) == find(b)) cout << "Yes" << endl;
            else cout << "No" << endl;
        }
    }

    return 0;
}
```

#### <b>AcWing 837. 连通块中点的数量</b>

AC，思路：每一个连通块（无向无环连通图，树）其实都是一个集合；

1. 对于连边操作，其实就是集合间的合并。

2. 对于查询是否在同一连通块，也就是集合的询问操作。

3. 对于查询连通块中点的数量，也就是查询集合的大小

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5;

int fa[N + 1], cnt[N + 1];

int find(int x)
{
    if (fa[x] == x) return x;
    return fa[x] = find(fa[x]);
}

void merge(int x, int y) {
    int fx = find(x), fy = find(y);
    if (fx == fy) return;
    fa[fx] = fy;
    cnt[fy] += cnt[fx];
}

int main()
{
    int n, m;
    cin >> n >> m;
    
    // 初始化集合
    for (int i = 1; i <= n; i ++ ) fa[i] = i, cnt[i] = 1;

    while (m --)
    {
        string op;
        int a, b;
        cin >> op;
        if (op == "C") {
            cin >> a >> b;
            merge(a, b);
        }
        else if (op == "Q1") {
            cin >> a >> b;
            if (find(a) == find(b)) puts("Yes");
            else puts("No");
        }
        else {
            cin >> a;
            cout << cnt[find(a)] << endl;
        }
    }

    return 0;
}
```

## 字典树（Trie树）

字典树讲解：

<img src="/assets/FZ9JbuATMoaYZJxyiw7cuvGxnXe.png" src-width="1159" src-height="582" align="center"/>

<img src="/assets/GRC8bz9M1oZKuRx6r1kcVu6onXb.png" src-width="1155" src-height="572" align="center"/>

<img src="/assets/UnK4bALteozq5bxsJM5c3FDGnic.png" src-width="1166" src-height="577" align="center"/>

<img src="/assets/LkCubKoUbo3dUTxIg7scsd1inxd.png" src-width="1166" src-height="579" align="center"/>

<img src="/assets/Bn2MbXzbzonbqFxkYEScrsx0nzd.png" src-width="1162" src-height="570" align="center"/>

<img src="/assets/GxFEbNuV8o7blfxxbd0caB5UnFb.png" src-width="1156" src-height="574" align="center"/>

<img src="/assets/VEYQbc2s0o8EYVxyrAZc5oBxnhb.png" src-width="1156" src-height="618" align="center"/>

Yxc Trie树模板讲解：https://www.acwing.com/solution/content/14695/

总结：

字典树是一种高效存储和查找字符串的数据结构；

字典树实际是一棵多叉树，对于每个点，它最多有（字符集个数）个子节点；所以我们还是以多叉树的方式来存储字典树；

模板：

acm模式：

字典树存储

```cpp
// 二维数组存储
const int N = 10010         // 最大节点个数
const int charsize = 26     // 字符集大小，这里是每个节点最多有26个子节点
// son二维数组，存储每个节点的每个字符子节点的编号，son[i][j]是i节点的j字符子节点的编号；
int son[N + 1][charsize];  // 为什么N + 1，因为编号从1开始
int cnt[N + 1]  // cnt数组，存储以每个节点结尾的字符串个数（同时也起标记作用）
// bool is_end  // 标记 当前点是某个字符串的结尾，一般记录cnt就已经包括标记的作用了
int idx;        // 当前节点编号数

// struct和指针存储
struct Node {
    Node* son[];   // son数组，存储每个字符子节点的节点指针  son[i] 当前节点i字符节点的节点指针
    cnt;           // 当前节点结尾的字符串个数
}
```

字典树插入，查询模板（二维数组存储字典树）

```cpp
void insert(string& str)
{
    int now = 0;   // now在根节点
    for(int i = 0; i < str.size(); i ++)  { // 遍历字符串
        int x = str[i] - 'a';     // 字符转化为对应数字，方便存储
        if(!son[now][x]) {        // 当前节点的x字符子节点不存在
            son[now][x] = ++idx;  // 创建子节点
        }
        now = son[now][x];         // 走到子节点
    }
    cnt[now]++;                  // 记录以字符串尾部节点结尾的字符串个数
}

int search(string& str)
{
    int now = 0;
    for(int i = 0; i < str.size(); i ++) {
        int x = str[i] - 'a';
        if(!son[now][x]) {
            return 0;  // 当前节点的x字符子节点不存在，字符串不存在，不继续查找，直接返回0
        }
        now = son[now][x];  // 走到子节点 
    }
    return cnt[now];       //返回以字符串尾部节点结尾的字符串个数，其实也就是字符串出现的次数
}
```

leetcode模式：

字典树插入，查询模板（struct + 指针存储，直接看leetcode208的代码）

#### [835. Trie字符串统计](https://www.acwing.com/problem/content/description/837/)

AC，思路：Trie树模板题，之后如果想要复习Trie树，先把这个题写一遍

```cpp
#include <bits/stdc++.h>

using namespace std;

// 字典树模板
const int N = 1e5;                   // 最大节点个数
const int charsize = 26;             // 字符集大小，每个节点最多有charsize个子节点

// 存储Trie树
int son[N + 1][charsize];            // son[now][x] now节点的x字符子节点         
int cnt[N + 1];                      // cnt[now] now节点结尾的字符串个数
int idx;                             // 当前节点个数和编号

void insert(string& str) {
    int now = 0;   // now在根节点
    for (int i = 0; i < str.size(); i ++) {  // 遍历字符串
        int x = str[i] - 'a';                // 拿到字符
        if (!son[now][x]) {                  // 当前节点的x字符子节点不存在
            son[now][x] = ++idx;             // 创建子节点
        }
        now = son[now][x];                   // 走到子节点
    }
    cnt[now] ++;                             // 以字符串尾部节点结束的字符串个数++
}

int find(string& str) {
    int now = 0;
    for (int i = 0; i < str.size(); i ++) {
        int x = str[i] - 'a';
        if (!son[now][x]) return 0;
        now = son[now][x];
    }
    return cnt[now];                       // 返回以字符串尾部节点结尾的字符串个数 = 字符串的出现次数
}


int main()
{
    int n;
    cin >> n;
    while (n --) {
        string op, x;
        cin >> op >> x;
        if (op == "I") insert(x);
        else cout << find(x) << endl;
    }
    
    return 0;
}
```

#### [208. 实现 Trie (前缀树)](https://leetcode.cn/problems/implement-trie-prefix-tree/)

AC，思路：Trie树模板题，这里就是使用struct和指针来存Trie树，这种方式也要熟练掌握；

```cpp
class Trie {
public:
    // 定义trie树的节点 结构体
    struct Node {
        Node* son[26];    // 子节点数组
        int cnt;          // 以当前节点结尾的字符串个数
        // 默认构造函数 初始化成员
        Node() 
        {
            for (int i = 0; i < 26; i ++) son[i] = nullptr;
            cnt = 0;
        }
    };

    // 成员变量
    Node* root;

    Trie() {
        root = new Node(); // 创建一个根节点
    }
    
    void insert(string word) {
        Node* now = root;    // now指向根节点
        for (int i = 0; i < word.size(); i ++) {
            int x = word[i] - 'a';
            if (!now->son[x]) {
                now->son[x] = new Node();
            }
            now = now->son[x];
        }
        now->cnt ++;        // 以字符串尾部节点 结尾的字符串个数 ++
    }
    
    bool search(string word) {
        Node* now = root;
        for (int i = 0; i < word.size(); i ++) {
            int x = word[i] - 'a';
            if (!now->son[x]) {
                return false;
            }
            now = now->son[x];
        }
        return now->cnt > 0;  // now->cnt 字符串出现次数
    }
    
    bool startsWith(string prefix) {
        Node* now = root;
        for (int i = 0; i < prefix.size(); i ++) {
            int x = prefix[i] - 'a';
            if (!now->son[x]) {
                return false;
            }
            now = now->son[x];
        }
        // 只要能把该字符串搜完，说明树中绝对存在该字符串路径（前缀），但不能保证路径结尾是叶节点（可能不存在该字符串）
        return true;   
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```

# 排序

排序是一个很经典的算法，我们排序算法分为两大类，比较和非比较

<img src="/assets/R3jUbD522o8Y8xx4XoDcRETcnag.png" src-width="800" src-height="493"/>

两张图来大概看一下所有排序的时间复杂度和空间复杂度

<img src="/assets/E9ihbzx3eoNQ2hx0BVecEXCLnXb.png" src-width="762" src-height="415"/>

<img src="/assets/ZiQJbAwUno2nS6x3AW3cgZ9Gnoc.png" src-width="1445" src-height="592"/>

我们先看三种初级（最暴力）的排序算法，选择排序，插入排序，冒泡排序

选择排序：每次从未排序区间中找最小值（选择），放到已排序区间的末尾

插入排序：依次取出未排序区间中的每一个数，在已排序区间中找到合适的位置插入（插入）

冒泡排序：不断循环扫描，每次查看相邻的元素，如果逆序，则交换，每一次冒泡，会将一个元素移动到它相应的位置，该元素就是未排序元素中最大的元素

<img src="/assets/OqZkbqiHZoE2AyxBvndcwPyAnOe.png" src-width="881" src-height="496"/>

堆排序：对选择排序的优化，利用二叉堆高效地选出最小值

希尔排序：对插入排序地优化，增量分组的插入排序（不做要求）

然后我们来看两个常用的比较排序算法，归并排序，快速排序，它们都是基于分治的算法

<img src="/assets/HK6fb043qoK54Px5sFHc6cJInEc.png" src-width="711" src-height="125"/>

递归主要就是看原问题是什么，子问题是什么（涉及到子问题的划分），然后原问题和子问题的关系

归并排序：原问题（一段数组排序），子问题（左右两段数组排序），原问题和子问题的关系（一段数组排序 = 左右两段数组排序，然后把这两段排序数组有序合并）所以归并排序是在递归的归的时候做了一些计算

归并排序的伪代码

```cpp
mergeSort(int *arr, int l, int r) {
    if (l >= r) return;
    int mid = l + (r - l) / 2;
    mergeSort(arr, l, mid);
    mergeSort(arr, mid + 1, r);
    merge;
}
```

归并排序由于是分治算法，要注意是否可能会死循环，我们mid = l + r &gt;&gt; 2; 这种mid可能取到l，mid = l + r + 1 &gt;&gt; 2, 这种mid可能取到r，不管左右两段怎么划分，如果递归处理两段时出现[l,r]就会造成死循环

快速排序：原问题（一段数组排序），子问题（左右两段数组排序），原问题和子问题的关系（一段数组排序 = 左右两段数组处理成，左段都小于pivot，右段都大于pivot，然后左右两段数组排序，之后直接回溯自动合并）；所以快排是在递归的递的时候做了一些计算

快速排序的伪代码

```cpp
void quickSort(int *arr, int l, int r) {
    if (l >= r) return;
    int pivot = partition(arr, l, r);
    quickSort(arr, l, pivot);
    quickSort(arr, pivot + 1, r);
}
```

快速排序核心就是partition算法，有很多种实现，我们这里是采用了hoare partition算法https://en.wikipedia.org/wiki/Quicksort

<img src="/assets/RNfNbbCk8obSS2xPIxwcTGIpnOd.png" src-width="1026" src-height="645" align="center"/>

然后因为分治算法，有可能会死循环，也是要注意边界问题，我们递归处理的时候，要避免出现[l,r]; 写的时候可以看循环不变量 [l, i - 1], [j + 1, r]肯定是有序的，所以可以根据循环不变量来写递归的两段

上面我们所探讨的都是比较类排序，时间复杂度最快也只能达到O(nlogn)，所以我们也称这类排序算法称为非线性时间比较类排序；

---

现在我们来看非比较类排序，典型的三个非比较类排序就是，计数排序，桶排序，基数排序

计数排序：输入的数据必须是有确定范围的整数，然后将输入的数据放入一个频次数组中，然后将数据按出现次数取出

频次数组直接利用数组实现，索引是数据，槽里是出现次数，这是最原始的做法，频次数组需要是[0, max]

后续我们发现其实频次数组里[0, min - 1]这一段都没有用到，所以我们可以向左偏移进行优化，这样频次数组的大小就可以变成max - min + 1;

相关资料：

1. [超详细的十大排序算法总结](https://www.acwing.com/file_system/file/content/whole/index/content/424406/)
2. [1.0 十大经典排序算法](https://www.runoob.com/w3cnote/ten-sorting-algorithm.html)
3. https://en.wikipedia.org/wiki/Quicksort
4. [912. 排序数组 - 力扣（LeetCode）](https://leetcode.cn/problems/sort-an-array/solutions/1540000/by-peaceful-thompsonfsu-b3bu/)

#### 选择排序

最好，平均，最坏时间复杂度：都要遍历双重循环两次，所以`O(n^2)`

空间复杂度：属于原地算法，空间复杂度`O(1)`

不稳定：因为会涉及到把最小值元素交换到前面，可能会把后面的相同元素换到前面

```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        // 遍历未排序区间的起点，倒数第二个元素完成后后，最后一个元素必然有序
        for (int i = 0; i < nums.size() - 1; i ++) {
            int min = i;   // 最小值索引
            // 和未排序区间剩下的元素比较，找到最小值索引
            for (int j = i + 1; j < nums.size(); j ++) {
                if (nums[j] < nums[min]) min = j;
            }
            // 将最小值交换到未排序区间的头部，此时它是已排序区间的尾部
            swap(nums[min], nums[i]);
        }
        return nums;
    }
};
```

#### 插入排序

最好时间复杂度O(n);    平均，最坏时间复杂度：都要遍历双重循环两次，所以`O(n^2)`

空间复杂度：属于原地算法，空间复杂度`O(1)`

稳定：其实，我们在插入的过程中，如果遇到相同的元素，我们可以选择将其插入到之前元素的前面也可以选择插入到后面（稳定）所以，插入排序可以是稳定的也可能是不稳定的，一般实现为稳定的

```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        // 遍历未排序的元素，首元素可以直接插入
        for (int i = 1; i < nums.size(); i ++) {
            int key = nums[i]; //拿到当前的未排序元素
            // 从后向前遍历已排序区间
            int j = i - 1;
            while (j >= 0 && key < nums[j]) {
                nums[j + 1] = nums[j];  // key < nums[j], key向前移动 => nums[j]向后移动
                j --;
            }
            nums[j + 1] = key;   // key >= nums[j], 那么就插在j的后面，也就是nums[j + 1];
        }
        return nums;
    }
};
```

#### 冒泡排序

最好情况：`O(n)` 只需要进行一次冒泡操作，没有任何元素发生交换，此时就可以结束程序

平均，最坏情况：`O(n^2)`

属于原地算法，空间复杂度`O(1)`

稳定：在冒泡排序的过程中，在元素相等的情况下，我们不予交换，此时冒泡排序即为稳定的排序算法。

```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        // 冒泡n - 1次  开始0，现在i
        for (int i = 0; i < nums.size() - 1; i ++) {
            bool flag = false;   // 优化冒泡排序
            // 每次未排序区间，相邻的元素比较，逆序交换，冒泡出一个最大值放在后面
            // 开始n - 1, 现在n - 1 - i
            for (int j = 0; j < nums.size() - 1 - i; j ++) {
                if (nums[j] > nums[j + 1]) swap(nums[j], nums[j + 1]);
                flag = true;
            }
            if (flag == false) break;   // 扫描一次发现没有交换，已经排好序了
        }
        return nums;
    }
};
```

#### 堆排序

堆排序实际就是对选择排序的优化，选择排序每次我们需要O(n)找最小值，通过堆的性质，我们只需O(logn)来找最小值；

时间复杂度：堆排序在所有情况下，即最好最坏以及平均情况下的时间复杂度均为O(nlogn).

空间复杂度：如果直接在原先数组上构造小根堆O(1)，我的实现利用了STL的小根堆O(n)

不稳定：因为本质上时选择排序的优化，还是会涉及交换可能把相同元素的顺序改变

```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        // STL的小根堆
        priority_queue<int, vector<int>, greater<int>> heap(nums.begin(), nums.end());

        for (int i = 0; i < nums.size(); i ++) {
            nums[i] = heap.top();
            heap.pop();
        }
        return nums;
    }
};
```

#### 归并排序

最好，平均，最坏时间复杂度：O(nlogn)：递归log n层，每层我们需要遍历所有序列合并O(n)，所以O(nlogn)

空间复杂度：在归并排序过程中我们需要分配临时数组temp，所以不是原地排序算法，空间复杂度为O(n)

稳定：当我们遇到左右数组中的元素相同时，我们可以先把左边的元素放入temp数组中，再放入右边数组的元素，这样就保证了相同元素的前后顺序不发生改变。所以，归并排序是一个稳定的排序算法

```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        mergeSort(nums, 0, nums.size() - 1);
        return nums;
    }

    void mergeSort(vector<int> &nums, int l, int r) {
        if (l >= r) return;    // 递归边界
        
        // 递归排序左右两段
        int mid = l + r >> 1;
        mergeSort(nums, l, mid), mergeSort(nums, mid + 1, r);

        
        // 二路归并
        int i = l, j = mid + 1, k = 0;
        vector<int> tmp(r - l + 1);    // 这个地方很容易写错，注意这里的临时数组大小
        // 两段都没有越界时，有序归并
        while (i <= mid && j <= r) {
            if (nums[i] <= nums[j]) tmp[k++] = nums[i++]; 
            else tmp[k++] = nums[j++];
        }

        // 如果左段没有处理完，加进去
        while (i <= mid) tmp[k++] = nums[i++];

        // 如果右段没有处理完，加进去
        while (j <= r) tmp[k++] = nums[j++];

        // 拷贝回原数组，遍历现在的数组，然后原数组加偏移量放回原数组
        for (int i = 0; i < tmp.size(); i ++) nums[i + l] = tmp[i];
    }
};
```

#### 快速排序

最好，平均：O(nlogn)：递归log n层，每层我们partition需要O(n)，总时间O(nlogn)

最坏：每次p只移动一位，划分是1：n - 1；那么递归n层，每层partition需要O(n), 总时间O(nlogn)

空间复杂度：原地算法，O(1)

不稳定：分区操作涉及元素之间的交换，可能会改变顺序

```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        quickSort(nums, 0, nums.size() - 1);
        return nums;
    }

    void quickSort(vector<int> &arr, int l, int r) {
        if (l >= r) return;
        int p = partition(arr, l, r);
        quickSort(arr, l, p);
        quickSort(arr, p + 1, r);
    }

    // Hoare partition scheme
    int partition(vector<int> &arr, int l, int r) {
        int i = l - 1, j = r + 1, pivot = arr[l + r >> 1];
        while (i < j) {
            do i ++; while (arr[i] < pivot);
            do j --; while (arr[j] > pivot);
            if (i < j) swap(arr[i], arr[j]);
        }
        return j;
    }
};
```

#### 计数排序

时间复杂度：O(n + k)   k是数据范围

空间复杂度：O(k)    k是数据范围 max - min + 1

稳定：取决于实现

```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        // 查询数据范围
        int min_val = INT_MAX, max_val = INT_MIN;
        for (auto &x: nums) {
            if (x < min_val) min_val = x;
            if (x > max_val) max_val = x;
        }

        // 创建频次数组，索引是数据 - min_val，槽是次数
        vector<int> count(max_val - min_val + 1, 0);
        for (int i = 0; i < nums.size(); i ++) count[nums[i] - min_val]++;

        // 遍历频次数组，将数据按顺序取出
        int index = 0;
        for (int i = 0; i < count.size(); i ++) {
            for (int j = 0; j < count[i]; j ++) { 
                nums[index++] = i + min_val;   // 数据 = 索引 + min_val
            }
        }
        return nums; 
    }
};
```

# <b>前缀和，差分</b>

前缀和：区间求和

定义s[i], s[i] = a1 + a2 ... + a[i];

递推构建前缀和数组；s[i] = s[i - 1] + a[i] 证明很简单，画图理解

区间[l, r]求和；s[l, r] = s[r] - s[l - 1] 证明也很简单，画图理解

差分：区间加法

定义d[i] = a[i] - a[i - 1];

递推构建差分数组，d[i] = a[i] - a[i - 1];

区间[l, r]加c  &lt;=&gt; d[l] += c, d[r + 1] -= c;

证明如下： 

为了满足区间[l, r]加c

对于l，a[l] += c, a[l - 1]不变 =&gt; d[i] += c;

对于[l + 1, r]，a[i] += c, a[i - 1] += c =&gt; d[i] += 0;

对于r + 1，a[r + 1]不变，a[r] += c =&gt; d[r + 1] -= c;

证明完毕！

差分的思维步骤：

1. 原数组-&gt;差分数组
2. 差分数组 操作
3. 差分数组 -&gt; 原数组

对于第一步，构建差分数组，我们也可以边读区间边构造；就是假设原数组为空，所以差分数组为空；然后原数组插入元素，就相当于差分数组[i, i] + a[i]; 我们就边做差分操作，这样也可以得到差分数组

对于第三步，我们可以优化空间，直接从差分数组原地构建原数组；

<img src="/assets/Rp6HbyfKPodDsZxyNCVc2OVXn45.png" src-width="779" src-height="480"/>

前缀和 差分的关系

s[i], a[i], d[i];

s是a的前缀和，那么a是s的差分；

d是a的差分，那么a是d的前缀和；

所以对前缀和数组s，求差分得到原数组a；对差分数组d，求前缀和得到原数组a;

技巧：

<b>为了减少边界情况的考虑，我们更习惯性地将数组下标设置为从1开始</b>

模板：

```cpp
一维前缀和
构造前缀和数组：s[i] = s[i - 1] + a[i];
区间[l, r]求和：s[l, r] = s[r] - s[l - 1];

二维前缀和
构造前缀和数组：s[i, j] = s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1] + a[i][j];
[x1,y1] - [x2,y2]区间的和：s[x2][y2] - s[x1 - 1][y2] - s[x2][y1 - 1]  + s[x1 - 1][y1 - 1];


一维差分
构造差分数组：d[i] = a[i] - a[i - 1];
区间[l,r]加c：d[l] +=c, d[r + 1] -= c;

二维差分
构造差分数组：d[i][j] = a[i][j] - a[i - 1][j] - a[i][j - 1] + a[i - 1][j - 1];
区间[x1,y1] - [x2,y2]加c：
s[x1][y1] +=c, s[x2 + 1][y1] -=c, s[x1][y2 + 1] -= c, s[x2 + 1][y2 + 1] += c;
```

<img src="/assets/EW8kbVNkoomMfxxmsS5ctvtNnbb.png" src-width="797" src-height="511"/>

 

## <b>朴素前缀和</b>

#### <b>795. 前缀和</b>

模板题 一维前缀和

AC，思路：前缀和模板题，减少边界，从1开始；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100001;
 

int n, m, l ,r;
int a[N], s[N];

int main() {
    cin  n  m;
    
    for (int i = 1; i <= n; i ++) cin >> a[i];
    
    for (int i = 1; i <= n; i ++) s[i] = s[i - 1] + a[i];
    
    while (m --) {
        cin  l  r;
        cout << s[r] - s[l - 1] << endl;
    }
    
    return 0;
}
```

#### <b>796. 子矩阵的和</b>

模板题 二维前缀和

NOT AC，思路：二维前缀和的模板还是需要反复记忆；记忆口诀 构造：异加同减，计算： 先是x2, y2， 然后y2 换成 y1 - 1 减一次，x2换成x1 - 1 减一次，最后加上x1 - 1， y1 - 1；减少边界，从（1，1）开始

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1010;

int n, m, q;
int a[N][N], s[N][N];

int main()
{
    cin >> n >> m >> q;

    for (int i = 1; i <= n; i ++ )
        for (int j = 1; j <= m; j ++ )
            cin >> a[i][j], s[i][j] = s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1] + a[i][j];

    while (q -- )
    {
        int x1, y1, x2, y2;
        cin >> x1 >> y1 >> x2 >> y2;
        cout << s[x2][y2] - s[x1 - 1][y2] - s[x2][y1 - 1] + s[x1 - 1][y1 - 1] << endl;
    }
    return 0;
}
```

#### <b>剑指 Offer II 013. 二维子矩阵的和</b>

AC，思路：就是二维前缀和模板题，但是这里是封装在类里，类的话就是要注意需要什么变量，和什么函数；然后初始化放在构造里，功能定义成函数；减少边界，从（1，1）开始

```cpp
class NumMatrix {
public:
    NumMatrix(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        
        for (int i = 1; i <= m; i ++) {
            for (int j = 1; j <= n; j ++) {
                v[i][j] = matrix[i - 1][j - 1];
                s[i][j] = s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1] + v[i][j];
            }
        }
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        row1 ++, col1 ++, row2 ++, col2 ++;
        return s[row2][col2] - s[row1 - 1][col2] - s[row2][col1 - 1] + s[row1 - 1][col1 - 1];
    }

    vector<vector<int>> v{201, vector<int>(201)};
    vector<vector<int>> s{201, vector<int>(201)};
};

/**
Your NumMatrix object will be instantiated and called as such:
NumMatrix* obj = new NumMatrix(matrix);
int param_1 = obj->sumRegion(row1,col1,row2,col2);
 */
```

#### <b>2023 美团-塔子哥抓敌人</b>

NOT AC, 思路：很明显矩阵相关的题，但是我不知道怎么用前缀和去做；题解后，首先转化题意，我们需要统计横坐标差不超过a，纵坐标差不超过b的所有矩阵里的最大个数和；所以我们可以考虑枚举所有矩阵，然后求矩阵内的个数和；然后因为求最大个数和，所以贪心的发现肯定矩阵越大越好，所以就变成枚举长a，宽b的所有矩阵，求矩阵内的个数和；枚举矩阵，技巧就是枚举右下端点；然后枚举多次，求矩阵里的个数和，这里是和，很明显二维前缀和；由于这里关注的个数，所以原矩阵统计个数，然后前缀和按模板来写，统计个数和；这是一道非常好的二位前缀和题目；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1010;

int n, a, b, x, y;
int matirx[N][N];
int s[N][N];


int main() {
    cin  n  a  b;
    while (n --) {
        cin >> x >> y;
        // 前缀矩阵关注个数，所以原矩阵统计个数;
        matirx[x][y] ++;
    }

    for (int i = 1; i < N; i ++) {
        for (int j = 1; j < N; j ++) {
            s[i][j] = s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1] + matirx[i][j];
        }
    }

    int ans = 0;
    // 枚举长a宽b的矩阵，技巧枚举右下端点;
    for (int x2 = a + 1; x2 < N; x2 ++) {
        for (int y2 = b + 1; y2 < N; y2 ++) {
            int x1 = x2 - a, y1 = y2 - b;
            int cnt = s[x2][y2] - s[x1 - 1][y2] - s[x2][y1 - 1] + s[x1 - 1][y1 - 1];
            ans = max(ans, cnt);
        }
    }

    cout << ans << endl;

    return 0;
}
```

#### <b>2023京东-塔子哥划分</b>

NOT AC, 思路：感觉也是枚举矩阵，但是之前矩阵大小可以通过贪心发现可以枚举固定矩阵，方便前缀和；现在不行了，这题比较难，回过头再看；

## 差分

#### <b>797. 差分模板题</b>

模板题 差分

AC，思路：差分模板题，主要就是运用模板；紧扣差分步骤，原数组-&gt;差分数组，差分操作，差分数组-&gt;原数组；简化边界，从1开始

构建差分数组：1. 原数组转化 2. 直接边读区间边构造；前者适合输入给原数组，后者适合输入只给区间；

1. 原数组转化

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5 + 10;

int n, m, l, r, c;
int a[N], d[N];

int main() {
    cin >> n >> m;
    
    // 原数组构建差分数组
    for (int i = 1; i <= n; i ++) cin >> a[i], d[i] = a[i] - a[i - 1];
    
    while (m --) {
        cin >> l >> r >> c;
        d[l] += c, d[r + 1] -= c;
    }
    
    memset(a, 0, sizeof(a));
    // 差分数组前缀和=>原数组
    for (int i = 1; i <= n; i ++) a[i] = a[i - 1] + d[i];
    
    for (int i = 1; i <= n; i ++) cout << a[i] << " ";
    
    return 0;
}
```

1. 边读区间边构造

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5 + 10;

int n, m, l, r, c;
int d[N];

int main() {
    cin >> n >> m;
    
    // 边读区间，边构造差分数组
    for (int i = 1; i <= n; i ++) cin >> c, d[i] += c, d[i + 1] -= c;
    
    // 差分操作
    while (m --) {
        cin >> l >> r >> c;
        d[l] += c, d[r + 1] -= c;
    }
    
    // 差分数组原地前缀和得到原数组
    for (int i = 1; i <= n; i ++) {
        d[i] += d[i - 1];
        cout << d[i] << " ";
    }

    return 0;
}
```

#### <b>LeetCode 1094. 拼车</b><b>   </b>

AC，这种题目有一个模式叫做【区间修改，单点查询】；暴力可以过，当然多次区间修改也可以用差分优化；

这里我们设置1为起点，所以涉及到现在是0，变化成1，偏移 + 1操作；

```cpp
class Solution {
public:
    bool carPooling(vector<vector<int>>& trips, int capacity) {
        int n = 1010;
        // 原数组和差分数组
        vector<int> a(n, 0);
        vector<int> d(n, 0);

        // 区间操作
        for (int i = 0; i < trips.size(); i ++) {
            int l = trips[i][1], r = trips[i][2] - 1, c = trips[i][0];
            d[l + 1] += c, d[r + 2] -= c;
        }

        // 差分数组前缀和=>原数组
        for (int i = 1; i <= 1001; i ++) {
            a[i] = a[i - 1] + d[i];
            if (a[i] > capacity) return false;
        }

        return true;
    }
};
```

#### <b>LeetCode 1109. 航班预订统计</b>

模板题 差分

AC, 思路：也是一道模板题，小技巧：对于原数组全为0的情况，差分数组也全为0；一般只定义差分数组，然后差分数组上原地构建原数组；

甚至原始数组不是全为0，我们也可以假设全为0，那么差分数组也全为0；然后模拟原数组的元素逐个插入，每插入一个元素，我们一边做差分操作，这样最后也可以构建出差分数组；

```cpp
class Solution {
public:
    vector<int> corpFlightBookings(vector<vector<int>>& bookings, int n) {
        vector<int> d(n + 2);    //1开始，最大r + 1 = n + 1, 所以空间n + 2

        for (int i = 0; i < bookings.size(); i ++) {
            int l = bookings[i][0], r = bookings[i][1], c = bookings[i][2];
            d[l] += c, d[r + 1] -= c;
        }

        vector<int> ans;
        for (int i = 1; i <= n; i ++) {
            d[i] += d[i - 1];     // 直接差分数组上构建原数组，前缀和=>累加   
            ans.push_back(d[i]);
        }

        return ans;
    }
};
```

#### <b>2023VISA-轮换字符串</b>

AC, 思路：还是一样的差分思路，注意字符的转换，取模运算注意负数；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5 + 10;

int n, m, k;
string s, ans;

int a[N], d[N];

int main() {
    cin >> n >> m;
    cin >> s;

    for (int i = 1; i <= n; i ++) {
        a[i] = s[i - 1] - 'a';
    }

    for (int i = 1; i <= n; i ++) {
        d[i] = a[i] - a[i - 1];
    }

    while (m --) {
        cin >> k;
        d[1] += 1, d[k + 1] -= 1;
    }

    memset(a, 0, sizeof(a));
    for (int i = 1; i <= n; i ++) {
        a[i] = ((a[i - 1] + d[i]) % 26 + 26) % 26;
    }

    for (int i = 1; i <= n; i ++) {
        char c = a[i] + 'a';
        ans.push_back(c);
    }

    cout << ans << endl;

    return 0;
}
```

#### <b>2023华为-塔子哥监考</b>

NOT AC, 思路：看出了时间作为区间，但是区间统计的值没有想到；收费取决于每时刻的考试数，所以区间内+1；多次区间+1， 差分操作；然后注意审题待机操作只发生在考试之间，所以需要统计起点和终点，即minl和maxr；

去除边界小技巧：1. 从1开始 2. 特判i =0 3. 不用数组，直接一个数纪录前缀和；

构建差分数组：1. 原数组转化 2. 直接边读区间边构造；前者适合输入给原数组，后者适合输入只给区间；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e6 + 10;
int n, l, r;
int d[N], a[N];

int minl = 1e6 + 1, maxr = 1;

int main() {
    cin >> n;

    while (n --) {
        cin >> l >> r;
        d[l + 1] += 1, d[r + 2] -= 1;
        minl = min(minl, l + 1), maxr = max(maxr, r + 1);
    }

    for (int i = minl; i <= maxr; i ++) {
        a[i] = a[i - 1] + d[i];
    }
    int cost = 0;
    for (int i = minl; i <= maxr; i ++) {
        if (a[i] == 0) cost +=1;
        else if (a[i] == 1) cost += 3;
        else if (a[i] >= 2) cost += 4;
    }

    cout << cost;

    return 0;
}
```

#### 
## <b>前后缀分解</b>

场景：

枚举多次，求前面区间的某种性质 前缀优化 

枚举多次，求后面区间的某种性质 后缀优化 

区间性质常见的有max，min，sum，frequency等 

本质上就是通过预处理的操作，把每一次操作降到O(1)

方法：

预处理前缀数组，后缀数组，枚举，通过前后缀数组快速求出性质

技巧：

对于前后缀分解的题目，如果采取前后缀数组的写法，要注意两点；1. 数组从几开始；2. 数组[i]代表什么；

这里统一写法，前缀，后缀，原数组都当作从1开始，[1, n]；pre[i]: [1, i]的前缀积，suf[i]：[i, n]的前缀积；这样可以避免很多边界情况，初始化也会比较简单，更适配ACM模式；

#### <b>LeetCode 238. 除自身以外数组的乘积</b>

> 模板题, leetcode hot100

AC, 思路：题目很简单，就是枚举i，然后计算前面区间的积，和后面区间的积；因为多次计算，利用前缀数组和后缀数组统计前缀积和后缀积；这里给出两种写法

1. 前后缀数组

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> pre(n + 1), suf(n + 2);
        // pre[i] [1, i]  suf[i] [i, n]
        pre[0] = 1;
        for (int i = 1; i <= n; i ++) pre[i] = pre[i - 1] * nums[i - 1];
        
        suf[n + 1] = 1;
        for (int i = n; i >= 1; i --) suf[i] = suf[i + 1] * nums[i - 1];

        vector<int> ans(n);
        // 原本遍历[0, n - 1]，改为1开始，遍历[1,n]
        for (int i = 1; i <= n; i ++) {
            ans[i - 1] = pre[i - 1] * suf[i + 1];
        }

        return ans;
    }
};
```

1. 空间O(1)优化

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(n);

        int pre = 1; //初始pre i = 0时 pre = 左侧乘积 = 1
        for (int i = 0; i < n; i ++ ) {
            ans[i] = pre;
            pre = pre * nums[i];
        }

        int suf = 1; //初始suff i = n - 1时 suf = 右侧乘积 = 1
        for (int i = n - 1; i >= 0; i --) {
            ans[i] *= suf;
            suf = suf * nums[i];
        }

        return ans;
    }
};
```

#### <b>LeetCode 2483. 商店的最少代价</b><b> </b>

AC, 思路：就是枚举i，然后计算的前面区间N的个数，和后面区间Y的个数；因为多次计算，利用前缀数组和后缀数组统计；

然后注意两个易错点；1. ==优先级很低，所以一般要加括号 2. 时刻注意最后枚举什么区间；前后缀分解里蛙佬的模板很好，可以参照它的；

```cpp
class Solution {
public:
    int bestClosingTime(string customers) {
        int n = customers.size();
        // 枚举j，前面区间[...j - 1]找N的个数，后面区间[j ...]找Y的个数;
        
        // pre[i] [1, i] N的个数  suf[i] [i, n]里Y的个数;
        vector<int> pre(n + 1), suf(n + 2);
        for (int i = 1; i <= n; i ++) pre[i] = pre[i - 1] + (customers[i - 1] == 'N' ? 1 : 0);
        for (int i = n; i >= 1; i --) suf[i] = suf[i + 1] + (customers[i - 1] == 'Y' ? 1 : 0);

        int min_cost = 1e9, ans = 0;
        // 原本遍历[0, n]，改为1开始后，遍历[1, n + 1];
        for (int j = 1; j <= n + 1; j ++) {
            int cost = pre[j - 1] + suf[j];
            if (cost < min_cost) {
                ans = j - 1;
                min_cost = cost;
            }
        }

        return ans;
    }
};
```

## <b>前缀和 + 哈希表</b>

针对满足条件的子串/子数组个数这类问题

举例子：

和为target的子数组数目

我们其实就是求满足s[i] - s[j - 1] = target (1&lt;= j &lt;= i) 的i，j对数目

那么我们就枚举i，然后找满足的j的个数，其实就是找s[j] = s[i] - target  (0 &lt;= j &lt;= i - 1]的数目，最后就是找所有前缀和(s[0], s[1] ... s[i - 1]) 里前缀和 = s[i] - target的数目

最终就是，枚举i，找i前面的前缀和里 = s[i] - target的数目 =&gt; 枚举i，找i前面的前缀和s[i] - target的出现次数

为了快速找到前缀和s[i] - target的出现次数，我们可以使用一个哈希表来维护 i前面的前缀和的出现次数数组，从而快速找到对应的前缀和的出现次数

注意初始情况下，i = 0，前面为空，存在前缀和为0，所以hash[0] = 1;

#### <b>LeetCode 930. 和相同的二元子数组</b>

> 模板题

AC，模板题，主要就是把问题转化为，枚举i，找i前面的前缀和s[i] - goal的出现次数；

```cpp
class Solution {
public:
    int numSubarraysWithSum(vector<int>& nums, int goal) {
        int n = nums.size();
        vector<int> s(n + 1);
        for (int i = 1; i <= n; i ++) s[i] = s[i - 1] + nums[i - 1];
        
        unordered_map<int, int> hash;   //哈希表维护 i前面的前缀和出现次数
        int ans = 0;

        hash[0] = 1;   //初始 i = 0, 前面存在前缀和 = 0

        for (int i = 1; i <= n; i ++) {
            int t = s[i] - goal;  // 要找的前缀和
            ans += hash[t];      // 哈希表查到该前缀和的出现次数
            hash[s[i]]++;        // 更新哈希表
        }

        return ans;
    }
};
```

#### <b>LeetCode 560.和为 k 的子数组</b>

> Leetcode hot100

AC, 就是上面那道题，换了个数字而已；

```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int n = nums.size();

        vector<int> s(n + 1, 0);
        for (int i = 1; i <= n; i ++) s[i] = s[i - 1] + nums[i - 1];

        unordered_map<int, int> hash;
        hash[0] = 1;

        int ans = 0;
        for (int i = 1; i <= n; i ++) {
            int t = s[i] - k;
            ans += hash[t];
            hash[s[i]] ++;
        }

        return ans;
    }
};
```

#### <b>LeetCode 974. 和可被 K 整除的子数组</b>

NOT AC, 思路：首先也是枚举i  找所有以i为右端点的区间里，区间和被k整除的数目；=&gt; （s[i] - s[j - 1]) 被k整除(1 &lt;= j &lt;= i)    =&gt;   (s[i] - s[j'] ）被k整除 (0 &lt;= j' &lt;= i - 1)   =&gt;  s[i] 和s[j'] 同余k （0 &lt;= j'  &lt;= i - 1)；所以就是找 所有的前缀和模(s[0] % k, s[1] % k ... s[i - 1] % k) 里 前缀和模 = s[i] % k的数目 ，我们可以利用哈希表记录前缀和模，然后统计次数；注意，初始情况下s[0] % k = 0，放入哈希表里，hash[0] ++;

注意C++ mod可能为负数，所以a % k 要写成 (a % k + k) % k;

```cpp
class Solution {
public:
    int subarraysDivByK(vector<int& nums, int k) {
        int n = nums.size();
        vector<int s(n + 1);
        for (int i = 1; i <= n; i ++) s[i] = s[i - 1] + nums[i - 1];
        
        int res = 0;
        unordered_map<int, int hash; //key: 前缀和mod，value：次数
        hash[0]++;

        for (int i = 1; i <= n; i ++) {
            int t = (s[i] % k + k) % k;
            res += hash[t];
            hash[t] ++;
        } 

        return res;
    }
};
```

#### <b>LeetCode 1590. 使数组和能被 P 整除</b>

NOT AC，思路：很难的一道题目；这里涉及到一些数学推导 最后发现 还是前缀和 + 哈希表解决；具体推导在代码里；

```cpp
class Solution {
public:
    int minSubarray(vector<int>& nums, int p) {
        int n = nums.size();
        long long x = accumulate(nums.begin(), nums.end(), 0LL);
        if (x % p == 0) return 0;   //注意空

        vector<long long> s(n + 1);
        for (int i = 1; i <= n; i ++) s[i] = s[i - 1] + nums[i - 1];
        // x - sum[j, i] 被k整除 => sum[j, i] 和 x 同余k => s[i] - s[j - 1] 和 x 同余k （1 <= j <= i)
        // => s[i] - s[j'] 和 x 同余k (0 <= j' <= i - 1) => (s[i] - s[j']) % k = x % k 
        // => s[j'] 和 s[i] - x 同余k => s[j'] % k = (s[i] - x) % k; (0 <= j' <= i - 1)
        // 初始化 s[0] % k = 0, 所以 hash[0] = 0; val = index = j' = j - 1; len = i - j'
        unordered_map<int, int> hash;   
        hash[0] = 0;

        int res = n;
        for (int i = 1; i <= n; i ++) {
            int t = ((s[i] - x) % p + p) % p;
            if (hash.count(t)) {
                res = min(res, i - hash[t]);
            }
            hash[((s[i] % p) + p) % p] = i;
        }

        return res == n ? -1 : res;
    }
};
```

#### <b>2023阿里-切割环形数组</b>

NOT AC, 思路：首先要思考环形切割，本质就是找一段子数组和 = 剩余子数组和 = &gt; 找子数组和 = sum / 2；其中sum是奇数肯定找不到直接返回0；然后找子数组和 = sum/2的数目；前缀和 + 哈希表模板；然后注意之前要把s0放进前缀和数组，代表考虑子数组和 = 前缀和的方案，也就是考虑所有前缀子数组；但是这里是分割两次，如果分割完后 所有的前缀子数组 还是原来的前缀子数组，说明重复分割相同的位置，所以我们这里不考虑，把s[0]去掉；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e5 + 10;

int n;
long long a[N], s[N];


int main() {
    cin >> n;
    for (int i = 1; i <= n; i ++) cin >> a[i];

    for (int i = 1; i <= n; i ++) s[i] = s[i - 1] + a[i];
    long long x = s[n];
    if (x % 2 != 0) {
        cout << 0 << endl;
    }
    else {
        x /= 2;
        unordered_map<long long, int> hash;
        long long res = 0;

        // hash[0] ++;   //防止分割线重合
        for (int i = 1; i <= n; i ++) {
            int target = s[i] - x;
            res += hash[target];
            hash[s[i]]++;
        }
        cout << res;
    }

    
    return 0;
}
```

# <b>二分查找</b>

## 
二分是一种高效查找算法，二分问题常分为整数二分，实数二分，二分答案；

## <b>整数二分</b>

场景：

区间内有一条分界线，左边满足某种性质，右边满足性质，两性质互斥（二段性：满足/不满足 or 一定不满足/不一定满足），我们去找这一条分界线（的左边界或右边界）

区间：...l|r...    l是左段边界（左边界），r是右段边界（右边界）

方法：

红蓝染色法 // 透彻理解二分，包含无解

分界线法  // 易懂易写，包含无解

主要弄懂红蓝染色法，弄懂了以后基本可以写出所有的二分变种，然后了解一下分界线法，方便平时讲解

1. 红蓝染色法：

搜索区间，确定所有元素的颜色，同时找到分界线的左右边界；

做法是 在区间不断取mid，看mid满足左侧还是右侧（满足左侧，mid及其左侧都确定（染红色），更新左边界；满足右侧，mid及其右侧都确定（染蓝色），更新右边界)，所以每次确定一半元素的颜色（缩小一半的搜索空间），最后区间为空时退出循环，确定了所有元素的颜色，找到左右边界

区间定义和循环不变量：区间内部为查询空间（未确定），区间左侧满足左侧性质（红色，确定）区间左侧第一个位置左边界，区间右侧满足右侧性质（蓝色，确定）区间右侧第一个位置有边界；更新的时候，mid及其一侧已经确定，所以更新后的区间不能有mid =&gt; 左边界or右边界更新成mid（因为左右边界一定不在区间内部）

左闭右闭[l, r]，实际范围是[l, r]，搜索[0, n - 1]，初始区间l = 0, r = n - 1;

左边界l - 1满足左侧性质, 右边界r + 1满足右侧性质；边界更新成mid；返回左右边界

左闭右开[l, r)，实际范围[l, r - 1]，搜索[0, n - 1]，初始区间l = 0, r = n（r - 1 = n - 1）; 

左边界l - 1满足左侧性质, 右边界r满足右侧性质；边界更新成mid；返回左右边界

左开右闭(l, r]，实际范围[l + 1, r]，搜索[0, n - 1]，初始区间l = -1（l + 1= 0）, r = n - 1;

左边界l满足左侧性质, 右边界r + 1满足右侧性质；边界更新成mid；返回左右边界

左开右开(l, r)，实际范围[l + 1, r - 1]，初始区间l = -1, r = n（l + 1 = 0, r - 1 = n - 1);

左边界l满足左侧性质, 右边界r满足右侧性质；边界更新成mid；返回左右边界

注意：

(1) 求左右边界时，有可能无解；

求左边界无解，左边界一直不更新，l不变；

求右边界无解，右边界一直不更新，r不变

(2) 除了左闭右闭的其他写法，mid的取值有可能会导致死循环

左闭右闭的左右边界是 l - 1和 r + 1；更新的时候，无论mid怎么取值，边界都会变化；

但是其他的写法里，

例如左闭右开区间里右边界是r，如果此时mid上取整可能取到r，然后又是更新右边界，就会造成r = r，死循环；同理左开右闭区间里左边界是l，如果此时mid下取整可能取到l，然后又是更新左边界，就会曹成l = l，死循环；左开右开上取整和下取整都有可能造成死循环；

所以如果使用红蓝染色法的话，使用左闭右闭区间会方便很多；

1. 分界线法 （左开右开写法的另一种直观解释）

搜索区间，找分界线，循环不断取mid，看mid满足左侧还是右侧（满足左侧，分界线在mid右侧，更新l = mid；满足右侧，分界线在mid左侧，更新r = mid)

所以每次缩小一半的搜索空间，l + 1 = r时确定分界线，退出循环，找到分界线(分界线的左右边界）

区间定义和循环不变量：分界线在l，r之间，分界线左边满足左侧性质，分界线右边满足右侧性质

求左右边界时，有可能无解，求左边界无解，l不变；求右边界无解，r不变

模板：

```cpp
模板题 
lc_34. 在排序数组中查找元素的第一个和最后一个位置

首先确定求什么
1. >= x的第一个数  < x | >= x  求>=x的右边界
2. <=x的最后一个数 <= x | > x  求<=x的左边界

假设区间是[0, n - 1]

- 红蓝染色法：1. 左闭右闭 2.左闭右开 3. 左开右闭 4. 左开右开
初始区间 l = xxx, r = xxx;
while (区间不为空) {
    if (mid满足左侧) update l
    else update r
}
return 左右边界 //根据要求确定求左or右边界，根据循环不变量确定具体左右边界是什么

- 分界线法：实际是就是左开右开
初始区间 l = -1, r = n
while (l + 1 < r) {
    if (mid满足左侧) l = mid;
    else r = mid;
}
return 左右边界 //根据要求确定求左or有边界，左边界是l，右边界是r


- 注意事项
1. 因为库函数的lower_bound 和 upper_bound 都是找右边界
求左边界的话 可以直接求（该返回值即可），或者通过右边界转化
转化规则：
>= x lower_bound
> x upper_bound --- >= x + 1
< x --- (<= x) - 1
<= x --- (> x) - 1 --- (>= x + 1) - 1

2. 求左右边界，都可能无解
求左边界无解，l不变；求右边界无解，r不变
注意左开右闭写法，mid不能下取整；如果只剩一个元素，更新l和r都不会变化，死循环；mid上去整的话可以避免

3. mid = (l + r) / 2 有可能溢出 所以写成 mid = l + (r - l) / 2
*/
```

技巧：

二分找某一段的边界的时候，情况是有解无解；

二分找某一段的边界和target的关系的时候，情况是无解，有解=target，有解!=target

二分找某一段的边界的时候，最好是设计成该段一定存在，这样的话一定有解，得到的结果不会越界，会省略很多边界判断；

旋转数组相关题目：

旋转数组题目的核心思路就是 要找到前后两段区间，所以我们可以去找前段的终点，或者后段的起点

找前段的终点：最好设计成前段一定存在 所以 &gt;= nums[0] | &lt; nums[0] 找左边界；因为nums[0]一定存在，所以前段的终点一定有解；现在我们就可以得到前后两段的区间了，再根据题目要求继续做

找后段的起点：最好设计成后段一定存在 所以 &gt;nums[n - 1] | &gt;= nums[n - 1]; 因为nums[n - 1]一定存在，所以后段的起点一定有解；现在我们就可以得到前后两段的区间了，再根据题目要求继续做

#### <b>LeetCode 34. 在排序数组中查找元素的第一个和最后一个位置</b>

> 模板题

AC，思路：二分模板题，这里放一个左开右开和一个左闭右闭的写法

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int n = nums.size();
        // <x | >=x 右边界 and  <=x | >x 左边界

        // 左开右开（l, r） 左右边界l，r
        vector<int> ans;
        int l = -1, r = n;
        while (l + 1 < r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] >= target) r = mid;
            else l = mid;
        }

        if (r == n || nums[r] != target) return {-1, -1};
        else ans.push_back(r);

        l = -1, r = n;
        while (l + 1 < r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] <= target) l = mid;
            else r = mid;
        }

        if (l == -1 || nums[l] != target) return {-1, -1};
        else ans.push_back(l);

        return ans;
    }
};
```

左闭右闭：

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int n = nums.size();
        // <x | >=x 右边界 and  <=x | >x 左边界

        // 左闭右闭 [l, r] 左右边界l - 1，r + 1
        vector<int> ans;
        int l = 0, r = n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] >= target) r = mid - 1;
            else l = mid + 1;
        }

        if (r == n - 1 || nums[r + 1] != target) return {-1, -1};
        else ans.push_back(r + 1);

        l = 0, r = n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] <= target) l = mid + 1;
            else r = mid - 1;
        }

        if (l == 0 || nums[l - 1] != target) return {-1, -1};
        else ans.push_back(l - 1);

        return ans;
    }
};
```

#### [LeetCode 153. 寻找旋转排序数组中的最小值](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/)

> 模板题

AC，思路，整数二分，&gt; nums[end] | &lt;= nums[end]  右边界；这里也是给出左开右开，左闭右闭两种解法

左开右开：

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int n = nums.size();

        // > nums[end] | <= nums[end]  右边界
        // 左开右开 （l,r) l r
        int l = -1, r = n;
        while (l + 1 < r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] <= nums[n - 1]) r = mid;
            else l = mid;
        }
        
        // 考虑直接升序序列的情况，综合选出最小值
        return min(nums[r], nums[0]);
    }
};
```

左闭右闭：

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int n = nums.size();

        // > nums[end] | <= nums[end]  右边界
        // 左闭右闭 [l,r] l - 1 r + 1
        int l = 0, r = n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] <= nums[n - 1]) r = mid - 1;
            else l = mid + 1;
        }
        
        // 考虑直接升序序列的情况，综合选出最小值
        return min(nums[r + 1], nums[0]);
    }
};
```

#### [240. 搜索二维矩阵 II](https://leetcode.cn/problems/search-a-2d-matrix-ii/)

> Leetcode hot100

AC，思路：首先最简单肯定是暴力遍历，时间复杂度O(m * n)；考虑到每列和每行有序，可以对每列或者每行二分；最后介绍小众的z形变换

暴力

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n = matrix[0].size();
        for (int i = 0; i < m; i ++)
            for (int j = 0; j < n; j ++) {
                if (matrix[i][j] == target) return true;
            }
        return false;
    }
};
```

二分

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        for (const auto& row: matrix) {
            auto it = lower_bound(row.begin(), row.end(), target);
            if (it != row.end() && *it == target) {
                return true;
            }
        }
        return false;
    }
};
```

z形变换：todo

#### 
## 实数二分

直接左闭右闭写法，然后因为这里是实数二分，左右边界无限逼近，所以是l，r

然后循环可以两种写法

1. esp写法 while(l + esp &lt; r)
2. 固定次数循环 1000次

模板：

```cpp
模板题
lc_69. x 的平方根


- 设置esp法
double eps = 1e-(k + 2);   // eps 表示精度，一般多取两位，k为保留位数
while (l + eps < r)
{
    double mid = (l + r) / 2;
    if (check(mid)) r = mid;
    else l = mid;
}

- 规定循环次数法
for (int i = 0; i < 100; i++) {
    double mid = (l + r) / 2;
    if (check(mid)) r = mid; 
    else l = mid;        
}
*/
```

#### [LeetCode 69. x 的平方根 ](https://leetcode.cn/problems/sqrtx/)

模板题 实数二分

AC，思路，实数二分， 答案平方 &lt; x | 答案平方 &gt;= x 的有边界，这里给出两种写法，esp法和固定循环次数法

esp法

```cpp
class Solution {
public:
    int mySqrt(int x) {
        double esp = 1e-6;
        double l = 0, r = x;
        while (l + esp < r) {
            double mid = l + (r - l) / 2;
            if (mid * mid >= x) r = mid;
            else l = mid;
        }
        return (int)r;
    }
};
```

固定循环次数法

```cpp
class Solution {
public:
    int mySqrt(int x) {
        double l = 0, r = x;
        for (int i = 0; i < 1000; i ++) {
            double mid = l + (r - l) / 2;
            if (mid * mid >= x) r = mid;
            else l = mid;
        }
        return (int)r;
    }
};
```

## <b>二分答案  </b>

二分答案的本质是最优化问题 转化为 判定问题

首先对于一个最优化问题，我们可以直接求解，也可以枚举答案空间 + 判定答案是否合法（是否满足条件）

那么当解空间基于合法情况（条件），具有单调性的时候，

我们就可以利用二分代替枚举，利用二分答案空间 + 判定 求解，这就是二分答案

方法：

那么关于二分答案，思考步骤如下：

1. 答案是什么，看题目要求，其实就是自己猜测的值
2. 条件是什么，来自于题目的限制，通常是一个不等式，这样解空间才能基于条件（合法情况)具有单调性（简称二段性）
3. 思考答案与条件之间的单调性，如果有就图像化（01分段函数），二分答案求解
4. 返回答案，可能是左边界，也可能是右边界，根据（是/否满足条件）的（最大/最小值）来判断；

技巧：

条件是一个判定问题，一般单独写一个check函数

二分答案一般使用左闭右闭，初始化会更直观一些

最大化最小值，最小化最大值，这种字眼可以尝试二分答案；

最大化最小值：答案是最小值，条件是最大化的限制

最小化最大值：答案是最大值，条件是最小化的限制    

二分答案最经典的例子：

猜数字

1. 答案：数值x （猜一个数）
2. 条件：x &gt;= target
3. x越大，x &gt;= target越满足，找到单调性，0|1，二分答案求解
4. 求&gt;=target的最小值，返回右边界

#### [LeetCode 875. 爱吃香蕉的珂珂](https://leetcode.cn/problems/koko-eating-bananas/)

模板题 二分答案

AC，思路：求满足h小时吃完的最小速度k；我们尝试二分答案，答案 速度k，条件h小时内吃饭；速度k越大，条件越容易满足；所以 0 | 1，可以二分答案；然后这里注意k = 0时的特判，同时还有total数据可能会溢出，要用long long；这里也给出左闭右闭，左开右开两种写法

左闭右闭

```cpp
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        // 答案 速度k，条件 h小时内吃完
        // k越大，条件越满足 发现单调性 0|1

        function<bool(int)> check = [&](int k) -> bool{
            if (k == 0) return false;
            long long total = 0;
            for (int i = 0; i < piles.size(); i ++) {
                int t = (piles[i] + k - 1) / k;
                total += t;
            }
            if (total <= h) return true;
            else return false;
        };

        int l = 0, r = 1e9;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (check(mid)) r = mid - 1;
            else l = mid + 1;
        }

        return r + 1;
    }
};
```

左开右开

```cpp
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        // 答案 速度k，条件 h小时内吃完
        // k越大，条件越满足 发现单调性 0|1

        auto check = [&](int k) -> bool{
            if (k == 0) return false;
            long long total = 0;
            for (int i = 0; i < piles.size(); i ++) {
                int t = (piles[i] + k - 1) / k;
                total += t;
            }
            if (total <= h) return true;
            else return false;
        };

        int l = -1, r = 1e9 + 1;
        while (l + 1 < r) {
            int mid = l + (r - l) / 2;
            if (check(mid)) r = mid;
            else l = mid;
        }

        return r;
    }
};
```

#### <b>2023美团-分糖果</b>

NOT AC，一道很经典的二分答案题，最大化最小值；答案是最小值，条件是最大化

答案：最少糖果x =&gt; 糖果最小值x

条件：所有小朋友的糖果最小值是否&lt;= x; 转化一下就是，糖果最小值为x时，是否分够所有小朋友；

单调性：我们发现糖果最小值越大，越不能分够；满足单调性，1|0，

二分答案：二分的答案就是mid（糖果最小值）；一般二分答案为了区间判定方便，我比较喜欢用左闭右闭写法；

```cpp
#include <iostream>

using namespace std;

int t, n, a, b;

// 所有小朋友糖果数最小值 <= t ==> 糖果最小值为t时，能否分够所有小朋友
bool check(int t) {
    return a / t + b / t >= n;
}

int main() {
    cin >> t;

    while (t --) {
        cin >> n >> a >> b;

        int l = 1, r = max(a, b);
        while (l <= r) {
            int mid = l + (r - l) / 2;
            // 1 | 0
            if (check(mid)) l = mid + 1;
            else r = mid - 1; 
        }
        cout << l - 1 << endl; 
    }
    return 0;
}
```

# <b>搜索和图</b>

搜索和图交集比较多，所以我们这里把他们归在同一个专题里；

<b>搜索定义：</b>

搜索搜的是什么？搜索状态空间或者是图；

搜索是一类算法：通过搜索 状态空间/图 寻找答案



<b>搜索和图论的关系：</b>

搜索和图论是交集关系：

1. 搜索 会用于图的遍历，但图论除了遍历还有很多其他的算法，例如最短路，最小生成树
2. 图论 遍历只用搜索算法里的DFS，BFS，但搜索还有很多其他的搜索算法，例如A*，迭代加深等

> 点，状态，问题其实是一个集合，里面有很多信息，但是我们一般只关注有用的信息，如位置，已搜路径等等，其中我们在画图/状态图时，一般都以位置作为图上节点/状态的代表信息；


抽象对应关系：
图(点的集合)                         点 ----------边 ---------图 点的代表信息 位置，核心信息 已搜路径
状态空间(状态图,状态集合)     状态--------决策 --------状态空间 状态的代表信息 位置，核心信息 已搜路径
问题集合(问题图,问题的集合)  问题--------扩大缩小------问题集合 问题的代表信息 位置，核心信息 已搜路径

所以我们发现，搜索关键在于，点/状态/问题的 位置和已搜路径，位置决定搜索顺序，已搜路径决定边界


思想总结

1. 求解问题，经常分为很多个阶段，那么对于每个阶段，会求解不同的问题，可以是原问题，子问题，问题边界 （这些都是状态，通常初始状态是问题边界，最终状态是原问题)
2. 状态空间就是隐式图，从上面的表可以看出，把状态作为点，如果一个状态可以达到另一个状态，就连一条边，这样就把整个状态空间抽象为了一张有向图，对问题的求解就是对这张图的遍历
3. np问题的求解，就是遍历状态空间（图），根据遍历方式不同，可分为不同的搜索算法<b>，</b>注意的是，状态空间是非树图的时候，需要判重，因为树无环，不会重复遍历，而非树图有可能有环 


<b>搜索解题步骤： </b>

1. 搜索方式：按什么搜索，每一步选择是什么，选择后的结果是什么，脑海里构建搜索图 （eg: 按坐标搜索，每一步上下左右，选择后得到当前路径） 
2. 定义状态：状态最初始就是程序维护的所有动态数据构成的集合
但我们只关注有用的状态信息得到搜索的状态   这一步很关键，介绍 状态定义 的几种常用方法
1- 模拟搜索流程，提取每步之间的有用变化信息，得到状态
2- 关注轮廓变化（轮廓就是已处理和未处理部分的分界线，可以关注已处理部分变化，或者未处理部分变化），提取有用变化信息，得到状态
    3-直接分析状态需要哪些信息，一般有 搜索顺序，选择范围，结果，操作信息汇总在一起得到状态
这三种任选一种分析即可（个人的话喜欢第三种）

3. 搜索框架：

     对于DFS，选择一部分状态放入DFS参数 （集合类的状态信息可以全局共享维护，节省空间，选择如果是决策       选or不选，就不存在选择范围了）
     对于BFS，状态用队列保存

<b>递推，递归，回溯，DFS，分治：</b>

首先我们来探讨多个概念，递推，递归，回溯，DFS，分治
递推：以问题边界出发，根据推导路线正向推导，达到原问题  （例如阶乘 n！推导路线是确定的）

递归：有些时候推导路线不确定，那么就从原问题出发，不断缩减成更小的子问题，达到问题边界，之后通过路线反向回溯，达到原问题<b> </b>(例如树的信息，从根节点往下看不确定路径）

回溯：回溯又分回溯过程和回溯算法
- 回溯过程：从递归的定义可以看到，到达边界后需要反向回溯到原问题，这个过程，就是回溯过程, 所以递归包含回溯过程，回溯过程就是递归的“归”
- 回溯算法：穷举所有的解，然后遇到不合法的不再向下搜索，转而搜索另一条链；就是暴搜，一般使用DFS实现

DFS：搜索的时候，一直往下搜索，到达最终节点后，返回上一个节点继续搜索，直到搜完所有的节点，一般利用递归函数实现搜索

分治：将原问题划分成若干个子问题，分别求解后，合并子问题的结果得到原问题的结果<b> </b>（一般来说每次划分是两个子问题，否则时间复杂度会过高）

<b>建图模板</b>

建图的模板五花八门，ACM模式和leetcode模式下有些区别；

<b>ACM模式</b>

这里主要参考代码源的模板为主，然后同时也看了一些其他的资料，在此列出

1. [笔试刷题指南](CAbedNJ5KobvinxdyKgcKsrlnrd)
2. [oi-wiki.org](https://oi-wiki.org/graph/save/)
3. [邻接表模板（算法竞赛进阶指南）](https://www.acwing.com/blog/content/4689/)

建图主要就是邻接矩阵和邻接表

邻接矩阵：

```cpp
int n, m;                    // n点数 m边数
int g[N + 1][N + 1];         // N最大点数 M最大边数

for (int i = 1; i <= m; i ++) {
    int x, y;
    cin >> x >> y;
    g[x][y] = g[y][x] = 1;   //无向简单图
    g[x][y]++, g[y][x]++;    //无向非简单图
    g[x][y] = 1;             //有向简单图
    g[x][y]++;               //有向非简单图
    g[x][y] = z;             //带边权的图
}
```

邻接表:

邻接表建图，注意三种输入，不带权值，带边权，带点权

不带权值

```cpp
int n, m;                    // n点数 m边数
vector<int> g[N + 1];     // N最大点数 M最大边数

for (int i = 1; i <= m; i ++) {
    int x, y;
    cin >> x >> y;
    
    // 无向图
    g[x].push_back(y);
    g[y].push_back(x);
    
    // 有向图
    g[x].push_back(y);
}
```

带边权

```cpp
#include<bits/stdc++.h>

using namespace std;

typedef pair<int,int> pii;
vector<pii> g[N + 1];

int n, m;

int main() {
    cin >> n >> m;
    for(int i = 1; i <= m; i ++){
        int x, y, z;
        cin >> x >> y >> z;
        
        // 无向图
        g[x].push_back({y, z});
        g[y].push_back({x, z});
        
        // 有向图
        g[x].push_back({y, z});
    }
    return 0;
}
```

带点权

```cpp
#include<bits/stdc++.h>

using namespace std;

vector<int> g[N + 1];
int w[N + 1];    // 点权

int n, m;

int main() {
    cin >> n >> m;
    for(int i = 1; i <= m; i ++){
        int x, y;
        cin >> x >> y;
        
        // 无向图
        g[x].push_back(y);
        g[y].push_back(x);
        
        // 有向图
        g[x].push_back(y);
    }
    
    for(int i = 1; i <= n; i ++) cin >> w[i];
    
    return 0;
}
```

<b>leetcode模式</b>

leetcode模式下的建图模板，我们参照[2316. 统计无向图中无法互相到达点对数](https://leetcode.cn/problems/count-unreachable-pairs-of-nodes-in-an-undirected-graph/)这道题的灵神题解和ylb题解提供的模板即可，其实跟之前ACM模式的模板基本一致；

输入，直接是传入了边数组，然后读边数组，建图；

## <b>暴搜/回溯 - DFS</b>

介绍：

暴搜/回溯 暴力枚举所有情况，找到满足条件的所有解/最优解/方案数

一般使用DFS实现，从DFS角度来说：枚举所有情况其实就是枚举所有搜索路径，一般会关注满足条件的 所有路径/最优路径/路径数量

场景：

统计所有的解，统计所有解里的最优解/方案数

DFS暴搜步骤：

(1) 思考搜索方式：

按什么搜索（eg: 位，行，列） -&gt; 决策是什么（eg: 选不选 or 选哪个）-&gt; 结果是什么(eg: 路径，集合）

(2) 思考DFS状态：DFS函数的意义一般是 当前位置xxx，已搜xxx；我们会关注当前DFS的一些信息，这些信息构成了DFS状态；DFS关注信息 = DFS状态

DFS状态一般有 搜索位置，选择范围，结果，操作信息（如果选择是选不选，就不存在选择范围了，操作信息 eg:分割字符串需要起点）

DFS状态里，方便用栈维护的信息放入DFS函数参数，其余的可以全局维护减少栈内存的消耗 (集合类性质的信息，不用栈维护，全局维护比较方便)

(3) 确定答案：答案包含DFS哪些层的结果，具体题目具体分析，一般是最后一层，有的时候也可能是所有层

DFS暴搜和状态空间/图的关系：

DFS暴搜实际上就是维护了一棵搜索树（特殊的图），搜索树上的每个节点其实就是一个DFS状态，状态包括当前位置，结果，已搜路径等信息，为了更直观的画这棵搜索树，一般节点上只画出结果；

DFS状态中的结果取决于已搜路径，所以一般命名为path；

回溯时恢复现场的问题：

如果信息在DFS函数参数里，信息在每个DFS函数中是独立的，不需要恢复现场；如果是信息是全局维护的，那么可能多个DFS函数共用，所以此时回溯到上一个DFS函数的时候需要将信息恢复现场；

DFS边界问题：

DFS函数的意义是 当前位置xxx，已搜xxx； DFS的边界跟已搜路径有关

DFS初始状态不同，最后的边界也不同

例如[1, n]子集问题

如果初始状态是 1 已搜[]，最后边界是 n + 1, 已搜[1, n];

如果初始状态是 1 已搜[1], 最后边界是 n，已搜[1, n]; 

判断答案的代码最好写在边界前，否则最后一层无法判断答案；

常见回溯问题分类：

回溯/暴搜 分为子集型回溯，组合型回溯，排列型回溯

子集型回溯：每个元素都可以选or不选  时间复杂度O(2^n) 

延申出 指数型回溯 更泛化的子集型回溯  时间复杂度O(k^n)

组合型回溯：n个数选k个数的组合 时间复杂度O(C(n, k))

看作长度固定的子集 

子集型回溯 剪枝 得到

剪枝1：已选 &gt; 已选所需

剪枝2：剩余 &lt; 剩余所需

拿个数剪枝举例

剪枝1：已选个数（cnt）&gt; 已选所需（k)

剪枝2：剩余个数（n - i + 1) &lt; 剩余所需（k - cnt);

排列型回溯：n个数排列，时间复杂度O(n!)

排列型回溯 只能答案视角搜索

元素选择后，不能再选，记录访问情况

模板：

```cpp
不方便栈维护的状态信息，全局维护

返回值 dfs(状态信息作为参数) {
    // 剪枝代码
    
    // 构造答案
    
    // 递归边界
    
    // 非边界代码
}
```

#### [LeetCode 78. 子集](https://leetcode.cn/problems/subsets/)

模板题 暴搜

AC，思路：子集暴搜，DFS来做；输入没有重复 

可以按输入搜索，也可以按答案搜索，这里给出两种方式的代码；

子集型回溯一般还是按输入每位搜索比较直观一些

按输入每位搜索，决策是选or不选，答案是最后一层的结果

```cpp
class Solution {
public:
    // 维护的全局变量
    vector<vector<int>> ans;
    vector<int> path;
    int n;
    vector<int> nums;

    vector<vector<int>> subsets(vector<int>& _nums) {
        nums = _nums;
        n = nums.size();
        dfs(0);
        return ans;
    }

    // 按输入每位搜，决策是选or不选
    void dfs(int i) {
        // ans包含最后一层的结果
        if (i == n) ans.push_back(path);

        // 递归边界
        if (i == n) return;

        // 选
        path.push_back(nums[i]);
        dfs(i + 1);
        path.pop_back();

        // 不选
        dfs(i + 1);
    }
};
```

按答案每位搜，决策是选哪个，答案包含所有层的结果

```cpp
class Solution {
public:
    // 维护的全局变量
    vector<vector<int>> ans;
    vector<int> path;
    int n;
    vector<int> nums;

    vector<vector<int>> subsets(vector<int>& _nums) {
        nums = _nums;
        n = nums.size();
        dfs(0, 0);
        return ans;
    }

    // 按答案每位搜，决策是选哪个
    void dfs(int i, int start) {   // 状态加上操作信息，选择头
        // ans包含所有层的结果
        ans.push_back(path);

        // 递归边界
        if (i > n - 1 && start > n - 1) return;

        // 选哪个
        for (int j = start; j < n; j ++) {
            path.push_back(nums[j]);
            dfs(i + 1, j + 1);
            path.pop_back();
        }
    }
};
```

#### [LeetCode 90. 子集 II](https://leetcode.cn/problems/subsets-ii/)

NOT AC，输入有重复 思路：子集型回溯的基础上加了输入重复，我们需要考虑三个去重，层内去重，分支内去重，分支间去重；这里提供了多个方法

按输入每位搜索，不存在层内去重，分支内去重: 对于相同的数，不选就一直不选；分支间去重: 排序

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> nums;
    vector<int> path;
    int n;
    vector<vector<int>> subsetsWithDup(vector<int>& _nums) {
        nums = _nums;
        n = nums.size();
        sort(nums.begin(), nums.end()); // 分支间去重
        dfs(0);
        return ans;
    }

    // 按输入每位搜索，决策 选or不选
    void dfs(int i) {
        // ans包含最后一层的结果
        if (i == n) ans.push_back(path);

        // 递归边界
        if (i == n) return;

        // 选
        path.push_back(nums[i]); 
        dfs(i + 1);
        path.pop_back();

        // 不选 分支内去重 相同的不选就一直不选   i共用会影响到下面，一般放下面
        while(i + 1 < n && nums[i + 1] == nums[i]) i ++;
        dfs(i + 1);
    }
};
```

按输入每位搜索，不存在层内去重，分支内去重对于相同的数，选了就一直选；分支间去重，排序

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> nums;
    vector<int> path;
    int n;
    vector<vector<int>> subsetsWithDup(vector<int>& _nums) {
        nums = _nums;
        n = nums.size();
        sort(nums.begin(), nums.end()); // 分支间去重
        dfs(0);
        return ans;
    }

    // 按输入每位搜索，决策 选or不选
    void dfs(int i) {
        // ans包含最后一层的结果
        if (i == n) ans.push_back(path);

        // 递归边界
        if (i == n) return;

        // 不选
        dfs(i + 1);

        // 选  分支内去重 相同的就一直选 i共用会影响到下面，一般放下面
        int cnt = 1;
        while (i + 1 < n && nums[i + 1] == nums[i]) i ++, cnt ++;
        for (int k = 0; k < cnt; k ++) path.push_back(nums[i]); 
        dfs(i + 1);
        for (int k = 0; k < cnt; k ++) path.pop_back();
    }
};
```

按答案每一位搜索，决策选哪个 

层内去重：每层用一个set or 排序后跳过重复的 分支间和分支内去重：排序

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> nums;
    vector<int> path;
    int n;
    vector<vector<int>> subsetsWithDup(vector<int>& _nums) {
        nums = _nums;
        n = nums.size();
        sort(nums.begin(), nums.end()); // 分支间去重
        dfs(0, 0);
        return ans;
    }

    // 按答案每位搜索，决策 选哪个
    void dfs(int i, int start) {
        // ans包含每一层的结果
        ans.push_back(path);

        // 递归边界
        if (i >= n && start >= n) return;

        // 选哪个
        for (int j = start; j < n; j ++) {
            if (j - 1 >= start && nums[j] == nums[j - 1]) continue;   // 层内去重
            path.push_back(nums[j]); 
            dfs(i + 1, j + 1);
            path.pop_back();
        }
    }
};
```

先对输入去重，直接变成频次数组，相当于输入无重复，然后按输入每位搜索，决策选几个   

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> nums;
    vector<int> path;
    int n;
    unordered_map<int, int> map;

    vector<vector<int>> subsetsWithDup(vector<int>& _nums) {
        nums = _nums;
        n = nums.size();

        // 使用频次数组，给输入去重
        for (int i = 0; i < n; i ++) map[nums[i]]++;
        nums.clear();
        for (auto &[k, v]: map) nums.push_back(k);
        n = nums.size();

        dfs(0);
        return ans;
    }

    // 按输入每位搜索，决策 选几个
    void dfs(int i) {
        // ans包含最后一层的结果
        if (i == n) ans.push_back(path);

        // 递归边界
        if (i == n) return;

        // 选几个
        for (int j = 0; j <= map[nums[i]]; j ++) {
            for (int k = 0; k < j; k ++) path.push_back(nums[i]);
            dfs(i + 1);
            for (int k = 0; k < j; k ++) path.pop_back();
        }
    }
};
```

#### [LeetCode 77. 组合](https://leetcode.cn/problems/combinations/)

模板题 组合型回溯

AC，组合型回溯：子集型回溯的基础上加了剪枝：

剪枝1：已选（cnt) &gt; 已选所需（k）

剪枝2：剩余(n - i + 1) &lt; 剩余所需(k - cnt)

两种方法，输入角度和答案角度：

方法1-输入角度：按输入每一位搜索，选择是 选or不选

方法2-答案角度：按答案每一位搜索 选择是 选哪个数

方法1：按输入每位搜索

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;
    int n, k;
    vector<vector<int>> combine(int _n, int _k) {
        n = _n, k = _k;
        dfs(1, 0);
        return ans;
    }

    void dfs(int i, int cnt) {
        // 组合剪枝 已选（cnt) > 已选所需（k） || 剩余(n - i + 1) < 剩余所需(k - cnt)
        if (cnt > k || n - i + 1 < k - cnt) return;
        
        // ans包含最后一层cnt = k的结果
        if (i == n + 1 && cnt == k) ans.push_back(path);
        
        // 边界
        if (i == n + 1) return;

        // 选
        path.push_back(i);
        dfs(i + 1, cnt + 1);
        path.pop_back();

        // 不选
        dfs(i + 1, cnt);
    }
};
```

#### [LeetCode 39. 组合总和](https://leetcode.cn/problems/combination-sum/)

AC，思路：组合型回溯，这里是有一个注意的点，虽然输入无重复，但是每个数可以无限选

方法1：按输入每一位搜索，选择是 选or不选

重复无限次，所以剪枝2 剩余和 &lt; 剩余需要和 没有必要算，因为当前剩余和无限大一定不满足

方法2：按答案每一位搜索，选择是 选哪个数

重复无限次，所以边界 i == n无效，因为答案可以是无限位

方法1：

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;
    vector<int> candidates;
    int target, n;
    vector<vector<int>> combinationSum(vector<int>& _candidates, int _target) {
        candidates = _candidates;
        target = _target;
        n = candidates.size();
        dfs(0, 0);
        return ans;
    }

    void dfs(int i, int sum) {
        // 剪枝
        if (sum > target) return;

        // 构造答案
        if (i == n && sum == target) ans.push_back(path);

        // 递归边界
        if (i == n) return;

        // 选 注意这里是无限制重复被选取
        path.push_back(candidates[i]);
        dfs(i, sum + candidates[i]);
        path.pop_back();

        // 不选
        dfs(i + 1, sum);
    }
};
```

#### [LeetCode 40. 组合总和 II](https://leetcode.cn/problems/combination-sum-ii/)

AC, 思路：子集2和组合总和的综合题目，注意输入有重复如何去重，注意组合型回溯如何剪枝

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;
    vector<int> candidates;
    int target, n;
    vector<vector<int>> combinationSum2(vector<int>& _candidates, int _target) {
        candidates = _candidates;
        target = _target;
        n = candidates.size();
        sort(candidates.begin(), candidates.end());
        dfs(0, 0);
        return ans;
    }

    // 按输入每位搜索，决策 选or不选
    void dfs(int i, int sum) {
        // 剪枝
        if (sum > target) return;

        // 构造答案
        if (i == n && sum == target) ans.push_back(path);

        // 递归边界
        if (i == n) return;

        // 选 注意这里是无限制重复被选取
        path.push_back(candidates[i]);
        dfs(i + 1, sum + candidates[i]);
        path.pop_back();

        // 不选
        while (i + 1 < n && candidates[i + 1] == candidates[i]) i ++;
        dfs(i + 1, sum);
    }
};
```

#### [LeetCode 216. 组合总和 III](https://leetcode.cn/problems/combination-sum-iii/)

AC, 思路：组合型回溯，这里既有cnt剪枝，也有sum剪枝

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;
    int k, n;
    vector<vector<int>> combinationSum3(int _k, int _n) {
        n = _n, k = _k;
        dfs(1, 0, 0);
        return ans;
    }

    void dfs(int i, int cnt, int sum) {
        // 剪枝1 cnt
        if (cnt > k || 9 - i + 1 < k - cnt) return;
        // 剪枝2 sum
        if (sum > n || 45 - sum < n - sum) return;

        // 构造答案
        if (i == 10 && cnt == k && sum == n) ans.push_back(path);
        
        // 递归边界
        if (i == 10) return;

        // 选
        path.push_back(i);
        dfs(i + 1, cnt + 1, sum + i);
        path.pop_back();

        // 不选
        dfs(i + 1, cnt, sum);
    }
};
```

#### [46. 全排列](https://leetcode.cn/problems/permutations/)

模板题 排列型回溯

AC，思路：输入无重复，排列只能答案视角搜索，不能输入视角搜索，因为因为排列问题，每个数都要选

按答案每位搜索，决策是选哪个；其中需要一个状态数组记录每个位置是否备选，状态数组可以使用状态压缩进行进一步优化；

状态数组：

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;
    vector<int> nums;
    int n;
    vector<bool> vis;
    vector<vector<int>> permute(vector<int>& _nums) {
        nums = _nums;
        n = nums.size();
        vis.resize(n, false);
        dfs(0);
        return ans;
    }

    // 按答案每位搜索，决策是 选哪个
    void dfs(int i) {
        // 构造答案
        if (i == n) ans.push_back(path);
        
        // 边界
        if (i == n) return;

        // 非边界
        for (int j = 0; j < n; j ++) {
            if (!vis[j]) {
                path.push_back(nums[j]);
                vis[j] = true;
                dfs(i + 1);
                vis[j] = false;
                path.pop_back();
            }
        }
    }
};
```

状态压缩：注意位运算相关的优先级，左移右移(&gt;&gt; &lt;&lt;) 关系(&gt;, &gt;=, ==, !=) 位运算符(& |) 复合(+=， -=)

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;
    vector<int> nums;
    int n;
    int state = 0;
    vector<vector<int>> permute(vector<int>& _nums) {
        nums = _nums;
        n = nums.size();
        dfs(0);
        return ans;
    }

    // 按答案每位搜索，决策是 选哪个
    void dfs(int i) {
        // 构造答案
        if (i == n) ans.push_back(path);
        
        // 边界
        if (i == n) return;

        // 非边界
        for (int j = 0; j < n; j ++) {
            if ((state >> j & 1) == 0) {
                path.push_back(nums[j]);
                state += 1 << j;
                dfs(i + 1);
                state -= 1 << j;
                path.pop_back();
            }
        }
    }
};
```

#### [47. 全排列 II](https://leetcode.cn/problems/permutations-ii/)

AC，思路：输入有重复，层内重复，层内去重后，不存在分支之间重复

两种方法：

1. 先层内去重，之后不存在分支间重复

层内去重： 排序+vis[j - 1] = false跳过重复的 或者 每层放一个set实现

2. 直接分支间去重

分支之间去重：排序 + vis[j - 1] = true跳过重复的;

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;
    vector<int> nums;
    int n;
    int state = 0;
    vector<vector<int>> permuteUnique(vector<int>& _nums) {
        nums = _nums;
        n = nums.size();
        dfs(0);
        return ans;
    }

    // 按答案每位搜索，决策是 选哪个
    void dfs(int i) {
        // 构造答案
        if (i == n) ans.push_back(path);
        
        // 边界
        if (i == n) return;

        // 非边界
        unordered_set<int> set;
        for (int j = 0; j < n; j ++) {
            if (set.count(nums[j])) continue;
            if ((state >> j & 1) == 0) {
                set.insert(nums[j]);
                path.push_back(nums[j]);
                state += 1 << j;
                dfs(i + 1);
                state -= 1 << j;
                path.pop_back();
            }
        }
    }
};
```

#### <b>acwing 94. 递归实现排列型枚举</b>

模板题 排列型枚举

AC，思路：递归实现排列型枚举的模板题；主要就是写法的注意

1. 按xx搜索，决策是什么，结果是什么；

2. 边界根据 搜索位置xxx，已搜空间xxx，来确定，全部搜完时对应的搜索位置自然就是边界了；

3. DFS参数 一定会放搜索顺序，至于其他的结果集合，操作信息等等根据情况可以放入参数，函数栈维护，也可以全局变量维护，一般来说ACM模式下，全局变量维护更好；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 12;

int n;
int path[N];
int state[N];


void dfs(int i) {
    if (i == n + 1) {
        for (int i = 1; i <= n; i ++) cout << path[i] << " ";
        cout << endl;
    }
    
    for (int num = 1; num <= n; num ++) {
        if (state[num] == 0) {
            state[num] = 1;
            path[i] = num;
            dfs(i + 1);
            state[num] = 0;
        }
    }
}

int main() {
    cin >> n;
    dfs(1);
    return 0;
}
```

#### <b>2023柠檬微趣-排队</b>

AC, 全排列模板，多了一个全局计数的操作，然后注意这里是找到一个就返回，所以dfs返回值改为bool，提前判断；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 12;

int m, n;
int id;
int path[N];
int state[N];



bool dfs(int i) {
    if (i == m + 1) {
        id ++;
        if (id == n) {
            for (int i = 1; i <= m; i ++) cout << path[i] << " ";
            return true;
        }
        return false;
    }

    for (int num = 1; num <= m; num ++) {
        if (state[num] == 0) {
            path[i] = num;
            state[num] = 1;
            if (dfs(i + 1)) return true;
            state[num] = 0;
        }
    }

    return false;
}

int main() {
    cin  m;
    cin  n;
    if (dfs(1) == false) cout << -1 << endl;
    return 0;
}
```

## 图论概念

<b>图定义，点集，边集</b>
图是由点集V和边集E组成的，一般我们记作 图 G=&lt;V,E&gt;, 一条边连接两个顶点
点集V包含了所有顶点，边界E包含了所有边，点集V为空叫做空图

<b>有向图，无向图</b>
由无向边构成的图称为无向图，由有向边构成的图称为有向图

<img src="/assets/G382bGP2mowyNpxufeZcJQpnnBh.png" src-width="1138" src-height="574" align="center"/>


<b>自环，重边，孤点，简单图</b>
自环：边连接的两个点是同一个点
重边：无向图重边：两点之间有多条边（&gt;=2)连接  有向图重边：两点之间有多条同方向的边(&gt;=2)连接
孤点：没有连接边的点称为孤点
简单图：没有自环和重边的图称为简单图

<img src="/assets/ZJwQbzrY9os8unxZjvfcZEtpn8b.png" src-width="1171" src-height="576" align="center"/>




<b>度数</b>
无向图的度数：对于顶点v，v作为边的端点的次数称为v的度数（v的边数）记为d(v)
有向图的度数：对于顶点v，v作为边的起点的次数称为v的出度（v的出边) 记为d+(v); v作为边的终点的次数称为v的入度（v的入边数）记为d-(v);顶点v的度数d(v) = d+(v) + d-(v) （v的边数）
图的最大度为所有顶点度数的最大值，记作Δ(G); 最小度为所有顶点度数的最小值，记作δ(G).
图的所有点的度数和为边数的两倍，有向图的所有顶点的出度和 = 入度和

<img src="/assets/MoCQbIt6ionc5zxRVdzce6wynCa.png" src-width="1183" src-height="627" align="center"/>


<b>完全图，竞赛图</b>
完全图（无向图): 设G为一个有n个节点的无向简单图，若G中每个顶点都与其余n-1个顶点有边相连，则称G为n阶无向完全图，简称为n阶完全图，记作Kn   边数：n(n - 1) / 2 = Cn2
完全图（有向图): 设G为一个有n个节点的有向简单图，若G中每个顶点都有连到其余n-1个顶点的边，且都有这些节点连向它的边（双向边),则称G为n阶有向完全图  边数：n(n-1)
竞赛图: 基于n阶无向完全图，给每条边任意确定一个方向形成的图称为n阶竞赛图

<img src="/assets/VQpCbIspRoh79ZxzR5rc5OXTn9c.png" src-width="1162" src-height="598" align="center"/>


<b>子图，生成子图</b>
G = &lt;V,E&gt; G' = &lt;V',E'&gt; 两张图（同为无向图或有向图），如果V'⊆ V且E'⊆ E,则称G'为G的子图，G称为G'的母图，记作G'⊆ G
如果V' = V，则称G'为G的生成子图
如果V'⊂ V 或 E'⊂ E，则称G'为G的真子图

<img src="/assets/AfTlbHIK7oz6GLxVAX3cnYzlnOf.png" src-width="1163" src-height="577" align="center"/>


<b>补图</b>
设G = &lt;V, E&gt;是一个n阶无向简单图，以V为顶点集，以所有使G称为完全图Kn需要添加的边的集合为边集的图，称为G的补图，记作G上划线
图和它的补图顶点集相同；边集的交集为空，边集的并集是完全图的边集

<img src="/assets/C6edbAOXKotjlbxEopJcRnicn1c.png" src-width="1190" src-height="613" align="center"/>


<b>同构</b>
设G和G'是分别具有顶点集V和V'的两个图，如果存在一个双射（11对应）h：V-&gt;V'，满足当且仅当（vi，vj）是G的边时，（h(vi), h(vj))是G'的边，则称图G和G'同构

<img src="/assets/WTSqbpHITobSdCxaPascMb3YnXg.png" src-width="1186" src-height="589" align="center"/>


<b>路（通路，回路，环，路径，距离）</b>
对于一个图G，G中顶点与边的交替序列v0e1v1e2...envn称为v0到vn的通路，其中v0,vn称为通路的起点和终点，通路中边的条数称为它的长度，有向图中，要保持边的方向一致；点数 = 边数 + 1
对于一条通路，如果v0=vn,则称为回路。如果v0=vn且其他所有顶点都不相同，则称为环
如果通路中的所有边都不相同，称为迹；如果通路中所有顶点不同（点不同，边肯定也不同）,则称为路径
途中两点之间最短的路径长度称为距离

<img src="/assets/YswTbC4q2ojRpNxcNjlcAMMgnhg.png" src-width="1172" src-height="599" align="center"/>



<b>连通性与连通块</b>
无向图：
连通性：设无向图G=&lt;V,E&gt;, u,v∈V，如果u，v之间存在通路，则称为u，v是连通的。对于所有v，v和v自己是连通的
连通图：对于任意非空无向图G，若任意两点都是连通的，则称为G为连通图
连通块：对于无向图G的一个连通子图H，若H是一个极大连通子图，则称H为G的一个连通块/连通分量


有向图：
连通性：设有向图G=&lt;V,E&gt;，u,v∈V,如果存在u到v的通路，则称u可达v。如果u,v相互可达，则称u，v连通
强连通：如果有向图G中的顶点两两可达，则称G为强连通图
强连通块：与无向图类似，可以定义有向图的强连通块/强连通分量 （极大的强连通子图）

<img src="/assets/PtpobGn18oeOy6xM1QBcr1ManDe.png" src-width="1170" src-height="582" align="center"/>

#### [简单图判定](http://oj.daimayuan.top/course/14/problem/596)

<img src="/assets/W2tZbQrofokjaaxhvfvc2J6nn6g.png" src-width="1157" src-height="675" align="center"/>

AC，思路：简单图就是看，图中是否有重边和自环

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1000;

int n, m, a[N + 1][N + 1];

int main() {
    int n, m;
    cin >> n >> m;

    for (int i = 1; i <= m; i ++) {
        int x, y;
        cin >> x >> y;
        if (x == y || a[x][y]) {
            cout << "No" << endl;
            return 0;
        }
        a[x][y] = a[y][x] = 1;
    }
    cout << "Yes" << endl;
    return 0;
}
```

#### [顶点度数统计](http://oj.daimayuan.top/course/14/problem/597)

<img src="/assets/H0ofbjAG5owoORxcfGTcYHsknad.png" src-width="1178" src-height="682" align="center"/>

AC，思路：无向图的度数概念，每读一条边，两端顶点的各自度数 + 1；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1000;

int n, m, d[N + 1];

int main() {
    int n, m;
    cin >> n >> m;

    for (int i = 1; i <= m; i ++) {
        int x, y;
        cin >> x >> y;
        d[x]++, d[y]++;
    }

    for (int i = 1; i <= n; i ++) cout << d[i] << " ";

    return 0;
}
```

#### [顶点度数合法性](http://oj.daimayuan.top/course/14/problem/598)

<img src="/assets/QIbubVa20oPPGKxdRfEc1NSpnJd.png" src-width="1234" src-height="659" align="center"/>

AC，思路：图中的每一条边，会贡献两个度数，所以图的度数和 是 边数的两倍，那么我们可以通过判断度数和是否为偶数，来判断度数数组是否合法

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1000;

int main() {
    int n;
    cin >> n;

    int sum = 0;
    for (int i = 1; i <= n; i ++) {
        int x;
        cin >> x;
        sum += x;
    }

    if (sum % 2 == 0) cout << "Yes" << endl;
    else cout << "No" << endl;
    
    return 0;
}
```

## 图论基础 - DFS/BFS/并查集

<b>图上DFS</b>

图上DFS的基础运用，找连通块、判断是否有环等

图上DFS的初始 要么是 初始 点0 已搜0，要么是 初始 点0 已搜空 

但是void dfs(i)的含义一定是 `i处,已搜到i(包含i)`，所以对于不同的初始化，我们DFS的代码不同

`初始 点0 已搜0`，进入DFS满足定义，不需要处理；`初始 点0 已搜空`，进入DFS需要先处理i点，满足定义

具有返回值的dfs，我们就需要紧扣递归思想了；

<b>图上BFS</b>

#### [代码源-BFS模板题-求距离](http://oj.daimayuan.top/course/14/problem/630)

<img src="/assets/USsrbaw75odKybxVsrncdc7sndh.png" src-width="1166" src-height="728" align="center"/>

AC，思路：BFS找两点之间距离，距离的含义是最短路径

手写队列：

```cpp
#include <bits/stdc++.h>

using namespace std;
const int N = 20000, M = 100000;

int n, m, k, q[N + 1], dist[N + 1];
vector<int> edge[N + 1];


int main() {
    cin >> n >> m >> k;
    
    // 建图
    for (int i = 1; i <= m; i ++) {
        int x, y;
        cin >> x >> y;
        edge[x].push_back(y);
        edge[y].push_back(x);
    }

    while (k --) {
        int s, t;
        cin >> s >> t;
        
        // BFS
        // 初始化队列，距离数组（所有点距离源点的距离）
        memset(dist, 255, sizeof(dist));
        int front = 1, rear = 0;
        // 源点入队
        dist[s] = 0;                        
        q[++rear] = s;
        
        // 队列非空，层层出队入队
        while (front <= rear) {
            int x = q[front];
            ++front;
            for (auto &y: edge[x]) {
                if (dist[y] == -1) {
                    dist[y] = dist[x] + 1;
                    q[++rear] = y;
                }
            }
        }
        cout << dist[t] << endl;
    }
    return 0;
}
```

使用STL队列

```cpp
#include <bits/stdc++.h>

using namespace std;
const int N = 20000, M = 100000;

int n, m, k, dist[N + 1];
vector<int> edge[N + 1];


int main() {
    cin >> n >> m >> k;
    
    // 建图
    for (int i = 1; i <= m; i ++) {
        int x, y;
        cin >> x >> y;
        edge[x].push_back(y);
        edge[y].push_back(x);
    }

    while (k --) {
        int s, t;
        cin >> s >> t;
        
        // BFS
        // 初始化队列，距离数组（所有点距离源点的距离）
        queue<int> q;
        memset(dist, 255, sizeof(dist));
        // 源点入队
        q.push(s);
        dist[s] = 0;                        
      
        // 队列非空，层层出队入队
        while (q.size()) {
            int x = q.front(); q.pop();
            for (auto &y: edge[x]) {
                if (dist[y] == -1) {
                    q.push(y);
                    dist[y] = dist[x] + 1;
                }
            }
        }
        cout << dist[t] << endl;
    }
    return 0;
}
```

#### [代码源-DFS模板题-连通块计数](http://oj.daimayuan.top/course/14/problem/629)

<img src="/assets/NNZGbVs1Foj2J9xzUbscKlthnjf.png" src-width="1173" src-height="656" align="center"/>

AC，思路：dfs找连通块，每次dfs都会遍历完一个连通块，然后同时计数

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 20000, M = 100000;

int n, m;
vector<int> edge[N + 1];
bool vis[N + 1];

void dfs(int x) {
    vis[x] = true;
    for (auto &y: edge[x]) {
        if (!vis[y]) dfs(y);
    }
}

int main() {
    cin >> n >> m;
    for (int i = 1; i <= m; i ++) {
        int x, y;
        cin >> x >> y;
        edge[x].push_back(y);
        edge[y].push_back(x);
    }

    int cnt = 0;
    for (int i = 1; i <= n; i ++) {
        if (!vis[i]) {
            dfs(i);
            ++cnt;
        }
    }
    cout << cnt << endl;
    return 0;
}
```

#### [547. 省份数量](https://leetcode.cn/problems/number-of-provinces/)

看答案学习，本题就是连通块计数问题，连通块相关一题三解，DFS，BFS，并查集，都可以用来解决连通块相关问题；然后注意这里的图是使用邻接矩阵存的，然后编号是矩阵的下标；

DFS

```cpp
class Solution {
public:
    vector<vector<int>> isConnected;
    int n;
    vector<bool> vis;
    int findCircleNum(vector<vector<int>>& _isConnected) {
        isConnected = _isConnected;
        n = isConnected.size();
        vis.resize(n, false);
        
        // dfs找连通块
        int cnt = 0;
        for (int i = 0; i < n; i ++) {   // 下标代表节点编号，遍历所有节点
            if (!vis[i]) {
                dfs(i);
                ++cnt;
            }
        }
        return cnt;
    }

    // 邻接矩阵 dfs模板
    void dfs(int i) {
        vis[i] = true;
        for (int j = 0; j < n; j ++) {
            if (isConnected[i][j] && !vis[j]) dfs(j);
        }
    }
};
```

BFS

```cpp
class Solution {
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();

        // BFS 初始化队列，vis数组
        queue<int> q;
        vector<bool> vis(n, false);
        
        // 遍历所有点 BFS找连通分量
        int cnt = 0;
        for (int i = 0; i < n; i ++) {
            if (!vis[i]) {
                // 一次BFS
                q.push(i);
                vis[i] = true;
                while (q.size()) {
                    int j = q.front(); q.pop();
                    for (int k = 0; k < n; k ++) {
                        if (isConnected[j][k] == 1 && !vis[k]) {
                            q.push(k);
                            vis[k] = true;
                        }
                    }
                }
                cnt ++;
            }
        }

        return cnt;
    }
};
```

并查集

```cpp
class Solution {
public:
    vector<int> fa;
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();
        fa.resize(n);

        // 初始化并查集
        for (int i = 0; i < n; i ++) fa[i] = i;

        // 连边，集合合并
        for (int i = 0; i < n; i ++) {
            for (int j = i + 1; j < n; j ++) {
                if (isConnected[i][j] == 1) merge(i, j);
            }
        }

        // 统计连通块数，就是统计集合数
        int cnt = 0;
        for (int i = 0; i < n; i ++) {
            if (fa[i] == i) cnt ++;
        }
        return cnt;
    }

    // 并查集模板
    int find(int x) {
        if (fa[x] == x) return x;
        return fa[x] = find(fa[x]);
    }

    void merge(int x, int y) {
        int fx = find(x), fy = find(y);
        if (fx == fy) return;
        fa[fx] = fy;
    }
};
```

#### [1971. 寻找图中是否存在路径](https://leetcode.cn/problems/find-if-path-exists-in-graph/)

看答案学习，思路：本题是通路问题，也是连通块相关，一题三解；

DFS：DFS起点，然后看中途是否可以遍历到终点，如果找到就可以提前返回；所以这里涉及到找到通路就提前返回，一般这种找到就返回；我们DFS的返回值设为bool值，有返回值的DFS紧扣递归定义来写

BFS：BFS起点，然后遍历的时候看是否路过终点，遇到终点直接返回

并查集：看起点和终点是否在一个集合里

DFS

```cpp
class Solution {
public:
    int n;
    vector<vector<int>> edges;
    int source; 
    int destination;
    vector<bool> vis;
    vector<vector<int>> g;
    bool validPath(int _n, vector<vector<int>>& _edges, int _source, int _destination) {
        n = _n, edges = _edges, source = _source, destination = _destination;
        g.resize(n);
        vis.resize(n, false);
        
        // 读边数组，建图 邻接表
        for (auto &e: edges) {
            int x = e[0], y = e[1];
            g[x].push_back(y);
            g[y].push_back(x);
        }

        // 使用DFS来发现是否有通路
        return dfs(source);
    }
    
    // dfs含义，已搜i，i到终点有通路
    bool dfs(int i) {
        if (i == destination) return true;

        vis[i] = true;
        for (auto j: g[i]) {
            if (!vis[j]) {
                // i可以到j，j到终点有通路，i可以到终点
                if (dfs(j)) return true;
            }
        }
        // 遍历完所有的j都不行，那么i不能到终点
        return false;
    }
};
```

BFS

```cpp
class Solution {
public:
    bool validPath(int n, vector<vector<int>>& edges, int source, int destination) {
        if (source == destination) return true;
        
        vector<vector<int>> g(n);
        
        // 读边数组，建图 邻接表
        for (auto &e: edges) {
            int x = e[0], y = e[1];
            g[x].push_back(y);
            g[y].push_back(x);
        }

        // BFS 查连通
        queue<int> q;
        vector<bool> vis(n, false);

        q.push(source);
        vis[source] = true;

        while (q.size()) {
            int j = q.front(); q.pop();
            for (auto &k: g[j]) {
                if (!vis[k]) {
                    if (k == destination) return true;
                    q.push(k);
                    vis[k] = true;
                }
            }
        }

        return false;
    }
};
```

并查集

```cpp
class Solution {
public:
    vector<int> fa;
    bool validPath(int n, vector<vector<int>>& edges, int source, int destination) {
        if (source == destination) return true;  // 提前判断
        
        // 并查集 查连通
        fa.resize(n);
        for (int i = 0; i < n; i ++) fa[i] = i;
        
        for (auto &e: edges) merge(e[0], e[1]);
        return find(source) == find(destination);
    }
    
    int find(int x) {
        if (fa[x] == x) return x;
        return fa[x] = find(fa[x]);
    }

    void merge(int x, int y) {
        int fx = find(x), fy = find(y);
        if (fx == fy) return;
        fa[fx] = fy;
    }
};
```

#### [797. 所有可能的路径](https://leetcode.cn/problems/all-paths-from-source-to-target/)

看答案学习，思路：所有路径，很明显DFS暴搜整张图；然后注意：因为本题中的图为有向无环图，搜索过程中不会反复遍历同一个点，因此我们无需使用vis数组记录每个点的访问状态

DFS含义始终是已搜到i点，DFS不同的初始化，DFS函数里的写法会有些区别

-如果初始已搜空，那么DFS里先处理当前节点，然后再递归搜索后面的节点；

-如果初始已搜初始节点，那么DFS直接递归搜索后面的节点，递归之前处理后面的节点；

DFS：初始 点0 已搜空 路径空

```cpp
class Solution {
public:
    vector<vector<int>> graph;
    int n;
    vector<int> path;
    vector<vector<int>> ans;
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& _graph) {
        graph = _graph;
        n = graph.size();

        // 初始 点0 已搜空 路径空
        dfs(0);
        return ans;
    }
    
    // dfs含义 已搜到i
    void dfs(int i) {
        path.push_back(i);

         // 构造答案
        if (i == n - 1) ans.push_back(path);

        for (auto &j: graph[i]) {
            dfs(j);
        }

        path.pop_back();
    }
};
```

DFS：初始 点0 已搜0 路径0

```cpp
class Solution {
public:
    vector<vector<int>> graph;
    int n;
    vector<int> path;
    vector<vector<int>> ans;
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& _graph) {
        graph = _graph;
        n = graph.size();

        // 初始 点0 已搜0 路径0
        path.push_back(0);
        dfs(0);
        return ans;
    }
    
    // dfs含义 已搜到i
    void dfs(int i) {
         // 构造答案
        if (i == n - 1) ans.push_back(path);

        for (auto &j: graph[i]) {
            path.push_back(j);
            dfs(j);
            path.pop_back();
        }
    }
};
```

#### [841. 钥匙和房间](https://leetcode.cn/problems/keys-and-rooms/)

看答案学习，思路：首先转化题意，给定一张有向图，询问从0号节点出发是否能够到达所有的节点；有向图，连通相关的问题，一题两解

DFS: DFS遍历计数，最后判断计数和节点数的关系；

BFS：BFS遍历计数，出队的时候cnt ++；

DFS：初始 点0 已搜空 cnt = 0

```cpp
class Solution {
public:
    vector<vector<int>> rooms;
    int n;
    vector<int> vis;
    int cnt;
    bool canVisitAllRooms(vector<vector<int>>& _rooms) {
        rooms = _rooms;
        n = rooms.size();
        vis.resize(n, false);
        
        // 初始 点0 已搜空 cnt = 0
        cnt = 0;
        dfs(0);
        return cnt == n;
    }
    
    // dfs含义，已搜到i
    void dfs(int i) {
        // 处理当前节点i
        cnt ++;
        vis[i] = true;
        // 递归
        for (auto &j: rooms[i]) {
            if (!vis[j]) dfs(j);
        }
    }
};
```

DFS: 初始 点0 已搜0 cnt = 1；

```cpp
class Solution {
public:
    vector<vector<int>> rooms;
    int n;
    vector<int> vis;
    int cnt;
    bool canVisitAllRooms(vector<vector<int>>& _rooms) {
        rooms = _rooms;
        n = rooms.size();
        vis.resize(n, false);
        
        // 初始 点0 已搜0 cnt = 1
        cnt = 1; vis[0] = true;
        dfs(0);
        return cnt == n;
    }
    
    // dfs含义，已搜到i
    void dfs(int i) {
        // 直接递归处理
        for (auto &j: rooms[i]) {
            if (!vis[j]) {
                // 递归之前处理后面的节点
                ++ cnt;
                vis[j] = true;
                dfs(j);
                // 回溯，不需要恢复现场，因为回溯到该点，该点还是应该遍历过，计数过   
            }
        }
    }
};
```

BFS:

```cpp
class Solution {
public:
    bool canVisitAllRooms(vector<vector<int>>& rooms) {
        int n = rooms.size();

        // BFS
        queue<int> q;
        vector<bool> vis(n, false);

        q.push(0);
        vis[0] = true;

        int cnt = 0;
        while (q.size()) {
            int x = q.front(); q.pop();
            cnt ++;
            for (auto &y : rooms[x]) {
                if (!vis[y]) {
                    q.push(y);
                    vis[y] = true;
                }
            }
        }
        return cnt == n;
    }
};
```

#### [2316. 统计无向图中无法互相到达点对数](https://leetcode.cn/problems/count-unreachable-pairs-of-nodes-in-an-undirected-graph/)

看答案学习，思路：无向无环简单图，连通相关问题，一题多解；

DFS：DFS求出每个连通块中的点数

BFS：BFS求出每个连通块中的点数

并查集：加上sizes数组，记录每个集合中的点数，也就是每个连通块中的点数

计算无法相互到达的点对数，有两种方法：

1. 当前连通块节点个数为a, 与其他节点构成的互不联通的对数为a*(n-a)，点对会重复计算一次，所以最后/2
2. 当前连通块节点个数为a，与前面的其他连通块的总点数total无法到达，ans += a * total, 更新total += a;

DFS：

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n, m;
    vector<bool> vis;
    long long countPairs(int _n, vector<vector<int>>& edges) {
        m = edges.size(), n = _n;
        g.resize(n);
        vis.resize(n, false);
        

        // 建图
        for (auto &e: edges) {
            int a = e[0], b = e[1];
            g[a].push_back(b);
            g[b].push_back(a);
        }

        long long ans = 0;
        // 变量 total维护前面求出的连通块的大小之和
        for (int i = 0, total = 0; i < n; i ++) {
            if (!vis[i]) {      // 未访问的点：说明找到了一个新的连通块
                int cnt = dfs(i);
                ans += (long) cnt * total;
                total += cnt;
            }
        }

        return ans;
    }

    // dfs返回i点所在的连通块节点数，递归思想
    int dfs(int i) {
        vis[i] = true;
        int cnt = 1;   // 当前节点

        for (auto &j: g[i]) {
            if (!vis[j]) {
                cnt += dfs(j);  // 邻接节点的连通块节点数 叠加
            }
        }
        return cnt;
    }
};
```

BFS:

```cpp
class Solution {
public:
    long long countPairs(int n, vector<vector<int>>& edges) {
        // 建图
        vector<vector<int>> g(n);
        for (auto &e: edges) {
            int x = e[0], y = e[1];
            g[x].push_back(y);
            g[y].push_back(x);
        }

        // BFS准备 初始化队列和vis数组
        queue<int> q;
        vector<bool> vis(n, false);
        
        long long ans = 0;   // 一定要long long 否则大数据会出错
        for (int i = 0; i < n; i ++) {
            if (!vis[i]) {
                // BFS 搜索连通块
                int cnt = 0;
                q.push(i);
                vis[i] = true;
                while (q.size()) {
                    int x = q.front(); q.pop();
                    cnt ++;
                    for (auto &y: g[x]) {
                        if (!vis[y]) {
                            q.push(y);
                            vis[y] = true;
                        }
                    }
                }
                ans += 1LL * cnt * (n - cnt);
            }
        }

        return ans / 2;
    }
};
```

并查集：

```cpp
class Solution {
public:
    vector<int> fa;
    vector<int> sizes;
    long long countPairs(int n, vector<vector<int>>& edges) {
        fa.resize(n);
        sizes.resize(n, 0);

        // 并查集初始化
        for (int i = 0; i < n; i ++) fa[i] = i, sizes[i] = 1;

        // 连边，集合合并
        for (auto &e: edges) {
            merge(e[0], e[1]);
        }

        // 某一联通块节点个数为a, 与其他节点构成的互不联通的对数为a*(n-a)
        long long ans = 0;
        for (int i = 0; i < n; i ++) {
            if (fa[i] == i) { // 只有集合代表的size有意义，代表集合的点数
                ans += (long long)sizes[i] * (n - sizes[i]);
            }
        }
        // 每个点对会重复计算一次，/2
        return ans / 2;
    
    }

    // 并查集模板
    int find(int x) {
        if (fa[x] == x) return x;
        return fa[x] = find(fa[x]);
    }

    void merge(int x, int y) {
        int fx = find(x), fy = find(y);
        if (fx == fy) return;
        fa[fx] = fy;
        sizes[fy] += sizes[fx];
    }
};
```

#### [1319. 连通网络的操作次数](https://leetcode.cn/problems/number-of-operations-to-make-network-connected/)

看答案学习，思路：连通网络，本质就是要让这个图成为一个连通块，要成为一个连通块，最少需要n - 1条边，所以先用这个条件提前判断；然后就是统计连通块个数，然后让这些连通块合并成一个大连通块，需要加cnt - 1边（从原来的边转换而来）；统计连通块，三种写法

DFS：

```cpp
class Solution {
public:
    int n, m;
    vector<vector<int>> g;
    vector<bool> vis;
    int makeConnected(int _n, vector<vector<int>>& connections) {
        n = _n;
        m = connections.size();

        if (m < n - 1) return -1;   // 提前判断，n个点连通至少需要n-1条边

        vis.resize(n, false);
        g.resize(n);
        // 建图
        for (auto &e: connections) {
            int x = e[0], y = e[1];
            g[x].push_back(y);
            g[y].push_back(x);
        }

        // dfs求连通块个数
        int cnt = 0;
        for (int i = 0; i < n; i ++) {
            if (!vis[i]) {
                dfs(i);
                ++cnt;
            }
        }

        return cnt - 1;
    }

    void dfs(int i) {
        vis[i] = true;
        for (auto &j: g[i]) {
            if (!vis[j]) dfs(j);
        }
    }
};
```

BFS:

```cpp
class Solution {
public:
    int makeConnected(int n, vector<vector<int>>& connections) {
        int m = connections.size();
        if (m < n - 1) return -1;

        // 建图
        vector<vector<int>> g(n);
        for (auto &e: connections) {
            int x = e[0], y = e[1];
            g[x].push_back(y);
            g[y].push_back(x);
        }

        // 初始化队列和vis数组
        queue<int> q;
        vector<bool> vis(n, false);
        
        int cnt = 0;
        // 遍历所有节点找连通块数
        for (int i = 0; i < n; i ++) {
            if (!vis[i]) {
                cout << i << endl;
                // BFS找连通块
                q.push(i);
                vis[i] = true;
                while (q.size()) {
                    int x = q.front(); q.pop();
                    for (auto &y: g[x]) {
                        if (!vis[y]) {  // 这句千万不能忘！
                            q.push(y);
                            vis[y] = true;
                        }
                    }
                }
                cnt ++;
            }
        }

        return cnt - 1;

    }
};
```

并查集

```cpp
class Solution {
public:
    vector<int> fa;
    int makeConnected(int n, vector<vector<int>>& connections) {
        if (connections.size() < n -1) return -1;

        fa.resize(n);

        // 初始化并查集
        for (int i = 0; i < n; i ++) fa[i] = i;

        // 连边，集合合并
        for (auto &e: connections) {
            int x = e[0], y = e[1];
            merge(x, y);
        }

        // 找集合个数 = 连通块个数
        int cnt = 0;
        for (int i = 0; i < n; i ++) {
            if (fa[i] == i) cnt ++;
        }

        return cnt - 1;
    }

    int find(int x) {
        if (fa[x] == x) return x;
        return fa[x] = find(fa[x]);
    }

    void merge(int x, int y) {
        int fx = find(x), fy = find(y);
        if (fx == fy) return;
        fa[fx] = fy;
    }
};
```

#### [2492. 两个城市间路径的最小分数](https://leetcode.cn/problems/minimum-score-of-a-path-between-two-cities/)

看答案学习，思路：由于每条边可以经过多次，而且保证节点1与n都在同一连通块内，因此本题实际上求的就是节点1所在连通块的最小边权; 一题多解

DFS:

```cpp
class Solution {
public:
    typedef pair<int, int> pii;
    int n;
    vector<vector<pii>> g;
    vector<bool> vis;
    int ans = 1e4 + 10;
    int minScore(int _n, vector<vector<int>>& roads) {
        n = _n;
        g.resize(n + 1);
        vis.resize(n + 1, false);

        // 建图
        for (auto &e: roads) {
            int x = e[0], y = e[1], z = e[2];
            g[x].push_back({y, z});
            g[y].push_back({x, z});
        }

        dfs(1);
        return ans;
    }

    // dfs遍历
    void dfs(int i) {
        vis[i] = true;
        for (auto &j: g[i]) {
            ans = min(ans, j.second);
            if (!vis[j.first]) {
                dfs(j.first);
            }
        }
    }
};
```

BFS:

```cpp
class Solution {
public:
    typedef pair<int, int> pii;
    int minScore(int n, vector<vector<int>>& roads) {
        vector<vector<pii>> g(n + 1);

        // 建图
        for (auto &e: roads) {
            int x = e[0], y = e[1], z = e[2];
            g[x].push_back({y, z});
            g[y].push_back({x, z});
        }

        int ans = 1e4;

        // BFS 遍历1到n的连通块
        queue<int> q;
        vector<bool> vis(n + 1, false);

        q.push(1);
        vis[1] = true;
        while (q.size()) {
            int x = q.front(); q.pop();
            for (auto &[y, z]: g[x]) {
                ans = min(ans, z);
                if (!vis[y]) {
                    q.push(y);
                    vis[y] = true;
                }
            }
        }

        return ans;
    }
};
```

#### [2685. 统计完全连通分量的数量](https://leetcode.cn/problems/count-the-number-of-complete-components/)

看答案做题，思路：首先找连通块，然后完全连通分量，其实就是连通块满足完全图的概念，完全图定义 e = v(v - 1) / 2; 然后我们在dfs的时候，可以统计一个连通块的e和v，然后以此判断该连通块是否是完全连通块

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n;
    vector<bool> vis;
    int e, v;
    int countCompleteComponents(int _n, vector<vector<int>>& edges) {
        n = _n;
        g.resize(n);
        vis.resize(n, false);

        // 建图
        for (auto &e: edges) {
            int x = e[0], y = e[1];
            g[x].push_back(y);
            g[y].push_back(x);
        }

        int ans = 0;
        for (int i = 0; i < n; i ++) {
            if (!vis[i]) {
                e = 0, v = 0;
                dfs(i);
                if (e == v * (v - 1)) ans ++;  // 判断连通块是否是完全图，e = v(v - 1) / 2;
            }
        }
        return ans;
    }

    // dfs含义，i处，已搜到i，注意维护此时的状态
    void dfs(int i) {
        vis[i] = true;
        v ++;
        e += g[i].size();

        for (auto &j: g[i]) {
            if (!vis[j]) dfs(j);
        }
    };
};
```

## 网格图 - DFS/BFS/并查集

网格图是一种特殊的图，图中的点此时就是坐标（一般的图中的点一般都是编号）

网格图，不需要存邻接表或者邻接矩阵，因为每个点的邻接点是固定的（该点的上下左右四个方向的点，或者八个方向的点），所以我们可以直接利用方向数组，轻松得到当前点的邻接点

网格图技巧：网格图的搜索条件一般是 不越界 + 没有访问过 + 题目要求；

判断是否访问过，我们常用vis数组；但有的时候我们可以直接设置已搜格子的值来判断是否访问过；

思路：首先思考 已搜格子不影响搜索 网格值置为什么，已搜格子不影响一些其他的判断 网格值置为什么，如果不冲突那就选一个值即可，冲突的话就只能用vis数组

举个例子：

岛屿数量这道题目，搜索条件是g[x][y] = 1，为了已搜格子不影响搜索，可以把已搜格子的值g[x][y]置为非1的数；之后没有其他判断，所以可以直接设置已搜格子的值来代替vis数组

边界着色这道题目，为了已搜格子的值不影响搜索，g[a][b] != origin；这里还有其他判断，为了已搜格子的值不能影响边界判断，g[a][b]必须是原来的值；这里发生冲突了，无法通过只改变原来格子的值来达满足这两个条件，

所以必须使用vis数组，

题单：

https://leetcode.cn/circle/discuss/YiXPXW/

#### [200. 岛屿数量](https://leetcode.cn/problems/number-of-islands/)

看答案学习，思路：网格图内，找全为1的连通块的个数；遍历所有格子，统计全为1的连通块的个数；该题也是flood fill算法的模板题； 一题多解

DFS:

```cpp
class Solution {
public:
    vector<vector<char>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    int numIslands(vector<vector<char>>& grid) {
        g = grid;
        n = grid.size(), m = grid[0].size();

        // 遍历所有格子，找全为1的连通块数
        int cnt = 0;
        for (int i = 0; i < n; i ++ )
            for (int j = 0; j < m; j ++ )
                if (g[i][j] == '1') {
                    dfs(i, j);
                    cnt ++;
                }
        return cnt;
    }

    void dfs(int x, int y) {
        g[x][y] = '2';   // 可以省略vis数组，直接设置网格图的值来判断是否访问过
        for (int i = 0; i < 4; i ++ ) {
            int a = x + dx[i], b = y + dy[i];
            if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] == '1')
                dfs(a, b);
        }
    }
};
```

BFS:

```cpp
class Solution {
public:
    typedef pair<int, int> pii;
    vector<vector<char>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    queue<pii> q;
    int numIslands(vector<vector<char>>& grid) {
        g = grid;
        n = grid.size(), m = grid[0].size();
        
        // 遍历所有格子，找全为1的连通块数
        int cnt = 0;
        for (int i = 0; i < n; i ++ )
            for (int j = 0; j < m; j ++ )
                if (g[i][j] == '1') {
                    bfs(i, j);
                    cnt ++;
                }
        return cnt;
    }

    void bfs(int sx, int sy) {
        q.push({sx, sy});
        g[sx][sy] = '2';
        while (q.size()) {
            auto t = q.front(); q.pop();
            int x = t.first, y = t.second;
            for (int i = 0; i < 4; i ++) {
                int a = x + dx[i], b = y + dy[i];
                if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] == '1') {
                    q.push({a, b});
                    g[a][b] = '2';
                }
            } 
        }
    }
};
```

#### [695. 岛屿的最大面积](https://leetcode.cn/problems/max-area-of-island/)

AC，思路：其实就是网格图中统计最大连通块的点数；一题多解

DFS:

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        g = grid;
        n = grid.size(), m = grid[0].size();

        int ans = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if (g[i][j] == 1) {
                    ans = max(ans, dfs(i, j));
                }
            }
        }

        return ans;
    }

    // 当前点所在的连通块的总点数
    int dfs(int x, int y) {
        g[x][y] = 2;
        int cnt = 1;
        for (int i = 0; i < 4; i ++) {
            int a = x + dx[i], b = y + dy[i];
            if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] == 1) {
                cnt += dfs(a, b);
            }
        }
        return cnt;      
    }
};
```

BFS

```cpp
class Solution {
public:
    typedef pair<int, int> pii;
    vector<vector<int>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    queue<pii> q;
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        g = grid;
        n = grid.size(), m = grid[0].size();

        int ans = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if (g[i][j] == 1) {
                    ans = max(ans, bfs(i, j));
                }
            }
        }

        return ans;
    }

    // bfs统计该点所在的连通块的节点数
    int bfs(int sx, int sy) {
        q.push({sx, sy});
        g[sx][sy] = 2;
        int cnt = 0;

        while (q.size()) {
            auto t = q.front(); q.pop();
            int x = t.first, y = t.second;
            cnt ++;
            for (int i = 0; i < 4; i ++) {
                int a = x + dx[i], b = y + dy[i];
                if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] == 1) {
                    q.push({a, b});
                    g[a][b] = 2;
                }
            }
        }

        return cnt;
    }
};
```

#### [面试题 16.19. 水域大小](https://leetcode.cn/problems/pond-sizes-lcci/)

看答案学习，思路：这个题的难点在于我们现在不是上下左右四个方向了，而是八个方向；八个方向可以直接枚举周围的坐标，八方向模板题！

DFS：

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n, m;
    vector<int> pondSizes(vector<vector<int>> &land) {
        g = land;
        n = land.size(), m = land[0].size();
        
        vector<int> ans;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                if (g[i][j] == 0) // dfs或者bfs使用的是g，那么这里一定也要用g！
                    ans.push_back(dfs(i, j));
        
        sort(ans.begin(), ans.end());
        return ans;
    }

    int dfs(int x, int y) {
        g[x][y] = 2; // 标记 (x,y) 被访问，避免重复访问
        int cnt = 1;

        // 访问八方向的 0
        for (int a = x - 1; a <= x + 1; a ++)
            for (int b = y - 1; b <= y + 1; b ++) 
                if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] == 0) 
                    cnt += dfs(a, b);
        return cnt;
    }
};
```

BFS:

```cpp
class Solution {
public:
    typedef pair<int, int> pii;
    vector<vector<int>> g;
    int n, m;
    queue<pii> q;
    vector<int> pondSizes(vector<vector<int>> &land) {
        g = land;
        n = land.size(), m = land[0].size();
        
        vector<int> ans;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                if (g[i][j] == 0) // dfs或者bfs使用的是g，那么这里一定也要用g！
                    ans.push_back(bfs(i, j));
        
        sort(ans.begin(), ans.end());
        return ans;
    }

    int bfs(int sx, int sy) {
        q.push({sx, sy});
        g[sx][sy] = 1;
        int cnt = 0;
        while (q.size()) {
            auto t = q.front(); q.pop();
            cnt ++;
            int x = t.first, y = t.second;
            for (int a = x - 1; a <= x + 1; a ++) {
                for (int b = y - 1; b <= y + 1; b ++) {
                    if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] == 0) {
                        q.push({a, b});
                        g[a][b] = 1;
                    } 
                }
            }
        }
        return cnt;
    }
};
```

#### [463. 岛屿的周长](https://leetcode.cn/problems/island-perimeter/)

NOT AC, 思路：还是找到连通块，但是这里是统计连通块的周长，这里利用贡献法，统计每个格子对周长的贡献，统计的方式：遍历每个陆地格子，看其四个方向（对应4个边）是否为边界或者水域，如果是将这条边的贡献（即 1）加入答案ans中

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    int ans = 0;
    int islandPerimeter(vector<vector<int>>& grid) {
        g = grid, n = grid.size(), m = grid[0].size();

        // 遍历图，找连通块
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if (g[i][j] == 1) {
                    dfs(i, j);
                    break;
                }
            }
        }
        return ans;
    }

    // 遍历连通块时，利用贡献法统计每个格子对周长的贡献
    void dfs(int x, int y) {
        g[x][y] = 2;
        for (int i = 0; i < 4; i ++) {
            int a = x + dx[i], b = y + dy[i];
            // 统计当前格子对周长的贡献
            if (a < 0 || a >= n || b < 0 || b >= m || g[a][b] == 0) ans ++;
            // 搜索邻接格子
            else if (g[a][b] == 1) dfs(a, b);
        }
    }
};
```

#### [2658. 网格图中鱼的最大数目](https://leetcode.cn/problems/maximum-number-of-fish-in-a-grid/)

AC, 思路：还是连通块相关，这里需要统计连通块内所有格子的参数和

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    int findMaxFish(vector<vector<int>>& grid) {
        g = grid, n = grid.size(), m = grid[0].size();
        
        int ans = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if (g[i][j] != 0) {
                    ans = max(ans, dfs(i, j));
                }
            }
        }

        return ans;
    }

    int dfs(int x, int y) {
        int cnt = g[x][y];
        g[x][y] = 0;
        for (int i = 0; i < 4; i ++) {
            int a = x + dx[i], b = y + dy[i];
            if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] > 0) {
                cnt += dfs(a, b);
            }
        }
        return cnt;
    }
};
```

#### [1034. 边界着色](https://leetcode.cn/problems/coloring-a-border/)

NOT AC, 思路：这题的难点在于如何判断连通块边界，跟周长那题的判断有点类似，但是有些区别；然后重点注意：这里必须使用vis数组，因为已搜格子的值不能影响搜索，g[a][b] != origin, 已搜格子的值不能影响边界判断，g[a][b] = origin，所以我们无法通过只改变原来格子的值来达满足这两个条件！

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    vector<pair<int, int>> target;
    vector<vector<bool>> vis;
    int origin;

    vector<vector<int>> colorBorder(vector<vector<int>>& grid, int row, int col, int color) {
        g = grid, n = grid.size(), m = grid[0].size();
        origin = g[row][col];
        vis = vector<vector<bool>>(n, vector<bool>(m, false));
        dfs(row, col);
        for (auto &[x, y]: target) {
            g[x][y] = color;
        }
        return g;
    }

    void dfs(int x, int y) {
        vis[x][y] = true;
        bool is_border = false;
        for (int i = 0; i < 4; i ++) {
            int a = x + dx[i], b = y + dy[i];
            if (a < 0 || a >= n || b < 0 || b >= m || g[a][b] != origin) {
                is_border = true;
            }
            else if (!vis[a][b]) {
                dfs(a, b);
            }
        }

        if (is_border) target.push_back({x, y});
    }
};
```

#### [1020. 飞地的数量](https://leetcode.cn/problems/number-of-enclaves/)

NOT AC, 思路：很经典的题目，多源BFS或者DFS来做；

基本思路：

从矩形边界上的1出发，深搜遍历所有与其相邻的1，并将它们置为0，以表示它们不可能为飞地。

遍历所有网格，统计剩余1的数量即为答案。

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    int numEnclaves(vector<vector<int>>& grid) {
        g = grid, n = grid.size(), m = grid[0].size();
        
        // 先把边界上的1通过DFS泛洪成0，排除干扰
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if ((i == 0 || j == 0 || i == n - 1 || j == m - 1) && g[i][j] == 1) {
                    dfs(i, j);
                }
            }
        }
        
        // 遍历所有网格，找还为1的格子即为飞地
        int ans = 0;
        for (int i = 1; i < n - 1; i ++) {
            for (int j = 1; j < m - 1; j ++) {
                if (g[i][j] == 1) ans ++;
            }
        }
        return ans;
    }

    void dfs(int x, int y) {
        g[x][y] = 0;
        for (int i = 0; i < 4; i ++) {
            int a = x + dx[i], b = y + dy[i];
            if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] == 1) {
                dfs(a, b);
            }
        }
    }
};
```

#### [1254. 统计封闭岛屿的数目](https://leetcode.cn/problems/number-of-closed-islands/)

NOT AC，思路和飞地那题很像，也是先排除边界的干扰，然后正常求连通块个数

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    int closedIsland(vector<vector<int>>& grid) {
        g = grid, n = grid.size(), m = grid[0].size();

        // 先把边界上的0通过DFS泛洪成1，排除干扰
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if ((i == 0 || j == 0 || i == n - 1 || j == m - 1) && g[i][j] == 0) {
                    dfs(i, j);
                }
            }
        }

        // 然后再对内部的0进行泛洪，能泛洪几次就有几个封闭岛屿
        int ans = 0;
        for (int i = 1; i < n - 1; i ++) {
            for (int j = 1; j < m - 1; j ++) {
                if (g[i][j] == 0) {
                    ans ++;
                    dfs(i, j);
                }
            }
        }
        return ans;
    }

    void dfs(int x, int y) {
        g[x][y] = 1;
        for (int i = 0; i < 4; i ++) {
            int a = x + dx[i], b = y + dy[i];
            if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] == 0) {
                dfs(a, b);
            }
        }
    }
};
```

#### [130. 被围绕的区域](https://leetcode.cn/problems/surrounded-regions/)

AC，思路：跟飞地和封闭岛屿基本是一样的做法，先边界泛洪，然后再遍历矩阵找"飞地“; 这里注意如果不使用vis数组，已搜格子的值既不能影响搜索 != 'O', 也不能影响之后的还原 != 'X';

使用vis数组

```cpp
class Solution {
public:
    vector<vector<char>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    vector<vector<bool>> vis;
    void solve(vector<vector<char>>& board) {
        g = board, n = g.size(), m = g[0].size();
        vis = vector<vector<bool>>(n, vector<bool>(m, false));

        // 矩阵边界为O的格子泛洪
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if ((i == 0 || i == n - 1 || j == 0 || j == m - 1) && g[i][j] == 'O') {
                    dfs(i, j);
                }
            }
        }

        // 遍历矩阵，排除掉之前泛洪的格子
        for (int i = 1; i < n - 1; i ++) {
            for (int j = 1; j < m - 1; j ++) {
                if (g[i][j] == 'O' && !vis[i][j]) {
                    g[i][j] = 'X';
                }
            }
        }

        board = g;
    }

    void dfs(int x, int y) {
        vis[x][y] = true;
        for (int i = 0; i < 4; i ++) {
            int a = x + dx[i], b = y + dy[i];
            if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] == 'O') {
                if (!vis[a][b]) dfs(a, b);
            }
        }
    }
};
```

不使用vis数组

```cpp
class Solution {
public:
    vector<vector<char>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    vector<vector<bool>> vis;
    void solve(vector<vector<char>>& board) {
        g = board, n = g.size(), m = g[0].size();
        vis = vector<vector<bool>>(n, vector<bool>(m, false));

        // 矩阵边界为O的格子泛洪
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if ((i == 0 || i == n - 1 || j == 0 || j == m - 1) && g[i][j] == 'O') {
                    dfs(i, j);
                }
            }
        }

        // 遍历矩阵，找到围绕区域
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if (g[i][j] == 'O') g[i][j] = 'X';
                else if (g[i][j] == 't') g[i][j] = 'O';
            }
        }

        board = g;
    }

    void dfs(int x, int y) {
        g[x][y] = 't';
        for (int i = 0; i < 4; i ++) {
            int a = x + dx[i], b = y + dy[i];
            if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] == 'O') {
                dfs(a, b);
            }
        }
    }
};
```

#### [542. 01 矩阵](https://leetcode.cn/problems/01-matrix/)

NOT AC, 思路：网格图中多源BFS运用的模板题；

题目的要求简要就是每个1找最近的0；找最短路BFS

如果只有一个0，那么直接从这个0作为源点做BFS，统计其他格子到源点的距离；

但这里有多个0，所以我们把多个0作为源点；这里引入超级源点，其他格子到最近0的距离 = 其他格子到超级源点的距离 - 1；初始状态，超级源点会出队，多源点入队，dist（超级源点） = 1，因为最近0的距离 = 其他格子到超级源点的距离 - 1；所以初始化 多源点入队，dist（最近0） = 0；

ps: BFS最短路模板，一般不用vis数组，也不需要改变g格子的值来代替vis数组，因为dist数组既可以统计距离也可以代替vis数组

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};

    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        g = mat, n = mat.size(), m = mat[0].size();
        vector<vector<int>> dist(n, vector<int>(m, -1));
        typedef pair<int, int> pii;
        queue<pii> q;

        // 多源BFS
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if(g[i][j] == 0) {
                    q.emplace(i, j);
                    dist[i][j] = 0;
                }
            }
        }
        
        while (q.size()) {
            auto [x, y] = q.front(); q.pop();
            for (int i = 0; i < 4; i ++) {
                int a = x + dx[i], b = y + dy[i];
                if (a >= 0 && a < n && b >= 0 && b < m && dist[a][b] == -1) {
                    q.emplace(a, b);
                    dist[a][b] = dist[x][y] + 1;
                }
            }
        }

        return dist;
    }
};
```

使用vis数组的话，只需要把dist == -1的地方改成用vis判断，然后加上标记过程即可

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};

    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        g = mat, n = mat.size(), m = mat[0].size();
        vector<vector<bool>> vis(n, vector<bool>(m, false));
        vector<vector<int>> dist(n, vector<int>(m, 0));
        typedef pair<int, int> pii;
        queue<pii> q;

        // 多源BFS
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if(g[i][j] == 0) {
                    q.emplace(i, j);
                    vis[i][j] = true;
                }
            }
        }
        
        while (q.size()) {
            auto [x, y] = q.front(); q.pop();
            for (int i = 0; i < 4; i ++) {
                int a = x + dx[i], b = y + dy[i];
                if (a >= 0 && a < n && b >= 0 && b < m && !vis[a][b]) {
                    q.emplace(a, b);
                    vis[a][b] = true;
                    dist[a][b] = dist[x][y] + 1;
                }
            }
        }

        return dist;
    }
};
```

#### [994. 腐烂的橘子](https://leetcode.cn/problems/rotting-oranges/)

AC, 思路：多源BFS的模板题，求最少时间其实就是多源BFS后统计每个新鲜橘子所在的格子和腐烂橘子（源点）的最短距离，然后拿到最大值；

ps: 网格图里很多问题其实都是flood fill，如果flood fill里只是需要遍历那么倾向于DFS求解，如果同时要统计每个格子和源点的最短路，那么肯定用BFS求解；

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    typedef pair<int, int> pii;
    int orangesRotting(vector<vector<int>>& grid) {
        g = grid, n = grid.size(), m = grid[0].size();
        
        // 多源BFS
        queue<pii> q;
        vector<vector<int>> dist(n, vector<int>(m, -1));
        
        int fresh = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if (g[i][j] == 2) {
                    q.emplace(i, j);
                    dist[i][j] = 0;
                }
                else if (g[i][j] == 1) fresh ++;
            }
        }

        int ans = 0;
        while(q.size()) {
            auto [x, y] = q.front(); q.pop();
            for (int i = 0; i < 4; i ++) {
                int a = x + dx[i], b = y + dy[i];
                if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] == 1 && dist[a][b] == -1) {
                    q.emplace(a, b);
                    dist[a][b] = dist[x][y] + 1;
                    ans = max(ans, dist[a][b]);
                    fresh --;
                }
            }
        }   

        return fresh > 0  ? -1 : ans; 
    }
};
```

如果不想用dist数组来判断重复搜索，可以直接修改g[x][y]的值为！=1的值，来作为判断条件，不过这样写意义不大，因为dist数组还是要统计最短路

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int n, m;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    int orangesRotting(vector<vector<int>>& grid) {
        g = grid, n = grid.size(), m = grid[0].size();
        
        // 多源BFS
        typedef pair<int, int> pii;
        queue<pii> q;
        vector<vector<int>> dist(n, vector<int>(m, 0));
        
        int fresh = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if (g[i][j] == 2) {
                    q.emplace(i, j);
                    dist[i][j] = 0;
                }
                else if (g[i][j] == 1) fresh ++;
            }
        }

        int ans = 0;
        while(q.size()) {
            auto [x, y] = q.front(); q.pop();
            for (int i = 0; i < 4; i ++) {
                int a = x + dx[i], b = y + dy[i];
                if (a >= 0 && a < n && b >= 0 && b < m && g[a][b] == 1) {
                    q.emplace(a, b);
                    g[a][b] = 2;
                    dist[a][b] = dist[x][y] + 1;
                    ans = max(ans, dist[a][b]);
                    fresh --;
                }
            }
        }   

        return fresh > 0  ? -1 : ans; 
    }
};
```

#### [2684. 矩阵中移动的最大次数](https://leetcode.cn/problems/maximum-number-of-moves-in-a-grid/)

AC，思路：还是多源BFS求解，将第一列都放入队列，然后做多源BFS

```cpp
class Solution {
public:
    typedef pair<int, int> pii;
    int maxMoves(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();

        // 多源BFS
        queue<pii> q;
        vector<vector<int>> dist(m, vector<int>(n, -1));
        for (int i = 0; i < m; i ++) {
            q.emplace(i, 0);
            dist[i][0] = 0;
        }

        int ans = 0;
        while(q.size()) {
            auto [x, y] = q.front(); q.pop();
            for (int dx = -1; dx <= 1; dx ++) {
                int a = x + dx, b = y + 1;
                if (a >= 0 && a < m && b >= 0 && b < n && grid[a][b] > grid[x][y] && dist[a][b] == -1) {
                    q.emplace(a, b);
                    dist[a][b] = dist[x][y] + 1;
                    ans = max(ans, dist[a][b]);
                }
            }
        }
        return ans;
    }
};
```

## 拓扑排序

讲解：

<img src="/assets/MS9sbpG8YoEznQxb13Ec7tmbnLR.png" src-width="1143" src-height="571" align="center"/>

<img src="/assets/NSrdbc19Kop301xefBFcv8Csn4g.png" src-width="1160" src-height="637" align="center"/>

<img src="/assets/NOPAbFobwoWd6oxJOUUcF1VYnBh.png" src-width="1161" src-height="613" align="center"/>

<img src="/assets/SqiabPpMEoEXpgx8x9ZcGEB6ndh.png" src-width="1154" src-height="581" align="center"/>

yxc讲解：只有有向无环图才存在拓扑排序，简单来讲如果一个序列是拓扑序列，水平绘图的话，它只会存在向后的边，不会存在向前的边；
https://www.acwing.com/activity/content/code/content/47106/

acm模式 模板：

```cpp
const int N = 10000;    // 最大点数
vector<int> g[N + 1];   // 邻接表存图，为什么N + 1，因为节点编号从1开始
int n, m                // 点数，边数
int q[N + 1], d[N + 1]; // 队列，入度数组

void topoSort() 
{
    int front = 1, rear = 0;
    for (int i = 1; i <= n; i ++) {// 遍历所有节点
        if (!d[i]) q[++rear] = i;  // 入度为0的节点入队
    }
    
    while (front <= rear) {
        int x = q[front]; ++ front;  // 弹出队头节点
        for (auto y: g[x]) {         // 遍历x点的每个邻接点y点
            --d[y];                  // 删掉连向y点的的边，
            if (--d[y] == 0) {       // 此时y点的入度是否为0
                q[++rear] = y;       // 如果y点的入度为0，入队
        }
    }
    
    if (rear == n) {        // 弹出的点在 1 ~ rear；如果弹出点数 = 图中点数，说明存在拓扑序列
        for (int i = 1; i <= n; i ++) cout << q[i] << " ";  // 输出拓扑序列
    }
    else cout << -1 << endl;
}
```

leetcode模式 模板：直接看 leetcode207课程表

题单：

https://leetcode.cn/circle/discuss/01LUak/

#### 848. 有向图的拓扑序列

AC，思路：拓扑排序ACM模式的模板题，用于日常复习

```cpp
#include <bits/stdc++.h>

using namespace std;

// acm模式邻接表存图固定写法
const int N = 1e5;    // 最大点数
vector<int> g[N + 1];  // 邻接表存图
int n, m;             // 点数，边数

// 拓扑序列 还需要使用入度数组和队列
int q[N + 1], d[N + 1]; // 队列和入度数组



void topoSort() {
    int front = 1, rear = 0;
    for (int i = 1; i <= n; i ++) {
        if (!d[i]) q[++rear] = i;
    }
    
    while (front <= rear) {
        auto x = q[front]; front ++;
        for (auto y: g[x]) {
            -- d[y];         // 删除连向y点的边
            if (d[y] == 0) { // 如果此时y点入队为0，入队
                q[++rear] = y;
            } 
        }
    }
    
    if (rear == n) {        // 弹出的点在 1 ~ rear
        for (int i = 1; i <= n; i ++) cout << q[i] << " ";
    }
    else cout << -1 << endl;
}


int main()
{
    int k;    // m已经用来存边数了，所以这里用k来存输入
    cin >> n >> k;
    
    // 读边 建图
    while (k --) {
        int x, y;
        cin >> x >> y;
        g[x].push_back(y);
        d[y] ++;    // 不要忘了更新入度数组！！！
    }
    
    topoSort();
    
    return 0;
}
```

#### [1557. 可以到达所有点的最少点数目](https://leetcode.cn/problems/minimum-number-of-vertices-to-reach-all-nodes/)

AC，思路：拓扑排序的前置题目，其实就是找拓扑排序中，队列S里的点；

```cpp
class Solution {
public:
    vector<vector<int>> g;   // 邻接表存图
    int n, m;                // 点数，边数
    vector<int> d;           // 入度数组
    vector<int> findSmallestSetOfVertices(int n_, vector<vector<int>>& edges) {
        int n = n_, m = edges.size();
        g.resize(n); d.resize(n, 0);

        // 读 边数组建图 存入邻接表
        for (auto& e: edges) {
            int x = e[0], y = e[1];
            g[x].push_back(y);
            d[y] ++;  // 更新入读数组
        }

        // 找入度为0的点加入答案
        vector<int> ans;
        for (int i = 0; i < n; i ++) {
            if (!d[i]) {
                ans.push_back(i);
            }
        }
        return ans;
    }
};
```

#### [207. 课程表](https://leetcode.cn/problems/course-schedule/)

AC，思路：拓扑排序模板题，利用拓扑排序判断图中是否有环

```cpp
class Solution {
public:
    vector<vector<int>> g;   // 邻接表
    int n, m;                // 点数，边数
    vector<int> d;           // 入度数组
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        n = numCourses, m = prerequisites.size();
        g.resize(n); d.resize(n);
        
        // 读 边数组建图 存入邻接表
        for (auto& e: prerequisites) {
            int x = e[0], y = e[1];
            g[x].push_back(y);
            ++d[y];  // 拓扑排序需要统计每个点的入度
        }

        // 拓扑排序
        queue<int> q;
        // 入度为0的点加入队列s
        for (int i = 0; i < n; i ++) {
            if (!d[i]) q.push(i);
        }

        int cnt = 0;   // 统计队列s中弹出的点数，如果为n代表没有环
        while (q.size()) {
            auto x = q.front(); q.pop();  // 队列s中选择一个点弹出
            cnt ++;
            for (auto y: g[x]) {
                // 删除相连的边，邻接点度数 - 1，如果度数为0，加入队列l
                if (--d[y] == 0) q.push(y);  
            }
        }

        return cnt == n;
    }
};
```

## 最短路

### <b>bellman-ford</b>

最短路问题：

<img src="/assets/HyApbEgtho0KvaxJ8FWc8Gyknef.png" src-width="1153" src-height="606" align="center"/>

bellman-ford讲解：

<img src="/assets/AnjLbiLPnoDbawxiLTtcVOKjnZf.png" src-width="1150" src-height="587" align="center"/>

<img src="/assets/Nlo4bac4Zom5sCx48acc5MvFn0f.png" src-width="1153" src-height="597" align="center"/>

<img src="/assets/JOvDbuktLovm1px4FQHcWLkBnuh.png" src-width="1160" src-height="554" align="center"/>

<img src="/assets/QDWLb86PLowXCnxv5VKcXIeTnid.png" src-width="1170" src-height="595" align="center"/>

<img src="/assets/KJR7bW0lYo56GfxGTi9ciRBon2d.png" src-width="1168" src-height="605" align="center"/>

<img src="/assets/SFCgbYWrhocWH9xeuwNcsDy8nC7.png" src-width="1153" src-height="640" align="center"/>

bellman-ford算法总结：

bellman-ford算法有点类似于BFS找最短路，BFS是每次循环，最短路走一步，找到距离+1的点；而bellman-ford是每次迭代（枚举所有边，松弛操作），最短路至少走一步（注意这里是至少走一步，最短路的边数至少加一），也就是说迭代i次的时候，我们至少可以固定最短路边数为i的点的最短路（固定是说，之后的迭代里这些点的最短路还是可以更新的）

最短路存在的情况下，如果有n个点，源点到每个顶点的最短路边数最多为n - 1，所以n - 1次迭代后，可以找到源点到每个顶点的最短路；

bellman-ford算法应用：

(1) bellman-ford算法最经典的应用，就是在限制最短路最大边数的情况下，求最短路

(2) 判断是存在负环，如果一个图有n个点，m条边，

当从S点出发能到达一个负环时，就会进行n轮以上的迭代，也就是说第n次迭代的时候会更新

所以暴力做法就是 对每个点作为源点，做一次bellman-ford，然后如果出现第n次迭代更新，那么存在负环，时间复杂度O(n^2 * m)；

超级源点优化：我们可以添加一个超级源点，然后将超级源点和所有点连权值为0的边，那么我们就可以直接从超级源点做一次bellman-ford，此时如果存在最短路，最多会进行n次迭代，所以如果第n + 1次迭代更新，存在负环；上面的是显示添加超级源点，但其实对于超级源点我们可以隐式添加，隐式添加超级源点，就是添加超级源点后，直接迭代一次，此时所有顶点的dist为0，然后已经进行了一次迭代，还剩下n - 1次迭代；所以问题就转化为，初始顶点dist = 0，然后如果第n次迭代时还存在更新，存在负环，其实理念和多源BFS比较类似！

以上也是bellman-ford的模板题

bellman-ford模板：直接看模板题 
853. 有边数限制的最短路 
[787. K 站中转内最便宜的航班](https://leetcode.cn/problems/cheapest-flights-within-k-stops/)

#### [853. 有边数限制的最短路](https://www.acwing.com/problem/content/855/)

AC，思路：bellman-ford的模板题，看代码注释

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 500, M = 1e4;   // N最大点数，M最大边数
struct Edge {
    int x, y, v;
} edge[M + 1];   // 因为枚举边不要求顺序，所以直接边集数组存图

int n, m, k;    // 点数，边数，最短路边数限制
int dist[N + 1], last[N + 1];   // 距离数组 dist[i] 1到i的距离 last[i] 备份当前迭代开始时的dist[i]

void bellman_ford()
{
    memset(dist, 0x3f3f3f3f, sizeof(dist));   // 初始化所有顶点的距离为极大值
    dist[1] = 0;                              // 源点到源点的距离当然是0
    
    // 最多进行k次迭代
    for (int i = 0; i < k; i ++) {
        memcpy(last, dist, sizeof dist);   // 备份当前迭代开始时的dist数组
        
        // 枚举所有边
        for (int j = 0; j < m; j ++) {
            int x = edge[j].x, y = edge[j].y, v = edge[j].v;
            // 只有起点已经被更新了，才可以进行松弛操作
            if (last[x] != 0x3f3f3f3f && last[x] + v < dist[y]) {
                dist[y] = last[x] + v;
            }
        }
    }
    
    if (dist[n] == 0x3f3f3f3f) cout << "impossible" << endl;
    else cout << dist[n] << endl;
}

int main()
{
    cin >> n >> m >> k;
    
    for (int i = 0; i < m; i ++) {
        cin >> edge[i].x >> edge[i].y >> edge[i].v; 
    }
    
    bellman_ford();
    
    return 0;
}
```

#### [787. K 站中转内最便宜的航班](https://leetcode.cn/problems/cheapest-flights-within-k-stops/)

AC，思路：bellman-ford找有边数限制的最短路的模板题

```cpp
class Solution {
public:
    const int INF = 1e6;
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        vector<int> dist(n, INF);
        dist[src] = 0;

        for (int i = 0; i < k + 1; i ++) {
            auto last = dist;
            for (auto& e: flights) {
                int x = e[0], y = e[1], v = e[2];
                if (last[x] != INF) dist[y] = min(dist[y], last[x] + v);
            }
        }
        if (dist[dst] == INF) return -1;
        return dist[dst];
    }
};
```

#### 852. spfa判断负环

思路：这题虽然是spfa判断负环，但是我们可以直接使用bellman-ford来判断负环

```cpp
#include <bits/stdc++.h>

using namespace std;

const int INF = 1e8;

struct Edge {
    int u, v, w; // 起点u, 终点v, 权重w
};


bool detectNegativeCycle(int n, int m, const vector<Edge>& edges) {
    // 初始化距离数组，dist[i] 表示从隐式超级源点到 i 号点的最短距离
    vector<int> dist(n + 1, 0);  // 初始化所有点的距离为 0，相当于超级源点出发迭代了一次

    // 如果存在最短路，还需要进行n - 1次迭代，如果存在负环第n次迭代后会更新，所以迭代n次
    for (int i = 1; i <= n; i ++) {
        bool updated = false;
        // 枚举所有边
        for (const auto& edge : edges) {
            int u = edge.u, v = edge.v, w = edge.w;
            // 松弛操作
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                updated = true;  // 最短路更新
            }
        }
        // 如果在第n轮还可以更新，说明存在负权环
        if (i == n && updated) {
            return true;
        }
    }
    return false;
}

int main() {
    int n, m;
    cin >> n >> m;
    vector<Edge> edges(m);
    
    for (int i = 0; i < m; ++i) {
        cin >> edges[i].u >> edges[i].v >> edges[i].w;
    }

    if (detectNegativeCycle(n, m, edges)) cout << "Yes" << endl;
    else cout << "No" << endl;

    return 0;
}
```

### <b>Dijkstra</b>

讲解:

<img src="/assets/Ic7hb9QZboo8TrxL6QlcCtkHnXf.png" src-width="2456" src-height="1342" align="center"/>

<img src="/assets/Sp0Vbp5gBoCqbwxd3ticfoL7npM.png" src-width="2406" src-height="1165" align="center"/>

<img src="/assets/BrhPbJHoWoQxBmxgyNPcHuYenrf.png" src-width="2435" src-height="1298" align="center"/>

<img src="/assets/SZb0bYTQKoj0o9xW4ZhcWtSqnKb.png" src-width="2411" src-height="1352" align="center"/>

<img src="/assets/WWnKbw1k9orbSVxhJvGcCRr8n7b.png" src-width="2414" src-height="1079" align="center"/>

<img src="/assets/AEQHbwC2Zon9rRxe167c8amznBb.png" src-width="2350" src-height="1284" align="center"/>

<img src="/assets/R9BKbYrEhoKgYUxsqdJcJlY0n5g.png" src-width="2428" src-height="1357" align="center"/>

伪代码

<img src="/assets/M63yb8dQUoCW03x16IAcbTtTnBd.png" src-width="1329" src-height="474" align="center"/>

```cpp
初始化  集合C为空，dist[] = INF, dist[1] = 0;

for 1 ~ n:
    找当前不在C中距离源点最近的点x的最短路
    if (x是终点 || 找不到x）break;
    将x放入C中
    对x的出边做松弛操作

每次循环，可以找到一个点的最短路；找不到t意味着找不到当前点的最短路，后面点的的最短路也无法找到，直接退出循环
```

代码模板：

直接看模板题 AcWing 849. Dijkstra求最短路 I

注意：

1. 如果我们严格地 不允许将距离为无穷的点加入C中，那么找不到x对应的情况就是x = -1；
2. 如果我们允许将无穷点加入C中，那么找不到x对应的情况就是dist[x] = inf；

两种写法都是可以的，我个人喜欢第二种

松弛操作的溢出问题

对一个x-&gt;y的边的松弛操作 dist[y] = min(dist[y], dist[x] + l(x, y)); 其中dist[x] + l(x, y)是有可能溢出的，为了防止溢出，我们可以有两种解决办法

1. 直接将inf设为极大值，而不是最大值，常见的是INT_MAX / 2，或者是0x3f3f3f3f；这样我们达到了无穷的效果，同时也确保了加法不会溢出
2. 只有dist[x] != inf的时候，才进行松弛操作，这样就可以确保不会溢出，同时也是遵循了算法的意义，因为dist[x]= inf代表x没有找到最短路，对它进行松弛操作也是没有意义的；

堆优化dijkstra：

之前的朴素dijkstra算法，时间复杂度是O(n^2 + m)，我们尝试对找到距离最小的点的最短路这一步进行优化，我们可以用最小堆去存可能是距离最小的点；由于点有可能多次入堆，所以堆最大是m，这样就可以把时间复杂度优化成O(mlogm); 对于稀疏图来说，效率还是更高的；

代码模板就直接看 模板题 850 dijkstra求最短路2

#### [AcWing 849. Dijkstra求最短路 I](https://www.acwing.com/problem/content/851/)

AC，思路：dijkstra的模板题；主要就是注意最标准的写法

```cpp
#include <bits/stdc++.h>

using namespace std;

const int inf = INT_MAX;   // 正无穷
int n, m;  // 点数，边数
vector<vector<int>> g;  // 邻接矩阵存稠密图
vector<int> dist;       // 距离数组
vector<bool> st;        // 已经找到最短路的顶点集合

void dijkstra() 
{
    // 初始化 集合和dist数组，源点到源点的dist = 0;
    dist.resize(n + 1, inf);
    st.resize(n + 1, false);
    dist[1] = 0;
    
    // 循环n次，每次找到一个点的最短路
    for (int i = 1; i <= n; i ++) {
        // 找不在集合中，dist最小的点的最短路
        int x = -1;
        for (int j = 1; j <= n; j ++) {
            if (!st[j] && (x == -1 || dist[j] < dist[x])) {
                x = j;
            }
        }
        
        // dist[x] = inf说明，没有找到x的最短路，后面的也无法找到，直接结束循环
        if (dist[x] == inf) break;
        
        // 找到x的最短路，加入集合，然后对x的出边做松弛操作
        st[x] = true;
        for (int y = 1; y <= n; y ++) {
            // 这里是邻接矩阵，所以出边需要多个条件 g[x][y] != inf
            if (g[x][y] != inf) dist[y] = min(dist[y], dist[x] + g[x][y]);
        }
    }
    
    if (dist[n] == inf) cout << -1 << endl;
    else cout << dist[n] << endl;
}

int main()
{
    cin >> n >> m;
    
    g.resize(n + 1, vector<int>(n + 1, inf));

    for (int i = 1; i <= m; i ++) {
        int x, y, z;
        cin >> x >> y >> z;
        // 邻接矩阵的话，无法存重边，所以直接存min，如果是邻接表和边集数组可以存重边，不需要这么处理
        // 自环的话，因为松弛操作是取min，不会影响dist;
        g[x][y] = min(g[x][y], z);  
    }
    
    dijkstra();
    
    return 0;
}
```

#### <u>AcWing 850. Dijkstra求最短路 II</u>

AC, 思路：堆优化的dijkstra，优化了找距离最近的x的最短路这一操作；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int inf = INT_MAX;
int n, m;
vector<vector<pair<int, int>>> g;
vector<int> dist;
priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> heap;  // 最小堆


void dijkstra()
{
    dist.resize(n + 1, inf);
    dist[1] = 0;
    heap.emplace(0, 1);   // 源点入堆
    
    while (heap.size()) {
        auto [dx, x] = heap.top(); heap.pop();
        if (dx > dist[x]) continue;  // x在之前已经找到最短路了，跳过
        
        // 对x的出边做松弛操作
        for (auto& [y, z]: g[x]) {
            // 只有更小的最短路才会入堆
            if (dist[x] + z < dist[y]) {
                dist[y] = dist[x] + z;
                heap.emplace(dist[y], y);
            }
        }
    }
    
    if (dist[n] == inf) cout << -1;
    else cout << dist[n];
    
}

int main()
{
    cin >> n >> m;
    
    g.resize(n + 1);
    for (int i = 1; i <= m; i ++) {
        int x, y, z;
        cin >> x >> y >> z;
        g[x].emplace_back(y, z);
    }
    
    dijkstra();
    
    return 0;
}
```

#### [743. 网络延迟时间](https://leetcode.cn/problems/network-delay-time/)

AC，板子题

朴素dijkstra

```cpp
class Solution {
public:
    int networkDelayTime(vector<vector<int>>& times, int n, int k) {
        // 初始化 dijstra算法需要的东西
        const int inf = INT_MAX;
        int m = times.size();
        vector<vector<int>> g(n + 1, vector<int> (n + 1, inf));
        vector<int> dist(n + 1, inf);
        vector<bool> st(n + 1, false);

        // 邻接矩阵存图
        for (const auto& e: times) {
            int x = e[0], y = e[1], z = e[2];
            g[x][y] = min(g[x][y], z);
        }

        // dijkstra
        dist[k] = 0;
        for (int i = 0; i < n; i ++) {
            int x = -1;
            for (int j = 1; j <= n; j ++) {
                if (!st[j] && (x == -1 || dist[j] < dist[x])) 
                    x = j;
            }

            // 没有找到当前点的最短路，说明无法到达，直接返回-1
            if (dist[x] == inf) return -1;

            st[x] = true;
            for (int y = 1; y <= n; y ++) {
                if (g[x][y] != inf) dist[y] = min(dist[y], dist[x] + g[x][y]);
            }
        }

        // 此时，所有点可以找到最短路，找最长的最短路，就是传输时间
        return *max_element(dist.begin() + 1, dist.end());
    }
};
```

堆优化dijsktra

```cpp
class Solution {
public:
    int networkDelayTime(vector<vector<int>>& times, int n, int k) {
        // 初始化 dijstra算法需要的东西
        const int inf = INT_MAX;
        int m = times.size();
        vector<vector<pair<int, int>>> g(n + 1);
        vector<int> dist(n + 1, inf);
        // 最小堆
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> heap;

        // 邻接表阵存图
        for (const auto& e: times) {
            int x = e[0], y = e[1], z = e[2];
            g[x].emplace_back(y, z);
        }

        // dijkstra
        dist[k] = 0;
        heap.emplace(0, k);
        while (heap.size()) {
            // 找到距离最小的点x
            auto [dx, x] = heap.top(); heap.pop();
            if (dist[x] < dx) continue; // x之前出堆过，表示x已经找到最短路了

            // x的出边松弛操作
            for (auto& [y, z]: g[x]) {
                // 只有找到更小的最短路，才入堆
                if (dist[x] + z < dist[y]) {
                    dist[y] = dist[x] + z;
                    heap.emplace(dist[y], y);
                }
            }
            
        }

        // 此时并不是所有点都找到了最短路！所以需要判断是否找到了最短路
        int ans = *max_element(dist.begin() + 1, dist.end());
        return ans == inf ? -1 : ans;
    }
};
```

### 
### Floyd

讲解：

<img src="/assets/NuZCbYGiAoxKEZxa5GKcJBgEnDc.png" src-width="1162" src-height="557" align="center"/>

<img src="/assets/QOt1bujoJovpRuxYddocoEo2nfd.png" src-width="1150" src-height="582" align="center"/>

<img src="/assets/I0xMbdNkPoMrWHxJfV0c8bDkn7f.png" src-width="1878" src-height="995" align="center"/>

灵神的题解讲的更全面：https://leetcode.cn/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/solutions/2525946/dai-ni-fa-ming-floyd-suan-fa-cong-ji-yi-m8s51/

#### [AcWing 854. Floyd求最短路](https://www.acwing.com/problem/content/856/)

AC，思路：板子题，floyd的代码很短，但是写法比较巧妙，这里存图的邻接矩阵，距离数组，还有dp的状态数组都是用的同一个数组，所以代码比较简短；

```cpp
#include <bits/stdc++.h>

using namespace std;

const int inf = INT_MAX;
int n, m, q;
vector<vector<int>> f;   // 同时是邻接矩阵，距离数组，状态数组

// floyd算法 f[k][i][j] 表示从i到j的最短路长度，中间节点编号都≤k
void floyd()
{
    for (int k = 1; k <= n; k ++) {
        for (int i = 1; i <= n; i ++) {
            for (int j = 1; j <= n; j ++) {
                if (f[i][k] != inf && f[k][j] != inf)  // 如果i到k，k到j存在最短路，才进行更新
                    f[i][j] = min(f[i][j], f[i][k] + f[k][j]);
            }
        }
    }
}


int main()
{
    cin >> n >> m >> q;
    f.resize(n + 1, vector<int> (n + 1));
    for (int i = 1; i <= n; i ++) {
        for (int j = 1; j <= n; j ++) {
            if (i == j) f[i][j] = 0;   // 自己到自己的距离是0，这里是按照距离数组的意义
            else f[i][j] = inf;
        }
    }
    
    while (m--) {
        int x, y, z;
        cin >> x >> y >> z;
        f[x][y] = min(f[x][y], z);
    }
    
    floyd();
    
    while(q--) {
        int x, y;
        cin >> x >> y;
        if (f[x][y] == inf) cout << "impossible" << endl;
        else cout << f[x][y] << endl;
    }
    
    return 0;
}
```

#### [1334. 阈值距离内邻居最少的城市](https://leetcode.cn/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/)

AC，思路：转化一下题意，就是要求每个点到其他所有点的距离，然后统计当前点的到达个数，找最小到达个数的点，因为到达个数相等时，答案是最大的，所以找最小时使用&lt;= min_cnt，同时枚举每个点的时候从小到大；

```cpp
class Solution {
public:
    int findTheCity(int n, vector<vector<int>>& edges, int distanceThreshold) {
        // floyd算法需要的相关东西
        const int inf = INT_MAX;
        int m = edges.size();
        vector<vector<int>> f(n, vector<int>(n));
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < n; j ++) {
                if (i == j) f[i][j] = 0;
                else f[i][j] = inf;
            }
        }

        // 读边 存图
        for (auto& e: edges) {
            int x = e[0], y = e[1], z = e[2];
            f[x][y] = f[y][x] = z;   // 简单图，没有重边和自环
        }

        // floyd 
        for (int k = 0; k < n; k ++) {
            for (int i = 0; i < n; i ++) {
                for (int j = 0; j < n; j ++) {
                    if (f[i][k] != inf && f[k][j] != inf)
                        f[i][j] = min(f[i][j], f[i][k] + f[k][j]);
                }
            }
        }

        int ans = 0, min_cnt = n;
        for (int i = 0; i < n; i ++) {  // 遍历所有点
            int cnt = 0;
            for (int j = 0; j < n; j ++) {  // 统计距离限制能到达的点的个数
                if (j != i && f[i][j] <= distanceThreshold) cnt ++;
            }
            // 找到达个数最少的点
            if (cnt <= min_cnt) {  // 相等时取最大的i
                min_cnt = cnt;
                ans = i;
            }
        }
        return ans;
    }
};
```

# <b>动态规划</b>

这个视频讲的很好！[动态规划 | 空间换时间 (多P)_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1aa411f7uT?p=1&vd_source=cb02f779bd17a3aad9801e0c4464dfc9)

动态规划问题 本质是一个有限状态自动机问题，也就是有向无环图的求解

有向无环图里有起始节点，终止节点，每个节点代表一个状态，任何非起始节点都可以从其他节点转移过来，也叫做状态转移；

> 注意！这里的状态/节点 又叫总状态，其实是一个集合，集合信息一般有位置，已搜路径(初始节点到当前节点的路径）等等信息；

动态规划的状态（总状态的子集），是从这个状态集合里提取一些信息，作为状态值和状态维度

Ps: 搜索的状态，也是总状态的子集，一般也会从总状态里提取一些信息，来画搜索树

所以动态规划的思维步骤如下：

对于题目需求，人工模拟一下，首先想一下搜索，可以做后判断是否可以用动态规划求解

技巧：把状态用节点表示，然后人脑简单求一次拓扑排序，如果发现有环，那就一定不是动态规划！

1. 设计状态：动态规划的状态设计，分为状态值和状态维度，状态值一般显而易见，状态维度需要选取固定有限区间；
2. 确定状态转移方程：得到状态后，看第一步或者最后一步，根据决策，确定当前状态可以转移到哪些状态，或者状态由哪些状态转移，两种方式都可以
3. 边界和初始化：初始化分为 状态图的初始化和初始状态的初始化，状态图的初始化需要考虑合法状态不能受非法状态的影响；初始状态的初始化一般根据题意或者满足递推要求；边界就是数组不能越界

动态规划的实现方式：

动态规划可以递推（bottom-up) 也可以记忆化搜索（top-down）实现

递推：直接从初始状态出发，到达终止状态

记忆化搜索：从终止状态出发，递归搜索，先递到初始状态，再归到终止状态，中间用哈希表记录已经计算过的状

态，防止状态重复计算；

重点说一下边界和初始化的技巧

方法1：不改变原来的状态空间：

1. 首先按照题目给的状态空间，遍历计算状态，然后会因为数组越界，所以少计算一些状态；
2. 状态空间的初始化先默认为0，首先必须要满足循环内的依赖状态是合法的，根据这个原则初始化一些状态；
3. 然后状态空间内循环外的状态也正确初始化；
4. 如果发现初始化的值都一样，可以直接利用状态空间的初始化；

方法2：改变状态空间，避免越界：

1. 为了避免数组越界的边界判断，我们可以在数组前面插几位，这样就可以按照状态空间遍历状态，保证所有的状态都被遍历到，
2. 这个时候考虑两点 1-初始状态合法（循环内的依赖状态合法） 2-非法状态不影响，来初始化状态空间；

滚动数组优化：

只要是严格遍历整个状态空间，我们就可以滚动数组优化；第二步循环内完整遍历状态空间，所以滚动数组优化一般是基于第二步更方便，可以直接1：1翻译；

## DP入门

通过一些线性dp的题目来入门dp

#### [70. 爬楼梯](https://leetcode.cn/problems/climbing-stairs/)

AC，思路：动态规划入门题目，我们提供 暴搜 -&gt; 递归 -&gt; 记忆化搜索 -&gt; 递推 多种解法 中间一步步优化！

暴搜：搜索所有爬到n阶楼梯的路径，统计方案数，这种写法会超时

```cpp
class Solution {
public:
    int climbStairs(int n) {
        int ans = 0;
        function<void(int)> dfs = [&](int i) {
            if (i == n) ans ++;
            if (i >= n) return;
            dfs(i + 1);
            dfs(i + 2);
        };

        dfs(0);
        return ans;
    }
};
```

递归：搜索的状态里，我们将爬到当前位置i的方案数作为状态表示，发现状态之间存在关系 dfs(i) = dfs(i - 1) + dfs(i - 2)，所以递归求解

```cpp
class Solution {
public:
    int climbStairs(int n) {
        function<int(int)> dfs = [&](int i) {
            if (i == 1) return 1;
            if (i == 2) return 2;
            int cnt = dfs(i - 1) + dfs(i - 2);
            return cnt;
        };

        return dfs(n);
    }
};
```

递归的这种写法，之后会更普遍，首先边界i =1, return 1, 然后i=2时，dfs(1) + dfs(0), 为了使dfs(2)正确，i = 0也return 1；之后的3，4，5...肯定是正确的！

```cpp
class Solution {
public:
    int climbStairs(int n) {
        function<int(int)> dfs = [&](int i) {
            if (i <= 1) return 1;
            int cnt = dfs(i - 1) + dfs(i - 2);
            return cnt;
        };

        return dfs(n);
    }
};
```

动态规划-记忆化搜索：递归的时候，发现很多状态重复计算，所以我们利用一个cache数组记录已经计算过的状态

```cpp
class Solution {
public:
    int climbStairs(int n) {
        vector<int> cache(n + 1, 0);
        function<int(int)> dfs = [&](int i) {
            if (i == 1) return 1;
            if (i == 2) return 2;
            // 边界写成 if (i <= 1) return 1; 也可以
            if (cache[i] != 0) return cache[i];
            int cnt = dfs(i - 1) + dfs(i - 2);
            cache[i] = cnt;
            return cnt;
        };

        return dfs(n);
    }
};
```

递推：直接从初始状态 -&gt; 最终状态，一般可以由记忆化搜索地写法，1:1翻译过来

```cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n == 1) return 1;
        vector<int> f(n + 1, 0);        
        f[1] = 1, f[2] = 2;   // 防止越界 size > 最大下标 n + 1 > 2 => n > 1
        for (int i = 3; i <= n; i ++) f[i] = f[i - 1] + f[i - 2];
        return f[n];
    }
};
```

尝试把大下标放入循环里计算，避免n的特判，对应之前递归里 i &lt;= 1的边界判断

```cpp
class Solution {
public:
    int climbStairs(int n) {
        vector<int> f(n + 1, 0);        
        f[0] = f[1] = 1;   // 防止越界 size > 最大下标 n + 1 > 1 => n > 0
        for (int i = 2; i <= n; i ++) f[i] = f[i - 1] + f[i - 2];
        return f[n];
    }
};
```

空间优化: 观察状态转移方程，发现一旦算出 f[i]，那么 f[i−2] 及其左边的状态就永远不会用到了。

这意味着每次循环，只需要知道「上一个状态」和「上上一个状态」的 f 值是多少，分别记作f1和f0

```cpp
class Solution {
public:
    int climbStairs(int n) {     
        int f0 = 1, f1 = 1;
        for (int i = 2; i <= n; i ++) {
            int new_f = f1 + f0;
            f0 = f1;
            f1 = new_f;
        }
        return f1;
    }
};
```

#### [746. 使用最小花费爬楼梯](https://leetcode.cn/problems/min-cost-climbing-stairs/)

AC，思路：也是给出很多种解法

暴搜

```cpp
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size();
        int ans = 0x3f3f3f3f;
        function<void(int, int)> dfs = [&](int i, int _cost) {
            if (i == n) ans = min(ans, _cost);
            if (i >= n) return;

            dfs(i + 1, _cost + cost[i]);
            dfs(i + 2, _cost + cost[i]);
        };

        dfs(0, 0);
        dfs(1, 0);
        return ans;
    }
};
```

递归：

```cpp
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size();
        function<int(int)> dfs = [&](int i) {
            if (i == 0 || i == 1) return 0; 
            int _cost= min(dfs(i - 1) + cost[i - 1], dfs(i - 2) + cost[i - 2]);
            return _cost;
        };
        return dfs(n);
    }
};
```

记忆化搜索：

```cpp
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size();
        vector<int> cache(n + 1, -1);
        function<int(int)> dfs = [&](int i) {
            if (i == 0 || i == 1) return 0; 
            if (cache[i] != -1) return cache[i];
            cache[i] = min(dfs(i - 1) + cost[i - 1], dfs(i - 2) + cost[i - 2]);
            return cache[i];
        };
        return dfs(n);
    }
};
```

递推：

```cpp
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size();
        if (n == 0) return 0;
        vector<int> f(n + 1);
        f[0] = f[1] = 0;
        for (int i = 2; i <= n; i ++) {
            f[i] = min(f[i - 1] + cost[i - 1], f[i - 2] + cost[i - 2]);
        }
        return f[n];
    }
};
```

空间优化

```cpp
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size();
        int f0 = 0, f1 = 0;
        for (int i = 2; i <= n; i ++) {
            int new_f = min(f1 + cost[i - 1], f0 + cost[i - 2]);
            f0 = f1;
            f1 = new_f;
        }
        return f1;
    }
};
```

#### [377. 组合总和 Ⅳ](https://leetcode.cn/problems/combination-sum-iv/)

NOT AC，思路：其实不是背包问题，而是爬楼梯问题，首先人工模拟，答案第一位选哪个，第二个选哪个...，发现暴搜可以做，然后看看能否动态规划来做，动态规划首先要设计状态，设计状态，状态值一般好设计，就是答案，维度一定要选取固定有限区间，这样才能做状态转移；f[i]：和为i的组合数；注意溢出问题;计数相关的dp问题，状态首先都初始化为0，然后f[0] = 1；

```cpp
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        vector<unsigned int> f(target + 1, 0);
        f[0] = 1;
        for (int i = 1; i <= target; i ++) {
            for (int &num: nums) {
                if (i >= num) f[i] += f[i - num];
            }
        }
        return f[target];
    }
};
```

#### [2466. 统计构造好字符串的方案数](https://leetcode.cn/problems/count-ways-to-build-good-strings/)

AC，思路：首先人工模拟，第一步执行什么操作，第二步执行什么操作，发现暴搜可以做，然后看能否动态规划来做，动态规划第一步设计状态，我们根据模拟的步骤设计状态，状态值是字符串的数目，维度选择固定有限区间，所以选择长度；然后构建状态转移方程，成功；所以 状态 f[i]：长度为i的字符串数目 f[i] = f[i - zero] + f[i - one]；然后再其中统计好字符串数目，同时注意取模；计数相关的dp问题，状态首先都初始化为0，然后f[0] = 1；

```cpp
class Solution {
public:
    int countGoodStrings(int low, int high, int zero, int one) {
        const int mod = 1e9 + 7;

        vector<int> f(high + 1, 0);
        f[0] = 1;
        for (int i = 1; i <= high; i ++) {  
            if (i >= zero) f[i] = f[i - zero] % mod;
            if (i >= one) f[i] = (f[i] + f[i - one]) % mod;
        }

        int ans = 0;
        for (int i = low; i <= high; i ++) {
            ans = (ans + f[i]) % mod;
        }
        return ans;
    }
};
```

#### [509. 斐波那契数](https://leetcode.cn/problems/fibonacci-number/)

AC，动态规划模板题，首先人工模拟，然后设计状态，注意初始化和边界

```cpp
class Solution {
public:
    int fib(int n) {
        if (n == 0) return 0;
        vector<int> f(n + 1);
        f[0] = 0, f[1] = 1;
        for (int i = 2; i <= n; i ++) f[i] = f[i - 1] + f[i - 2];
        return f[n];
    }
};
```

#### [198. 打家劫舍](https://leetcode.cn/problems/house-robber/)

AC，思路：人工模拟，第一步偷哪座房子，第二步...，暴搜可以做，然后思考一下能否动态规划来做；设计状态，状态值，最大金额，状态维度必须是固定有限区间，房屋位置有限；状态f[i]，在i位置房屋时偷的最大金额；所以f[i] = max(f[i - 2] + nums[i], f[i - 1])；然后这题可以顺带讲解一下动态规划的边界和初始化的简单写法，核心还是一样，状态图的初始化需要考虑合法状态不能受非法状态的影响；初始状态的初始化一般根据题意或者满足递推要求；边界就是数组不能越界（size &gt; 最大下标）

严格按照定义的写法：

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        if (n == 0) return 0;
        if (n == 1) return nums[0];

        vector<int> f(n, 0);
        f[0] = nums[0], f[1] = max(nums[0], nums[1]);
        for (int i = 2; i <= n - 1; i ++) {
            f[i] = max(f[i - 2] + nums[i], f[i - 1]);
        }
        return f[n - 1];
    }
};
```

边界/初始化 简单写法：

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        vector<int> f(n + 2, 0);
        // 初始化 原来是f[0] = nums[0], 现在是f[2] = nums[0]，循环内部可以得到，省略初始化
        for (int i = 0; i < n; i++) {   // 遍历状态空间
        // 相当于在 f 前面插了两个空位，所以只会影响与 f 有关的下标，不会影响其它下标
            f[i + 2] = max(f[i + 1], f[i] + nums[i]); 
        }
        return f[n + 1];
    }
};
```

#### [213. 打家劫舍 II](https://leetcode.cn/problems/house-robber-ii/)

AC，其实是一个状态机dp，但是这里分成两种情况讨论，每种各自dp一次，打家劫舍系列的题目，关键还是要注意初始化和边界，方法在算法讲解里有

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        if (n == 1) return nums[0];

        // 第一个选 最后一个自然不能选
        vector<int> f1(n, 0);
        f1[0] = nums[0], f1[1] = nums[0];
        for (int i = 2; i < n - 1; i ++) {
            f1[i] = max(f1[i - 2] + nums[i], f1[i - 1]);
        }

        // 第一个不选 最后一个必须选
        vector<int> f2(n, 0);
        f2[0] = 0, f2[1] = nums[1];
        for (int i = 2; i < n; i ++) {
            f2[i] = max(f2[i - 2] + nums[i], f2[i - 1]);
        }

        return max(f1[n - 2], f2[n - 1]);  // 注意f1[n - 1]是0，f1的最大值在f1[n - 2]上
    }
};
```

边界/初始化 优化，插两个空位即可，可以省略初始状态的初始化，同时减少边界判断

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        if (n == 1) return nums[0];

        // 第一个选 最后一个自然不能选
        vector<int> f1(n + 2, 0);
        for (int i = 0; i <= n - 2; i ++) {
            f1[i + 2] = max(f1[i] + nums[i], f1[i + 1]);
        }

        // 第一个不选 最后一个必须选
        vector<int> f2(n + 2, 0);
        for (int i = 1; i <= n - 1; i ++) {
            f2[i + 2] = max(f2[i] + nums[i], f2[i + 1]);
        }

        return max(f1[n], f2[n + 1]);
    }
};
```

#### [740. 删除并获得点数](https://leetcode.cn/problems/delete-and-earn/)

NOT AC，思路：打家劫舍的变种问题；首先我们明确如果选了数x，那么x - 1, x + 1都不能选，所以选了x的时候，我们为了使点数最大，直接把x全取完；然后人工模拟，第一步选哪个数，第二步选哪个数，这种做法的顺序不能作为固定连续区间，所以换一个模拟思路；值为1的数选or不选，值为2的数选or不选，这种情况值使固定连续区间，尝试dp；f[i] 到达数值为i的数时的最大点数；然后注意初始化和边界

```cpp
class Solution {
public:
    int deleteAndEarn(vector<int>& nums) {
        int n = nums.size();
        unordered_map<int, int> mp;
        int max_val = 0;
        for (int i = 0; i < n; i ++) {
            mp[nums[i]] += nums[i];
            max_val = max(max_val, nums[i]);
        }

        vector<int> f(max_val + 1, 0);
        f[1] = mp[1];
        for (int i = 2; i <= max_val; i ++) {
            f[i] = max(f[i - 2] + mp[i], f[i - 1]);
        }
        return f[max_val];
    }
};
```

初始化/边界 简单写法

```cpp
class Solution {
public:
    int deleteAndEarn(vector<int>& nums) {
        int n = nums.size();
        unordered_map<int, int> mp;
        int max_val = 0;
        for (int i = 0; i < n; i ++) {
            mp[nums[i]] += nums[i];
            max_val = max(max_val, nums[i]);
        }

        vector<int> f(max_val + 3, 0);
        for (int i = 1; i <= max_val; i ++) {
            f[i + 2] = max(f[i] + mp[i], f[i + 1]);
        }
        return f[max_val + 2];

        
    }
};
```

#### [2320. 统计放置房子的方式数](https://leetcode.cn/problems/count-number-of-ways-to-place-houses/)

AC，思路：还是打家劫舍的变种题；这里我们首先发现两边其实是独立的，所以先一边分析；然后一边就是打家劫舍问题，注意初始化/边界

```cpp
class Solution {
public:
    int countHousePlacements(int n) {
        const int mod = 1e9 + 7;
        vector<int> f(n + 1, 0);
        f[0] = 1, f[1] = 2;
        for (int i = 2; i <= n; i ++) {
            f[i] = f[i - 2] % mod;
            f[i] = (f[i] + f[i - 1]) % mod;
        }
        return (long long)(f[n] % mod) * (f[n] % mod) % mod;
    }
};
```

边界/初始化 简化

```cpp
class Solution {
public:
    int countHousePlacements(int n) {
        const int mod = 1e9 + 7;
        vector<int> f(n + 3, 1);
        for (int i = 1; i <= n; i ++) {
            f[i + 2] = f[i] % mod;
            f[i + 2] = (f[i + 2] + f[i + 1]) % mod;
        }
        return (long long)(f[n + 2] % mod) * (f[n + 2] % mod) % mod;
    }
};
```

#### [53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray/)

> Leetcode hot100

NOT AC, 思路：首先人工模拟，输入选or不选肯定排除，因为要求是连续子数组，所以模拟第一个数选哪个，第二个数选哪个，看看能否动态规划；状态值 最大和；状态维度，必须是有限连续区间，所以是index，那么设计状态f[i]：i位置（以i位置结尾）的字符串的最大和（为什么说是以i结尾的字串的最大和而不是区间[0, i]构成的所有字符串的最大值呢，因为根据我们的模拟步骤，这里的i位置的已搜路径，其实是[start, i] start &lt;= i这一子串的最大和，所以i必须选，然后[start, i] start &lt;= i的最大和是可以由[start, i - 1] start &lt;= i - 1的最大和转化而来的；

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n = nums.size();
        vector<int> f(n + 1, 0);
        f[0] = nums[0];
        int ans = f[0];
        for (int i = 1; i < n; i ++) {
            f[i] = max(nums[i], f[i - 1] + nums[i]);
            ans = max(ans, f[i]);
        }
        return ans;   
    }
};
```

#### [2606. 找到最大开销的子字符串](https://leetcode.cn/problems/find-the-substring-with-maximum-cost/)

AC，思路：其实把条件转化后，得到一个开销数组，就是最大子数组和问题

```cpp
class Solution {
public:
    int maximumCostSubstring(string s, string chars, vector<int>& vals) {
        unordered_map<int, int> mp;
        for (int i = 0; i < chars.size(); i ++) {
            mp[chars[i]] = i;
        }

        int n = s.size();
        vector<int> a(n);
        for (int i = 0; i < n; i ++) {
            if (mp.count(s[i])) a[i] = vals[mp[s[i]]];
            else a[i] = s[i] - 'a' + 1;
        }

        vector<int> f(n, 0);
        f[0] = a[0];
        int ans = max(0, f[0]);
        for (int i = 1; i < n; i ++) {
            f[i] = max(a[i], f[i - 1] + a[i]);
            ans = max(ans, f[i]);
        }
        return ans;
    }
};
```

#### [1749. 任意子数组和的绝对值的最大值](https://leetcode.cn/problems/maximum-absolute-sum-of-any-subarray/)

AC，思路：题目本质是求 最大子数组和 和 最小子数组和的绝对值的 最大值；

```cpp
class Solution {
public:
    int maxAbsoluteSum(vector<int>& nums) {
        int n = nums.size();
        vector<int> f(n), g(n);
        f[0] = g[0] = nums[0];
        int ans = max(0, max(f[0], - g[0]));
        for (int i = 1; i < n; i ++) {
            f[i] = max(f[i - 1] + nums[i], nums[i]);
            g[i] = min(g[i - 1] + nums[i], nums[i]);
            ans = max(ans, max(abs(f[i]), abs(g[i])));
        }
        return ans;
    }
};
```

## 网格图DP

网格图dp是二维dp里比较经典且多见的一种类型，所以这里单独划分出来练习

#### [62. 不同路径](https://leetcode.cn/problems/unique-paths/)

AC, 思路：网格图dp的模板题，状态维度基本都是坐标

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> f(m, vector<int>(n, 1));
        for (int i = 1; i < m; i ++) {
            for (int j = 1; j < n; j ++) {
                f[i][j] = f[i - 1][j] + f[i][j - 1];
            }
        }
        return f[m - 1][n - 1];
    }
};
```

简化初始化/边界

```cpp
// 主要就是需要满足 0，0时 对应的 f[1][1] = 1;

class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> f(m + 1, vector<int>(n + 1, 0));
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                if (i == 0 && j == 0) f[i + 1][j + 1] = 1;
                else f[i + 1][j + 1] = f[i][j + 1] + f[i + 1][j];
            }
        }
        return f[m][n];
    }
};

// 主要就是需要满足 0，0时 对应的 f[1][1] = 1;
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> f(m + 1, vector<int>(n + 1, 0));
        f[0][1] = 1, f[1][0] = 0;
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                f[i + 1][j + 1] = f[i][j + 1] + f[i + 1][j];
            }
        }
        return f[m][n];
    }
};


// 1，1 -> m, n
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> f(m + 1, vector<int>(n + 1, 0));
        f[0][1] = 1, f[1][0] = 0;
        for (int i = 1; i <= m; i ++) {
            for (int j = 1; j <= n; j ++) {
                f[i][j] = f[i - 1][j] + f[i][j - 1];
            }
        }
        return f[m][n];
    }
};
```

#### [63. 不同路径 II](https://leetcode.cn/problems/unique-paths-ii/)

AC, 思路：还是不同路径，加上了障碍，这道题如果步简化 初始化/边界，会多写很多代码，所以直接简化版本

```cpp
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size(), n = obstacleGrid[0].size();
        vector<vector<int>> f(m + 1, vector<int>(n + 1));
        f[0][1] = 0, f[1][0] = 1;
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                if (obstacleGrid[i][j] == 1) f[i + 1][j + 1] = 0;
                else f[i + 1][j + 1] = f[i][j + 1] + f[i + 1][j];
            }
        }
        return f[m][n];
    }
};
```

#### [64. 最小路径和](https://leetcode.cn/problems/minimum-path-sum/)

NOT AC，思路：不同路径模板，这道题因为要求最小值，所以状态图初始化需要防止被非法状态影响，所以初始化为极大值；

```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();

        vector<vector<int>> f(m + 1, vector<int>(n + 1, 0x3f3f3f3f));
        f[0][1] = f[1][0] = 0;
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                f[i + 1][j + 1] = min(f[i][j + 1], f[i + 1][j]) + grid[i][j];
            }
        }

        return f[m][n];
    }
};
```

#### [120. 三角形最小路径和](https://leetcode.cn/problems/triangle/)

AC, 思路：不同路径的变种，这里注意最后我们需要遍历最后一层的所有状态来找到答案；

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size(), m = triangle[n - 1].size();

        vector<vector<int>> f(n + 1, vector<int>(m + 1, 0x3f3f3f3f));
        f[0][1] = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < triangle[i].size(); j ++) {
                f[i + 1][j + 1] = min(f[i][j], f[i][j + 1]) + triangle[i][j];
            }
        }

        int ans = 0x3f3f3f3f;
        for (int j = 0; j < triangle[n - 1].size(); j ++) {
            ans = min(ans, f[n][j + 1]);
        }
        return ans;
    }
};
```

## 背包DP

背包问题模型：有一堆物品和背包体积，每个物品有体积，求背包体积限制下的最优方案/方案数/方案是否存在

<b>背包问题分类</b>
01背包：每个物品只能选一次
求最优方案：f[i][j] = max/min(f[i - 1][j] + f[i - 1][j - v[i]] + w[i]) 或者 f[j] = max/min(f[j] + f[j - v[i]] + w[i])
求方案数： f[i][j] = f[i - 1][j] + f[i - 1][j - v[i]] 或者 f[j] = f[j] + f[j - v[i]]
求方案是否存在：f[i][j] = f[i - 1][j] || f[i - 1][j - v[i]] 或者 f[j] = f[j] || f[j - v[i]]   //只在恰好等于的模型有意义


完全背包：每个物品可以选无限次
01背包的总结照抄过来，然后二维dp选部分的i - 1改成i,如果优化到1维的话，注意遍历顺序需要改成正序

<b>背包问题转化</b>
如果原问题翻译过后是：从一些物品里选，物品属性和有限制（属性不能是物品个数），求解最优方案/方案数/方案是否存在；此时可以尝试用背包模型


解题思路：找到限制 ==&gt; 物品是什么， 背包体积v是什么，物品体积v[i]是什么
eg:找到限制 数字和 = target，那么物品是数，背包体积v是target，物品体积v[i]是每个数的值nums[i]


常见转化：
最多装capacity，求方案数/最大价值和
恰好装capacity，求方案数/最大价值和/最小价值和/方案是否存在
最少装capacity，求方案数/最小价值和



<b>边界，初始化：</b>

状态空间都是从1开始，状态计算更容易；


求最优：
恰好等于：先初始化dp数组为+-inf，边界为f[0]或者f[0, 0]，初始化为0
至多：先初始化dp数组为0，边界为f[0]或者f[0, 0]，初始化为0


求方案数：
恰好等于：先初始化dp数组为0，边界为f[0]或者f[0, 0]，初始化为1
至多：先初始化dp数组为1，边界为f[0]或者f[0, 0]，初始化为1


求方案是否存在：
恰好等于：先初始化dp数组为false，边界为f[0]或者f[0, 0]，初始化为true

<b>背包问题的考察点</b>
01背包，二维dp的时候内外层循环可以颠倒，一维dp的时候内外层不能颠倒
完全背包，二维dp的时候内外层可以颠倒，一维dp的时候内外层可以颠倒
完全背包，如果先遍历物品后遍历背包，方案是组合不重复，如果先遍历背包后遍历物品，方案是排列重复，直接转化为了爬楼梯问题，不是完全背包问题了！

#### [494. 目标和](https://leetcode.cn/problems/target-sum/)

NOT AC，思路：首先思考暴搜，每个数前面选 + 还是 -，这个数值范围是可以尝试暴搜的；然后思考动态规划，这里设 正数和为p，负数和为q，那么可以列出方程 p - q = t, p + q = s;  p = (s + t) / 2, q = (s - t) / 2；所以我们可以将问题转化为，从一些数里选，正数和恰好为p/负数和恰好为q 的方案数；

现在可以转化为01背包问题，物品就是数，体积有两种选择，p和q都可以，哪个小就选哪个；物品体积就是数值；现在是统计方案数，并且是恰好等于，注意边界/初始化

```cpp
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int target) {
        int n = nums.size();
        int sum = accumulate(nums.begin(), nums.end(), 0);
        int v = min(sum + target, sum - target);

        if (v < 0 || v % 2 != 0) return 0;
        v /= 2;

        vector<vector<int>> f(n + 1, vector<int>(v + 1));
        f[0][0] = 1;
        for (int i = 0; i < n; i ++) { 
            for (int j = 0; j <= v; j ++) {
                if (j >= nums[i]) f[i + 1][j] = f[i][j - nums[i]] + f[i][j];
                else f[i + 1][j] = f[i][j];
            }
        }
        return f[n][v];
    }
};
```

#### [416. 分割等和子集](https://leetcode.cn/problems/partition-equal-subset-sum/)

AC，思路：01背包模板题，从一些数里选，和恰好等于target/2，是否存在方案；注意边界/初始化；首先为了消除边界，多插一位；然后为了保证循环内的依赖项正确，f[0][0] = true；之后为了防止被非法状态影响，状态图初始化为false；边界/初始化 大概就是这样的思维步骤！

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
        int sum = accumulate(nums.begin(), nums.end(), 0);
        if (sum % 2 != 0) return false;
        int v = sum / 2;
        
        vector<vector<bool>> f(n + 1, vector<bool>(v + 1, false));
        f[0][0] = true;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j <= v; j ++) {
                if (j >= nums[i]) f[i + 1][j] = f[i][j] || f[i][j - nums[i]];
                else f[i + 1][j] = f[i][j];
            }
        }
        return f[n][v];
    }
};
```

#### [474. 一和零](https://leetcode.cn/problems/ones-and-zeroes/)

NOT AC，思路：01背包，一开始的思路是统计两个二维dp，然后最后取他们两个的最小值；但是仔细一想这样做是不对的，因为有可能在中间的状态里，及已经违背了各自都不超过m，n的限制，所以应该是放在一起dp，三维dp；f[i][j][k]：前i个物品里选，0的个数不超过j，1的个数不超过1的最大子物品长度

三维dp用vector写法会很复杂，直接用数组 + memset写法更简单

```cpp
class Solution {
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        // 转化为物品的权值数组
        int len = strs.size();
        vector<int> zero(len), one(len);
        for (int i = 0; i < len; i ++) {
            int zeros = 0, ones = 0;
            for (int j = 0; j < strs[i].size(); j ++) {
                if (strs[i][j] == '0') zeros++;
                else ones ++;
            }
            zero[i] = zeros, one[i] = ones;
        }

        // 三维dp 01背包 i物品 j0的个数 k1的个数
        int f[len + 1][m + 1][n + 1];
        memset(f, 0, sizeof(f));
        f[0][0][0] = 0;
        for (int i = 0; i < len; i ++) {
            for (int j = 0; j <= m; j ++) {
                for (int k = 0; k <= n; k ++) {
                    if (j >= zero[i] && k >= one[i]) 
                        f[i + 1][j][k] = max(f[i][j - zero[i]][k - one[i]] + 1, f[i][j][k]); 
                    else f[i + 1][j][k] = f[i][j][k];
                }

            }
        }
        return f[len][m][n];
    }
};
```

#### [322. 零钱兑换](https://leetcode.cn/problems/coin-change/)

AC，思路：完全背包的模板题，每个物品可以选无数次

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int n = coins.size();
        vector<vector<int>> f(n + 1, vector<int>(amount + 1, 0x3f3f3f3f));
        f[0][0] = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j <= amount; j ++) {
                if (j >= coins[i]) f[i + 1][j] = min(f[i + 1][j - coins[i]] + 1, f[i][j]);
                else f[i + 1][j] = f[i][j];
            }
        }
        return f[n][amount] == 0x3f3f3f3f ? -1 : f[n][amount];
    }
};
```

#### [518. 零钱兑换 II](https://leetcode.cn/problems/coin-change-ii/)

AC，思路：跟上面的题是一样的，只是换成了求方案数而已

```cpp
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        int n = coins.size();
        vector<vector<int>> f(n + 1, vector<int>(amount + 1, 0));
        f[0][0] = 1;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j <= amount; j ++) {
                if (j >= coins[i]) f[i + 1][j] = f[i + 1][j - coins[i]] + f[i][j];
                else f[i + 1][j] = f[i][j];
            }
        }
        return f[n][amount];
    }
};
```

#### [279. 完全平方数](https://leetcode.cn/problems/perfect-squares/)

NOT AC，思路：问题转化一下，变为从一堆平方数里选，可以重复选，然后数值和恰好等于n的最小物品长度；完全背包问题；然后注意 这一堆平方数的最大值需要 &lt;= n；

```cpp
class Solution {
public:
    int numSquares(int n) {
        vector<int> a;
        for (int i = 1; i * i <= n; i ++) a.push_back(i * i);
        int m = a.size();

        vector<vector<int>> f(m + 1, vector<int>(n + 1, 0x3f3f3f3f));
        f[0][0] = 0;
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j <= n; j ++) {
                if (j >= a[i]) f[i + 1][j] = min(f[i + 1][j - a[i]] + 1, f[i][j]);
                else f[i + 1][j] = f[i][j]; 
            }
        }
        return f[m][n];
    }
};
```

## 最长公共子序列（LCS）

最长公共子序列模型：f[i][j]对应的状态集合 字符串a[1, i]和字符串b[1, j]的公共子序列集合

常见问题：

最长公共子序列：f[i][j]表示字符串a[1, i]和字符串[1, j]的最长公共子序列长度；

#### [1143. 最长公共子序列](https://leetcode.cn/problems/longest-common-subsequence/)

AC，思路：模板题，f[i][j]表示 字符串a[0, i]区间和字符串b[0, j]区间的最长公共子序列长度；

```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int n = text1.size(), m = text2.size();

        vector<vector<int>> f(n + 1, vector<int>(m + 1, 0));
        f[0][0] = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if (text1[i] == text2[j]) f[i + 1][j + 1] = f[i][j] + 1;
                else f[i + 1][j + 1] = max(f[i][j + 1], f[i + 1][j]); 
            }
        }
        return f[n][m];
    }
};
```

#### [583. 两个字符串的删除操作](https://leetcode.cn/problems/delete-operation-for-two-strings/)

AC，思路：正难则反，题目最后要得到的是一个公共子序列，为了让步数最小，所以要尽可能使这公共子序列最长；那么就是求一个lcs，最后答案就是总长度 - lcs

```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int n = word1.size(), m = word2.size();

        vector<vector<int>> f(n + 1, vector<int>(m + 1, 0));
        f[0][0] = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < m; j ++) {
                if (word1[i] == word2[j]) f[i + 1][j + 1] = f[i][j] + 1;
                else f[i + 1][j + 1] = max(f[i][j + 1], f[i + 1][j]); 
            }
        }
        return n + m - f[n][m] * 2;
    }
};
```

## 最长递增子序列（LIS)

最长递增子序列模型：f[i]对应的状态集合是 以nums[i]结尾的子序列 方案集合

状态转移方程怎么想：思考最后一步，nums[i]前面的一个数未确定，需要选择；枚举nums[i]前面的一个数nums[j];

常见问题

最长递增子序列长度：f[i] 表示 以nums[i]结尾的最长递增子序列长度

#### [300. 最长递增子序列](https://leetcode.cn/problems/longest-increasing-subsequence/)

NOT AC，思路：最长递增子序列，很经典的动态规划模型，f[i]表示以nums[i]结尾的最长递增子序列长度；初始化/边界，为了循环内依赖项正确，需要f[0] = 1，然后每次计算状态时最小是1，所以状态空间都初始化为1；

```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();

        vector<int> f(n, 1);
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < i; j ++) {
                if (nums[j] < nums[i]) 
                    f[i] = max(f[i], f[j] + 1);
            }
        }
        
        int ans = 0;
        for (int i = 0; i < n; i ++) {
            ans = max(ans, f[i]);
        }
        return ans;
    }
};
```

#### [673. 最长递增子序列的个数](https://leetcode.cn/problems/number-of-longest-increasing-subsequence/)

NOT AC，思路：LIS的变种题，一开始的思路错了，以为找到一个更长的LIS，就是从1开始，其实应该是从cnt[j]开始；可以这么想，之前以nums[j]为结尾的LIS个数是x，那么如果以nums[i]结尾的LIS长度更长，它都由之前的LIS + 1构成，之前有x个方案，他们都+1构成新的LIS，所以新的LIS的个数是x；然后如果相等，就相当于在目前LIS个数的基础上，又找到了相同长度的LIS，那么就在之前的个数上 加上 新找到的相同长度的LIS的个数；所以得到公式 f[i] &gt; f[j] + 1  cnt[i] = cnt[j];  f[i] = f[j] + 1 cnt[i] += cnt[j];

```cpp
class Solution {
public:
    int findNumberOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<int> f(n, 1), cnt(n, 1);
        int max_len = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < i; j ++) {
                if (nums[j] < nums[i]) {
                    if (f[j] + 1 > f[i]) cnt[i] = cnt[j];
                    else if (f[j] + 1 == f[i]) cnt[i] += cnt[j];
                    f[i] = max(f[i], f[j] + 1);
                }
            }
            max_len = max(max_len, f[i]);   // 直接计算LIS长度
        }

        int ans = 0;   // 答案是 LIS长度对应的f[i]的cnt[i](方案数）的总和
        for (int i = 0; i < n; i ++) {
            if (f[i] == max_len) ans += cnt[i];
        }
        return ans;
    }
};
```

#### 
## 状态机dp

状态机dp，就是当决策比较多的时候，我们可以把一些决策放入状态维度里，这样可以使决策更清晰，更容易写出状态转移方程；

#### [121. 买卖股票的最佳时机](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/)

NOT AC，思路：这题用dp会使用状态机dp比较复杂，直接暴力后，利用前缀 + 贪心来想；

从左到右枚举卖出价格 prices[i]，那么要想获得最大利润，我们需要知道第 i 天之前，股票价格的最小值是什么，也就是从 prices[0] 到 prices[i−1] 的最小值，把它作为买入价格，最朴素是维护一个前缀最大值数组，但是前缀最大值数组可以在遍历的时候就建立出来，直接用一个变量 min_price 维护；

前缀数组 就是要注意 初始状态正确，也就是i = 0的时候，代表0之前的最小值，这是非法的，但为了不影响ans和之后的min_price计算，min_price需要设为极大值；

前缀 + 贪心：

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();

        int min_price = 0x3f3f3f3f, ans = 0;
        for (int i = 0; i < n; i ++) {
            ans = max(ans, prices[i] - min_price);
            min_price = min(min_price, prices[i]);
        }
        return ans;
    }
};
```

#### [122. 买卖股票的最佳时机 II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)

NOT AC，思路：这题可以使用状态机dp来做，但是仔细一想可以直接贪心来做，因为可以反复买卖，最大利润就是所有上升段的利润；画图以后很直观的可以看出来；

贪心：

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();

        int ans = 0;
        for (int i = 1; i < n; i ++) {
            // 只要有上升段，就进行交易，相当于统计所有上升段的利润
            if (prices[i] > prices[i - 1]) ans += prices[i] - prices[i - 1];
        }
        return ans;
    }
};
```

#### [123. 买卖股票的最佳时机 III](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/)

NOT AC，思路：在之前的基础上加了个维度，最多交易2次；最多2次可以看作 最多k次，k = 2；状态机dp来做了；f[i][0/1][j] 第i天结束时是否持有股票最多交易j次的利润；但是我们习惯将大的维度放前面，小的维度放后面，所以最后设计状态 是 f[i][j][0/1] 第i天结束时最多交易j次，是否持有股票的最大利润；

为了保证初始状态正确 f[0][j][0]需要初始化为0，然后为了防止非法状态影响，状态空间初始化为-inf；

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size(), k = 2;
        int f[n + 1][k + 2][2];
        memset(f, -0x3f, sizeof(f));
        for (int j = 0; j <= k; j ++) f[0][j + 1][0] = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j <= k; j ++) {
                f[i + 1][j + 1][0] = max(f[i][j + 1][0], f[i][j][1] + prices[i]);
                f[i + 1][j + 1][1] = max(f[i][j + 1][0] - prices[i], f[i][j + 1][1]);
            }
        }
        return f[n][k + 1][0];
    }
};
```

#### [188. 买卖股票的最佳时机 IV](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/)

AC，思路：和上一题完全一样，上一题最多交易2次（最多交易k次，k = 2），这一题直接是最多交易k次；

```cpp
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size();
        int f[n + 1][k + 2][2];
        memset(f, -0x3f, sizeof(f));
        for (int j = 0; j <= k; j ++) f[0][j + 1][0] = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j <= k; j ++) {
                f[i + 1][j + 1][0] = max(f[i][j + 1][0], f[i][j][1] + prices[i]);
                f[i + 1][j + 1][1] = max(f[i][j + 1][0] - prices[i], f[i][j + 1][1]);
            }
        }
        return f[n][k + 1][0];
    }
};
```

#### [309. 买卖股票的最佳时机含冷冻期](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

AC，思路：关键思路在于，如果一天买了，那么前一天一定不能卖，所以如果第i天买了，因为第 <em>i</em> 天买股票的话第 <em>i</em>−1 天不能卖，只能从第 <em>i</em>−2 天没有股票的状态转移过来；相当于直接从i-2的状态转移过来了；

然后边界/初始化牢记自己总结好的步骤，首先插位消除边界，之后初始化 初始状态，初始状态是0,0和0,1分别对应f[2][0]和f[2][1]，前者必须是0，所以初始化f[1][0] = 0，然后防止非法状态影响，其余状态空间赋值-inf，后者必须是-prices[0],所以初始化f[1][1] = 0, 然后防止非法状态影响，其余状态空间赋值-inf；

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();

        int f[n + 2][2];
        memset(f, -0x3f, sizeof(f));
        f[1][0] = f[0][0] = 0;
        for (int i = 0; i < n; i ++) {
            f[i + 2][0] = max(f[i + 1][0], f[i + 1][1] + prices[i]); 
            f[i + 2][1] = max(f[i + 1][1], f[i][0] - prices[i]);
        }
        return f[n + 1][0];
    }
};
```

## 题单

[LC-Rating & Training](https://huxulm.github.io/lc-rating/search)

[动态规划入门50题_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1aa411f7uT/?spm_id_from=333.788.recommend_more_video.1&vd_source=cb02f779bd17a3aad9801e0c4464dfc9)

# <b>贪心</b>

## 
贪心算法概念：

1. 在每一步选择中，都采取在当前状态下的最优决策 （局部最优）
2. 并希望由此导致的最终结果也是全局最优

总结：贪心的本质是选择每一阶段的局部最优，从而达到全局最优

贪心算法和动态规划，搜索不同，不同之处在于：贪心不对整个状态空间进行遍历或计算，而是始终按照局部最优选择执行下去，不再回头 （搜索是遍历整个状态空间；动态规划是计算了整个状态空间，但是利用空间换时间的思想，避免了一些重复状态的计算；贪心只计算了一部分状态空间）所以能用贪心解决的题目，动态规划和搜索也是可以求解的，但是贪心效率最高；

所以贪心是基于局部的算法，而动态规划和搜索是基于全局的算法；

因为这个特性，贪心算法不一定能得到正确的结果，除非可以证明，局部最优可以达到全局最优

运用：

一上来去想贪心其实效率是很低的，我们一般先从动态规划和搜索入手，然后去看能否贪心；

贪心算法并没有固定的套路，做题的时候手动模拟一下感觉可以局部最优推出全局最优，而且想不到反例，那么就试一试贪心

证明：数据归纳法和反证法为主

## <b>贪心策略</b>

#### [455. 分发饼干](https://leetcode.cn/problems/assign-cookies/)

思路：AC，思路就是 胃口大的尽量分大饼干，然后注意遍历胃口和遍历饼干，注意全部跳过的情况，以此来判断循环这么写是否正确；

```cpp
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
        
        // 遍历饼干 饼干大的分胃口大的 
        // 如果第一个饼干满足不了所有人的胃口，全部跳过，后面的饼干更小更满足不了胃口，正确
        // int cnt = 0;
        // for (int j = s.size() - 1, i = g.size() - 1; i >= 0 && j >= 0; i --, j --) {
        //     while (i >= 0 && s[j] < g[i]) i --;
        //     if (i >= 0) cnt ++;
        // }
        // return cnt;

        // 遍历饼干 饼干小的分胃口小的 
        // 如果第一个饼干满足不了所有人胃口，全部跳过，后面的饼干变大可能满足胃口，错误
        // int cnt = 0;
        // for (int j = 0, i = 0; i < g.size() && j < s.size(); i ++, j ++) {
        //     while (i < g.size() && s[j] < g[i]) i ++;
        //     if (i < g.size()) cnt ++;
        // }
        // return cnt;

        // 遍历胃口，胃口大的分饼干大的
        // 如果第一个人吃不到，全部跳过，后面的人胃口小了可能可以迟到，错误
        // int cnt = 0;
        // for (int i = g.size() - 1, j = s.size() - 1; i >= 0 && j >= 0; i --, j --) {
        //     while (j >= 0 && s[j] < g[i]) j --;
        //     if (j >= 0) cnt ++;
        // }
        // return cnt;

        // 遍历胃口，胃口小的分饼干小的
        // 如果第一个人吃不到，全部跳过，后面的人胃口更大更吃不到，正确                        
        int cnt = 0;
        for (int i = 0, j = 0; i < g.size() && j < s.size(); i ++, j ++) {
            while (j < s.size() && s[j] < g[i]) j ++;
            if (j < s.size()) cnt ++;
        }
        return cnt;
    }
};
```

#### 
## 中位数贪心

#### [462. 最小操作次数使数组元素相等 II](https://leetcode.cn/problems/minimum-moves-to-equal-array-elements-ii/)

AC，思路：中位数贪心模板题，这个最后相等的数应该选择中位数；偶数个数时，中间两个数的闭区间内的任意一个数都可以；

```cpp
class Solution {
public:
    int minMoves2(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n = nums.size();
        int med = 0;
        if (n % 2 != 0) med = nums[n / 2];
        else med = (nums[n / 2] + nums[n / 2 - 1]) / 2;

        int ans = 0;
        for (auto& x: nums) {
            ans += abs(x - med);
        }

        return ans;
    }
};


// 继续简化代码
class Solution {
public:
    int minMoves2(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int n = nums.size();
        int target = nums[n / 2];

        int ans = 0;
        for(auto& x: nums){
            ans += abs(x - target);
        }
        return ans;
    }
};
```

#### [2023字节跳动-优雅数组](https://codefun2000.com/p/P1474)

NOT AC，思路：其实就是考虑去除最后一个数/第一个数，做中位数贪心，然后得到最小次数；

技巧：[a, b] 索引a到索引b的 中位数索引是 (a + b + 1) / 2

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 1e9 + 10;
int n, a[N];

int main() 
{
    cin >> n;
    for (int i = 0; i < n; i ++) cin >> a[i];
    sort(a, a + n);

    // 如果所有的数都相等
    if (a[0] == a[n - 1]) {
        cout << 1 << endl;
        return 0;
    }
    
    // 两次中位数贪心

    // 去除最后一位，其他的数相等
    long long res1 = 0;
    int target1 = a[(n - 1) / 2];
    for (int i = 0; i < n - 1; i ++) {
        res1 += abs(a[i] - target1);
    }

    // 去除第一位，其他数相等
    long long res2 = 0;
    int target2 = a[(n + 1) / 2];
    for (int i = 1; i < n; i ++) {
        res2 += abs(a[i] - target2);
    }

    cout << min(res1, res2) << endl;
    return 0;
}
```

#### [2033. 获取单值网格的最小操作数](https://leetcode.cn/problems/minimum-operations-to-make-a-uni-value-grid/)

NOT AC，思路：首先要把矩阵数组转化为一维数组，然后再转化的时候去判断能否转化，如果+-x，可以转化为相同的数；那么任意的两个数的差一定是x的倍数，利用这个性质，我们任选一个数为基准去检测其他的数和它的差值是否为x的倍数，如果发现任何一个不是x的倍数，那么就无法转化成功；

发现可以转化成相同的数后，我们就中位数贪心，转化为中位数是最优解，中位数可以通过排序或者快选来得到；

```cpp
class Solution {
public:
    int minOperations(vector<vector<int>>& grid, int x) {
        // 判断是否可以转化为相同的数，并转化为一维数组
        vector<int> a;
        for (int i = 0; i < grid.size(); i ++) {
            for (int j = 0; j < grid[0].size(); j ++) {
                // 以其中一元素为基准，若所有元素与它的差均为 x 的倍数，则任意两元素之差为x的倍数
                // 那么最终可以转化为相同的数
                if ((grid[i][j] - grid[0][0]) % x != 0) return -1;
                a.push_back(grid[i][j]);
            }
        }

        // 中位数贪心
        sort(a.begin(), a.end());
        int ans = 0, mid = a[a.size() / 2];
        for (int i = 0; i < a.size(); i ++) {
            ans += abs(a[i] - mid) / x;
        }
        return ans;
    }
};
```

#### [2448. 使数组相等的最小开销](https://leetcode.cn/problems/minimum-cost-to-make-array-equal/)

NOT AC，思路：把cost[i]理解成 nums[i]的出现次数，考虑第`i`个数字的操作开销为`cost[i]`，可以考虑为有cost[i]个nums[i]，然后再求这个新数组的中位数，即为最终所要变成的数字，然后按照开销来计算最终的最少总开销；注意这里不能直接转化为新数组来求中位数，因为如果数据非常大的话，新数组的size会非常大，此时排序会报TLE，所以只能利用原数组排序 + cnt &gt;= (sum + 1) / 2这种方式来找中位数；

```cpp
class Solution {
public:
    long long minCost(vector<int>& nums, vector<int>& cost) {
        int n = nums.size();

        // 不改变原数组的情况下，得到排序索引数组，这样nums和cost还是一一对应的
        vector<int>pos(n, 0);
        for(int i = 0; i < n; i++) pos[i] = i;
        sort(pos.begin(),pos.end(),[&](auto &a,auto &b) {
            return nums[a] < nums[b];
        });

        // 将cost看作出现次数，中位数贪心
        long long sum = accumulate(cost.begin(), cost.end(), 0ll);
        long long target = 0, cnt = 0;
        for(int i = 0; i < n; i ++){
            cnt += cost[pos[i]];
            // 找到中位数
            if(cnt >= (sum + 1) / 2){
                target = nums[pos[i]];
                break;
            }
        }

        long long ans = 0;
        for(int i = 0; i < n; i ++){
            ans += 1ll * abs(nums[i]- target) * cost[i];
        }
        return ans;
    }
};
```

## 题单

[相关讨论](https://leetcode.cn/circle/discuss/g6KTKL/)

# <b>数学</b>

# <b>思维题</b>

# 华为校招题单

#### <b>P1497</b><u>  2024.8.21-秋招-第1题-数据重删</u>

NOT AC，思路：华为的机考题，一般都需要先从繁琐的文字描述中翻译出简单的模型，然后再尝试去做；这一题翻译过来，就是我们有很多个块，现在要对块去重，并统计每个块的个数；

很明显，我们需要一个哈希表来统计，每个块的个数；但是这里我们需要输出和输入是一致的，所以我们同时要记录块放入哈希表时的顺序；

除此之外，有几个坑点

(1) 输入输出，原始数据我们使用vector&lt;int&gt;来存，然后放入哈希表，key的话如果是数组的话放入哈希表，还要自定义哈希函数比较麻烦，所以我们一般是转化为字符串，这样可以直接放入哈希表，那么问题来了，如何优雅的转化为字符串呢；

如果块的大小是2的话，元素12，34和元素123，4如果直接放入哈希表，那么得到的是一样的块1234，但是很明显这两个列表形成的块是不同的，所以我们转化字符串的时候，需要在元素和元素直接加上分隔符（，或者空格都可以），将int数组转化为字符串我们一般使用stingstream操作比较简单，将int对象转化为字符串一般使用to_string；

最后我们输出的时候，其实最简单的方式是自己定义一个output的格式化string，然后自己最后可以pop出最后的空格，这也是输入输出的技巧

(2) 哈希表一定要记录块放进哈希表的顺序，因为我们哈希表内部是无序的，记录顺序的话，一般直接使用一个同步的unique vector数组。

本题是一个很好的，锻炼acm的输入输出，还有字符串转化的题目，核心逻辑不难，但是输入输出还有坑点比较多

```cpp
#include <bits/stdc++.h>

using namespace std;  

int main() {  
    // 处理输入
    int N, K;  
    cin >> N >> K; 
    vector<int> data(N);  
    for (int i = 0; i < N; ++i) cin >> data[i]; 

    unordered_map<string, int> block_count; // 哈希表统计每个块的出现次数    
    vector<string> unique_blocks;           // 记录块放入哈希表时的顺序

    // 切分每个块
    for (int i = 0; i < N; i += K) {  
        // 拿到块数组
        int current_block_size = min(K, N - i);  
        vector<int> block(data.begin() + i, data.begin() + i + current_block_size); // 获取当前块  
        
        // 将块数组转换为字符串，便于哈希索引  
        stringstream ss;  
        for (int num : block) {  
            ss << num << ",";  
        }

        // 放入哈希表，并记录放入的顺序
        string block_str = ss.str();  
        if (block_count.count(block_str)) {
            block_count[block_str]++;
        }
        else {
            // 初次放入哈希表，记录顺序
            block_count[block_str]++;
            unique_blocks.push_back(block_str);
        }
    }

    // 输出
    string output; // 使用字符串输出，方便最后pop空格
    for (const auto& block_str: unique_blocks) {
        stringstream ss(block_str);
        string token;
        while (getline(ss, token, ',')) {
            output += (token + " ");
        }
        output += (to_string(block_count[block_str]) + " ");
    }
    output.pop_back();
    cout << output << endl;
    return 0;    
}
```

#### <b>P1498</b>[  2024.8.21-秋招-第2题-Devops任务调度](https://codefun2000.com/d/HWHW/p/P1498)

NOT AC，思路：又是一道模拟题，也是先翻译，我们有两个序列，task序列，machine序列，我们想让machine序列去匹配task序列，其中task序列有优先级，必须头部先匹配才能匹配下一个，machine序列每次匹配消耗掉一个对应的machine即可，循环匹配，machine序列不关注顺序。然后machine序列里，还有一个万能机器，它只能转化为一种机器。

说几个注意点

(1) 注意task序列是有优先级的，一开始我是直接统计task和machine的01个数，这样做是不对的，因为这样做意味着可以先匹配后面的task

(2) 2号机器只能转化为一种，我们有两种思路

贪心：直接贪心，将2号机器留到当前machine序列无法匹配时，才进行转化，使用队列模拟，得到2号机器转化为哪一种

枚举：直接分类讨论，转化为0或1，直接分类讨论代码更简单

不考虑顺序，直接使用数量

```cpp
#include <bits/stdc++.h>

using namespace std;

int n;
vector<int> tasks, machines;

int calMatchCount(int machines_zeros, int machines_ones);

int main()
{
    // 处理输入
    cin >> n;
    tasks.resize(n), machines.resize(n);
    for (int i = 0; i < n; i ++) cin >> tasks[i];
    for (int i = 0; i < n; i ++) cin >> machines[i];

    // task序列的匹配明确了优先级，必须前面的先匹配
    // machine序列匹配task[i]，循环匹配，每次匹配掉一个task[i]就行
    // 没有规定必须用前面的machine[i]先去匹配, 跟顺序无关，只跟每种type的数量有关
    int machines_zeros = 0, machines_ones = 0, machines_twos = 0;
    for (int i = 0; i < n; i ++) {
        machines_zeros += (machines[i] == 0);
        machines_ones += (machines[i] == 1);
        machines_twos += (machines[i] == 2);
    }
    
    // 类型2都转为0或者1
    int choose_zero_ans = calMatchCount(machines_zeros + machines_twos, machines_ones);
    int choose_one_ans = calMatchCount(machines_zeros, machines_ones + machines_twos);
    int ans = min(n - choose_zero_ans, n - choose_one_ans);
    
    cout << ans << endl;
    return 0;
}

// 计算匹配总数
int calMatchCount(int machines_zeros, int machines_ones) {
    int match_cnt = 0;
    for (int i = 0; i < n; i ++) {
        if (tasks[i] == 0) machines_zeros--;
        else machines_ones--;
        if (machines_zeros < 0 || machines_ones < 0) break;
        match_cnt++;
    }
    return match_cnt;
}
```

贪心 + 队列 模拟

```cpp
#include <iostream>  
#include <vector>  
#include <queue>  

using namespace std;

int n;
vector<int> tasks;
vector<int> machines;
queue<int> machine_queue;

int main() {  
    // 输入
    cin >> n;               
    tasks.resize(n);        
    machines.resize(n);       

    for (int i = 0; i < n; ++i) cin >> tasks[i];       
    for (int i = 0; i < n; ++i) cin >> machines[i];   
    for (int i = 0; i < n; ++i) machine_queue.push(machines[i]);  
    
    // machine序列匹配task序列的过程，使用队列维护
    bool use_machine2 = false;
    for (size_t task_idx = 0; task_idx < tasks.size(); task_idx ++) {  
        bool ok = false;
        // 遍历队列，但是还要push的时候，使用队列大小遍历
        int queue_size = machine_queue.size();
        for (int machine_idx = 0; machine_idx < queue_size; machine_idx ++) {
            int machine = machine_queue.front();  
            machine_queue.pop(); 

            // 匹配，直接退出，去匹配下一个task_idx
            if (tasks[task_idx] == machine) {  
                ok = true;
                break;
            }
            // 不匹配，把当前machine放入队尾
            else {    
                machine_queue.push(machine);
            } 
        }
        
        // 队列为空，结束匹配
        if (machine_queue.empty()) break;
        if (!ok ) {
            // 队列不为空，但是没有找到匹配的machine，使用machine2
            if (!use_machine2) {
                for (int i = 0; i < queue_size; i ++) {
                    int machine = machine_queue.front();
                    machine_queue.pop();
                    if (machine == 2) machine = tasks[task_idx];
                    machine_queue.push(machine);
                }
                use_machine2 = true;
                task_idx --;  // 继续匹配当前的task_idx
            }
            else break;  // 否则结束匹配
        } 
    }

    cout << machine_queue.size() << endl;  
    return 0;  
}
```

#### <b>P1494</b>[  2024.8.28-秋招-第1题-老鼠串门](https://codefun2000.com/d/HWHW/p/P1494)

NOT AC，思路：这道题比较裸，翻译过来其实就是给出入栈序列，求出栈序列。主要就是 栈 + 模拟，模拟这个入栈出栈的过程，其中我们发现如果栈中出现过即将入栈的元素，那么就要它后面的元素都pop出来，为了判断出现过，我们使用set去同步维护，这在栈的题目里经常出现，使用其他的数据结构同步维护。

```cpp
#include <bits/stdc++.h>

using namespace std;

int main()
{
    vector<int> a;
    int x;
    while (cin >> x) a.push_back(x);
    int n = a.size();

    stack<int> stk;
    unordered_set<int> set;
    vector<int> ans;

    for (int i = 0; i < n; i ++) {
        int x = a[i];
        if (!set.count(x)) {
            stk.push(x);
            set.insert(x);
        }
        else {
            while (stk.top() != x) {
                auto top = stk.top(); stk.pop();
                ans.push_back(top);
                set.erase(top);
            }
            ans.push_back(stk.top());
        }
    }

    // 将最后还在栈里的元素弹出，放入出栈序列
    while (!stk.empty()) {
        auto top = stk.top(); stk.pop();
        ans.push_back(top);
    }

    for (int i = 0; i < n; i ++) cout << ans[i] << " ";

    return 0;
}
```

#### <b>P1495</b><u>  2024.8.28-秋招-第2题-数组消除</u>

NOT AC，思路：这道题的翻译比较难，本质上是在原序列里找所有d = interval的等差序列，然后找到长度最长的那个等差序列，答案是这个等差序列的起点。

找所有d = interval的等差序列：这里使用同余 + 哈希表，等差序列一个很重要的性质是同余，等差序列 其实就是一个同余类，所以我们利用同余去找等差序列，然后这里要找到长度最长的，所以我们使用哈希表记录每个等差序列的长度，也就是同余类的个数。

注意一点：同余类的起点 不是等差序列的起点，所以我们需要再开一个哈希表或者在原来的哈希表里使用pair记录同余类对应的等差序列的起点。

```cpp
#include <bits/stdc++.h>

using namespace std;

int main()
{
    // 输入
    int n;
    cin >> n;

    vector<int> a(n);
    for (int i = 0; i < n; i ++) cin >> a[i];

    int interval;
    cin >> interval;

    // 统计序列所有d = interval的等差序列，使用同余 + 哈希表
    unordered_map<int, int> diff_count;  // 记录每个同余类的count
    unordered_map<int, int> diff_start;  // 记录每个同余类的min_start
    int d = interval;

    // 遍历序列，转化为同余序列，放入哈希表
    for (int i = 0; i < n; i ++) {
        int diff_mod = a[i] % d;
        diff_count[diff_mod] ++;

        if (diff_start[diff_mod] == 0) diff_start[diff_mod] = a[i];
        else diff_start[diff_mod] = min(diff_start[diff_mod], a[i]);
    }

    int ans = 1e8;
    int max_count = 0;
    // 找到同余类count最大的，然后拿到它的min_start
    for (auto& [diff_mod, count]: diff_count) {
        if (count >= max_count) {
            if (count == max_count) {  // count相等的时候 ans取最小的
                ans = min(ans, diff_start[diff_mod]);
                max_count = count;
            }
            else {   // count不等的时候，ans更新，千万不能取min(ans, diff_start[diff_mod])
                ans = diff_start[diff_mod];
                max_count = count;
            }
        }
    }

    cout << ans << endl;

    return 0;
}
```

最后说一个坑点

```cpp
// if (count >= maxCount) {  
//     maxCount = count;  
//     bestStart = min(bestStart, start);  
// }  

if (count > maxCount || (count == maxCount && start < bestStart)) {  
    maxCount = count;  
    bestStart = start;  
}  

我们虽然bestStart要取最小的，但是一定要记住取最小的前提是 count = maxCount, count > maxCount的时候
是直接更新，而不是取最小；
如果我们按照注释的代码来做

count start
24 32 31 53

如果按照注释的写法，那么ans = 1，因为我们从count 3->5的时候 取了最小，这样所以是1，可是题目要求的其实
是如果最大的count有多个，取最小的start，所以下面没有注释的代码才是符合要求的。
```

#### <b>P1496</b>[  2024.8.28-秋招-第3题-参加博览会](https://codefun2000.com/d/HWHW/p/P1496)

NOT AC，这道题的难度还是非常大的，还是先翻译，坐标轴上有很多个区间，我们在每个点上，可以选择包含这个点的k个区间，求选择的最多区间数。

其实这是leetcode 1353的变种题。先去看一下leetcode1353的题解，然后说这道题

贪心 + 优先队列

我们每次选择 包含这个点里 end最小的k个区间

最后注意一个坑点，就是区间之间存在很大的gap的时候，我们需要跳过这段gap，否则会超时！

直接照搬，但是不跳过gap会超时

```cpp
#include <bits/stdc++.h>

using namespace std;

int n, k, starti, endi;
unordered_map<int, vector<int>> start_ends;
priority_queue<int, vector<int>, greater<>> pq;

int main()
{   
    cin >> n >> k;
    int max_day = 0;
    for (int i = 0; i < n; i ++) {
        cin >> starti >> endi;
        start_ends[starti].emplace_back(endi);
        max_day = max(max_day, endi);
    }
    
    int ans = 0;
    for (int i = 1; i <= max_day; i ++) {
        // 合法的end入堆
        for (auto& end: start_ends[i]) {
            pq.push(end);
        }

        // 不合法的end出堆
        while (!pq.empty() && pq.top() < i) {
            pq.pop();
        }

        // 选出最小的k个参加
        int cnt = k;
        while (!pq.empty() && cnt--) {
            pq.pop();
            ans ++;
        }
    }

    cout << ans << endl;
    
    return 0;
}
```

通过直接遍历区间，可以跳过gap，解决超时

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>

using namespace std;

int main() {
    int n, k; // 输入博览会的数量n和每次可以参加的博览会数量k
    cin >> n >> k;
    
    vector<vector<int>> a(n, vector<int>(2)); // 用于存储博览会的开始和结束时间
    for (int i = 0; i < n; i++) {
        cin >> a[i][0] >> a[i][1]; // 读取开始和结束时间
    }

    // 根据开始时间排序
    sort(a.begin(), a.end(), [](const vector<int>& x, const vector<int>& y) {
        return x[0] < y[0];
    });

    int start = 0; // 当前时间
    priority_queue<int, vector<int>, greater<int>> queue; // 最小堆用于存储结束时间
    int idx = 0; // 当前处理的博览会索引
    int ans = 0; // 参加的博览会数量

    while (idx < n || !queue.empty()) {
        // 移除已结束的博览会
        while (!queue.empty() && queue.top() < start) {
            queue.pop();
        }

        // 添加当前可以参加的博览会
        while (idx < n && a[idx][0] <= start) {
            queue.push(a[idx][1]); // 将结束时间加入优先队列
            idx++;
        }

        // 如果没有可参加的博览会，更新开始时间
        if (queue.empty()) {
            if (idx == n) break;
            start = max(start, a[idx][0]);
            continue;
        }

        // 参加博览会
        for (int i = 0; i < k; i++) {
            if (!queue.empty()) {
                ans++; // 参加博览会
                queue.pop(); // 弹出结束时间
            }
        }

        start++; // 增加当前时间
    }

    cout << ans << endl; // 输出参加的博览会数量
    return 0; // 结束程序
}
```

# 华为OD题单

## 模拟

#### P1013. 绘图机器/计算面积(100分)

NOT AC，思路：计算每一个块的面积，每一个块的面积 = (x - pre_x) * abs(pre_y); 然后不要忘记计算最后终点块的面积

```cpp
#include <bits/stdc++.h>

using namespace std;

int n, e;

int main()
{
    cin >> n >> e;
    int pre_x = 0, pre_y = 0;
    long long total = 0;   // 使用long long 避免溢出
    
    while (n --) {
        int x, offset_y;
        cin >> x >> offset_y;

        // 当前块的底和高
        int l = x - pre_x;
        int h = abs(pre_y);

        // 计算面积，然后更新pre_x, pre_y为当前的x，y
        int area = l * h;
        total += area;
        pre_x = x;
        pre_y = pre_y + offset_y;
    }

    // 不要忘记算最后终点块的面积
    total += (e - pre_x) * abs(pre_y);

    cout << total << endl;
    return 0;
}
```

#### P1020. 密码解密(100分)

NOT AC，思路：我一开始的思路是，每三个作为一个token去判断，如果三个里面最后一个是*说明是10 -26，如果不足三个或者是最后一个不是*说明是1-9；但发现如果碰上1223*这种情况我们的解法是错误的；

所以我们需要把*及其前面的两个字符去优先匹配；需要考虑到数据结构，可以先把前面的字符缓存起来，这里采用队列去缓存字符

如果当前字符不是*，缓存，如果当前字符是*处理队列里的字符；然后注意特殊情况，最后的字符不是*，也要处理队列里的字符，此时都是1-9；

```cpp
#include <bits/stdc++.h>

using namespace std;

string s;
queue<int> q;

int main()
{
    cin >> s;
    int n = s.size();
    string res = "";
    
    for (int i = 0; i < n; i ++) {
        if (s[i] != '*') {
            q.push(s[i] - '0');
        }
        else {
            // 先把前面的单个字符pop出来；
            while (q.size() > 2) {
                int cur = q.front(); q.pop();
                res += cur - 1 + 'a';
            }
            // 再把*匹配的字符pop出来
            char cur1 = q.front(); q.pop();
            char cur2 = q.front(); q.pop();
            int num = cur1 * 10 + cur2;
            res += num - 1 + 'a';
        }
    }

    // 如果最后一个字符不是*，处理最后一段字符
    while (q.size()) {
        int cur = q.front(); q.pop();
        res += cur - 1 + 'a';
    }

    cout << res << endl;
    return 0;
}
```

#### P1021. 最大坐标值(100分)

AC，思路：模拟题比较简单，每次计算出当前的坐标，然后更新最大坐标即可

```cpp
#include <bits/stdc++.h>

using namespace std;

int n, m;

int main()
{
    cin >> n >> m;

    int max_pos = 0;
    int cur = 0;
    while(n --) {
        int x;
        cin >> x;

        if (x == m) {
            if (x < 0) x --;
            else x ++;
        }
        cur += x;
        max_pos = max(max_pos, cur);
    }
    cout << max_pos << endl;

    return 0;
}
```

#### P1022. 查找接口成功率最优时间段(100分)

AC，思路：这题时间复杂度没有限制，所以直接暴力枚举所有子串，然后统计答案数组

```cpp
#include <bits/stdc++.h>

using namespace std;
typedef pair<int,int> pii;

int x;
vector<int> a;
vector<pii> ans;

int main()
{
    cin >> x;
    int e;
    while (cin >> e) a.push_back(e);

    int n = a.size(), max_len = 0;
    for (int i = 0; i < n; i ++) {
        for (int j = 0; j <= i; j ++) {
            int len = i - j + 1;
            int sum = accumulate(a.begin() + j, a.begin() + i + 1, 0);
            if (sum <= len * x) {
                if (len > max_len) {
                    ans.clear();
                    ans.push_back({j, i});
                    max_len = len;
                }
                else if (len == max_len) ans.push_back({j, i});
            }
        }
    }

    for (auto& [j, i]: ans) {
        cout << j << "-" << i << " ";
    }
    return 0;
}
```

#### 
## 双指针

#### <b>P1014</b>[  最长的指定瑕疵度的元音子串(200分)](https://codefun2000.com/d/hwod/p/P1014)

NOT AC，不得不说，笔试题目确实灵活性比leetcode高很多，还是要多做笔试题目。这题看到最长子串，首先想到滑动窗口，然后滑动窗口需要证明单调性，单调性体现在，窗口维护的性质，扩展和收缩时都满足单调性，窗口维护的时瑕疵度，扩展时单调递增，收缩时单调递减，所以满足单调性，使用滑动窗口。

然后判断元音子串，就比较简单了。

```cpp
#include <bits/stdc++.h>

using namespace std;  

// 判断字符是否为元音  
bool isVowel(char c) {  
    unordered_set<char> vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};  
    return vowels.count(c) > 0;  
}  
 
int main() {  
    int flaw;  
    string s;  

    // 输入瑕疵度和字符串  
    cin >> flaw;  
    cin >> s;  
 
    int n = s.size();
    int cnt = 0;  // 窗口维护瑕疵度
    int ans = 0;  // 最大长度   

    // 滑动窗口使用cnt维护瑕疵度
    for (int i = 0, j = 0; i < n; i ++) {  
        // 右端点滑入，如果当前字符不是元音，则增加瑕疵度  
        if (!isVowel(s[i])) {  
            cnt ++;  
        }  

        // 找最长，cnt > flaw时收缩窗口
        while (j <= i && cnt > flaw) {  
            if (!isVowel(s[j])) {  
                cnt --;  
            }  
            j++;  
        }  

        // 检查是否为有效的元音子串  
        if (cnt == flaw && isVowel(s[j]) && isVowel(s[i])) {  
            ans = max(ans, i - j + 1);  
        }  
    }  

    // 窗口没有移动也是0，不需要特判
    cout << ans << endl;  

    return 0;  
}
```

#### <b>P1015</b>[  橱窗宝石(100分)](https://codefun2000.com/d/hwod/p/P1015)

AC，笔试题一般先翻译，其实就是求最长 和不超过val的 子数组长度，不定长滑动窗口解决

```cpp
#include <bits/stdc++.h>

using namespace std;

int main()
{
    // 输入
    int n, val;
    cin >> n;

    vector<int> gems(n);
    for (int i = 0; i < n; i ++) cin >> gems[i];
    cin >> val;

    int sum = 0;
    int ans = 0;
    for (int i = 0, j = 0; i < n; i ++) {
        // 窗口扩展
        sum += gems[i];

        // 窗口收缩
        while (j <= i && sum > val) {
            sum -= gems[j];
            j++;
        }

        // 判断答案
        if (sum <= val) {
            ans = max(ans, i - j + 1);
        }
    }

    cout << ans << endl;
    return 0;
}
```

## 二分

#### <b>P1017</b><u>  孙悟空吃蟠桃(200分)</u>

AC，思路：其实就是leetcode原题[875. 爱吃香蕉的珂珂](https://leetcode.cn/problems/koko-eating-bananas/)

注意输入，while(cin)会读完所有的行，而不是仅读一行，所以我们只能先getline第一行，然后使用stringstream解析数据

```cpp
#include <bits/stdc++.h>

using namespace std;

int n, h;
vector<int> a;

bool check(int v);

int main()
{   
    // 输入，必须使用getline读第一行
    string line;
    getline(cin, line);
    stringstream ss(line);
    int num;
    while (ss >> num) {
        a.push_back(num);
        n ++;
    }
    cin >> h;

    // 二分答案，速度越大，越能在h小时内吃完
    int l = 0, r = 10000;
    while (l <= r) {
        int mid = (l + r) / 2;
        if (check(mid)) r = mid - 1;
        else l = mid + 1;
    }

    int ans = (r == 10000) ? 0 : r + 1;
    cout << ans << endl;

    return 0;
}

// 判断当前速度，能不能在h小时内吃完
bool check(int v) {
    if (v == 0) return false;

    long long total_time = 0;   // 注意求和溢出
    for (int i = 0; i < n; i ++) {
        int time = (a[i] + v - 1) / v;
        total_time += time;
    }
    return total_time <= h;
}
```

#### <b>P1035</b>[  部门人力分配(200分)](https://codefun2000.com/d/hwod/p/P1035)

NOT AC，这题的意思首先就很难理解，翻译一下，就是现在有n个需求，然后有m个月，每个月需要固定的人力，求m个月可以完成的最小人力。我们尝试二分答案，最小人力越大，m个月完成越容易满足，所以可以二分答案。

但是这里有个坑，那就是如果人力比最大需求小，那么无论多少个月也无法完成，所以我们需要在check开头判断，或者干脆把二分下界设为需求最大值。

然后就是选定人力后，每个月做需求的时候，为了使月份满足要求，我们贪心地每次尽可能地做 多 的需求，也就是尽可能满足2个需求，尽可能做需求量多的需求，所以我们这里使用双指针来贪心的选取最大最多的需求。

```cpp
#include <bits/stdc++.h>

using namespace std;

int m, n;
vector<int> a;

bool check(int x);

int main()
{
    cin >> m;
    int x;
    while (cin >> x) {
        a.push_back(x);
        n ++;
    }

    sort(a.begin(), a.end());

    // 二分答案 最小人力越大 m个月内越可以完成
    int l = 0, r = 1e9;
    while (l <= r) {
        int mid = (l + r) / 2;
        if (check(mid)) r = mid - 1;
        else l = mid + 1;
    }
    
    int ans = (r == 1e9) ? 0 : r + 1;
    cout << ans << endl;

    return 0;
}

bool check(int k) {
    // 如果人力 < 需求最大值，永远完不成所有需求
    if (k < a[n - 1]) return false; 

    // 要想人力小，贪心，每个月尽可能多的完成需求
    // 优先做大的, 尽量做两个需求
    int cnt = 0;  // 月数
    int l = 0, r = n - 1;
    while (l <= r) {
        if (l != r && a[l] + a[r] <= k) {
            l++, r--; 
        }
        else r--;
        cnt ++;
    }
    return cnt <= m;
}
```

优化

```cpp
#include <bits/stdc++.h>

using namespace std;

int m, n;
vector<int> a;

bool check(int x);

int main()
{
    cin >> m;
    int x;
    while (cin >> x) {
        a.push_back(x);
        n ++;
    }

    sort(a.begin(), a.end());

    // 二分答案 最小人力越大 m个月内越可以完成
    
    // 如果人力 < 需求最大值，永远完不成所有需求，所以下界设为a[n - 1]
    int l = a[n - 1], r = 1e9;
    while (l <= r) {
        int mid = (l + r) / 2;
        if (check(mid)) r = mid - 1;
        else l = mid + 1;
    }
    
    int ans = (r == 1e9) ? 0 : r + 1;
    cout << ans << endl;

    return 0;
}

bool check(int k) {
    // 要想人力小，贪心，每个月尽可能多的完成需求
    // 优先做大的, 尽量做两个需求
    int cnt = 0;  // 月数
    int l = 0, r = n - 1;
    while (l <= r) {
        if (l != r && a[l] + a[r] <= k) {
            l++, r--; 
        }
        else r--;
        cnt ++;
    }
    return cnt <= m;
}
```

## 哈希表

#### <b>P1003</b>[  掌握单词数(100分)](https://codefun2000.com/d/hwod/p/P1003)

AC，思路：首先翻译题目，判断每个word的字符集合 是否是 chars的字符集合的子集合。

tips：子串，子序列，子集合，子串是子集合 + 顺序 + 连续，子序列是 子集合 + 顺序，子集合就是要统计两者的集合的所有元素的出现次数，然后判断一个集合是否是另一个集合的子集合

```cpp
#include <bits/stdc++.h>
#include <climits>

using namespace std;

int main()
{
    // 输入
    int n;
    cin >> n;

    vector<string> words;
    string word;
    for (int i = 0; i < n; i ++) {
        cin >> word;
        words.push_back(word);
    }

    string chars;
    cin >> chars;

    // 统计chars的字符集合
    unordered_map<char, int> chars_map;
    int magic_cnt = 0;
    for (int i = 0; i < (int)chars.size(); i ++) {
        chars_map[chars[i]] ++;
        if (chars[i] == '?') magic_cnt ++;
    }

    int ans = 0;
    // 判断word的字符集合 是否 是chars的字符集合
    for (int i = 0; i < (int)words.size(); i ++) {
        // 统计word字符集合
        unordered_map<char, int> word_map;
        string word = words[i];
        for (int j = 0; j < (int)word.size(); j ++) {
            word_map[word[j]] ++;
        }

        bool flag = true;
        int cnt = magic_cnt;

        // 判断是否是 chars的字符集合的子集合
        for (int j = 0; j < 26; j ++) {
            char c = j + 'a';
            if (word_map[c] <= chars_map[c]) continue;
            else {
                if (cnt == 0 || chars_map[c] + cnt < word_map[c]) {
                    flag = false;
                    break;
                }
                else {
                    // 每次拼写，万能字符可以当作多种字符，而不是一种字符 
                    cnt -= (word_map[c] - chars_map[c]);
                }
            }
        }
        ans += (flag == true);
    }

    cout << ans << endl;

    return 0;
}
```

优化的时候，考虑diff数组，我们可以直接在chars的哈希表上减去word的每个字符的出现次数去判断，是否为子集合。https://blog.csdn.net/m0_73659489/article/details/134498199

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=110;
string w[N],t;
int n;
vector<int>cnts(26,0);  //记录匹配串每个字符的数量
int ask=0;  //问号字符的数量
bool check(string &s){  //检查当前匹配串能否匹配字符串s
    auto v=cnts;
    int num=ask; //当前可用的问号数量
    for(char &ch:s){
        int u=ch-'a';
        if(v[u]==0&&num==0){  //当前没有字母可以匹配，也没有问号可以匹配
            return false;
        }
        else if(v[u]){  //如果有字母可以匹配，优先匹配字母
            --v[u];
        }
        else{
            num--;
        }
    }
    return true;
}
int main(){
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>w[i];
    }
    cin>>t;
    for(auto &ch:t){
        if(ch=='?')ask++;
        else cnts[ch-'a']++;
    }
    int res=0;  //统计最终匹配的单词个数
    for(int i=0;i<n;i++){
        if(check(w[i]))res++;
    }
    cout<<res<<endl;
    return 0;
}
```

#### <b>P1002</b>[  API集群负载统计(100分)](https://codefun2000.com/d/hwod/p/P1002) 其实是模拟

AC，思路：直接模拟，然后解析每个字符串

```cpp
#include <bits/stdc++.h>

using namespace std;

int main()
{
    // 输入
    int n;
    cin >> n;

    vector<string> urls;
    for (int i = 0; i < n; i ++) {
        string url;
        cin >> url;
        urls.push_back(url);
    }

    int level;
    cin >> level;
    string key;
    cin >> key;

    // 解析每个url
    int ans = 0;
    for (int i = 0; i < n; i ++) {
        string url = urls[i];

        stringstream ss(url);
        string token;
        int cnt = 0;
        while (getline(ss, token, '/')) {
            if (cnt == level) {
                // cout << token << endl;
                if (token == key) ans ++;
            }
            cnt ++;
        }
    }
    cout << ans << endl;

    return 0;
}
```

## 排序

#### <b>P1016</b>[  智能成绩表(100分)](https://codefun2000.com/d/hwod/p/P1016)

NOT AC, 这一题首先要思考，用什么数据存储，一般复杂的数据，我们考虑自己封装类对象进行存储，这里使用struct Student进行存储。

然后就是排序，排序主要考察自定义排序 写法比较固定，bool compare(const xx& a, const xx& b)

最后就是思考根据什么排序，我们是根据分数排序，考虑到我们用的类对象，实际就是要知道Student对象的分数数组里对应的学科分数的下标sortIndex，我们知道对于每个Student对象里分数数组的下标和subjects数组的下标是一致的，所以我们可以直接在subjects数组里找到分数下标sortIndex。

```cpp
#include <bits/stdc++.h>

using namespace std;

// student结构体
struct Student {
    string name;        // name
    vector<int> scores; // 分数数组
    int totalScore;     // 总分
};

const int N = 100;
const int M = 10;
Student students[N]; // 学生数组
string subjects[M];  // 学科数组

int sortIndex; // 用于排序的分数下标

// 自定义排序函数
bool compare(const Student& a, const Student& b) {
    if (sortIndex == -1) {
        if (a.totalScore != b.totalScore) return a.totalScore > b.totalScore;  // 下标不存在比较总分
        else return a.name < b.name;
    }
    else {
        if (a.scores[sortIndex] != b.scores[sortIndex])      // 下标存在，比较对应下标分数
            return a.scores[sortIndex] > b.scores[sortIndex];
        else return a.name < b.name; // 分数相同，按名字字典序排序
    }
}

int main() {    
    // 输入
    int n, m; 
    cin >> n >> m;

    for (int i = 0; i < m; i++) cin >> subjects[i];

    for (int i = 0; i < n; i++) {
        cin >> students[i].name;
        int sum = 0;
        for (int j = 0; j < m; j++) {
            int score;
            cin >> score;
            students[i].scores.push_back(score);
            sum += score;
        }
        students[i].totalScore = sum;
    }

    string key;
    cin >> key;

    // 找要排序的分数下标
    sortIndex = -1;
    for (int i = 0; i < m; i++) { 
        if (subjects[i] == key) {
            sortIndex = i;
            break;
        }
    }
    sort(students, students + n, compare); // 排序
    
    // 输出
    string output = "";
    for (int i = 0; i < n; i++) {
        output += (students[i].name + " ");
    }
    output.pop_back();
    cout << output << endl;

    return 0;
}
```

#### <b>P1041</b>[  字符串筛选排序(100分)](https://codefun2000.com/d/hwod/p/P1041)

NOT AC，思路：这题我想复杂了，我以为要自定义排序，其实仔细看，按照ascii码排序，直接sort就可以了；然后找最小索引，这里其实是要使用到原来的字符串，所以这题的核心，就是要保留原来的字符串，然后在新的排序的字符串中找到目标字母，之后在原来的字符串上找最小索引

```cpp
#include <bits/stdc++.h>

using namespace std;

int main()
{
    // 输入
    string s;
    cin >> s;
    
    int k;
    cin >> k;

    // 按照ascii码排序
    string tmp = s;
    int n = tmp.size();
    sort(tmp.begin(), tmp.end());

    // 找到目标字符
    char target;
    if (k > n) target = tmp[n - 1];
    else target = tmp[k - 1];

    // 拿到目标字符在原来字符串中的最小位置索引
    int min_index = -1;
    for (int i = 0; i < n; i ++) {
        if (s[i] == target) {
            min_index = i;
            break;
        }
    }

    // 输出
    cout << min_index;
    return 0;
}
```

## 网格图

#### <b>P1026</b>[  小华和小为的聚餐地点(200分)](https://codefun2000.com/d/hwod/p/P1026)

NOT AC，翻译一下，从两个起点开始遍历，找到都访问过，并且网格值为3的点的个数。

很明显，我们对两个起点，各做一次bfs，然后网格图可以尝试将网格值更改代替是否访问过，但是需要考虑两点成立才行，已搜格子不影响继续搜素，所以值 = 1，已搜格子不影响后续判断，值需要不变，所以我们还是使用vis数组，注意对不同起点做BFS，使用两个vis数组

使用多个vis数组

```cpp
#include <bits/stdc++.h>

using namespace std;

// 网格图通用
vector<vector<int>> g;
int m, n;
int dx[4] = {0, -1, 0, 1}, dy[4] = {-1, 0, 1, 0};

// 网格图bfs通用
typedef pair<int, int> pii;
queue<pii> q;

// 访问数组
vector<vector<bool>> vis1, vis2;

void bfs(int sx, int sy, vector<vector<bool>>& vis);

int main()
{
    // 输入
    cin >> m >> n;
    g.resize(m, vector<int>(n, 0));
    vis1.resize(m, vector<bool>(n, false));
    vis2.resize(m, vector<bool>(n ,false));
    
    vector<pii> start_points;  // 存储两个起点
    for (int i = 0; i < m; i ++) {
        for (int j = 0; j < n; j ++) {
            cin >> g[i][j];
            if (g[i][j] == 2) {
                start_points.emplace_back(i, j);
            }
        }
    }

    // 从两个起点，各做一次bfs
    bfs(start_points[0].first, start_points[0].second, vis1);
    bfs(start_points[1].first, start_points[1].second, vis2);

    // 都访问过，并且值为3，那么就是聚餐位置
    int ans = 0;
    for (int i = 0; i < m; i ++) {
        for (int j = 0; j < n; j ++) {
            if (g[i][j] == 3 && vis1[i][j] && vis2[i][j]) ans ++;
        }
    }
    cout << ans << endl;

    return 0;
}

void bfs(int sx, int sy, vector<vector<bool>>& vis) {
    q.emplace(sx, sy);
    vis[sx][sy] = true;

    while (q.size()) {
        auto& [x, y] = q.front(); q.pop();
        for (int i = 0; i < 4; i ++) {
            int a = x + dx[i], b = y + dy[i];
            if (a < 0 || a >= m || b < 0 || b >= n) continue;
            if (!vis[a][b] && g[a][b] != 1) {
                q.emplace(a, b);
                vis[a][b] = true;
            }
        }
    }
}
```

状态压缩，使用一个vis数组，int的每一位对应每个人在这个点是否访问，所以我们每个人设置的val为1，2，4，...本质就是状态压缩；原来是每个数代表一个人，多个人使用数组；现在是每个bit代表一个人，多个人使用一个数就可以了。

```cpp
#include <bits/stdc++.h>

using namespace std;

// 网格图通用
vector<vector<int>> g;
int m, n;
int dx[4] = {0, -1, 0, 1}, dy[4] = {-1, 0, 1, 0};

// 网格图bfs通用
typedef pair<int, int> pii;
queue<pii> q;

// 只使用一个访问数组，多个人访问情况进行状态压缩
vector<vector<int>> vis;

void bfs(int sx, int sy, int val);

int main()
{
    // 输入
    cin >> m >> n;
    g.resize(m, vector<int>(n, 0));
    vis.resize(m, vector<int>(n));
    
    vector<pii> start_points;  // 存储两个起点
    for (int i = 0; i < m; i ++) {
        for (int j = 0; j < n; j ++) {
            cin >> g[i][j];
            if (g[i][j] == 2) {
                start_points.emplace_back(i, j);
            }
        }
    }

    // 从两个起点，各做一次bfs
    bfs(start_points[0].first, start_points[0].second, 1);
    bfs(start_points[1].first, start_points[1].second, 2);

    // 都访问过，并且值为3，那么就是聚餐位置
    int ans = 0;
    for (int i = 0; i < m; i ++) {
        for (int j = 0; j < n; j ++) {
            if (g[i][j] == 3 && vis[i][j] == 3) ans ++;
        }
    }
    cout << ans << endl;

    return 0;
}

void bfs(int sx, int sy, int val) {
    q.emplace(sx, sy);
    vis[sx][sy] |= val;

    while (q.size()) {
        auto& [x, y] = q.front(); q.pop();
        for (int i = 0; i < 4; i ++) {
            int a = x + dx[i], b = y + dy[i];
            if (a < 0 || a >= m || b < 0 || b >= n) continue;
            if (g[a][b] != 1 && (vis[a][b] & val) == 0) {
                q.emplace(a, b);
                vis[a][b] |= val;
            }
        }
    }
}
```

# LeetCode Hot100

### 哈希

#### [1. 两数之和](https://leetcode.cn/problems/two-sum/)

AC，思路：哈希表，快速查找元素基本应用；可以两种写法，枚举左端点，维护右边的哈希表，或者枚举右端点，维护左边的哈希表；考虑到前者既有插入也有删除，后者只有插入，所以一般选择后者，枚举右端点，维护左边的哈希表；

```cpp
// 在集合中查找元素，使用哈希表
// 还需要记录下标，使用unordered_map

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hash;
        vector<int> ans;
        int n = nums.size();
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < i; j ++) {
                if (hash.count(target - nums[i])) {
                    // cout << target - nums[i] << " " << nums[i] << endl;
                    ans.push_back(hash[target - nums[i]]);
                    ans.push_back(i);
                    return ans;
                }
            }
            hash[nums[i]] = i;
        }
        return ans;
    }
};
```

#### [49. 字母异位词分组](https://leetcode.cn/problems/group-anagrams/)

NOT AC，思路：将字符串分组放入哈希表中，哈希表中key是分组，value是分组中的字符串集；所以核心问题在于，哈希表的key是什么，我们要想办法找到一个分组中的字符串的共同特征；这里有一个技巧，异位词分组的每种字母出现次数都相同；所以对于key，我们最直接的设计思路就是这些字符串排序都是相同的，所以直接将排序后的字符串作为key；

另一种思路就是将每个出现次数大于 0 的字母和出现次数按顺序拼接成字符串，作为key;

排序字符串作为key

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> hash;
        vector<vector<string>> ans;

        for (const auto& str: strs) {
            string key = str;
            sort(key.begin(), key.end());
            hash[key].push_back(str);
        }

        for (auto& [k, v]: hash) {
            ans.push_back(v);
        }
        return ans;
    }
};
```

#### [128. 最长连续序列](https://leetcode.cn/problems/longest-consecutive-sequence/)

AC，思路：注意这里的序列不是子序列，当前的序列是可以随意取数组成序列；

暴力的做法，就是先排序，然后找每段连续数组（注意这里的连续数组可以包含相同的元素，计算长度的时候不包括它们即可）时间复杂度由排序决定了，O(nlogn)

哈希表：枚举当前的数，判断是否是连续序列起点（如果num - 1不存在，那么就是起点），如果是就判断后面num + 1, num + 2..是否存在，统计当前数作为起点的最大长度；遍历所有的起点，得到最大长度；其中判断是否存在，使用哈希表复杂度减小到O(1)，时间复杂度降低到O(n）

暴力做法：O(nlogn)

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());

        int ans = 0;
        for (int i = 0; i < n; i ++) {
            int len = 1;
            while (i + 1 < n && (nums[i + 1] == nums[i] + 1 || nums[i + 1] == nums[i])) {
                if (nums[i + 1] == nums[i]) i ++;
                else i ++, len ++;
            }
            ans = max(ans, len);
        }
        return ans;
        
    }
};
```

哈希表：O(n)

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> hash;
        for (auto num: nums) {
            hash.insert(num);
        }
        
        int ans = 0;
        for (auto num: nums) {
            int len = 1;
            if (!hash.count(num - 1)) {
                int cur = num + 1;
                while (hash.count(cur)) cur ++, len ++; 
            }
            ans = max(ans, len);
        }
        return ans;  
    }
};
```

#### 
### 双指针

#### [283. 移动零](https://leetcode.cn/problems/move-zeroes/)

AC，思路：很多种做法，最简单的想法就是先把非0元素放入数组，然后再把0元素放入数组

放入新数组：遍历原数组，非零元素放入新数组，同时统计0元素个数，然后0元素放入新数组，原数组 = 新数组

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int cnt = 0;
        vector<int> nums1;
        for (int num: nums) {
            if (num != 0) nums1.push_back(num);
            else cnt ++;
        }
        while(cnt --) nums1.push_back(0);
        nums = nums1; 
    }
};
```

覆盖原数组：遍历原数组，非0元素覆盖原数组，同时统计当前的非0元素的index，最后index - end覆盖成0元素

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int n = nums.size();
        int idx = 0;   // 非零元素的遍历index
        for (int i = 0; i < n; i ++) {
            if (nums[i] != 0) {
                nums[idx++] = nums[i];
            }
        }

        // 现在idx为第一个0元素的位置，补齐0即可
        for (int i = idx; i < n; i ++) {
            nums[i] = 0;
        }
    }
};
```

#### [11. 盛最多水的容器](https://leetcode.cn/problems/container-with-most-water/)

AC，思路：相向双指针模板题，首先找到单调性发现可以双向双指针，最后再根据木桶原理，只能移动短板

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int n = height.size();
        int l = 0, r = n - 1;
        
        int ans = 0;
        while (l < r) {
            int w = r - l, h = min(height[l], height[r]);
            int area = w * h;
            ans = max(ans, area);
            // 移动长板没有意义面积绝对会变小，移动短板面积才有增大的可能性
            if (height[l] < height[r]) l++;
            else r --; 
        }
        return ans;
    }
};
```

#### [15. 三数之和](https://leetcode.cn/problems/3sum/)

NOT AC，思路：双指针模板题，但是我犯了一个错误，我把l,r的去重逻辑写在了sum != 0的情况里，但其实应该现在满足条件的情况里，毕竟我们是对满足条件的情况去重！

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        vector<vector<int>> ans;
        for (int i = 0; i < n - 2; i ++) {
            if (i - 1 >= 0 && nums[i] == nums[i - 1]) continue;
            int l = i + 1, r = n - 1;
            while (l < r) {
                int sum = nums[i] + nums[l] + nums[r];
                if (sum == 0) {
                    ans.push_back({nums[i], nums[l], nums[r]});
                    // l,r的去重逻辑一定要写在满足条件的情况里！
                    do l ++; while (l < r && nums[l] == nums[l - 1]);
                    do r --; while (r > l && nums[r] == nums[r + 1]);
                }
                else if (sum > 0) r--;
                else if (sum < 0) l ++;
            }
        }
        return ans;
    }
};
```

#### [42. 接雨水](https://leetcode.cn/problems/trapping-rain-water/)

NOT AC，思路：

前后缀分解：首先图中的每个位置，我们看作是一个宽度为1的桶，首先我们要统计每个桶的容量，那就是要算出木桶的高，木桶的左板高度其实就是左边的最大值，我们可以利用前缀最大值O(1)计算，木桶的右板高度就是右边的最大值，我们可以利用后缀最大值O(1)计算，这样我们的木桶容量就得出来了，也就是min(左板高度，右板高度）* 宽度1；但是我们实际接雨水的容量需要减去原本的体积，所以每个木桶接雨水的容量 = min(左板高度，右板高度）* 1 - height * 1;

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size();
        
        // 数组从1开始，方便构造前后缀数组;
        vector<int> pre_max(n + 1);
        for (int i = 1; i <= n; i ++) pre_max[i] = max(pre_max[i - 1], height[i - 1]);
    
        vector<int> suf_max(n + 2);
        for (int i = n; i >= 1; i --) suf_max[i] = max(suf_max[i + 1], height[i - 1]);
        
        int ans = 0;
        // 遍历数组 1~n
        for (int i = 1; i <= n; i ++) {
            ans += min(pre_max[i], suf_max[i]) - height[i - 1];
        }
        return ans;
    }
};
```

#### 
### 滑动窗口

#### [3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

AC，思路：滑动窗口模板题，窗口维护无重复字符，窗口用哈希表统计字符出现次数去维护

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.size();
        // 滑动窗口维护无重复字符，用哈希表记录字符出现次数
        unordered_map<char, int> hash;
        int ans = 0;
        // 滑动窗口，求最长，最小的j，while不满足
        for (int i = 0, j = 0; i < n; i ++) {
            hash[s[i]]++;  // 右端点滑入
             // 之前无重复，现在不满足，只有可能是新加入的字符导致
            while(hash[s[i]] > 1) {
                hash[s[j]] --;  //左端点滑出
                j ++;
            }
            ans = max(ans, i - j + 1); 
        }
        return ans;   // 考虑到窗口未滑动的情况下，ans = 0; 直接返回ans
    }
};
```

#### [438. 找到字符串中所有字母异位词](https://leetcode.cn/problems/find-all-anagrams-in-a-string/)

NOT AC，思路：在s中找p的异位词子串，可以固定长度的滑动窗口来做，然后每次判断s和p是否为异位词；那么如何判断呢，就是它们的每个字母的出现次数要相同；所以你可以使用两个数组各自统计窗口和p的字符出现次数；但是这样的比较显然不是最高效的；我们可以使用diff数组直接统计每个字母的出现次数之差，当差为0，说明有一种字符满足了，当所有的字符都满足，说明两个数组为异位词了，具体看代码

```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        if (p.size() > s.size()) return {};     // p比s大，不可能是异位词
        
        // 哈希表统计，p和s每个字符的出现次数差
        unordered_map<char, int> hash;
        for (auto c: p) hash[c] ++;
        vector<int> res;

        // cnt代表字符种数，ok代表满足的字符总数
        int cnt = hash.size();
        for (int i = 0, j = 0, ok = 0; i < s.size(); i ++ ) {
            // 右端点滑入，出现次数差减小
            hash[s[i]]--;
            if (hash[s[i]] == 0) ok ++;  // 如果减完是0，说明当前字符满足要求了，ok++

            // 窗口满足长度了
            if (i - j + 1 == p.size()) {
                if (ok == cnt) res.push_back(j);
                if (hash[s[j]] == 0) ok--;   // 如果当前是0，说明左端点滑出后不满足要求了，ok--;
                hash[s[j]]++;
                j++;
            }
        }

        return res;
    }
};
```

#### 
### 子串

#### [560. 和为 K 的子数组](https://leetcode.cn/problems/subarray-sum-equals-k/)

NOT AC，思路：前缀和 + 哈希表模板题，记住应用场景满足条件的子数组数目，记住一定是数目；然后哈希表维护的是i前面的前缀和的出现次数

```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> s(n + 1);
        for (int i = 1; i <= n; i ++) s[i] = s[i - 1] + nums[i - 1];

        unordered_map<int, int> hash;   // 哈希表维护 前缀和的出现次数
        hash[0] = 1;  // 初始i = 0, 前缀和为0，出现一次

        int ans = 0;
        for (int i = 1; i <= n; i ++) {
            int t = s[i] - k;   // 要找的前缀和 s[i] - goal
            ans += hash[t];     // 该前缀和的出现次数，就是当前i满足的个数，加入ans;
            hash[s[i]] ++;      // 移动i后，当前的前缀和加入哈希表维护
        }
        return ans;

    }
};
```

#### [239. 滑动窗口最大值](https://leetcode.cn/problems/sliding-window-maximum/)

NOT AC，思路：难点在于如何判断窗口的最大值，多次判断窗口内的最大值

堆：用堆去维护窗口遍历过的元素，如果最大值出现在窗口左侧，就把该值pop出去，直到最大值出现在窗口内部，我们不需要关心堆中的元素数量和窗口的元素数量相等，我们只需要关心堆中的最大元素是窗口中的最大元素即可；

```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> ans;
        // 堆中的元素需要维护下标，这样才能判断是否在窗口中
        priority_queue<pair<int, int>> heap;
        for (int i = 0; i < n; i ++) {
            heap.emplace(nums[i], i);
            if (i >= k - 1) {  // 第一个窗口的右端
                // 不断地移除堆顶的元素，直到其确实出现在滑动窗口中 
                while (heap.top().second <= i - k) heap.pop();
                ans.push_back(heap.top().first);
            }
        }
        return ans;
    }
};
```

单调队列：todo

#### [76. 最小覆盖子串](https://leetcode.cn/problems/minimum-window-substring/)

AC，思路：首先发现是不定长滑动窗口，然后关键在于覆盖子串怎么判断，当该子串和目标串的每个字符的出现次数相同时说明该串是覆盖子串；其中统计子串和目标串的每个字符出现次数相同，看438题，可以通过hash表记录每个字符的出现次数之差；最后有两个易错点，首先不要再while里直接记录答案，极端情况下会超时；然后就是注意特判窗口没有滑动的情况

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        int k = t.size(), n = s.size();
        if (k > n) return "";

        unordered_map<int, int> hash;
        for (auto c: t) hash[c]++;
        int cnt = hash.size();

        int min_len = n + 1, start = 0;
        for (int i = 0, j = 0, ok = 0; i < n; i ++) {
            // 右端点滑入
            hash[s[i]] --;
            if (hash[s[i]] == 0) ok ++;

            // 最小，求最大的j，while满足
            while (ok == cnt){
                if (i - j + 1 < min_len) {
                    // res = s.substr(j, i - j + 1);  这样写某些极端情况会反复统计超时
                    start = j;
                    min_len = i - j + 1;
                }
                if (hash[s[j]] == 0) ok --;
                hash[s[j]]++;
                j ++;
            }
        }
        return min_len == n + 1 ? "": s.substr(start, min_len);
    }
};
```

#### 
### 普通数组

#### [53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray/)

AC，思路：动态规划子数组相关的模板题，定义f[i]表示以nums[i]结尾的最大子数组和

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n = nums.size();

        vector<int> f(n + 1);
        int res = -0x3f3f3f3f;
        for (int i = 0; i < n; i ++) {
            f[i + 1] = max(f[i] + nums[i], nums[i]);
            res = max(res, f[i + 1]);
        }
        return res;
    }
};
```

#### [56. 合并区间](https://leetcode.cn/problems/merge-intervals/)

NOT AC，思路：合并区间是一个很巧妙的题，关键就在于记住要左端点排序，然后l &gt; mr和l &lt;= mr的情况，这里给出两种不同的板子；

yxc的板子：

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());  // 按照左端点从小到大排序
        
        vector<vector<int>> ans;
        int l = intervals[0][0], r = intervals[0][1];  // 第一个区间
        for (int i = 1; i < intervals.size(); i ++) {
            if (intervals[i][0] > r) {      // 当前区间和上一个区间不相交
                ans.push_back({l, r});      // 将上一个区间加入到答案
                l = intervals[i][0], r = intervals[i][1];  // 更新上一个区间为当前区间
            }
            else {  // 当前区间和上一个区间相交
                r = max(r, intervals[i][1]);   // 上一个区间的l不会变，r有可能变大
            }
        }
        ans.push_back({l, r});   // 加入最后一段区间
        return ans;
    }
};
```

灵神的板子：看灵神题解很容易分析的[56. 合并区间 - 力扣（LeetCode）](https://leetcode.cn/problems/merge-intervals/solutions/2798138/jian-dan-zuo-fa-yi-ji-wei-shi-yao-yao-zh-f2b3/?envType=study-plan-v2&envId=top-100-liked)

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());  // 按照左端点从小到大排序
        vector<vector<int>> ans;
        for (auto p: intervals) {
            int l = p[0], r = p[1];
            if (!ans.size() || l > ans.back()[1]) {  // 当前区间和上一个区间不相交，无法合并
                // 加入当前区间，左端点是确定下来了，右端点有可能更新
                ans.push_back({l, r});   
            }
            // 当前区间和上一个区间相交，可以合并，更新上一个区间的右端点
            else ans.back()[1] = max(ans.back()[1], r);
        }
        return ans;
    }
};
```

#### [189. 轮转数组](https://leetcode.cn/problems/rotate-array/)

AC，思路：比较简单的下标转换问题

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> tmp(n);
        
        // 遍历原数组
        for (int i = 0; i < n; i ++) {
            // 新位置 (i + k) % n, 老位置 i
            tmp[(i + k) % n] = nums[i];
        }
        nums = tmp;
    }
};
```

#### [238. 除自身以外数组的乘积](https://leetcode.cn/problems/product-of-array-except-self/)

AC，思路：前后缀分解模板题，这里主要比较一下不同写法的优势，以后前后缀分解的问题多看看这道题的写法

原始状态空间

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        
        // 最原始的前后缀分解写法，状态空间老老实实 0 ~ n - 1
        vector<int> pre(n), suf(n);
        pre[0] = nums[0]; for (int i = 1; i < n; i ++) pre[i] = pre[i - 1] * nums[i];
        suf[n - 1] = nums[n - 1]; for (int i = n - 2; i >= 0; i --) suf[i] = suf[i + 1] * nums[i];
        
        vector<int> ans(n);
        for (int i = 1; i < n - 1; i ++) {
            ans[i] = pre[i - 1] * suf[i + 1];
        }
        // 因为数组边界问题，会漏掉一些状态，需要自己计算
        ans[0] = suf[1];
        ans[n - 1] = pre[n - 2];

        return ans;
    }
};
```

数组前面插一位（状态空间改变了），状态相关下标改变就行，动态规划中常用这一种！

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        
        // 数组前面插一位，状态相关下标改变，其余都不变
        vector<int> pre(n + 1), suf(n + 2);
        pre[0] = 1; for (int i = 0; i < n; i ++) pre[i + 1] = pre[i] * nums[i];
        suf[n + 1] = 1; for (int i = n - 1; i >= 0; i --) suf[i + 1] = suf[i + 2] * nums[i];
        
        vector<int> ans;
        for (int i = 0; i < n; i ++) {
            ans.push_back(pre[i] * suf[i + 2]);
        }
        return ans;
    }
};
```

数组前面插一位（状态空间改变了），遍历改变后的状态空间，状态相关下标不变，其余的需要变化

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        
        // 数组前面插一位，遍历改变后的状态空间，状态相关下标不变，其余的需要变化
        vector<int> pre(n + 1), suf(n + 2);
        pre[0] = 1; for (int i = 1; i <= n; i ++) pre[i] = pre[i - 1] * nums[i - 1];
        suf[n + 1] = 1; for (int i = n; i >= 1; i --) suf[i] = suf[i + 1] * nums[i - 1];
        
        vector<int> ans;
        for (int i = 1; i <= n; i ++) {
            ans.push_back(pre[i - 1] * suf[i + 1]);
        }
        return ans;
    }
};
```

空间优化：首先前缀数组优化成前缀值，然后由于统计答案的遍历区间和前缀统计的遍历区间一样，直接将前缀值的统计放入答案中

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        
        // 数组前面插一位，遍历改变后的状态空间，状态相关下标不变，其余的需要变化
        vector<int> suf(n + 2);
        suf[n + 1] = 1; for (int i = n; i >= 1; i --) suf[i] = suf[i + 1] * nums[i - 1];
        
        // 空间优化，前缀积的计算放在统计答案的时候
        vector<int> ans; int pre = 1;
        for (int i = 1; i <= n; i ++) {
            ans.push_back(pre * suf[i + 1]);
            pre = pre * nums[i - 1];
        }
        return ans;
    }
};

class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        
        // 数组前面插一位，状态相关下标改变，其余都不变
        vector<int> suf(n + 2);
        suf[n + 1] = 1; for (int i = n - 1; i >= 0; i --) suf[i + 1] = suf[i + 2] * nums[i];
        
        vector<int> ans; int pre = 1;
        for (int i = 0; i < n; i ++) {
            ans.push_back(pre * suf[i + 2]);
            pre = pre * nums[i];
        }
        return ans;
    }
};
```

#### [41. 缺失的第一个正数](https://leetcode.cn/problems/first-missing-positive/)

AC，思路：我自己的屎山代码过了，核心思路就是我们的答案范围只能是 1 ~ n + 1，其中如果在数组里缺失就是1 ~n, 数组里都满足就是n + 1; 这里把简单做法和原地哈希做法都写一下

排序：

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int ans = 1;
        // 先找1，1找到了再用剩下的数去找2，遍历完后当前还未找到的数就是答案
        for (int i = 0; i< nums.size();i++) {
            if (nums[i] == ans) {
                ans++;
            }
        }
        return ans;
    }
};
```

哈希表：在数组里依次寻找可能的res，没有找到就是第一个缺失的正数

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();
        unordered_set<int> hash;
        for (int x: nums) hash.insert(x);

        int res = 1;
        while (hash.count(res)) res ++;
        return res;
    }
};
```

原地哈希：遍历每一个数，然后我们想让每个数都放在它应在的下标处（原地哈希），例如1就应该放在index 0处，2就应该放在index 1处；所以index i上正确存放的元素是i + 1 =&gt; nums[i] = i + 1;如果遍历的时候nums[i] = i + 1说明已经放置正确的元素，如果不是i + 1，那我们就需要把nums[i]放在它应该在的下标处，应在的下标是nums[i] - 1；同时为了不覆盖数组中原有的值，所以我们使用swap；所以是把下标i和下标nums[i] - 1这两处的数值交换；完成后，再次遍历数组，第一个不满足的下标，对应的正确放置元素的值就是答案

[LeetCode 41. 缺失的第一个正数---java版、修改数组模拟哈希set、完整注释 - AcWing](https://www.acwing.com/solution/content/94283/)

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();
        for (int i = 0; i < n; i ++) {
            // 数组中<1的数和>n的数不需要找到哈希index
            // nums[i] = i + 1, 当前的index已经放了应有的元素
            // 如果该元素不是正确元素，nums[i]的哈希index = nums[i - 1], nums[i]放入index nums[i - 1]处
            // 放入前要注意 index处的值是否一样，如果一样就不需要swap，否则会值重复死循环
            while(nums[i] >= 1 && nums[i] <= n && nums[i] != i + 1 && nums[nums[i] - 1] != nums[i]) {
                swap(nums[i], nums[nums[i] - 1]);
            }
        }

        for (int i = 0; i < n; i ++) {
            if (nums[i] != i + 1) return i + 1;
        }
        return n + 1;
    }
};
```

#### 
### 矩阵

#### [73. 矩阵置零](https://leetcode.cn/problems/set-matrix-zeroes/)

AC，思路：开始犯了个错误，我想试图边找到0的位置，然后同时置0操作，这样做会有逻辑的错误，因为置0的位置有可能在后期被当作找到的0来操作，但题目的要求显然是我们只把初始为0的位置进行置0操作；所以如果非要这么写，那么我们就需要在置0操作的时候去区分初始0和后期置0；这样的话代码会复杂很多；

所以干脆直接 先找到初始0的位置，然后直接对初始0的位置进行置0操作；代码也简洁可读性高

以下代码可以空间进一步优化，把state优化成row，col两个数组，同时判断

```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        vector<vector<int>> state(m, vector<int>(n, 0));

        // 找到初始0的地方
        for (int i = 0; i < m; i ++) 
            for (int j = 0; j < n; j ++) 
                if (matrix[i][j] == 0) state[i][j] = 1;

        // 置0
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                if (state[i][j] == 1) {
                    // 行置0
                    for (int k = 0; k < n; k ++) matrix[i][k] = 0;
                    // 列置0
                    for (int k = 0; k < m; k ++) matrix[k][j] = 0;
                }
            }
        }
    }
};
```

#### [54. 螺旋矩阵](https://leetcode.cn/problems/spiral-matrix/)

NOT AC，思路：很经典的题目；属于网格图的范畴，一般要使用方向数组，但是螺旋矩阵这里，我们需要按照螺旋的方向去定义方向数组，然后就是确定遍历多少次，这里有m*n个数，所以遍历m*n次；然后初始化螺旋矩阵的起点和起点方向，之后就是正常网格图解法

[756. 蛇形矩阵 - AcWing题库](https://www.acwing.com/problem/content/description/758/) acm模式练习

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        // 方向数组，按照螺旋矩阵的顺序，右下左上
        int dx[4] = {0, 1, 0, -1}, dy[4] = {1, 0, -1, 0};
        
        // 螺旋矩阵起点 x,y 起点方向d, i是ans的索引，总共有m * n个数
        int x = 0, y = 0, d = 0;
        vector<int> ans(m * n);
        for (int i = 0; i < m * n; i ++) {
            ans[i] = matrix[x][y];
            matrix[x][y] = 101;  // 网格图技巧，可以省略vis数组
            int a = x + dx[d], b = y + dy[d];  // a，b新坐标
            // 出界，或者碰到已经遍历过的数
            if (a < 0 || a > m - 1 || b < 0 || b > n - 1 || matrix[a][b] == 101) {
                d = (d + 1) % 4;  // 改变方向
                a = x + dx[d], b = y + dy[d];
            }
            // 新坐标设为当前坐标
            x = a, y = b;
        }
        return ans;
    }
};
```

#### [48. 旋转图像](https://leetcode.cn/problems/rotate-image/)

NOT AC，矩阵相关的题目，这题是顺时针旋转90度；通过这题我们要快速复习，矩阵变换，主要掌握不同变换，矩阵坐标怎么变，代码怎么写！

方法1：顺时针旋转90度后，找规律发现，原来的(i, j)元素 转移到 倒数第i列的第j个位置，根据这个规律，利用辅助数组达到新矩阵；

技巧：坐标的计算主要看起点和偏移量，之前是0，偏移量i - 0，反转后起点n - 1，偏移量不变 =&gt; n - 1 - i；

如果是1为起点，之前是1，偏移量i - 1，反转后起点n，偏移量i - 1 =&gt; n - (i - 1) = n - i + 1

正数第i个位置，起点0，偏移量i - 1 =&gt; i - 1

倒数第i个位置，起点n - 1，偏移量i - 1 =&gt; n - 1 - (i - 1) = n - i;

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        auto tmp = matrix;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < n; j ++) {
                // 对于矩阵中第 i 行的第 j 个元素，在旋转后，它出现在倒数第 i 列的第 j 个位置
                tmp[j][n - i - 1] = matrix[i][j];
            }
        }
        matrix = tmp;
    }
};
```

方法2：方法1使用了额外的数组，不使用额外数组的话；我们就考虑 [i][j] =&gt; [j][n - i - 1]，怎么要经过多次操作得到；可以结合线性代数的矩阵变换来想；变换方法有很多种，这里提供两种思路；

首先对角线翻转[i][j] = &gt; [j][i]，然后左右翻转[j][i] = &gt; [j][n - 1 - i];

首先上下翻转[i][j] = &gt;[n - 1 - i][j]，然后对角线翻转[n - 1 - 1][j] =&gt; [j][n - i - 1];

首先副对角线翻转[i][j] = [n - j - 1][n - i - 1]，然后上下翻转[n - j - 1][n - i - 1] =&gt; [j][n - i - 1]

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        // 对角线翻转
        for (int i = 0; i < n; i ++) 
            for (int j = 0; j < i; j ++)
                swap(matrix[i][j], matrix[j][i]);
        
        // 左右翻转
        for (int i = 0; i < n; i ++) 
            for (int j = 0; j < n / 2; j ++)
                swap(matrix[i][j], matrix[i][n - j - 1]);
    }
};


class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        // 上下翻转
        for (int i = 0; i < n / 2; i ++) 
            for (int j = 0; j < n; j ++)
                swap(matrix[i][j], matrix[n - i - 1][j]);
        
        // 对角线翻转
        for (int i = 0; i < n; i ++) 
            for (int j = 0; j < i; j ++)
                swap(matrix[i][j], matrix[j][i]);
    }
};

class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        // 副对角线翻转
        for (int i = 0; i < n; i ++) 
            for (int j = 0; i + j < n - 1; j ++)
                swap(matrix[i][j], matrix[n - 1 - j][n - 1 - i]);
        
        // 上下翻转
        for (int i = 0; i < n / 2; i ++) 
            for (int j = 0; j < n; j ++)
                swap(matrix[i][j], matrix[n - i - 1][j]);
        
    }
};
```

#### [240. 搜索二维矩阵 II](https://leetcode.cn/problems/search-a-2d-matrix-ii/)

AC，思路：首先最简单肯定是暴力遍历，时间复杂度O(m * n)；考虑到每列和每行有序，可以对每列或者每行二分；最后介绍小众的z形变换

暴力

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n = matrix[0].size();
        for (int i = 0; i < m; i ++)
            for (int j = 0; j < n; j ++) {
                if (matrix[i][j] == target) return true;
            }
        return false;
    }
};
```

二分

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        for (const auto& row: matrix) {
            auto it = lower_bound(row.begin(), row.end(), target);
            if (it != row.end() && *it == target) {
                return true;
            }
        }
        return false;
    }
};
```

z形变换：todo

#### 
### 链表

#### [160. 相交链表](https://leetcode.cn/problems/intersection-of-two-linked-lists/)

NOT AC，思路：这一题是典型的利用链表指针相遇去找交点。

这里是两个指针指向两个链表的头，同时往后走，走完以后就移动到另一个链表的头继续往后走；这样第一次相遇的地方就是他们的第一个交点。

技巧：链表中涉及到找目标点的问题，大部分都是利用指针相遇找目标点；

具体：构造确定点到目标点的距离关系，如果找到距离关系，我们就将指针放在确定点上，控制每次移动的步数，让他们相遇，此时相遇点就是目标点。

当然我们需要证明指针一定会在目标点相遇：证明很简单，我们得到确定点到目标点的距离，只要找到距离关系，然后根据速度关系，就可以证明相遇了。

证明：目标点是第一个相交点。链表头A到交点的距离是a，交点后面的距离是c，链表头B到交点的距离是b，后面由于是交点距离一样也是c；第一个指针到交点移动a + c + b，第二个指针到交点移动b + c + a，距离一样；两个指针每次都只移动一步，必然会在交点处相遇；

```cpp
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        auto pa = headA, pb = headB;
        while (pa != pb) {
            pa = pa ? pa->next : headB;
            pb = pb ? pb->next : headA;
        }
        return pa;
    }
};
```

当然也有暴力做法，直接把其中一个链表放入哈希表中，然后另一个链表从头开始遍历，第一个在哈希表中找到的节点就是答案

```cpp
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        unordered_set<ListNode*> hash;
        for (auto p = headA; p; p = p->next) {
            hash.insert(p);
        }

        for (auto p = headB; p; p = p->next) {
            if (hash.count(p)) return p;
        }
        return nullptr;
    }
};
```

#### [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

AC，思路：一开始认为头节点变化，就自己加了dummy节点，后来发现加完后，反转会多一个节点；所以不能加dummy；

反转链表的要点：

1. 逐个反转，我们需要两个指针，一个指向前一个指向后，然后把后面节点的next指针指向前一个节点，所以需要两个指针遍历；
2. 拿到尾节点，遍历cur指针，cur到达end，pre会到达尾节点；
3. pre节点的初始化，我们最后希望原来的头节点指向空，所以pre = nullptr

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* pre = nullptr, *cur = head;
        while(cur) {
            auto tmp = cur->next;
            cur->next = pre;
            pre = cur;
            cur = tmp;
        }
        return pre;
    }
};
```

```cpp
// 错误写法，这里会造成dummy指向head，head指向dummy，这样会死循环
// 链表题报错 一般要么就是nullptr调用了next成员，要么就是两个节点相互指死循环
// 从这一题的报错中，我们需要吸取教训
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        auto dummy = new ListNode(5001); dummy->next = head;
        auto pre = dummy, cur = head;
        while(cur) {
            auto tmp = cur->next;
            cur->next = pre;
            pre = cur;
            cur = tmp;
        }
        return pre;
    }
};
```

#### [234. 回文链表](https://leetcode.cn/problems/palindrome-linked-list/)

AC，思路：如果不考虑空间复杂度，直接将链表的元素放入数组中，然后判断回文串即可；

思考如何直接在链表中判断：较为复杂，首先得反转后半部分链表，然后就比较两段是否相等来判断回文

其中反转后半部分链表，需要两个操作：

1. 得到后半部分链表的两个端点，通过快慢指针就可以拿到这两个端点
2. 反转链表

```cpp
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        vector<int> list;
        for (auto p = head; p; p = p->next) list.push_back(p->val);

        int l = 0, r = list.size() - 1;
        while (l < r) {
            if (list[l++] != list[r--]) return false;
        }
        return true;
    }
};
```

#### [141. 环形链表](https://leetcode.cn/problems/linked-list-cycle/)

AC，思路：环形链表可以使用快慢指针来做，如果指针相遇那么就是有环；这里重点谈一下证明；快指针每次两步，慢指针每次一步，所以快指针的相对速度是1步，所以如果有环的话，快指针一定会和慢指针相遇，因为相对速度是1步，所以不可能跳过！！！

```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode* slow = head, *fast = head;
        while (fast && fast->next) {  // fast都不为空，slow肯定也不为空
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) return true;
        } 
        return false;
    }
};
```

#### [142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/)

NOT AC，思路：最暴力做法，遍历链表的时候放入哈希表中，如果遍历的节点在哈希表中出现过，说明这是环的起点，这个思路非常的暴力直观；

数学做法：假设快慢指针在环某处相遇，然后设置起点到环入口的距离为a，入口到相遇的距离为b，相遇到入口的距离为c；首先证明慢指针在环中走的距离绝对不超过一个环长，因为考虑最坏情况，slow指针在入口的时候，fast指针刚好在前面一步，那么此时相对速度1步，所以fast指针需要走环长 - 1次，此时慢指针也走环长-1次，每次一步，没有走完一个环长；

考虑到fast指针走的距离是slow指针的两倍，2(a + b) = a + b + k(b + c) = &gt;a = (k - 1)(b + c) + c；这个等式意味着head到入口的距离 = 相遇点到入口到距离 + 环长的倍数；距离相等，只要两个指针同时从head和相遇点出发，每次走1步，必然会相遇，相遇点就是入口！

总结：

(1) 先找环形链表快慢指针的相遇点，找相遇点，直接就利用环形链表的特征，快慢指针必然会相遇；

(2) 利用相遇点的等式关系，得到信息 相遇点到入口的距离 = 链表头到入口的距离

(3) 找目标点（入口），得到等式关系，将指针放在确定点移动，相遇在目标点；

tips：

找相遇点，不需要证明会在相遇点相遇，就不需要构造距离关系了。

找目标点，利用指针相遇找目标点，需要证明会在目标点相遇，需要构造距离关系。

```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* slow = head, *fast = head;
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
            if (fast == slow) {
                // a = (k - 1)(b + c) + c
                // slow到入口的距离和head到入口的距离相等，所以同时走相遇的点就是入口
                while (slow != head) {
                    slow = slow->next;
                    head = head->next;
                }
                return slow;
            }
        }
        return nullptr;
    }
};
```

#### [21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)

AC，思路：二路归并，只是这里用在链表；我的写法是答案链表使用的是新节点，也就是我自己new出来的；但是其实这里可以直接使用原链表的节点；节省空间！

new:

```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        // 涉及到头节点插入，使用dummy方便头插
        ListNode* dummy = new ListNode(0);
        auto tail = dummy;

        // 二路归并
        while(list1 && list2) {
            if (list1->val < list2->val) {
                tail = tail->next = new ListNode(list1->val);
                list1 = list1->next;
            }          
            else {
                tail = tail->next = new ListNode(list2->val);
                list2 = list2->next;
            }
        }
        while (list1) tail = tail->next = new ListNode(list1->val), list1 = list1->next;
        while (list2) tail = tail->next = new ListNode(list2->val), list2 = list2->next;

        return dummy->next;
    }
};
```

空间优化：

```cpp
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        // 涉及到头节点插入，使用dummy方便头插
        ListNode* dummy = new ListNode(0);
        auto tail = dummy;

        // 二路归并
        while(list1 && list2) {
            if (list1->val < list2->val) {
                tail = tail->next = list1;
                list1 = list1->next;
            }          
            else {
                tail = tail->next = list2;
                list2 = list2->next;
            }
        }
        tail->next = list1 ? list1 : list2;
        return dummy->next;
    }
};
```

#### [2. 两数相加](https://leetcode.cn/problems/add-two-numbers/)

AC，思路：其实就是高精度加法模板题；注意进位的用法；然后就是新链表的依次插入，一般要用到dummy和tail，dummy用来方便插入头节点和最后的返回头节点，tail用来方便尾插新节点；

```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        auto dummy = new ListNode(0);
        auto tail = dummy;

        int t = 0;
        while (l1 || l2 || t) {
            if (l1) t += l1->val, l1 = l1->next;
            if (l2) t += l2->val, l2 = l2->next;
            tail = tail->next = new ListNode(t % 10);
            t = t / 10;
        }
        return dummy->next;
    }
};
```

#### [19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

AC，思路：核心思路很简单，就是要找到倒数第n个节点的前一个节点（目标点）；两种做法，其实就是找目标点的方式不同

方法1：求出链表的总节点数，然后得到目标点的位置，之后指针移动到这个位置

方法2：使用前后指针，让后指针指向尾节点的时候，前指针指向目标点，我们计算一个它们两个之间的偏移量是n；所以先让前指针走n步；然后再让前后指针同时移动，后指针到尾节点的时候停止，这个时候前指针指向目标点；

tips：涉及到头节点的增删，常用哨兵节点方便操作

方法1

```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        // 可能会删除头节点，所以加入哨兵节点
        auto dummy = new ListNode(0); dummy->next = head;

        // 计算链表总节点数
        int cnt = 0;
        auto p = head;
        while (p) p = p->next, cnt ++;

        // 得到删除点的前一个点的位置
        int pos = cnt - n; ListNode* p1 = dummy;
        for (int i = 0; i < pos; i ++) p1 = p1->next;

        p1->next = p1->next->next;
        return dummy->next;
    }
};
```

方法2

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        auto dummy = new ListNode(0); dummy->next = head;

        auto l = dummy, r = dummy;
        while (n --) r = r->next;   // 右指针先向右走 n 步

        while (r->next) {
            r = r->next;
            l = l->next;   // 左右指针一起走
        }

        // 此时左指针 指向 删除点的前一个节点
        l->next = l->next->next;
        return dummy->next;
    }
};
```

#### [24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)

AC，思路：链表的题目，总体来说分析我们需要几个指针，然后就是调整步骤，最后注重以下while遍历的条件；

我们这里每次两两交换节点，需要4个指针，分别指向1，2，3，4这4个点；然后因为涉及到头节点更换，我们可以使用哨兵节点，所以我们定义p,a,b,c4个指针，p指向b，b指向a，a指向c就达到了效果

while遍历的时候，条件怎么确定呢，两种方法

1. 看开始的时候最少要有几个点，这里要交换最少要有2个点（反转链表那个题目最少是0个点），因为有哨兵节点的存在，p一定存在，所以就是判断p-&gt;next和p-&gt;next-&gt;next存在，注意一定要先判断p-&gt;next再判断p-&gt;next-&gt;next，直接判断p-&gt;next-&gt;next会报错的，因为有可能p-&gt;next已经为空指针了；
2. 看需要多少指针，然后只有最后一个指针可以指向空（因为前面的指针指向空，就拿不到后面的指针了），所以前面的指针必须都要存在，这里c可以指向空，前面的p，a，b，c必须存在；p开始的时候指向dummy必然存在，之后又移动到b也是必然存在，所以条件就是a和b要存在 =&gt; p-&gt;next && p-&gt;next-&gt;next;

```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if (!head || !head->next) return head; // 空和1个节点的特判，分析之后，其实可以省略
        auto dummy = new ListNode(0); dummy->next = head;

        auto p = dummy;
        // 至少有两个节点，注意写法一定要先p->next存在后，再判断p->next存在
        while (p->next && p->next->next) {  
            auto a = p->next, b = a->next, c = b->next;
            p->next = b;
            b->next = a;
            a->next = c;

            p = p->next->next;
        }
        return dummy->next;
    }
};
```

#### [25. K 个一组翻转链表](https://leetcode.cn/problems/reverse-nodes-in-k-group/)

NOT AC，k个一组翻转，前置知识是反转链表1和2；反转链表1是反转所有节点，需要两个指针pre和cur；反转链表2是反转一段节点，需要三个指针p0, pre, cur，为什么2需要三个指针呢，因为每次反转完以后，我们还需要把反转后的节点部分拼接到原链表去，需要用到反转之前的开始位置前面的节点，我们使用p0指向；k个一组反转就是多加了一个剩余节点数判断，每次反转k个就行；

```cpp
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        // 统计节点个数
        int n = 0; auto p = head;
        while (p) p = p->next, n ++;

        // 添加哨兵节点，方便反转
        auto dummy = new ListNode(-1); dummy->next = head;

        // 反转一段链表，需要这三个指针！
        ListNode* p0 = dummy, *pre = nullptr, *cur = p0->next;
        while (n >= k) {  // 剩余节点数 >= k，可以继续反转
            // k个节点反转，反转k次；每次就是反转链表2
            for (int i = 0; i < k; i ++) {
                auto tmp = cur->next; 
                cur->next = pre;
                pre = cur;
                cur = tmp;
            }

            auto p1 = p0->next;
            p0->next = pre;
            p1->next = cur;
            p0 = p1;

            // 更新剩余节点数
            n -= k;
        }
        return dummy->next;
    }
};
```

#### [138. 随机链表的复制](https://leetcode.cn/problems/copy-list-with-random-pointer/)

NOT AC，思路：首先思考复制一个只有next指针的链表还是挺容易的；在之前的链表题目里我们已经总结出了一套，构建新链表的写法，哨兵 + 尾插；但是现在我们还需要复制random指针，所以我们此时可以考虑建立一个原节点 -&gt; 新节点的映射，此时新节点的random指向就可以从原节点的random的映射拿到了；

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {
        // 构建新链表的基本操作，哨兵 + 尾插
        auto dummy = new Node(0), tail = dummy;
        
        // 构建原节点 -> 新节点的映射
        unordered_map<Node*, Node*> map;
        auto p = head;
        while (p) {
            map[p] = new Node(p->val);
            p = p->next;
        }

        // 新链表中插入新节点，然后初始化新节点的next和ranodom
        p = head;
        while (p) {
            tail = tail->next = map[p];      // 新链表中插入新节点（这种插入方式已经将前一个节点的next初始化了）
            // tail->next = map[p->next];    // 初始化新节点的next （可以省略，因为下次循环的时候，该节点next会初始化）
                                             // 最后一个节点的next如果不写上一句就没有在循环中初始化，默认为null
            tail->random = map[p->random];   // 初始化新节点的random
            p = p->next;
        }

        return dummy->next;
    }   
};
```

上述做法空间复杂度O(n)，可以继续优化成O(1)

Todo:

#### [148. 排序链表](https://leetcode.cn/problems/sort-list/)

AC，思路：时间复杂度最优的做法自然是直接转化为数组排序

```cpp
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        vector<pair<int, ListNode*>> nums;
        auto p = head;
        while (p) {
            nums.push_back({p->val, p});
            p = p->next;
        }
        sort(nums.begin(), nums.end());

        auto dummy = new ListNode(0), tail = dummy;
        for (int i = 0; i < nums.size(); i ++) {
            cout << nums[i].first << " ";
            tail = tail->next = nums[i].second;
        }
        tail->next = nullptr;   
        // 注意：新链表的节点不是new出来的，tail指向的最后一个节点使用的是原来的节点，原来的节点的next不为空，会导致有环
        return dummy->next;
    }
};
```

#### [23. 合并 K 个升序链表](https://leetcode.cn/problems/merge-k-sorted-lists/)

NOT AC，思路：这题有很多种解法，最应该掌握的就是小根堆和最小堆解法，其中最小堆是小根堆的优化

小根堆：把所有节点放入小根堆中维护，每次弹出最小节点；时间复杂度O(n*log(n))，空间复杂度O(n);

```cpp
class Solution {
public:
    ListNode *mergeKLists(vector<ListNode *> &lists) {
        // 维护一个小根堆，元素是listnode类指针
        auto cmp = [](const ListNode *a, const ListNode *b) {
            return a->val > b->val; // 最小堆
        };
        priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> pq;
        for (auto head: lists) {
            // 把当前链表的所有节点放入小根堆中
            auto p = head;
            while (p) {
                pq.push(p);
                p = p->next;
            }
        }

        // 构建答案链表
        auto dummy = new ListNode(0), tail = dummy;
        while (!pq.empty()) { // 循环直到堆为空
            // 每次拿到最小节点
            auto node = pq.top();
            pq.pop();
            // 添加到新链表
            tail = tail->next = node;
        }
        // 这里不能省略，因为如果最大节点val和前面节点的val相等，不能保证最后pop出的节点是链表中末尾节点
        tail->next = nullptr;    
        return dummy->next;
    }
};
```

最小堆：之前的小根堆解法中，我们直接把所有节点放进去，然后每次取堆顶（最小节点）；我们尝试去将小根堆优化成最小堆，最小堆中维护可能是最小节点的集合；因为给出的k个链表是有序的，所以初始情况下最小节点只可能是每个链表的头节点，之后拿到这个最小节点后，新的最小节点只可能是弹出最小节点的链表的下一个节点或者其他链表的头节点，所以我们每次弹出一个节点后，就将这个节点所在链表的下一个节点放入最小堆中；这样最小堆中最多只有k个元素，时间复杂度优化成O(n*log(k))，空间复杂度优化成O(k);

```cpp
class Solution {
public:
    ListNode *mergeKLists(vector<ListNode *> &lists) {
        // 维护一个最小堆，元素是listnode类指针
        auto cmp = [](const ListNode *a, const ListNode *b) {
            return a->val > b->val; // 最小堆
        };
        priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> pq;
        for (auto head: lists) {
            if (head) {
                pq.push(head);
            }
        }

        // 构建答案链表
        auto dummy = new ListNode(0), tail = dummy;
        while (!pq.empty()) { // 循环直到堆为空
            // 拿到最小节点
            auto node = pq.top();
            pq.pop();
            if (node->next) { // 下一个节点不为空
                pq.push(node->next); // 下一个节点有可能是最小节点，入最小堆
            }
            // 添加到新链表
            tail = tail->next = node;
        }
        // 这里可以省略，因为即使出现相同的最大节点，最小堆中可以保证最后的最大节点最后加入
        // 最大的节点肯定是其中一个链表的末尾节点， 它的next已经指向空
        // tail->next = nullptr;    
        return dummy->next;
    }
};
```

#### [146. LRU 缓存](https://leetcode.cn/problems/lru-cache/)

NOT AC，思路：我自己的思路首先实现增查改，我们可以使用哈希表，然后删的时候，发现需要维护一个队列，每次使用队列中的元素时，需要把这个元素移动到开头或者末尾；如果使用数组来维护这个队列肯定超过O(1)，使用链表维护这个队列，把元素移动到开头或者结尾，就是删除这个元素，然后新的位置添加元素，链表的增删是O(1)的所以可以达到这个要求；但是删除节点需要先找到这个节点，所以我们利用哈希表存储 key和节点（C++中存储节点这种类对象，一般使用节点类指针），我自己卡在这了；

但是现在我们删除需要的是该节点前面的节点，这个时候单向链表无法拿到前面的节点，所以这里可以使用双向链表，这样就可以拿到前面的节点了；总结：使用哈希表 + 双向链表

这里给出两种实现：

1. 直接使用std::unordered_map和std::list作为哈希表和双向链表

上述说的节点类指针，其实就是std::list中的元素指针，stl容器中的元素指针我们一般使用迭代器代替，这样的话就可以使用容器内部的一些函数方便操作；所以哈希表存储的是&lt;key, list容器的迭代器&gt;，然后list存储的是key value对，使用pair就行；具体实现看代码

```cpp
// 分析后需要使用 哈希表 + 双向链表（模拟队列）
// 使用stl容器 std::unordered_map, std::list

class LRUCache {
public:
    LRUCache(int capacity) {
        size_ = capacity;
    }
    
    int get(int key) {
        auto it = hash.find(key);
        if (it == hash.end()) return -1;
        else {
            cache.splice(cache.begin(), cache, hash[key]);  // 把当前元素放入链表头部
            return hash[key]->second;
        }
    }
    
    void put(int key, int value) {
        if (get(key) != -1) {  //key存在,调用get时已将缓存移到头部，再更新hash
            hash[key]->second = value; 
        }
        else {
            if (cache.size() == size_) {   // 超过容量了，删除链表尾部元素，删除map中的对应元素
                auto delKey = cache.back().first;
                cache.pop_back();
                hash.erase(delKey);
            }
            // 没有超过容量，链表中头插新元素，map中添加新元素
            cache.push_front({key, value});
            hash[key] = cache.begin();
        }
    }

private:
    list<pair<int, int>> cache;
    unordered_map<int, list<pair<int, int>>::iterator> hash;
    int size_;
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```

#### 
### 二叉树

#### [94. 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)

AC，思路：二叉树中序遍历，递归写法就是左中右

```cpp
class Solution {
public:
    vector<int> ans;
    vector<int> inorderTraversal(TreeNode* root) {
        dfs(root);
        return ans;
    }

    void dfs(TreeNode* p) {
        if (p == nullptr) return;
        dfs(p->left);
        ans.push_back(p->val);
        dfs(p->right);
    }
};
```

#### [104. 二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)

AC，思路：二叉树具有天然的子结构性质，因为树和子树就是很明显的原问题和子问题，所以可以尝试递归来做，递归就是思考原问题和子问题的关系；递归一般都是归的时候传递信息；

```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) return 0;
        return max(maxDepth(root->left), maxDepth(root->right)) + 1;
    }
};
```

#### [226. 翻转二叉树](https://leetcode.cn/problems/invert-binary-tree/)

NOT AC，思路：反转左右子树，然后交换左右儿子

```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (root == nullptr) return nullptr;
        auto left = invertTree(root->left);    // 翻转左子树
        auto right = invertTree(root->right);  // 翻转右子树
        // 交换左右儿子
        root->left = right;
        root->right = left;
        return root;
    }
};
```

#### [101. 对称二叉树](https://leetcode.cn/problems/symmetric-tree/)

AC，思路：首先转化题意，一个树是对称 =&gt; 左子树和右子树对称；然后尝试递归 左子树和右子树对称 = 左子树和右子树的root值相等，然后左子树的右子树 = 右子树的左子树，左子树的左子树 = 右子树的右子树；

```cpp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        return helper(root->left, root->right);
    }

    bool helper(TreeNode* ltree, TreeNode* rtree) {
        if (!ltree && !rtree) return true;
        if (ltree && rtree && ltree->val == rtree->val)
            return helper(ltree->left, rtree->right) && helper(ltree->right, rtree->left);
        else return false;
    }
};
```

#### [543. 二叉树的直径](https://leetcode.cn/problems/diameter-of-binary-tree/)

NOT AC，思路：我的初始思路是计算左子树的最大高度，右子树的最大高度，相加就是答案；但是后来经过灵神提示，发现有可能直径压根就不经过根节点；所以我们需要考虑树上的每个节点为拐弯点时的直径；

```cpp
class Solution {
public:
    int ans = 0;
    int diameterOfBinaryTree(TreeNode* root) {
        maxHeight(root);   // 计算根节点最大高度的时候，会遍历整个二叉树，顺便统计每个节点为拐弯点的直径
        return ans;
    }

    int maxHeight(TreeNode* p) {
        if (p == nullptr) return 0;
        auto l = maxHeight(p->left), r = maxHeight(p->right);
        ans = max(ans, l + r);  // 计算以当前节点拐弯的直径，因为直径可能不经过根节点
        return max(l, r) + 1;   // 直径 = 拐弯点左边路径 + 右边路径 = 左儿子的最大高度 + 右儿子的最大高度
    }
};
```

更标准的写法，使用链长

```cpp
class Solution {
public:
    int ans = 0;
    int diameterOfBinaryTree(TreeNode* root) {
        if (root == nullptr) return 0;
        helper(root);   // 递归遍历二叉树的时候，同时统计每个节点的最大链长
        return ans;
    }
    
    // 递归函数意义 当前节点的最大链长
    int helper(TreeNode* node) {
        if (node == nullptr) return -1;  // 为了让叶节点的链长是0，那么空节点的链长是-1;

        int l = helper(node->left);   // 左儿子的最大链长
        int r = helper(node->right);  // 右儿子的最大链长
        // 统计每个点为拐弯点的最大直径l + r + 2，更新答案
        ans = max(ans, l + r + 2);
        return max(l + 1, r + 1);   
    }
};
```

多说一下这个题目，二叉树的题目我们为什么不把边界写成叶节点呢，因为叶节点的判断条件是(!node-&gt;left && !node-&gt;right)，对于这道题目，到了叶节点直接返回1，看上去没什么问题；但是仔细一看你就会发现，叶节点判断的条件是node-&gt;left和node-&gt;right都为空；可是有可能会存在左右儿子只是其中一个为空的情况下，那么这样的话就会继续往下走，造成空指针解引用的错误；所以如果要使用叶节点作为边界的话，我们就得在之后的代码中仍然判断左右儿子是否为空，代码就会略微繁琐，当然还是可以写出来的

```cpp
class Solution {
public:
    int ans = 0;
    int diameterOfBinaryTree(TreeNode* root) {
        if (root == nullptr) return 0;
        helper(root);   // 递归遍历二叉树的时候，同时统计每个节点的最大链长
        return ans;
    }
    
    // 递归函数意义 当前节点的最大链长
    int helper(TreeNode* node) {
        if (node->left == node->right) return 0;  // 边界 叶节点直接返回，但是会漏掉左右儿子其中一个为空的情况

        int l = -1, r = -1;
        if (node->left) l = helper(node->left);   // 左儿子的最大链长
        if (node->right) r = helper(node->right);  // 右儿子的最大链长
        // 统计每个点为拐弯点的最大直径l + r + 2，更新答案
        ans = max(ans, l + r + 2);
        return max(l + 1, r + 1);   
    }
};
```

#### [102. 二叉树的层序遍历](https://leetcode.cn/problems/binary-tree-level-order-traversal/)

AC，思路：二叉树的层序遍历，其实就是BFS，BFS的话源节点入队，然后就是pop出队头，push队头的儿子们；这里需要记录每层的节点，所以在BFS里，记录每层的大小和集合即可，当前层pop 层的长度 次数后，当前层就全部pop出去了，下一层也都刚好push进队列；

写法上，我们可以允许每层push进空节点，也可以规定只能push进非空节点，写法上略微有一点点区别；

```cpp
// 层中只能有非空节点的写法！

class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        if (root == nullptr) return {};   // 此时保证源点是非空节点
        
        vector<vector<int>> ans;
        // BFS 然后记录每层的节点
        queue<TreeNode*> q;
        q.push(root);
        while (q.size()) {
            // 当前层的大小和节点集合，有了大小就可以记录每层的节点集合了
            int len = q.size();
            vector<int> level;
            while (len --) {
                auto node = q.front(); q.pop();
                level.push_back(node->val);  // 由于队列中都是非空节点，直接拿到val
                // 左右儿子非空才push进去，保证队列中都是非空节点
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);  
            }
            ans.push_back(level);  // 没有计算空节点层
        }
        return ans;
    }
};
```

```cpp
// 层中允许有空节点的写法！

class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        
        // BFS 然后记录每层的节点
        queue<TreeNode*> q;
        q.push(root);
        while (q.size()) {
            // 当前层的大小和节点集合，有了大小就可以记录每层的节点集合了
            int len = q.size();
            vector<int> level;
            while (len --) {
                auto node = q.front(); q.pop();
                if (node) level.push_back(node->val);
                if (node) q.push(node->left), q.push(node->right);
            }
            // 存在层中都是空节点的情况，也就是叶节点下一层;为了排除这一层，当前层的level非空才记录
            if (level.size()) ans.push_back(level);  
        }
        return ans;
    }
};
```

#### [108. 将有序数组转换为二叉搜索树](https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/)

NOT AC，思路：二叉搜索树的中序遍历就是一个升序数组，所以这题我们可以转化为 根据中序遍历构建二叉搜索树；递归构建，new出根节点，然后[l, mid - 1]构建左子树，[mid + 1, r]构建右子树；其实这道题最难的地方是为什么这么做，之后详细研究

```cpp
class Solution {
public:
    vector<int> nums;
    TreeNode* sortedArrayToBST(vector<int>& nums_) {
        nums = nums_;
        return build(0, nums.size() - 1);
    }

    TreeNode* build(int l, int r) {
        if (l > r) return nullptr;
        int mid = l + (r - l) / 2;  // 防止溢出
        // new出根节点
        TreeNode* root = new TreeNode(nums[mid]);
        // 递归构建左右子树
        root->left = build(l, mid - 1);
        root->right = build(mid + 1, r);
        return root;
    }
};
```

#### [98. 验证二叉搜索树](https://leetcode.cn/problems/validate-binary-search-tree/)

NOT AC，思路：首先说一下错误的写法，我的思路是 当前树是二叉搜索树 = 左子树是二叉搜索树 + 右子树是二叉搜索树 + 左子树的根节点val &lt; root val + 右子树的根节点val &gt; root -&gt;val；这样的思路通过了大部分用例，但很明显这个递归公式是不对的！举个反例：4为根的子树是二叉搜索树，6为根的子树是二叉搜索树，然后也满足4 &lt; 5, 6 &gt; 5，但是很明显3是小于5的，不满足二叉搜索树性质！

<img src="/assets/GKYXbv4mfoXdhvx9xw7cppaKnAg.png" src-width="671" src-height="234"/>

所以上述做法是错误的！

提供三种解法：

方法1：统计每个子树的节点是否在合法区间内，必须要先得到root-&gt;val；所以递归前序遍历的时候，统计每个子树是否在合法区间内，区间通过参数向下传递，递归函数的意义，当前子树是否在区间（lower，upper)内；

```cpp
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return helper(root, LONG_MIN, LONG_MAX);
    }

    // 当前子树的所有节点是否都在（lower，upper)内
    // lower和upper是根据root->val得到的，所以必须先递归root，前序遍历
    // 自顶向下（递）的时候统计了一些信息
    bool helper(TreeNode* root, long lower, long upper) {
        if (root == nullptr) return true;
        long x = root->val;
        return lower < x && x < upper && 
        helper(root->left, lower, root->val) && helper(root->right, root->val, upper);
    }
};
```

方法2：二叉搜索树的中序遍历是升序的，所以我们可以递归中序遍历的时候，记录上一个节点的值，同时统计当前子树是否为二叉搜索树；递归函数的意义，当前子树是否为二叉搜索树；

```cpp
class Solution {
public:
    long pre = LONG_MIN;
    bool isValidBST(TreeNode* root) {
        return helper(root);
    }

    // 中序遍历的时候记录一下上一个节点值，记录以下当前子树是否为二叉搜索树放入返回值
    // 递归函数含义：当前子树是否为二叉搜索树
    bool helper(TreeNode* root) {
        if (root == nullptr) return true;

        if (!helper(root->left)) return false;
        if (root->val <= pre) return false;
        pre = root->val;
        return helper(root->right);
    }
};
```

#### [230. 二叉搜索树中第 K 小的元素](https://leetcode.cn/problems/kth-smallest-element-in-a-bst/)

AC，思路：中序遍历二叉搜索树，得到有序数组，第k小的元素，就是第k个被遍历的元素

```cpp
class Solution {
public:
    vector<int> nums;
    int kthSmallest(TreeNode* root, int k) {
        inorder(root);
        // for (int i = 0; i < nums.size(); i ++) cout << nums[i] << " ";
        if (k >= 1) return nums[k - 1];
        else return -1;
    }

    void inorder(TreeNode* root) {
        if (root == nullptr) return;
        inorder(root->left);
        nums.push_back(root->val);
        inorder(root->right);
    }
};
```

#### [199. 二叉树的右视图](https://leetcode.cn/problems/binary-tree-right-side-view/)

AC，思路：方法有很多；我的思路是层序遍历，然后把最右边的节点值放入答案数组中

```cpp
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        if (root == nullptr) return {};
        vector<int> res;

        queue<TreeNode*> q;
        q.push(root);
        while (q.size()) {
            int len = q.size();
            while (len --) {
                auto node = q.front(); q.pop();
                if (len == 0) res.push_back(node->val);  // 当前层最后一个节点 就是 最右边的节点
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }
        }
        return res;
    }
};
```

#### [114. 二叉树展开为链表](https://leetcode.cn/problems/flatten-binary-tree-to-linked-list/)

NOT AC，思路：只要当前结点存在左子树，就将左子树的右链插入到当前结点的右面，如果不存在左子树了（本来就没有，或者已经被插入到当前结点右边了），就遍历到右儿子

```cpp
class Solution {
public:
    void flatten(TreeNode* root) {
        while (root) {
            auto p = root->left;
            if (p) {  // 如果存在左子树
                while (p->right) p = p->right;  // 拿到左子树右链的尾节点
                // 将左子树的右链插入到根节点的右边
                p->right = root->right;
                root->right = root->left;
                root->left = NULL;
            }
            root = root->right;  // 此时不存在左子树了，向右继续遍历
        }
    }
};
```

#### [105. 从前序与中序遍历序列构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

NOT AC，思路：这是一道非常经典的题目；我们使用递归来做，递归函数的功能是 从前序遍历和中序遍历的区间内构造二叉树，所以前序中序构造二叉树 = 拿到根节点 +前序中序构造左子树 + 前序中序构造右子树；递归的公式写出来了，得到了原问题和子问题的关系，可以递归来做；那么为了方便知道左右子树在前序遍历的区间范围，我们计算出左子树的长度，为了方便知道左右子树在中序遍历的区间范围，我们只需要知道根节点在中序遍历的位置就行；其中为了快速查找根节点在中序遍历中的位置，我们可以使用哈希表处理中序遍历，val-&gt;index，这样每次找根节点是O(1)的

https://www.acwing.com/activity/content/code/content/554673/

https://leetcode.cn/problems/construct-binary-tree-from-preorder-and-inorder-traversal/solutions/2646359/tu-jie-cong-on2-dao-onpythonjavacgojsrus-aob8/?envType=study-plan-v2&envId=top-100-liked

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    unordered_map<int, int> hash;
    vector<int> preorder, inorder;
    TreeNode* buildTree(vector<int>& preorder_, vector<int>& inorder_) {
        preorder = preorder_;
        inorder = inorder_;

        // 中序遍历记录值和下标的映射，这样可以快速找到preorder[pl]在inorder中的位置
        for (int i = 0; i < inorder.size(); i ++) hash[inorder[i]] = i;
        return build(0, preorder.size() - 1, 0, inorder.size() - 1);
    }

    TreeNode* build(int pl, int pr, int il, int ir) {  // 左闭右闭区间
        if (pl > pr) return nullptr;
        auto root = new TreeNode(preorder[pl]);
        int k = hash[root->val];   // 方便确立子树在中序遍历的区间
        int left_size = k - il;    // 方便确立子树在前序的遍历区间
        root->left = build(pl + 1, pl + left_size, il, k - 1);
        root->right = build(pl + left_size + 1, pr, k + 1, ir);
        return root;
    }
};
```

#### [112. 路径总和](https://leetcode.cn/problems/path-sum/)

AC，思路：这道题不难，但是从这道题我们来深度剖析递归角度和dfs角度；

递归和dfs的代码是非常相似的，都是递归写法；但是思维角度还是有一些不同的，这里我划分为递归角度和dfs角度；

递归角度：思考原问题，子问题，构建原问题和子问题的递归公式；其中二叉树有天然的子结构性质，原问题，子问题分别对应当前树和子树；

dfs角度：思考dfs，dfs的意义为已搜部分，已搜部分的信息一般放在dfs的参数里；这种dfs一般适合返回值为void或者bool的情况，因为此时返回值没有作用或者只是用来找到符合条件的方案后快速返回

dfs角度转递归角度：思考dfs，发现存在返回值且不为bool的时候，可以思考未搜索部分转化为递归；有的时候直接思考原问题和子问题会比较困难，所以我们可以先思考dfs，dfs是正向的搜索，一般来说更直观一些，搜索空间从0 -&gt; 一条路径全部搜完，然后搜完就回溯，直到整个空间搜索完毕；dfs的未搜索部分其实就是递归（因为dfs已搜部分逐渐扩大，未搜部分就逐渐减小，正好对应递归的问题），dfs的返回值对应的是未搜索部分！

树上路径和，递归两种写法，其实本质是一样的

递归1

```cpp
// 树上前缀和思考 f[u] = f[u->parent] + u->val;
// 递归角度1（常用）思考原问题和子问题 (原问题到子问题规模需要减小)，然后构建递归公式
// 递归角度2 根据dfs未搜部分来做（因为dfs搜索部分逐渐扩大，未搜索部分就逐渐减小，正好对应递归的问题）

class Solution {
public:
    // 递归函数的意义是 存在当前节点往下的路径和 = 目标和
    bool hasPathSum(TreeNode* root, int targetSum) {
        if (root == nullptr) return false;  // 为了root->val有意义加的边界条件
        targetSum -= root->val;  // 拿到儿子往下路径的目标和
        // 真正的边界条件，叶节点层，如果儿子往下为0，说明当前节点本身的路径和 = 目标和，返回true
        if (root->left == root->right) return 0 == targetSum;  
        return hasPathSum(root->left, targetSum) || hasPathSum(root->right, targetSum);
    }
};
```

递归2

```cpp
class Solution {
public:
    // 递归函数的意义是 存在当前节点往下路径和 = 目标和
    bool hasPathSum(TreeNode* root, int targetSum) {
        if (root == nullptr) return false;  // 为了root->val有意义加的边界条件
         // 真正的边界条件 叶节点层，如果当前节点本身的路径和 = 目标和，返回true
        if (root->left == root->right) return root->val == targetSum;
        return hasPathSum(root->left, targetSum - root->val) || hasPathSum(root->right, targetSum - root->val);
    }
};
```

dfs：dfs的意义不同，dfs的初始状态不同，代码略有差异，这里给出多种写法，其中树的问题dfs的意义必须是已搜根到当前节点；否则无法判断已搜路径是否是根节点到叶节点（举个例子，如果dfs的意义是已搜根到当前节点的父节点；边界就是 空，已搜完一条路径；但是该路径并不一定是到根到叶节点的路径，[1, 2]这个例子是典型，1的右儿子是空，所以我们找到了1这条路径，但是该路径不是根到叶节点的路径；初始状态的话，看个人喜好，我一般喜欢是初始为空，然后dfs里先得到当前的已搜部分；

dfs1

```cpp
class Solution {
public:
    int targetSum;
    bool hasPathSum(TreeNode* root, int targetSum_) {
        targetSum = targetSum_;
        return dfs(root, 0);  // 初始状态 根节点 已搜[]
    }

    // dfs表示已搜 根到当前节点，sum是已搜路径和，返回值是找到符合条件的路径了
    bool dfs(TreeNode* root, int sum) {
        if (root == nullptr) return false;      // 为了满足root->val的边界条件
        sum += root->val;                       // 得到根节点到当前节点的和

        if (root->left == root->right) {        // 真正的边界 叶节点层
            if (sum == targetSum) return true;  // 判断是否符合条件
        }

        // 一直往下搜索，只要是true就直接层层返回true
        if (dfs(root->left, sum)) return true;
        if (dfs(root->right, sum)) return true;

        // 否则返回false
        return false;    
    }
};
```

dfs2

```cpp
class Solution {
public:
    int targetSum;
    bool hasPathSum(TreeNode* root, int targetSum_) {
        targetSum = targetSum_;
        if (root == nullptr) return false;  // 为了满足root->val，需要特判
        return dfs(root, root->val);  // 初始状态 根节点 已搜[root]
    }

    // dfs表示已搜 根到当前节点，sum是已搜路径和，返回值是找到符合条件的路径了
    bool dfs(TreeNode* root, int sum) {
        // if (root == nullptr) return false;      // 因为一开始是非空，最后一层是叶节点，所以永远非空，可以省略该边界

        if (root->left == root->right) {        // 真正的边界 叶节点层
            if (sum == targetSum) return true;  // 判断是否符合条件
        }

        // 一直往下搜索，只要是true就直接层层返回true
        if (root->left && dfs(root->left, sum + root->left->val)) return true;
        if (root->right && dfs(root->right, sum + root->right->val)) return true;

        // 否则返回false
        return false;    
    }
};
```

dfs3 错误写法，dfs的含义不能是 根到当前节点的父节点；因为边界时，当前点是空节点，不能推出当前点的上一个节点是叶节点 例如[1, 2]；所以已搜路径不一定是根到叶节点的路径

```cpp
class Solution {
public:
    int targetSum;
    bool hasPathSum(TreeNode* root, int targetSum_) {
        targetSum = targetSum_;
        if (root == nullptr) return false;
        return dfs(root, 0);  // 初始状态 根节点 已搜[]
    }

    // dfs表示已搜根到当前节点的父节点，sum是已搜路径和，返回值是找到符合条件的路径了
    bool dfs(TreeNode* root, int sum) {
        // 这样的写法是错误的，因为当前节点是空，不意味着当前节点的父节点是叶节点，所以不能用来判断答案；
        // [1, 2] 1这个案例很明显，1的右儿子是空，但是1不是叶节点，不能用来判断答案
        if (root == nullptr) {  // 边界   空，已搜到叶节点
            return sum == targetSum;     
        }

        // 一直往下搜索，只要是true就直接层层返回true
        if (dfs(root->left, sum + root->val)) return true;
        if (dfs(root->right, sum + root->val)) return true;

        // 否则返回false
        return false;    
    }
};
```

#### [113. 路径总和 II](https://leetcode.cn/problems/path-sum-ii/)

NOT AC，思路：上面题目的变种，因为这里是求所有方案，所以只能暴搜dfs；

本题对dfs和递归的理解更加深刻了；对于C++而言，如果dfs参数是值传递，那么每层都有自己的参数，回溯的时候拿到当前层的状态，不需要恢复现场；而如果dfs参数是引用/指针传递，那么这个参数每层是共用的，回溯的时候拿到当前层的状态需要恢复现场；然后如果只搜索一条路径的话，我们回溯的时候不需要拿到当前层的状态，可以不恢复现场

当前层的改变和恢复现场一定是成对操作的，所以如果当前层有些if操作的时候，我们也需要保证改变和恢复现场是成对出现的，否则会出现错误；

树形路径问题，dfs意义都是 已搜根节点到当前节点

初始状态 root 已搜[]

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path{};
    int targetSum;
    vector<vector<int>> pathSum(TreeNode* root, int targetSum_) {
        targetSum = targetSum_;
        dfs(root, 0, path);   // 初始状态 root 已搜[]
        return ans;
    }

    // dfs意义 已搜根节点到当前节点，sum已搜路径的和，path已搜路径
    void dfs(TreeNode* root, int sum, vector<int>& path) {
        if (root == nullptr) return;   // 满足root->val的边界条件
        // 转化为当前层的dfs
        sum += root->val;
        path.push_back(root->val);

        if (root->left == root->right) { // 真正的边界 叶节点层
            if (sum == targetSum) ans.push_back(path);
            // sum -= root->val; 可以省略因为sum参数是值传递，每层有自己的sum
            path.pop_back(); // 回溯时恢复现场 如果不加这句直接return，会少一次pop
            return;
        }

        dfs(root->left, sum, path);
        dfs(root->right, sum, path);
        // sum -= root->val;  // 可以省略因为sum参数是值传递，每层有自己的sum
        path.pop_back();
    }
};
```

初始状态 root，已搜[root]

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path{};
    int targetSum;
    vector<vector<int>> pathSum(TreeNode* root, int targetSum_) {
        targetSum = targetSum_;
        if (root == nullptr) return {};

        // 初始状态 root 已搜[root]
        path.push_back(root->val);
        dfs(root, root->val, path);   
        return ans;
    }

    // dfs意义 已搜根节点到当前节点，sum已搜路径的和，path已搜路径
    void dfs(TreeNode* root, int sum, vector<int>& path) {
        if (root->left == root->right) { // 边界 叶节点层
            if (sum == targetSum) ans.push_back(path);
            return;
        }

        if (root->left) {
            path.push_back(root->left->val);
            dfs(root->left, sum + root->left->val, path);
            path.pop_back();
        }
        if (root->right) {
            path.push_back(root->right->val);
            dfs(root->right, sum + root->right->val, path);
            path.pop_back();
        }
    }
};
```

#### [437. 路径总和 III](https://leetcode.cn/problems/path-sum-iii/)

AC，路径总和系列题目的最终版，这里是要求树上所有路径和 = target的数目

暴力思路：遍历所有节点，然后统计每个节点为根的子树的路径和 = target的数目

dfs角度：

```cpp
class Solution {
public:
    int cnt = 0, targetSum = 0;
    int pathSum(TreeNode* root, int targetSum_) {
        targetSum = targetSum_;
        dfs1(root);
        return cnt;
    }

    // 遍历所有节点
    void dfs1(TreeNode* root) {
        if (root == nullptr) return;
        dfs2(root, 0);
        dfs1(root->left);
        dfs1(root->right);
    }
    
    // dfs意义 已搜根节点到当前点 sum是已搜路径的和
    void dfs2(TreeNode* root, long long sum) {
        if (root == nullptr) return;
        sum += root->val;   // 拿到当前层的dfs状态

        if (sum == targetSum) cnt ++;           // 判断答案
        // if (root->left == root->right) return;  // 边界 叶节点层

        dfs2(root->left, sum);
        dfs2(root->right, sum);
    }
};
```

递归角度 写法1

```cpp
class Solution {
public:
    int ans = 0, targetSum = 0;
    int pathSum(TreeNode* root, int targetSum_) {
        targetSum = targetSum_;
        dfs1(root);
        return ans;
    }

    // 遍历所有节点
    void dfs1(TreeNode* root) {
        if (root == nullptr) return;
        ans += dfs2(root, targetSum);
        dfs1(root->left);
        dfs1(root->right);
    }
    
    // dfs意义 当前点往下搜的路径和 = 目标和的数目，target是目标和
    int dfs2(TreeNode* root, long long target) {
        int cnt = 0;
        if (root == nullptr) return 0;

        if (root->val == target) cnt ++;   // 当前点本身 = 目标和的数目
        cnt += dfs2(root->left, target - root->val);   // 左儿子往下搜的路径和 = 目标和 - root->val的数目
        cnt += dfs2(root->right, target - root->val);  // 右儿子往下搜的路径和 = 目标 - root->val的数目
        return cnt;
    }
};
```

dfs角度转化为递归角度 写法2

```cpp
class Solution {
public:
    int ans = 0;
    int targetSum = 0;

    int pathSum(TreeNode* root, int targetSum_) {
        targetSum = targetSum_;
        dfs1(root);
        return ans;
    }

    // 遍历所有节点
    void dfs1(TreeNode* root) {
        if (root == nullptr) return;
        ans += dfs2(root, targetSum);
        dfs1(root->left);
        dfs1(root->right);
    }

    // 以当前节点为起点的所有路径中，和等于 target 的路径数
    int dfs2(TreeNode* root, long long target) {
        if (root == nullptr) return 0;
        
        int cnt = 0;
        target -= root->val; // 更新为儿子的目标值

        if (target == 0) cnt++; // 如果儿子往下和 = 0，说明当前点 = target，+1；

        cnt += dfs2(root->left, target);   // 当前点的左儿子往下满足target的数目
        cnt += dfs2(root->right, target);  // 当前点的右儿子往下满足target的数目

        return cnt;
    }
};
```

树上前缀和 + 哈希表，先理解序列前缀和 + 哈希表，然后迁移到树中即可；其中树上前缀和就是根到当前点的路径和；路径和 = target的数目 =&gt; 前缀和 = sum - target的次数

```cpp
class Solution {
public:
    unordered_map<long, int> hash;
    int target, ans;
    int pathSum(TreeNode* root, int targetSum) {
        target = targetSum;
        hash[0] = 1;
        dfs(root, 0);
        return ans;
    }

    // dfs意义 已搜根节点到当前节点，sum已搜路径和（前缀和）
    void dfs(TreeNode* node, long sum) {
        if (node == nullptr) return;
        sum += node->val;

        ans += hash[sum - target];              // 判断/加入 答案
        
        // if (node->left == node->right) return;  // 边界 叶节点层
        hash[sum]++;
        dfs(node->left, sum);
        dfs(node->right, sum);
        hash[sum]--;
    }
};
```

#### [236. 二叉树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/)

NOT AC，思路：二叉树的lca问题很经典，需要掌握两种方法；

递归：直接思考原问题和子问题，构建递归公式；原问题是 在当前树中找p，q的lca，子问题是在左子树中找lca，在右子树找lca，构建递归公式；

当前树中找p，q的lca = 根节点自己是否是lca，在左子树中找lca，在右子树中找lca后分类讨论

分类讨论：注意如果能返回非空结果，说明树中最起码有p或q（也就是有p，有q，有p,q三种）

如果root为空，或者root = p或q，说明当前节点就是lca；边界

否则开始在子树中继续找lca：
1. 左子树中找lca有非空结果，右子树找lca有非空结果，说明左子树和右子树都有p或q，所以p，q在左右子树两侧，lca是root
2. 左子树找lca有非空结果，右子树找lca没有非空结果，说明只有左子树有p或q，所以当前树的lca是左子树找lca的结果
3. 右子树找lca有非空结果，左子树找lca没有非空结果，说明只有右子树有p或q，所以当前树的lca是右子树找lca的结果
4. 左右子树找lca都是空，说明当前树不存在p，q节点，直接返回空；

```cpp
class Solution {
public:
    // 递归函数意义：在树中，找p,q的最近公共祖先
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == nullptr || root == p || root == q) return root;  // 边界 lca在根节点上

        // 否则在子树中继续找lca
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
        if (left && right) return root;   // 左右子树中都找到p，q; 说明p,q在左右子树两侧
        if (left) return left;            // 只有左子树中找到p，q; 说明p,q都在左子树
        if (right) return right;          // 只有右子树中找到p,q; 说明p,q都在右子树
        else return nullptr;              // 左右子树都没找到p，q，树不存在p，q，返回空
    }
};
```

记录fa指针，然后两个节点向上走，第一次相交的地方就是lca

```cpp
class Solution {
public:
    unordered_map<int, TreeNode*> fa;  // 记录节点的父节点
    unordered_map<int, bool> vis;      // 记录该节点是否被访问过
    
    // 遍历二叉树
    void dfs(TreeNode* root) {
        if (root->left != nullptr) {
            fa[root->left->val] = root;
            dfs(root->left);
        }
        if (root->right != nullptr) {
            fa[root->right->val] = root;
            dfs(root->right);
        }
    }

    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        // 遍历二叉树，初始化每个节点的parent
        fa[root->val] = nullptr;
        dfs(root);

        // p向上走
        while(p){
            // 将该节点标记为已访问过
            vis[p->val] = true;
            p = fa[p->val];
        }

        // q向上走
        while(q != nullptr){
            // 第一次相交的点就是lca
            if(vis[q->val] == true) return q;
            q = fa[q->val];
        }

        // 不相交说明没有lca
        return nullptr;
    }
};
```

#### [124. 二叉树中的最大路径和](https://leetcode.cn/problems/binary-tree-maximum-path-sum/)

NOT AC，思路：最大路径和 其实跟最大直径那道题差不多，只是从最大直径变为了最大直径和；

递归来做：递归函数的意义 当前点的最大链和

当前点的最大链和 = 左子树的最大链和 + 右子树的最大链和 + root-&gt;val;

两种写法，一种是最大链和可以为负数，还有一种是最大链和为负数直接截断

```cpp
class Solution {
public:
    int ans = -0x3f3f3f3f;   // 统计最大值，存在负数，初始化为极小值
    int maxPathSum(TreeNode* root) {
        helper(root);
        return ans;
    }

    // 递归函数意义 当前节点的最大链和
    int helper(TreeNode* root) {
        if (!root) return 0;

        int l = helper(root->left);         // 左儿子的最大链和
        int r = helper(root->right);        // 右儿子的最大链和
        // 统计当前点为拐点的最大直径和，更新ans
        
        // 写法1，常规写法最大链和可以为负数
        ans = max(ans, max(l, 0) + max(r,0) + root->val);  // 最大链和为负数的直接丢掉，可能只剩当前节点
        return max(max(l, r), 0) + root->val;              // 当前点的最大链和，可能只剩当前点
        // return max(l, r) + root->val;                      // 这样写是错误的，因为当前有可能只剩当前点
    }
};
```

```cpp
class Solution {
public:
    int ans = -0x3f3f3f3f;   // 统计最大值，存在负数，初始化为极小值
    int maxPathSum(TreeNode* root) {
        helper(root);
        return ans;
    }

    // 递归函数意义 当前节点的最大链和
    int helper(TreeNode* root) {
        if (!root) return 0;

        int l = helper(root->left);         // 左儿子的最大链和
        int r = helper(root->right);        // 右儿子的最大链和
        // 统计当前点为拐点的最大直径和，更新ans
        
        // 写法2，最大链和是负数的直接截断，只保留当前点
        ans = max(ans, l + r + root->val);      // 此时l和r一定是非负
        return max(max(l, r) + root->val, 0);   // 当前点的最大链和是负数，直接全部丢弃
    }
};
```

Ps: 543之所以不考虑负数截断，是因为直径长度本来就是非负数；

#### 
### 图论

#### [200. 岛屿数量](https://leetcode.cn/problems/number-of-islands/)

AC，思路：网格图模板题，复习一下网格图中的DFS找连通块即可，然后要明白网格图省略vis数组的本质；

```cpp
class Solution {
public:
    // 网格图常规"全局变量"
    vector<vector<char>> g;
    int m, n;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    int numIslands(vector<vector<char>>& grid) {
        g = grid;
        m = g.size(), n = g[0].size();
        
        // 遍历所有格子，找全为1的连通块数
        int cnt = 0;
        for (int i = 0; i < m; i ++) { 
            for (int j = 0; j < n; j ++) {
                if (g[i][j] == '1') {
                    dfs(i, j);
                    cnt ++;
                }
            }
        }
        return cnt;    
    }

    // dfs含义 已搜到当前节点
    void dfs(int x, int y) {
        // 网格图技巧，直接设置网格图的值来判断是否访问过，可以省略vis数组
        // 我们只需要让已经访问过的节点不影响判断即可，也就是让已经访问过的g[x][y] != '1'即可
        g[x][y] = '2';   // 处理当前节点
        
        for (int i = 0; i < 4; i ++) {
            int a = x + dx[i], b = y + dy[i];
            if (a >= 0 && a < m && b >= 0 && b < n && g[a][b] == '1') {
                dfs(a, b);
            }
        }
    }
};
```

#### [994. 腐烂的橘子](https://leetcode.cn/problems/rotting-oranges/)

AC，思路：网格图的多源BFS模板题，这里就是要转化题意变为 求所有新鲜橘子到最近腐烂橘子的最短距离，然后在其中找最大值；所以很明显多源BFS；BFS模板就是需要队列，距离数组，还有pair&lt;int, int&gt;在队列中存坐标；然后网格图中搜索最关键的就是要确定什么情况下才能继续往下搜索；一般继续搜索的条件是 不越界 + 没有访问过 + 题目要求；

```cpp
class Solution {
public:
    vector<vector<int>> g;
    int m, n;
    int dx[4] = {-1, 1, 0, 0}, dy[4] = {0, 0, -1, 1};
    typedef pair<int, int> pii; 
    int orangesRotting(vector<vector<int>>& grid) {
        g = grid;
        m = grid.size(), n = grid[0].size();

        // 求每个新鲜橘子的格子到最近腐烂橘子的最短距离 多源BFS
        
        // bfs常规写法 队列，距离数组，pair<int, int>
        queue<pii> q; 
        vector<vector<int>> dist(m, vector<int>(n , - 1));  // 初始距离为-1

        int fresh = 0;  // 可能无解，所以统计新鲜橘子的个数

        // 多源BFS初始状态，将所有腐烂橘子入队，dist = 0;
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {        
                if (g[i][j] == 2) {
                    q.emplace(i, j);
                    dist[i][j] = 0;
                }
                else if (g[i][j] == 1) fresh ++;  // 统计新鲜橘子的个数
            }
        }

        // bfs统计每个格子到源点的距离
        int ans = 0;
        while (q.size()) {
            auto[x, y] = q.front(); q.pop();
            for (int i = 0; i < 4; i ++) {
                int a = x + dx[i], b = y + dy[i];
                // 这里继续搜索的条件是必须为新鲜橘子，否则不会继续往下搜了！
                if (a >= 0 && a < m && b >= 0 && b < n && dist[a][b] == -1 && g[a][b] == 1) {
                    q.emplace(a, b);
                    dist[a][b] = dist[x][y] + 1;
                    ans = max(ans, dist[a][b]);
                    // g[a][b] = 2;  // 这一句加不加无所谓，因为我们不统计最后腐烂的橘子数
                    fresh --;
                }
            }
        }

        return fresh > 0 ? -1 : ans;
    }
};
```

#### [207. 课程表](https://leetcode.cn/problems/course-schedule/)

AC，思路：拓扑排序模板题，利用拓扑排序判断图中是否有环

```cpp
class Solution {
public:
    vector<vector<int>> g;   // 邻接表
    int n, m;                // 点数，边数
    vector<int> d;           // 入度数组
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        n = numCourses, m = prerequisites.size();
        g.resize(n); d.resize(n);
        
        // 读 边数组建图 存入邻接表
        for (auto& e: prerequisites) {
            int x = e[0], y = e[1];
            g[x].push_back(y);
            ++d[y];  // 拓扑排序需要统计每个点的入度
        }

        // 拓扑排序
        queue<int> q;
        // 入度为0的点加入队列s
        for (int i = 0; i < n; i ++) {
            if (!d[i]) q.push(i);
        }

        int cnt = 0;   // 统计队列s中弹出的点数，如果为n代表没有环
        while (q.size()) {
            auto x = q.front(); q.pop();  // 队列s中选择一个点弹出
            cnt ++;
            for (auto y: g[x]) {
                // 删除相连的边，邻接点度数 - 1，如果度数为0，加入队列l
                if (--d[y] == 0) q.push(y);  
            }
        }

        return cnt == n;
    }
};
```

#### [208. 实现 Trie (前缀树)](https://leetcode.cn/problems/implement-trie-prefix-tree/)

AC，思路：Trie树模板题，这里就是使用struct和指针来存Trie树，这种方式也要熟练掌握；

```cpp
class Trie {
public:
    // 定义trie树的节点 结构体
    struct Node {
        Node* son[26];    // 子节点数组
        int cnt;          // 以当前节点结尾的字符串个数
        // 默认构造函数 初始化成员
        Node() 
        {
            for (int i = 0; i < 26; i ++) son[i] = nullptr;
            cnt = 0;
        }
    };

    // 成员变量
    Node* root;

    Trie() {
        root = new Node(); // 创建一个根节点
    }
    
    void insert(string word) {
        Node* now = root;    // now指向根节点
        for (int i = 0; i < word.size(); i ++) {
            int x = word[i] - 'a';
            if (!now->son[x]) {
                now->son[x] = new Node();
            }
            now = now->son[x];
        }
        now->cnt ++;        // 以字符串尾部节点 结尾的字符串个数 ++
    }
    
    bool search(string word) {
        Node* now = root;
        for (int i = 0; i < word.size(); i ++) {
            int x = word[i] - 'a';
            if (!now->son[x]) {
                return false;
            }
            now = now->son[x];
        }
        return now->cnt > 0;  // now->cnt 字符串出现次数
    }
    
    bool startsWith(string prefix) {
        Node* now = root;
        for (int i = 0; i < prefix.size(); i ++) {
            int x = prefix[i] - 'a';
            if (!now->son[x]) {
                return false;
            }
            now = now->son[x];
        }
        // 只要能把该字符串搜完，说明树中绝对存在该字符串路径（前缀），但不能保证路径结尾是叶节点（可能不存在该字符串）
        return true;   
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```

#### 
### 回溯

#### [46. 全排列](https://leetcode.cn/problems/permutations/)

AC，思路：排列型回溯模板题，这里说一个技巧，什么变量写在全局里，dfs函数会用到都写在全局里，一般有输入，答案，结果；

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<bool> vis;
    vector<int> path;
    vector<int> nums;
    int n;
    // 按答案每位搜索，决策是选哪个
    vector<vector<int>> permute(vector<int>& nums_) {
        nums = nums_, n = nums.size();
        vis.resize(n, false);
        dfs(0, -1);
        return ans;
    }

    // dfs意义 当前答案位置i，已搜答案0 - i - 1
    void dfs(int i, int choose) {  // 关注信息 当前答案位置，选择了哪个数
        if (i == n) ans.push_back(path);  // 判断答案

        if (i == n) return;  // 边界

        // 选哪个
        for (int j = 0; j < n; j ++) {
            if (!vis[j]) {
                vis[j] = true;
                path.push_back(nums[j]);
                dfs(i + 1, j);
                vis[j] = false;
                path.pop_back();
            }
        }
    }
};
```

#### [78. 子集](https://leetcode.cn/problems/subsets/)

AC，思路：子集型回溯模板题

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;
    vector<int> nums;
    int n;
    vector<vector<int>> subsets(vector<int>& nums_) {
        // 按输入每位搜索，决策是选or不选
        nums = nums_, n = nums.size();
        dfs(0);
        return ans;
    }

    // dfs意义 当前输入位置i，已搜0 - i - 1
    void dfs(int i) { // dfs关注信息，当前输入位置i，结果全局维护
        if (i == n) ans.push_back(path);  // 判断答案
        
        if (i == n) return;   // 边界

        // 选
        path.push_back(nums[i]);
        dfs(i + 1);
        path.pop_back();

        // 不选
        dfs(i + 1);
    }
};
```

#### [17. 电话号码的字母组合](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)

AC，思路：按输入每位搜索，决策是选哪个；中间涉及到根据输入位置拿到对应的字符串 进行选哪个的决策；可以重复选！特判空输入；

```cpp
class Solution {
public:
    string digits;
    int n;
    vector<string> ans;
    string path;
    unordered_map<int, string> map{  // 输入位置对应的字符串映射表
        {2, "abc"},
        {3, "def"},
        {4, "ghi"},
        {5, "jkl"},
        {6, "mno"},
        {7, "pqrs"},
        {8, "tuv"},
        {9, "wxyz"}
    };

    vector<string> letterCombinations(string digits_) {
        // 按输入每位搜索，决策是选哪个
        digits = digits_; n = digits.size();
        if(n > 0) dfs(0);  // 特判空输入
        return ans;
    }

    // dfs意义 当前输入位置i，已搜0 - i - 1
    void dfs(int i) {
        if (i == n) ans.push_back(path);  // 判断答案
        if (i == n) return;   // 边界

        string str = map[digits[i] - '0'];  // 拿到输入位置对应的字符串
        // 选哪个  可以重复选
        for (int j = 0; j < str.size(); j ++) {
            char c = str[j];
            path.push_back(c);
            dfs(i + 1);
            path.pop_back();
        }
    }
};
```

#### [39. 组合总和](https://leetcode.cn/problems/combination-sum/)

AC，思路：组合型回溯模板题，注意边界和剪枝

```cpp
class Solution {
public:
    vector<int> candidates;
    int target;
    int n;
    vector<vector<int>> ans;
    vector<int> path;
    int total;
    vector<vector<int>> combinationSum(vector<int>& candidates_, int target_) {
        // 按输入每位搜索，决策 选or不选
        candidates = candidates_, target = target_, n = candidates.size();
        total = accumulate(candidates.begin(), candidates.end(), 0);
        dfs(0, 0);
        return ans;
    }

    // dfs意义 当前输入位置i，已搜0 - i- 1
    void dfs(int i, int sum) {
        if (sum > target) return;   // 剪枝
        if (i == n && sum == target) ans.push_back(path); // 答案
        if (i == n || sum > target) return;  // 边界

        // 选
        path.push_back(candidates[i]);
        dfs(i, sum + candidates[i]);
        path.pop_back();

        // 不选
        dfs(i + 1, sum);
    }
};
```

#### [22. 括号生成](https://leetcode.cn/problems/generate-parentheses/)

AC，思路：考察括号序列，括号序列的性质，左括号数 = 右括号数；任意前缀左括号数 &gt;= 右括号数；暴搜来做，DFS关注左右括号数，然后利用性质剪枝；

```cpp
class Solution {
public:
    int n;
    string path;
    vector<string> ans;
    vector<string> generateParenthesis(int n_) {
        // 按答案每一位搜，决策是左括号还是右括号
        n = n_;
        dfs(0, 0, 0);
        return ans;
    }

    void dfs(int i, int ln, int rn) {  // 关注当前答案位置，左右括号数
        if (rn > ln) return;  // 剪枝 右括号数 > 左括号数
        if (i == 2 * n && ln == rn) ans.push_back(path); // 判断答案
        if (i == 2 * n) return;  // 边界

        // 选左括号
        path.push_back('(');
        dfs(i + 1, ln + 1, rn);
        path.pop_back();

        // 选右括号
        path.push_back(')');
        dfs(i + 1, ln, rn + 1);
        path.pop_back();
    }
};
```

#### [79. 单词搜索](https://leetcode.cn/problems/word-search/)

AC，思路：由于不能确定起点，所以对网格图中的每个点都做一次DFS，然后决策就是上下左右走；

```cpp
class Solution {
public:
    vector<vector<char>> board;
    string word;
    int m, n;
    int dx[4] = {1, -1, 0, 0}, dy[4] = {0, 0, -1, 1};
    vector<vector<bool>> vis;
    
    bool exist(vector<vector<char>>& board_, string word_) {
        board = board_, word = word_;
        m = board.size(), n = board[0].size();
        vis = vector<vector<bool>> (m, vector<bool>(n, false));

        // 每个点都可以作为起点，所以对每个点dfs一次
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                if (dfs(i, j, 0)) return true; // 只要存在，直接返回true
            }
        }
        return false;  // 否则不存在，返回false;
    }

    // dfs意义 当前位置x，y，已搜起点到x，y
    bool dfs(int x, int y, int k) {  // 关注当前位置，已经匹配到word的哪个位置了
        if (board[x][y] != word[k]) return false;  // 剪枝 当前格子字符 ！= word的字符
        
        if (k == word.size() - 1) return true;         // 边界 + 答案

        // 往哪个方向走
        vis[x][y] = true;
        for (int i = 0; i < 4; i ++) {
            int a = x + dx[i], b = y + dy[i];
            if (a >= 0 && a < m && b >= 0 && b < n && !vis[a][b]) {
                if (dfs(a, b, k + 1)) return true;
            }
        }
        vis[x][y] = false;

        return false;
    }
};
```

#### [131. 分割回文串](https://leetcode.cn/problems/palindrome-partitioning/)

AC，思路：按输入每位搜索，决策是该位后是否加逗号；dfs函数状态信息有 输入位置i，分割起点start

```cpp
class Solution {
public:
    string s;
    int n;
    vector<vector<string>> ans;
    vector<string> path;
    vector<vector<string>> partition(string s_) {
        // 按输入每位搜索，选择是 后面是否放，
        s = s_; n = s.size();
        dfs(0, 0);
        return ans;
    }

    // dfs意义 当前输入位置i，已搜0 - i- 1；
    void dfs(int i, int start) {  // dfs关注 输入位置i，分割起点
        if (i == n && start == n) ans.push_back(path); // 答案
        if (i == n) return;  // 边界

        // 选，
        if (check(start, i)) {
            path.push_back(s.substr(start, i - start + 1));
            dfs(i + 1, i + 1);
            path.pop_back();
        }

        // 不选，
        dfs(i + 1, start);
    }

    bool check(int l, int r) {
        while (l < r) {
            if (s[l ++] != s[r --]) return false;
        }
        return true;
    }
};
```

#### [51. N 皇后](https://leetcode.cn/problems/n-queens/)

NOT AC，n皇后的题目，思路不难，但是如何表示其中一条对角线这个思路忘了，最后发现性质，正对角线中，每条对角线上r - c的值一样，反对角线中，每天对角线上r + c的值一样；所以我们可以使用r -c和r + c来代替不同的对角线，其中值有可能有负数，直接用哈希表映射 &lt;对角线值，对角线是否放置皇后&gt;；然后一般来说dfs中的结果我们一般用path，但是这里结果是一张图，所以直接用g更直观一些；

```cpp
class Solution {
public:
    int n;
    vector<string> g;   // 结果是一张图，所以直接用g代替
    vector<vector<string>> ans;
    // 对角线数组，正对角线 行-列一样，反对角线行+列一样，所以我们使用r + c和r-c来代表其中一条对角线
    unordered_map<int, bool> diag1, diag2;  // 因为对角线值的范围有可能有负数，直接用哈希表来存
    vector<bool> col;  // 列数组
    vector<vector<string>> solveNQueens(int n_) {
        // 按每行搜索，决策是放哪列
        n = n_;
        g = vector<string>(n, string(n, '.'));  // 初始化图
        col.resize(n, false);
        dfs(0);
        return ans;
    }

    // dfs意义 当前第i行，已搜 0 - i- 1行
    void dfs(int i) {
        if (i == n) ans.push_back(g);
        if (i == n) return;  // 边界

        // 选哪列
        for (int j = 0; j < n; j ++) {
            if (!col[j] && !diag1[i + j] && !diag2[i - j]) {
                g[i][j] = 'Q';
                col[j] = diag1[i + j] = diag2[i - j] = true;
                dfs(i + 1);
                col[j] = diag1[i + j] = diag2[i - j] = false;
                g[i][j] = '.';
            }
        }
    }
};
```

#### 
### 二分查找

#### [35. 搜索插入位置](https://leetcode.cn/problems/search-insert-position/)

AC，二分查找模板题，找 &gt;= target的第一个数（右边界） 比 找&lt;= target的最后一个数（左边界） 好；

因为前者的写法，无解，有解 != target，有解=target，三种情况都是返回一样的结果；而后者返回不一样的结果，要多写很多条件判断

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int n = nums.size();
        // < target | >= target   找>=target的第一个数，右边界
        int l = 0, r = n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] >= target) r = mid - 1;
            else l = mid + 1;
        }

        if (r == n - 1) return n;  // 右边界无解，全都 < target，最后一位后面插入
        return r + 1;              // 右边界有解时，= target，答案r + 1; != target，当前位置插入，还是r + 1
    }
};


class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int n = nums.size();
        // <= target | > target   找<=target的最后一个数，左边界
        int l = 0, r = n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] > target) r = mid - 1;
            else l = mid + 1;
        }

        if (l == 0) return 0;  // 左边界无解，全都 > target，第一位插入
        else if (nums[l - 1] == target) return l - 1;  // 左边界有解时，= target，答案l - 1; 
        else return l;              // 左边界有解，!= target，当前位置后面插入，l
    }
};
```

#### [74. 搜索二维矩阵](https://leetcode.cn/problems/search-a-2d-matrix/)

AC，思路：直接把矩阵转化为序列来做；

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n = matrix[0].size();
        vector<int> nums(m * n);
        for (int i = 0, k = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                nums[k ++] = matrix[i][j];
            }
        }

        int l = 0, r = m * n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] >= target) r = mid - 1;
            else l = mid + 1;
        }

        if (r == m * n - 1 || nums[r + 1] != target) return false;
        else return true;
    }
};
```

优化：

首先空间优化，其实我们不需要将矩阵转化为序列，可以直接将序列坐标转化为矩阵坐标 a[i]=matrix[i/n][imodn]，其中n是每行的元素数量，也就是列数n；然后时间优化，二分过程中，我们可以提前判断是否找到target

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size(), n = matrix[0].size();
        
        int l = 0, r = m * n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (matrix[mid / n][mid % n] == target) return true;  // 优化提前判断
            if (matrix[mid / n][mid % n] >= target) r = mid - 1;
            else l = mid + 1;
        }
        return false;
    }
};
```

#### [34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)

AC，整数二分模板题，可以练习一下不同的二分写法；然后查找完后的判断一般来说都是分三种情况，无解，有解 != target，有解 = target；其中前两者一般大多数题目归为一种情况返回-1；

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int n = nums.size();
        // <x | >=x 右边界 and  <=x | >x 左边界

        // 左闭右闭 实际范围 [l, r]
        vector<int> ans;
        int l = 0, r = n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] >= target) r = mid - 1;
            else l = mid + 1;
        }

        if (r == n - 1 || nums[r + 1] != target) return {-1, -1};  // 无解 或者 有解 != target 
        else ans.push_back(r + 1); // 有解 并且 = target

        // 左开右开 实际范围[l + 1, r - 1]
        l = -1, r = n;
        while (l + 1 < r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] <= target) l = mid;
            else r = mid;
        }

        if (l == -1 || nums[l] != target) return {-1, -1};  // 无解 或者 有解 != target
        else ans.push_back(l);  // 有解

        return ans;
    }
};
```

#### [33. 搜索旋转排序数组](https://leetcode.cn/problems/search-in-rotated-sorted-array/)

AC，思路：首先我们观察旋转数组，发现前后分成两段；所以我们首先先找到前后两段区间；所以先二分找到前面一段的终点或者后面一段的起点，这里找前面一段的终点； &gt;= nums[0] | &lt; nums[0]；二分找终点，由于元素中一定有nums[0]，所以肯定有解！

之后就判断 target是在前面一段还是后面一段，然后对于target在不同段的情景，做第二次二分，就可以得到答案了；

注意特判空和只有一段的情况；题目已经限制输入不为空，所以不需要特判空；然后只有一段的情况 end = n - 1，可以并入target在前面一段的情况；

上述这种写法虽然繁琐，但是非常的严谨，可以很轻松的将左闭右闭二分改为其他形式的二分；

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        // 画图分析 序列被分为 左右两段  我们需要找到前后两段的区间！
        // >= nums[0] | < nums[0]  找前面一段的终点，就是找>=nums[0]的左边界
        int n = nums.size();
        
        int l = 0, r = n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] >= nums[0]) l = mid + 1;
            else r = mid - 1;
        }
        // 因为前面一段必然有nums[0]，所以一定有解，找到终点l - 1;
        int end = l - 1;

        if (target >= nums[0] || end == n - 1) {  // target在前面一段
            l = 0, r = end;
            // < target | >= target 找>= target的右边界
            while (l <= r) {
                int mid = l + (r - l) / 2;
                if (nums[mid] >= target) r = mid - 1;
                else l = mid + 1;
            }
            // 三种情况 无解 有解!= target, 有解 = target
            if (r == end || nums[r + 1] != target) return -1;
            else return r + 1;
        }
        else {  // target在后面一段
            l = end + 1; r = n - 1;  
            // 极端情况end = n - 1, target肯定在前面一段，不会进入这个分支
            // < target | >= target 找>= target的右边界
            while (l <= r) {
                int mid = l + (r - l) / 2;
                if (nums[mid] >= target) r = mid - 1;
                else l = mid + 1;
            }
            // 三种情况 无解 有解!= target, 有解 = target
            if (r == n - 1 || nums[r + 1] != target) return -1;
            else return r + 1;
        }
    }
};
```

左开右开

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        // 画图分析 序列被分为 左右两段  我们需要找到前后两段的区间！
        // >= nums[0] | < nums[0]  找前面一段的终点，就是找>=nums[0]的左边界
        int n = nums.size();
        
        // 全都使用 左开右开 二分
        
        int l = -1, r = n;
        while (l + 1 < r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] >= nums[0]) l = mid;
            else r = mid;
        }
        // 因为前面一段必然有nums[0]，所以一定有解，找到终点l;
        int end = l;

        if (target >= nums[0] || end == n - 1) {  // target在前面一段
            l = -1, r = end + 1;
            // < target | >= target 找>= target的右边界
            while (l + 1 < r) {
                int mid = l + (r - l) / 2;
                if (nums[mid] >= target) r = mid;
                else l = mid;
            }
            // 三种情况 无解 有解!= target, 有解 = target
            if (r == end + 1 || nums[r] != target) return -1;
            else return r;
        }
        else {  // target在后面一段
            l = end; r = n;  
            // 极端情况end = n - 1, target肯定在前面一段，不会进入这个分支
            // < target | >= target 找>= target的右边界
            while (l + 1 < r) {
                int mid = l + (r - l) / 2;
                if (nums[mid] >= target) r = mid;
                else l = mid;
            }
            // 三种情况 无解 有解!= target, 有解 = target
            if (r == n || nums[r] != target) return -1;
            else return r;
        }
    }
};
```

#### [153. 寻找旋转排序数组中的最小值](https://leetcode.cn/problems/find-minimum-in-rotated-sorted-array/)

AC，和上一题差不多，也是找出前后两段，这里找前面一段的终点（最好确保一定有解，可以减少很多边界判断）；

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        // >= nums[0] | < nums[0] 找前面一段的终点
        // 答案要么是前面一段的起点，要么是第二段的起点
        int n = nums.size();
        int l = 0, r = n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] >= nums[0]) l = mid + 1;
            else r = mid - 1;
        }
        int end = l - 1;  // 因为nums[0]存在，所以一定有解，终点是l - 1

        if (end == n - 1) return nums[0];  // 特判只有一段的情况
        return nums[end + 1];              // 两段的话，最小值在后段，此时end + 1绝对不会越界
    }
};
```

找后段的起点，也是可以的，甚至最后的特判不需要，因为一段的时候也是return nums[start];

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        // > nums[n - 1] | <= nums[n - 1] 找后面一段的起点
        // 答案要么是前面一段的起点，要么是第二段的起点
        int n = nums.size();
        int l = 0, r = n - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] <= nums[n - 1]) r = mid - 1;
            else l = mid + 1;
        }
        int start = r + 1;  // 因为nums[n - 1]存在，所以一定有解，起点是r + 1

        if (start == 0) return nums[0];    // 特判只有一段的情况
        return nums[start];                // 两段的话，最小值在后段
    }
};
```

#### 
### 栈

#### [20. 有效的括号](https://leetcode.cn/problems/valid-parentheses/)

AC，序列多次匹配字符串的模板题；首先转化题意，这个序列是有效括号序列说明，我们可以多次匹配括号，然后将序列匹配完毕；一般序列多次匹配字符串，我们使用栈

写法1：通用的写法，直接将字符依次进入（字符串维护）栈，然后栈中出现匹配字符就弹出；

```cpp
// 多次匹配字符串，最通用的写法；
// 用字符串维护一个栈，字符依次入栈，如果栈里出现匹配字符串就弹出
// 最后检查栈是否为空判断 该序列能否匹配完毕
class Solution {
public:
    bool isValid(string s) {
        int n = s.size();
        string stk;

        for (int i = 0; i < n; i ++) {
            auto c = s[i];
            stk.push_back(c);
            if (stk.size() >= 2 && check(stk)) stk.erase(stk.end() - 2, stk.end());
        }
        return stk.size() == 0;
    }

    bool check(const string& stk) {
        string str = stk.substr(stk.size() - 2, 2);
        if ( str == "()" || str == "[]" || str == "{}") return true;
        return false;
    }
};
```

写法2：适用于匹配字符串长度为2个的情况，相当于把写法1变种一下，我们把匹配字符最后一位之前的都入栈，遇到最后一位匹配字符的时候，我们就判断和栈顶部的元素是否构成匹配字符串，如果构成就弹出；当匹配字符串长度为2的时候，我们就可以确保栈每次只弹出栈顶，这样就可以使用stl自带的栈了！

```cpp
// 多次匹配字符串，适用于匹配字符长度为两个的写法！
// 匹配字符最后一位之前的字符直接入栈，遇到最后一位匹配字符的时候
// 判断当前字符和栈里面的字符是否构成匹配字符串，如果构成，那就将栈里的匹配字符出栈
// 这种做法的好处就是，当匹配字符长度为2的时候，我们可以确保栈每次只弹出栈顶，可以直接用stl的栈
class Solution {
public:
    bool isValid(string s) {
        int n = s.size();
        stack<char> stk;

        for (int i = 0; i < n; i ++) {
            auto c = s[i];
            if (c != ')' && c != ']' && c != '}') stk.push(c);
            if (stk.size() >= 1 && (c == ')' && stk.top() == '(' || \
                                    c == ']' && stk.top() == '[' || \
                                    c == '}' && stk.top() == '{')) stk.pop();
        }
        return stk.size() == 0;
    }
};
```

#### [155. 最小栈](https://leetcode.cn/problems/min-stack/)

NOT AC，思路：一开始的解法是直接记录最小值，但是后来发现如果pop出最小值的话，没办法得到新的最小值了，所以我又记录了次最小值，但是次最小值的实现，逻辑是有错误的；

所以比较好的解法是同步栈，也就是我们在使用一个栈的时候，同时维护一个同步的最小栈，让他们同步操作；push的时候，同时也push了元素在栈里时对应的最小值，pop的时候，同时也pop了元素在栈里时对应的最小值；这样的话，主元素栈 最小栈里是同步的；

```cpp
class MinStack {
public:
    MinStack() {
        min_stk.push(INT_MAX);
    }
    
    void push(int val) {
        stk.push(val);
        min_stk.push(min(min_stk.top(), val));
    }
    
    void pop() {
        stk.pop();
        min_stk.pop();
    }
    
    int top() {
        return stk.top();
    }
    
    int getMin() {
        return min_stk.top();
    }

    stack<int> stk;
    stack<int> min_stk;
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```

#### [739. 每日温度](https://leetcode.cn/problems/daily-temperatures/)

AC，思路：单调栈模板题，这里是求下一个更大的温度，所以是使用单调递减栈，可以练习一下从左到右和从右到左两种写法

从左到右

```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int> &temperatures) {
        int n = temperatures.size();
        vector<int> ans(n);
        stack<int> stk;
        for (int i = 0; i < n; i++) {
            while (!stk.empty() && temperatures[i] > temperatures[stk.top()]) {
                int j = stk.top();
                stk.pop();
                ans[j] = i - j;
            }
            stk.push(i);
        }
        return ans;
    }
};
```

从右到左

```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int> &temperatures) {
        int n = temperatures.size();
        vector<int> ans(n);
        stack<int> stk;
        for (int i = n - 1; i >= 0; i --) {
            while (!stk.empty() && temperatures[i] >= temperatures[stk.top()]) {
                stk.pop();
            }
            if (stk.empty()) ans[i] = 0;
            else {
                int j = stk.top();
                ans[i] = j - i;
            }
            stk.push(i);
        }
        return ans;
    }
};
```

#### [84. 柱状图中最大的矩形](https://leetcode.cn/problems/largest-rectangle-in-histogram/)

NOT AC，单调栈的运用题目；首先想一下暴力做法，我们去枚举矩形的上边界（上边界一定是矩形高度），然后对于每个上边界，找最远的左边界和右边界；其中找最远的左边界，就是找左边第一个更小的柱子left，找最远的右边界right，就是找右边第一个更小的柱子；此时宽度就是right - left - 1，高度是h[i]；画图的话很显而易见；

所以首先我们可以暴力去找左边第一个更小和右边第一个更小：

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& h) {
        int n = h.size();
        int ans = 0;
        for (int i = 0; i < n; i ++) {
            // 求左边第一个满足的数，while不满足，跳出后left - 1满足
            int left = i;
            while (left >= 1 && h[left - 1] >= h[i]) left --;

            // 求右边第一个满足的数，while不满足，跳出后right + 1满足
            int right = i;
            while (right + 1 < n && h[right + 1] >= h[i]) right ++;

            // 其实w = right + 1 - (left - 1) + 1 = right - left + 1;
            ans = max(ans, h[i] * (right - left + 1));
        }
        return ans;
    }
};
```

单调栈优化：找左边xxx一般用从左到右写法，ans中的每位都会被计算；找右边xxx一般用从右到左写法，和前面同理；

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& h) {
        int n = h.size();
        vector<int> left(n), right(n);
        stack<int> stk;

        for (int i = 0; i < n; i ++ ) {
            while (stk.size() && h[stk.top()] >= h[i]) stk.pop();
            if (stk.empty()) left[i] = -1;
            else left[i] = stk.top();
            stk.push(i);
        }

        stk = stack<int>();
        for (int i = n - 1; i >= 0; i -- ) {
            while (stk.size() && h[stk.top()] >= h[i]) stk.pop();
            if (stk.empty()) right[i] = n;
            else right[i] = stk.top();
            stk.push(i);
        }

        int res = 0;
        for (int i = 0; i < n; i ++ ) {
            res = max(res, h[i] * (right[i] - left[i] - 1));
        }

        return res;
    }
};
```

#### 
### 堆

#### [215. 数组中的第K个最大元素](https://leetcode.cn/problems/kth-largest-element-in-an-array/)

AC，思路：快速选择模板题，快速选择是基于快速排序的，复习一下快速排序，首先是partition，将区间分为两段，左段&lt;=x，右段&gt;=x，然后这里因为求第k大，所以区间改为左段 &gt;= x，右段 &lt;=x；然后就找第k大的数在左段还是右段，然后只递归包含k的那一段即可；所以时间复杂度是 n + n / 2 + n / 4  + ... 1 = 2n；所以期望时间复杂度是O(n)，但是最坏时间复杂度跟快排一样还是有可能拿到O(n^2);

这道题目还可以用堆来做，但是时间复杂度没有快选好

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        return quick_select(nums, 0, nums.size() - 1, k - 1);
    }

    int quick_select(vector<int>& nums, int l, int r, int k) {
        if (l >= r) return nums[l];
        
        int i = l - 1, j = r + 1, x = nums[l + (r - l) / 2];
        while (i < j) {
            do i ++; while (nums[i] > x);
            do j --; while (nums[j] < x);
            if (i < j) swap(nums[i], nums[j]);
        }

        if (k <= j) return quick_select(nums, l, j, k);
        else return quick_select(nums, j + 1, r, k);
    }
};
```

#### [347. 前 K 个高频元素](https://leetcode.cn/problems/top-k-frequent-elements/)

AC，前k个高频元素，我们可以使用堆来做；堆维护前k个高频元素，也就是说低频元素要被pop出去，所以我们维护一个大小为k的小根堆，然后堆内的排序规则是，最小频率的在最上面；

技巧：关于堆的题目，维护最大的k个值，是pop小的值，说明是维护一个小根堆；如果是维护最小的k个值，是pop大的值，说明是维护一个大根堆；

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        // 哈希表 统计元素的出现次数
        unordered_map<int, int> hash;
        for (int num: nums) hash[num]++;
        
        // 维护最大频率的k个元素，小频率的被pop，所以是小根堆
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> heap;

        // 将[出现次数，元素]放入堆中，小根堆按照出现次数调整，堆顶是频率最低的
        for (auto& [key, val]: hash) {
            heap.emplace(val, key);
            if (heap.size() > k) heap.pop();
        }

        // 此时堆内的元素 就是 频率最大的k个元素
        vector<int> ans;
        while (heap.size()) {
            auto x = heap.top(); heap.pop();
            ans.push_back(x.second);
        }
        return ans;
    }
};
```

使用自定义的比较函数，会更直观一些

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        // 哈希表 统计元素的出现次数
        unordered_map<int, int> hash;
        for (int num: nums) hash[num]++;
        
        // 定义堆排序规则 小根堆是降序 >，这里是按照出现次数排序
        auto cmp = [](const pair<int, int>& a, const pair<int, int>& b) {
            return a.second > b.second;
        };

        // 维护最大频率的k个元素，小频率的被pop，所以是小根堆
        priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(cmp)> heap;

        // 将[元素，出现次数]放入堆中，小根堆按照出现次数调整，堆顶是频率最低的
        for (auto& [key, val]: hash) {
            heap.emplace(key, val);
            if (heap.size() > k) heap.pop();
        }

        // 此时堆内的元素 就是 频率最大的k个元素
        vector<int> ans;
        while (heap.size()) {
            auto x = heap.top(); heap.pop();
            ans.push_back(x.first);
        }
        return ans;
    }
};
```

#### [295. 数据流的中位数](https://leetcode.cn/problems/find-median-from-data-stream/)

NOT AC，对顶堆的经典运用；首先如果是动态维护有序序列，我们需要用到平衡树，但是这里其实只要求维护一个中间值，所以我们维护左右边界即可，维护左右边界，可以使用对顶堆；其中下面的堆down存放较小的部分，使用大根堆维护，上面的堆up存放较大的部分，使用小根堆维护；然后规定down.size()最多比up.size()大一；

现在我们就来维护这个对顶堆；插入元素num的时候，如果down为空，或者num &lt;= down的堆顶，就插入到下面的堆down中，插入之后根据堆的大小关系去调整；反之就插入到上面的堆up中，同样也是根据大小关系去调整；调整的时候很明显是将边界进行移动，也就是堆顶进行移动；

最后其实，我们插入的时候可以很灵活，例如可以down为空时插入up，或者num &lt; down堆顶时才插入down；为什么可以这么灵活呢，因为之后的调整总会达到一种状态就是down.size()比up.size()最多大1；

```cpp
class MedianFinder {
public:
    MedianFinder() {

    }
    
    void addNum(int num) {
        if (down.empty() || num <= down.top()) {
            down.push(num);
            if (down.size() > up.size() + 1) {
                up.push(down.top());
                down.pop();
            }
        }
        else {
            up.push(num);
            if (up.size() > down.size()) {
                down.push(up.top());
                up.pop();
            }
        }        
    }
    
    double findMedian() {
        if ((down.size() + up.size()) % 2 != 0) return down.top();
        else return (down.top() + up.top()) / 2.0;
    }

    // 对顶堆 规定down的size 最多比up的size 大1
    priority_queue<int, vector<int>> down;
    priority_queue<int, vector<int>, greater<int>> up;
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```

#### 
### 贪心

#### [121. 买卖股票的最佳时机](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/)

AC，思路：首先思考最暴力的做法，就是枚举卖出天i，然后枚举第i天之前的所有天j，计算利润，这样的话时间复杂度是O(n^2)；

由于这里是求最大利润，我们尝试贪心，枚举i，找前面最小的j，这样子可以得到枚举i时的局部最优；所有的i枚举完了之后，我们可以从所有的局部最优里得到全局最优，证明可以贪心来做；

找i前面最小的j，我们使用前缀最小值去维护，可以把每次找最小值的时间复杂度降低到O(1)；总时间复杂度O(n);

总结就是：枚举i，找前面最小的j，很明显的贪心 + 前缀最小值；

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();

        int ans = 0, min_price = 0x3f3f3f3f;
        for (int i = 0; i < n; i ++) {
            ans = max(ans, prices[i] - min_price);
            min_price = min(min_price, prices[i]);
        }
        return ans;
    }
};
```

#### [55. 跳跃游戏](https://leetcode.cn/problems/jump-game/)

AC，思路：转化一下题意，就是要求 最远可到达位置 &gt;= n - 1；那么如何得到最远可到达位置呢，我们尝试贪心，从头开始遍历，在每个位置上更新最远可到达位置（局部最优），中间如果不连续了说明无法达到终点了，遍历完后得到整体的最远可到达位置（全局最优）；当然也可以在循环中 r &gt;= n - 1时就返回 true，这可以让我们提前退出循环

```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int r = 0;   // 最远可达到位置
        for (int i = 0; i < nums.size(); i ++) {
            if (i > r) return false;  // 发现不连续，当前i无法达到，无法跳到终点
            r = max(r, i + nums[i]);  // 更新最远可达到位置
            // if (r >= nums.size() - 1) return true;  // 可以循环中提前判断
        }
        return true;  // 此时最远可达到位置一定 >= n - 1，返回true
    }
};
```

#### [45. 跳跃游戏 II](https://leetcode.cn/problems/jump-game-ii/)

NOT AC，思路：贪心，每次在起跳范围内选择可以使得跳的最远的位置；

```cpp
class Solution {
public:
    int jump(vector<int>& nums) {
        int r = 0;         // 最远位置
        int cnt = 0;       // 跳跃次数
        int end = 0;       // 当前起跳范围的end
        for (int i = 0; i < nums.size() - 1; i ++) {  // 终点不能作为起跳点！
            r = max(r, i + nums[i]);  // 更新最远位置
            if (i == end) {      // 遍历完当前的起跳范围
                end = r;         // 得到了下次起跳范围的end
                cnt ++;          // 从end处跳一步
            }
        }
        return cnt;
    }
};
```

先想动态规划，再优化贪心

https://leetcode.cn/problems/jump-game-ii/solutions/775090/gong-shui-san-xie-xiu-gai-shu-ju-fan-wei-wylq/?envType=study-plan-v2&envId=top-100-liked

https://leetcode.cn/problems/jump-game-ii/solutions/231856/dong-tai-gui-hua-tan-xin-yi-dong-by-optimjie/?envType=study-plan-v2&envId=top-100-liked

```cpp
// 动态规划
class Solution {
public:
    int jump(vector<int>& nums) {
        int n = nums.size();
        // 动态规划 f[i]表示到达i的最小步数
        vector<int> f(n, 0x3f3f3f3f);
        f[0] = 0;
        for (int i = 1; i < n; i ++) {
            for (int j = 0; j < i; j ++) {
                if (j + nums[j] >= i) { // 对于每一个可以跳到i的j都做状态计算
                    f[i] = min(f[i], f[j] + 1);
                }
            }
        }
        return f[n - 1];
    }
};

// 贪心优化
class Solution {
public:
    int jump(vector<int>& nums) {
        int n = nums.size();
        // 动态规划 f[i]表示到达i的最小步数
        vector<int> f(n, 0x3f3f3f3f);
        f[0] = 0;
        for (int i = 1, j = 0; i < n; i ++) {
            // 贪心的取离i点最远的点j（可达到i)来更新f[i]
            while (j + nums[j] < i) j ++;
            f[i] = f[j] + 1;
        }
        return f[n - 1];
    }
};
```

#### [763. 划分字母区间](https://leetcode.cn/problems/partition-labels/)

NOT AC，思路：实际上是一个区间合并问题；我们需要贪心地找到每一段极小区间；具体模拟方法，就是首先第一段区间是[0, 0] start = 0, end = 0；然后我们利用last哈希表去更新当前区间的终点，一直遍历下去，直到i == end说明当前区间合并完毕，找到一段极小区间；然后从start + 1处继续找下一段极小区间，直到字符串遍历完毕

```cpp
class Solution {
public:
    vector<int> partitionLabels(string s) {
        int n = s.size();
        
        // 统计每个字符的最后出现位置
        unordered_map<char, int> last;
        for (int i = 0; i < n; i ++) last[s[i]] = i;

        // 贪心 找到每一段极小区间
        vector<int> ans;
        int start = 0, end = 0;
        for (int i = 0; i < n; i ++) {
            end = max(end, last[s[i]]);  // 更新当前区间的终点
            if (end == i) {   // 当前区间合并完毕
                ans.push_back(end - start + 1);  // 区间长度加入答案
                start = i + 1; // 下一个区间的起点
            }
        }
        return ans;
    }
};
```

#### 
### 动态规划

#### [70. 爬楼梯](https://leetcode.cn/problems/climbing-stairs/)

AC，思路：动态规划，简单入门题；主要就是练习，初始化/边界；

```cpp
// 
class Solution {
public:
    int climbStairs(int n) {
        vector<int> f(n + 1, 1);
        for (int i = 2; i <= n; i ++) {
            f[i] = f[i - 1] + f[i - 2];
        }
        return f[n];
    }
};


class Solution {
public:
    int climbStairs(int n) {
        vector<int> f(n + 3, 0);

        f[1] = 0, f[2] = 1;
        for (int i = 1; i <= n; i ++) {
            f[i + 2] = f[i + 1] + f[i];
        }
        return f[n + 2];
    }
};

class Solution {
public:
    int climbStairs(int n) {
        int f0 = 0, f1 = 1;
        for (int i = 1; i <= n; i ++) {
            int new_f = f0 + f1;
            f0 = f1;
            f1 = new_f;
        }
        return f1;
    }
};
```

#### [118. 杨辉三角](https://leetcode.cn/problems/pascals-triangle/)

AC，杨辉三角，典型的路径dp；可以直接在ans上构造，也可以先构造出杨辉三角形矩阵再放入ans中

```cpp
class Solution {
public:
    vector<vector<int>> generate(int n) {

        vector<vector<int>> f(n + 1, vector<int>(n + 1, 0));
        f[0][0] = 1, f[0][1] = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < n; j ++) {
                f[i + 1][j + 1] = f[i][j + 1] + f[i][j];
            }
        }   

        vector<vector<int>> ans; ans.resize(n);
        int level = 0;
        for (int i = 1; i <= n; i ++) {
            for (int j = 1; j <= i; j ++) {
                ans[level].push_back(f[i][j]);
            }
            level ++;
        }

        return ans;
    }
};
```

直接构造：

```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> c(numRows);
        for (int i = 0; i < numRows; i++) {
            c[i].resize(i + 1, 1);
            for (int j = 1; j < i; j++) {
                // 左上方的数 + 正上方的数
                c[i][j] = c[i - 1][j - 1] + c[i - 1][j];
            }
        }
        return c;
    }
};
```

#### [198. 打家劫舍](https://leetcode.cn/problems/house-robber/)

AC，思路：打家劫舍，可以普通dp来做，状态的初始化稍微复杂一些，但是状态转移方程简单；也可以状态机dp来做，状态初始化简单一些，但是状态转移方程复杂一些；

普通dp：f[i]代表偷前i个房子的最大利润

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        vector<int> f(n + 2, 0);
        for (int i = 0; i < n; i++) {
            f[i + 2] = max(f[i + 1], f[i] + nums[i]); 
        }
        return f[n + 1];
    }
};
```

状态机dp: f[i][0] 代表偷到第i个房子，第i个房子不偷的最大利润，f[i][1]代表偷到第i个房子，第i个房子偷的最大利润；

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        int f[n + 1][2];
        memset(f, 0, sizeof(f));
        
        f[0][0] = f[0][1] = 0;
        for (int i = 0; i < n; i ++ ) {
            f[i + 1][0] = max(f[i][0], f[i][1]);
            f[i + 1][1] = f[i][0] + nums[i];             
        }
        return max(f[n][0], f[n][1]);
    }
};
```

#### [279. 完全平方数](https://leetcode.cn/problems/perfect-squares/)

NOT AC，思路：首先转化题意，从一堆完全平方数里选，完全平方数的和恰好等于n的最少完全平方数数量；因为可以重复选，所以转化为完全背包问题；物品是完全平方数，背包体积是n，物品体积是完全平方数的值a[i]

```cpp
class Solution {
public:
    int numSquares(int n) {
        // 获取所有<=n的完全平方数，构成一堆完全平方数
        vector<int> a;
        for (int i = 1; i * i <= n; i ++) a.push_back(i * i);
        int m = a.size();  // 物品数量是m

        // 从一些完全平方数里选，和恰好等于n的最少元素数量
        vector<vector<int>> f(m + 1, vector<int>(n + 1, 0x3f3f3f3f));
        f[0][0] = 0;
        for (int i = 0; i < m; i ++) {   // 遍历物品
            for (int j = 0; j <= n; j ++) {  // 遍历体积
                if (j >= a[i]) f[i + 1][j] = min(f[i + 1][j - a[i]] + 1, f[i][j]);
                else f[i + 1][j] = f[i][j]; 
            }
        }
        return f[m][n];
    }
};
```

#### [322. 零钱兑换](https://leetcode.cn/problems/coin-change/)

AC，思路：转化一下题意，从一些硬币里选，硬币面额和恰好等于amount的最少硬币数量，因为可以重复选，所以是完全背包问题；物品是硬币，背包体积是amount，物品体积是硬币面额coins[i]；

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int n = coins.size();
        vector<vector<int>> f(n + 1, vector<int>(amount + 1, 0x3f3f3f3f));
        f[0][0] = 0;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j <= amount; j ++) {
                if (j >= coins[i]) f[i + 1][j] = min(f[i + 1][j - coins[i]] + 1, f[i][j]);
                else f[i + 1][j] = f[i][j];
            }
        }
        return f[n][amount] == 0x3f3f3f3f ? -1 : f[n][amount];
    }
};
```

#### [139. 单词拆分](https://leetcode.cn/problems/word-break/)

NOT AC，思路：原字符串拆分后是有序的，所以这里不是背包dp；但是如果是求方案数或者方案是否存在，其实就和拆分顺序无关，也可以当作完全背包来做！如果是求最优方案，我们的方案要求有序，就不能看作背包dp了

我们可以定义f[i]为1-i的字符串可以被拆分；然后我们就要去构建状态转移方程，这里发现没办法直接找到前驱，所以不是线性dp；我们可以通过枚举最后一步，来尝试找到前驱，枚举最后一步的最后一段的左端点j，这样字符串就被分割为两部分 [1, j - 1], [j, n]；当前面可以被拆分，后面的字符串存在时，原字符串可以被分割；所以状态转移方程 f[i] = f[j - 1] && [j, n]存在；

https://leetcode.cn/problems/word-break/solutions/1945055/by-ac_oier-gh00/?envType=study-plan-v2&envId=top-100-liked

```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        int n = s.size();
        unordered_map<string, int> hash;
        for (auto word : wordDict) hash[word]++;
        
        int f[n + 1];
        memset(f, 0, sizeof(f));

        f[0] = 1;
        for (int i = 1; i <= n; ++ i) {   // 遍历状态
            for (int j = 1; j <= i && !f[i]; ++j) {  // 枚举最后一步，枚举最后一段的左端点
                string sub = s.substr(j - 1, i - j + 1);
                if (hash.count(sub)) f[i] = f[j - 1]; 
            }
        }

        return f[n];
    }
};
```

#### [300. 最长递增子序列](https://leetcode.cn/problems/longest-increasing-subsequence/)

AC，思路：LIS模型模板题

```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();

        vector<int> f(n + 1, 1);
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j < i; j ++) {
                if (nums[j] < nums[i]) 
                    f[i + 1]  = max(f[i + 1], f[j + 1] + 1);
            }
        }
        
        return ranges::max(f);
    }
};
```

#### [152. 乘积最大子数组](https://leetcode.cn/problems/maximum-product-subarray/)

AC，思路：f[i]表示 以nums[i]结尾的子数组乘积最大值；然后根据最后一步划分，构建状态转移方程，最后一步肯定是i - 1，然后选和不选；f[i] = max(f[i], f[i - 1] * nums[i]); 然后我们发现f[i]不仅可以从前面的乘积最大值转化过来，也可以从乘积最小值转化过来；所以我们还需要维护g[i] 表示 以nums[i]结尾的子数组的乘积最小值，得到最终的状态转移方程：

f[i] = max(f[i], max(f[i - 1] * nums[i], g[i - 1] * nums[i]);

g[i] = min(g[i], min(g[i - 1] * nums[i], f[i - 1] * nums[i]);

技巧：dp的初始化，如果是已经解决了边界问题的话，就看两步

1. 初始状态合法：循环内的依赖项合法，对于本题就是 i = 0时，f和g都是nums[0]；
2. 防止非法状态转移：一维dp，初始状态周围不存在非法状态，不需要做额外操作；然后最优化问题，可以把状态空间先初始化为极值，防止非法状态转移；

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int n = nums.size();

        vector<int> f(n + 1, 0), g(n + 1, 0);
        int ans = nums[0];
        f[0] = g[0] = 1;
        for (int i = 0; i < n; i ++) {
            f[i + 1] = max(nums[i], max(f[i] * nums[i], g[i] * nums[i]));  // f[i] 以nums[i]为结尾的乘积最大值
            g[i + 1] = min(nums[i], min(g[i] * nums[i], f[i] * nums[i]));  // g[i] 以nums[i]为结尾的乘积最小值
            ans = max(ans, f[i + 1]);
        }
        return ans;
    }
};
```

#### [416. 分割等和子集](https://leetcode.cn/problems/partition-equal-subset-sum/)

AC，思路：转化题意，从一堆数里面选，数字和 恰好等于 sum / 2 的方案是否存在；因为每个数只能选一次，很明显的01背包问题；物品是数，背包体积v是sum / 2，物品体积是数的值nums[i]；

```cpp
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
        int sum = accumulate(nums.begin(), nums.end(), 0);
        if (sum % 2) return false;

        int v = sum / 2;
        bool f[n + 1][v + 1];
        memset(f, false, sizeof(f));

        f[0][0] = true;
        for (int i = 0; i < n; i ++) {
            for (int j = 0; j <= v; j ++) {
                if (j >= nums[i]) f[i + 1][j] = f[i][j - nums[i]] || f[i][j]; 
                else f[i + 1][j] = f[i][j];
            }
        }

        return f[n][v];
    }
};
```

#### [32. 最长有效括号](https://leetcode.cn/problems/longest-valid-parentheses/)

NOT AC，有效括号题目，暴力做法肯定超时；我们尝试动态规划来做，这里定义 f[i]表示 以s[i]结尾的有效括号的最大长度；然后考虑最后一步，s[i]是右括号还是左括号，左括号的话直接是0，右括号的话，需要进一步考虑s[i - 1]是左括号还是右括号：

s[i - 1]是左括号，那就是f[i] = f[i - 2] + 2;

s[i - 1]是右括号，当对应的左括号位置 s[i - f[i - 1] - 1]是左括号时 f[i] = f[i - f[i - 1] - 2] + f[i - 1] + 2;

```cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        int maxans = 0, n = s.length();
        vector<int> dp(n, 0);
        for (int i = 1; i <= n; i++) {
            if (s[i] == ')') {
                if (s[i - 1] == '(') {
                    dp[i] = (i >= 2 ? dp[i - 2] : 0) + 2;
                } else if (i - dp[i - 1] > 0 && s[i - dp[i - 1] - 1] == '(') {
                    dp[i] = dp[i - 1] + ((i - dp[i - 1]) >= 2 ? dp[i - dp[i - 1] - 2] : 0) + 2;
                }
                maxans = max(maxans, dp[i]);
            }
        }
        return maxans;
    }
};
```

#### 
### 多维动态规划

#### [62. 不同路径](https://leetcode.cn/problems/unique-paths/)

AC，思路：网格图dp模板题；为了避免越界，我们一般从1，1开始；然后初始化注意两点；首先是初始状态的初始化（循环内的依赖状态) i = 0, j = 0时，f = 1 也就是 f[0][1] + f[1][0] = 1；所以我们可以初始化f[0][1] = 1, f[1][0]= 0；然后就是防止非法状态转移，因为这里是二维dp，初始状态周围存在非法状态转移，所以状态空间初始化为0；

```cpp
// 1，1 -> m, n
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> f(m + 1, vector<int>(n + 1, 0));
        f[0][1] = 1, f[1][0] = 0;
        for (int i = 1; i <= m; i ++) {
            for (int j = 1; j <= n; j ++) {
                f[i][j] = f[i - 1][j] + f[i][j - 1];
            }
        }
        return f[m][n];
    }
};
```

#### [64. 最小路径和](https://leetcode.cn/problems/minimum-path-sum/)

AC，思路：网格图dp，优化写法，从1，1开始；然后初始化考虑两点；1. 初始状态正确（循环依赖项正确）i = 0, j = 0时，f = grid[0][0]，所以min(f[0][1], f[1][0]) = 0，所以我们可以初始化f[0][1] = f[1][0] = 0; 2. 防止非法状态转移，由于网格图是二维dp，初始状态周围存在非法状态转移，这里是求极小值，所以我们可以把这些非法状态初始化为极大值，防止转移，所以初始化状态空间为极大值；

```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();

        vector<vector<int>> f(m + 1, vector<int>(n + 1, 0x3f3f3f3f));
        f[0][1] = f[1][0] = 0;
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                f[i + 1][j + 1] = min(f[i][j + 1], f[i + 1][j]) + grid[i][j];
            }
        }

        return f[m][n];
    }
};
```

#### [5. 最长回文子串](https://leetcode.cn/problems/longest-palindromic-substring/)

NOT AC，思路：首先暴力枚举O(n^3)肯定会超时；

动态规划：尝试动态规划优化；

首先考虑线性dp，发现回文的判断状态不好设计，所以使用区间dp，f[i][j] 表示s[i..j]是否为回文子串；

然后状态转移方程就很容易了：f[i][j] = s[i] == s[j] && (j - i + 1 &lt;= 2 || f[i + 1][j - 1]);

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.size();
        
        vector<vector<bool>> f(n, vector<bool>(n, false));
        string ans;
        for (int i = n - 1; i >= 0; i--) {
            for (int j = i; j < n; j++) {
                f[i][j] = (s[i] == s[j]) && (j - i + 1 <= 2 || f[i + 1][j - 1]);
                if (f[i][j] && j - i + 1 > ans.size()) ans = s.substr(i, j - i + 1);
            }
        }
        return ans;
    }
};
```

中心扩展法：

#### [1143. 最长公共子序列](https://leetcode.cn/problems/longest-common-subsequence/)

AC，思路：最长公共子序列，线性dp的模板题；

```cpp
class Solution {
public:
    int longestCommonSubsequence(string s, string t) {
        int n = s.length(), m = t.length();
        vector<vector<int>> f(n + 1, vector<int>(m + 1));
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                f[i + 1][j + 1] = s[i] == t[j] 
                    ? f[i][j] + 1 : max(f[i][j + 1], f[i + 1][j]);
        return f[n][m];
    }
};
```

#### [72. 编辑距离](https://leetcode.cn/problems/edit-distance/)

AC，思路：f[i][j] 表示word1 [1, i]转化为word2[1, j]的最少步数；

也是像最长公共子序列一样去构造状态转移方程

f[i][j] = word1[i] == word2[j] ? f[i - 1][j - 1] : min(f[i - 1][j - 1], f[i][j - 1], f[i - 1][j]) + 1; 

注意初始化，这里初始化初始状态（循环内的依赖状态，因为这里是二维dp且跟i - 1, j - 1有关），所以我们需要将f[1, j], f[i, 1]都初始化，而不是像之前的二维dp只初始化f[1, 1]；

```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int n = word1.size(), m = word2.size();

        vector<vector<int>> f(n + 1, vector<int>(m + 1));
        for(int i = 1; i <= n; i++) f[i][0] = i;
        for(int i = 1; i <= m; i++) f[0][i] = i;
        
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= m; j++) {
                word1[i - 1] == word2[j - 1] ? 
                    f[i][j] = f[i - 1][j - 1] :
                    f[i][j] = min(f[i - 1][j - 1], min(f[i - 1][j], f[i][j - 1])) + 1;
            }
        }
        return f[n][m];
    }
};
```

#### 
### 技巧

#### [136. 只出现一次的数字](https://leetcode.cn/problems/single-number/)

AC，思路：这题有很多种解法

排序，然后统计所有分段

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        for (int i = 0; i < n; i ++) {
            int len = 1;
            // 找连续xxx的一段 常用写法！！！
            while (i + 1 < n && nums[i] == nums[i + 1]) i ++, len ++;
            if (len == 1) return nums[i]; 
        }
        return -1;
    }
};
```

哈希表，统计每个数字的出现次数

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int n = nums.size();
        unordered_map<int, int> hash;
        for (int i = 0; i < n; i ++) hash[nums[i]] ++;

        for (auto& [key, val]: hash) {
            if (val == 1) return key;
        }
        return -1;
    }
};
```

最优解法：异或运算

异或运算 ⊕。异或运算有以下三个性质。

1. 任何数和 0 做异或运算，结果仍然是原来的数，即 a⊕0=a。
2. 任何数和其自身做异或运算，结果是 0，即 a⊕a=0。
3. 异或运算满足交换律和结合律，即 a⊕b⊕a=b⊕a⊕a=b⊕(a⊕a)=b⊕0=b。

所以根据异或，先调整一下顺序，然后次数为2的数组异或后直接为0，次数为1的最终会和0异或，得到自身；

初始我们将ans = 0，因为nums[0]和0异或还是nums[0]; 当然也可以直接将ans = nums[0]，然后从1开始遍历逐个异或

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ans = 0;
        for (int x: nums) {
            ans ^= x;
        }
        return ans;
    }
};
```

#### [169. 多数元素](https://leetcode.cn/problems/majority-element/)

NOT AC，思路：如果没有限制的话，排序或者哈希表都可以；但是这里限制O(n)的时间和O(1)的空间，所以我们这里就是介绍一下摩尔投票算法；初始的时候，设置leader和votes，代表选出的数和对应的票数；遍历所有的数，当votes=0时，说明当前的数就是leader，然后votes = 1；如果votes != 0，但是当前的数不是leader，就相当于抵消，票数 - 1；如果是leader，就相当于加分，票数 + 1；因为有一个数绝对过半，所以抵消过后，其他的数votes 都是0，就这个数的votes不为0，此时leader是这个过半的数；

这个算法成立的必要条件就是 这个数的出现次数必须过半！

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int leader = 0, votes = 0;   // 当前选出来的leader和对应的票数
        for (auto num: nums) {
            if (votes == 0) leader = num, votes = 1;  // 票数为0，当前数就是leader，票数为1
            else if (num != leader) votes--;   // 当前数不是leader，抵消，票数-1
            else votes++;  // 当前数是leader，加分，票数 + 1；
        }
        return leader;  // 最后其他的数都被抵消掉，只有过半的那个数会存活下来；
    }
};
```

#### [75. 颜色分类](https://leetcode.cn/problems/sort-colors/)

NOT AC，思路：荷兰国旗问题，只适用于这一道题目；

定义三个指针，i，j，k，区间定义和循环不变量：[0, j - 1] = 0，[j ,i - 1] = 1，[k + 1, n - 1] = 2；

所以初始化 i = 0, j = 0, k = n - 1; 

if nums[i] = 0, swap(nums[i], nums[j]) j ++,  因为交换完后j处是原来的nums[i] = 0，但是我们要j - 1处是0，j ++；同理交换完后i处是原来的nums[j] = 1,我们要i - 1是1，所以i ++;

if nums[i] = 2, swap(nums[i], nums[k]) k --; 交换完后k处是原来的nums[i] = 2, 但是我们要k + 1处是2，所以k--；同理交换完后i处事原来的nums[k]，我们的区间定义和循环不变量里，nums[k]是未知的，所以不做其他操作；

if nums[i] = 1, i ++; 当前就是1，说明i处是1，但是我们要i - 1处是1，所以i ++；

很明显，我们要紧扣区间定义和循环不变量来写！

https://www.acwing.com/solution/content/16177/

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        for (int i = 0, j = 0, k = nums.size() - 1; i <= k;) {
            if (nums[i] == 0) swap(nums[i ++ ], nums[j ++ ]);
            else if (nums[i] == 2) swap(nums[i], nums[k -- ]);
            else i ++ ;
        }
    }
};
```

#### [31. 下一个排列](https://leetcode.cn/problems/next-permutation/)

NOT AC，思路：最简单的方法就是调用stl的内置函数 next_permutation；

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        next_permutation(nums.begin(), nums.end());
    }
};
```

如果不让调用的话，我们就自己实现一下这个函数

#### [287. 寻找重复数](https://leetcode.cn/problems/find-the-duplicate-number/)

NOT AC，思路：这里建图来解决，数组下标i看作节点id，数组值nums[i]看作是节点的出边（出边值就是下一个节点id，入边值是当前节点id），因为nums[i]只有一个值，所以相当于每个点只有一条出边，然后因为有重复的两个数，说明有两个出边相同（指向相同的节点），所以一定有环，而且是尾部有环；

所以现在我们要求重复的数，就是要找到环的起点的入边；也就是当前节点的id；

参考这个图：https://leetcode.cn/problems/find-the-duplicate-number/solutions/179836/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--52/?envType=study-plan-v2&envId=top-100-liked

```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = 0, fast = 0;
        while (true) {
            slow = nums[slow];
            fast = nums[nums[fast]];
            if (slow == fast) {
                int head = 0;
                while (slow != head) {
                    slow = nums[slow];
                    head = nums[head];
                }
                return slow;   // 最后找的是当前点的入边 = 当前点的下标
            }
        }
        return -1;
    }
};
```

