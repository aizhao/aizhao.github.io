# 第14届蓝桥杯C++ B组题解(A-G)

[TOC]



## A 日期统计

------

#### 【问题描述】

**小蓝现在有一个长度为100的数组，数组中的每个元素的值都在0到9的范围之内。数组中的元素从左至右如下所示：**

> 5 6 8 6 9 1 6 1 2 4 9 1 9 8 2 3 6 4 7 7 5 9 5 0 3 8 7 5 8 1 5 8 6 1 8 3 0 3 7 9 2 7 0 5 8 8 5 7 0 9 9 1 9 4 4 6 8 6 3 3 8 5 1 6 3 4 6 7 0 7 8 2 7 6 8 9 5 6 5 6 1 4 0 1 0 0 9 4 8 0 9 1 2 8 5 0 2 5 3 3

**现在他想要从这个数组中寻找一些满足以下条件的子序列:**
        **1.子序列的长度为 8:**
        **2.这个子序列可以按照下标顺序组成一个 yyy,ymmdd 格式的日期，并且要求这个日期是 2023 年中的某一天的日期，例如 20230902，20231223。yyyy 表示年份，mm 表示月份，dd 表示天数，当月份或者天数的长度只有一位时需要一个前导零补充。**
**请你帮小蓝计算下按上述条件一共能找到多少个不同的 2023 年的日期。对于相同的日期你只需要统计一次即可。**

#### 【答案提交】

**这是一道结果填空的题，你只需要算出结果后提交即可。本题的结果为一个整数，在提交答案时只填写这个整数，填写多余的内容将无法得分。**

#### 【解析】

**首先我们可以手动找到2023的位置，减少数字，然后通过4个循环搞定，最后使用set进行去重**

#### 【代码】

```c++
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N = 100010;
int a[N], b[N];
int n, k, ans;
int m[13] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
void solve() {
	set<int> s;
	for (int i = 1; i <= 41; i++) cin >> a[i];
	for (int i = 1; i <= 41; i++) {
		for (int j = i + 1; j <= 41; j++) {
			n = a[i] * 10 + a[j];
			if (n >= 1 && n <= 12) {
				for (int k = j + 1; k <= 41; k++) {
					for (int q = k + 1; q <= 41; q++) {
						int d = a[k] * 10 + a[q];
						if (d <= m[n] && d > 0) {
							s.insert(n * 100 + d);
						}

					}
				}
			}
		}
	}
	cout << s.size();
}
signed main() {
	ios::sync_with_stdio(false);
	int t = 1;
//	cin>>t;
	while (t--) {
		solve();
	}
	return 0;
}
```

#### 【答案】

> 235B

## B 01串的熵

------

#### 【问题描述】

![image]:[![pFqp1pV.png](https://s21.ax1x.com/2024/04/05/pFqp1pV.png)](https://imgse.com/i/pFqp1pV)

#### 【答案提交】

**这是一道结果填空的题，你只需要算出结果后提交即可。本题的结果为一个整数，在提交答案时只填写这个整数，填写多余的内容将无法得分。**

#### 【解析】

**直接循环,由于他说0比1的数量少,因此循环到23333333/2即可,由于题目中给出最后的熵是浮点数,所以注意精度的处理.**

#### 【代码】

```c++
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N=100010;
int a[N],b[N];
int n,m,k;
double check(int x){
    double x1=x*1.0/n;
	double x2=(n-x)*1.0/n;
	double sum=-1.0*x*x1*log2(x1)-1.0*(n-x)*x2*log2(x2);
	return sum;
}
void solve(){
	n=23333333;
	double ans=11625907.5798;
	for(int i=1;i<=n/2;i++){
		if(abs(check(i)-ans)<0.0001){
			cout<<i<<'\n';
			break;
		}
	}
}
signed main(){
	ios::sync_with_stdio(false);
	int t=1;
//	cin>>t;
	while(t--){
		solve();
	}
	return 0;
}
```

#### 【答案】

> 11027421

## C 冶炼金属

------

#### 【问题描述】

**小蓝有一个神奇的炉子用于将普通金属 O 冶炼成为一种特殊金属 X。这个炉子有一个称作转换率的属性 V，V 是一个正整数，这意味着消耗 V 个普通金**
**属 O 恰好可以冶炼出一个特殊金属 X，当普通金属 O 的数目不足 V 时，无法继续冶炼。现在给出了 N 条冶炼记录，每条记录中包含两个整数 A 和 B，这表示本次**
**投入了 A 个普通金属 O，最终冶炼出了 B 个特殊金属 X。每条记录都是独立的，这意味着上一次没消耗完的普通金属 O 不会累加到下一次的冶炼当中。根据这 N 条冶炼记录，请你推测出转换率 V 的最小值和最大值分别可能是多少，题目保证评测数据不存在无解的情况。**

#### **【输入格式】**

**第一行一个整数 N，表示冶炼记录的数目。**
**接下来输入 N 行，每行两个整数 A、B，含义如题目所述。****

#### **【输出格式】**

**输出两个整数，分别表示 V 可能的最小值和最大值，中间用空格分开。**

#### **【样例输入】**

>3
>75 3
>53 2
>59 2

#### **【样例输出】**

> 20 25

#### 【解析】

**转化率必须每行记录都满足，那么所有的A/B当中，最小的那个v必须充当Vmax，因为较大的v不一定满足小的.因此Vmax=min(A/B).**

**下面推导vmin：**

 **当我们的B如果增加一个，即B’=B+1时，转化率v为A/B'，这个时候的v即为临界值，我们需要加1，即为原本最小满足要求的转化率，这个时候我们需要查找所有记录中最大的v,因为小的v可能会小于其他v的那个临界值，使大的转化记录不符合要求。因此Vmin=max(A/(B+1)+1)。**

#### 【代码】

```c++
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N=100010;
int a[N],b[N];
int n,m,k,ans;
void solve(){
	cin>>n;
	int Vmax=1e9;
	int Vmin=0;
	for(int i=1;i<=n;i++){
		int x,y;
		cin>>x>>y;
		Vmax=min(Vmax,x/y);
		Vmin=max(Vmin,(x+1)/(y+1));
	}
	cout<<Vmin<<' '<<Vmax;
}

signed main(){
	ios::sync_with_stdio(false);
	int t=1;
//	cin>>t;
	while(t--){
		solve();
	}
	return 0;
}
```

## D 飞机降落

------

#### 【问题描述】

**N 架飞机准备降落到某个只有一条跑道的机场。其中第 i 架飞机在 Ti 时刻到达机场上空，到达时它的剩余油料还可以继续盘旋 Di 个单位时间，即它最早可以于 Ti 时刻开始降落，最晚可以于 Ti + Di 时刻开始降落。降落过程需要 Li个单位时间。一架飞机降落完毕时，另一架飞机可以立即在同一时刻开始降落，但是不能在前一架飞机完成降落前开始降落。请你判断 N 架飞机是否可以全部安全降落。**

#### **【输入格式】**

**输入包含多组数据。**
**第一行包含一个整数 T，代表测试数据的组数。**
**对于每组数据，第一行包含一个整数 N。**
**以下 N 行，每行包含三个整数：Ti，Di 和 Li。**

#### **【输出格式】**

**对于每组数据，输出 YES 或者 NO，代表是否可以全部安全降落。**

#### **【样例输入】**

>2
>3
>0 100 10
>10 10 10
>0 2 20
>3
>0 10 20
>10 10 20
>20 10 20

#### **【样例输出】**

> YES
> NO

#### 【解析】

观察数据很小，考虑使用dfs暴搜每一种起飞顺序，只要当当前的起飞时间+等待时间>=上次降落时间，才可以进行下一步，只要能找到一种合法的顺序，即为YES，否则为NO

#### 【代码】

```c++
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N = 100010;
int a[N], b[N];
int n, m, k, ans;
struct node {
	int ti, di, li;
};
bool flag;
node plane[N];
bool v[N];
void dfs(int cnt, int last) {
	if (cnt == n) {
		flag = 1;
		return;
	}
	for (int i = 1; i <= n; i++) {
		if (!v[i] && plane[i].ti + plane[i].di >= last) {
			v[i] = 1;
			dfs(cnt + 1, max(last, plane[i].ti) + plane[i].li);
			v[i] = 0;
		}
	}
}
void solve() {
	memset(v, 0, sizeof(v));
	cin >> n;
	for (int i = 1; i <= n; i++) {
		cin >> plane[i].ti >> plane[i].di >> plane[i].li;
	}
	flag = 0;
	dfs(0, 0);
	if (flag) cout << "YES\n";
	else cout << "NO\n";

}

signed main() {
	ios::sync_with_stdio(false);
	int t = 1;
	cin >> t;
	while (t--) {
		solve();
	}
	return 0;
}
```



## E 接龙数列

------

#### 【问题描述】

**对于一个长度为 K 的整数数列：A1, A2, . . . , AK，我们称之为接龙数列，当且仅当 Ai 的首位数字恰好等于 Ai−1 的末位数字 (2 ≤ i ≤ K)。例如 12, 23, 35, 56, 61, 11 是接龙数列；12, 23, 34, 56 不是接龙数列，因为 56的首位数字不等于 34 的末位数字。所有长度为 1 的整数数列都是接龙数列。现在给定一个长度为 N 的数列 A1, A2, . . . , AN，请你计算最少从中删除多少个数，可以使剩下的序列是接龙序列？**

#### **【输入格式】E**

**第一行包含一个整数 N。**
**第二行包含 N 个整数 A1, A2, . . . , AN。**

#### **【输出格式】**

**一个整数代表答案。**

#### **【样例输入】**

>5
>11 121 22 12 2023

#### **【样例输出】**

> 1

#### 【解析】

**题目类似于最长上升子序列，我们如果能找出最长的接龙数列长度为L，那么需要删除的数量即为n-L。**

**下面考虑o(n^2)做法**  **（通过率：50%）**：

**我们设置a数组存首数字，b数组存尾数字，设置状态dp[i]表示以i结尾的最长接龙数列的长度**

**状态转移方程：**
$$
dp[i]=max(dp[i],dp[j]+1)
$$
**j的范围为1~i-1** 。**最后dp数组中最大的长度即为最长接龙数列**

**o(n)做法 （通过率：100%）**：

**继续研究发现，如果我们设置dp[y]表示以数字y结尾的最长接龙数列，那么每次转移需要考虑当前数字取还是不取，如果取，那么上一个数字的首数字x就必须等于上一个y，因此得出状态转移方程：**
$$
dp[y]=max(dp[y],dp[x]+1)
$$


#### 【代码 o(n^2）】

```c++
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N=100010;
int a[N],b[N];
int n,m,k,ans;
int dp[N];
void solve(){
	cin>>n;
	string s;
	for(int i=1;i<=n;i++){
		cin>>s;
		a[i]=s[0]-'0';
		b[i]=s[s.size()-1]-'0';
	}
	for(int i=1;i<=n;i++){
		dp[i]=1;
		for(int j=1;j<i;j++){
			if(b[j]==a[i])
				dp[i]=max(dp[i],dp[j]+1);
		}
		ans=max(ans,dp[i]);
	}
	cout<<n-ans<<'\n';
}

signed main(){
	ios::sync_with_stdio(false);
	int t=1;
//	cin>>t;
	while(t--){
		solve();
	}
	return 0;
}
```

#### 【代码 o(n）】

```c++
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N=100010;
int a[N],b[N];
int n,m,k,ans;
int dp[N];
void solve(){
	cin>>n;
	string s;
	int x,y;
	for(int i=1;i<=n;i++){
		cin>>s;
		x=s[0]-'0';
		y=s[s.size()-1]-'0';
		dp[y]=max(dp[y],dp[x]+1);
		ans=max(ans,dp[y]);
	}
	cout<<n-ans<<'\n';
}

signed main(){
	ios::sync_with_stdio(false);
	int t=1;
//	cin>>t;
	while(t--){
		solve();
	}
	return 0;
}
```

## F 岛屿个数

------

#### 【问题描述】

**小蓝得到了一副大小为 M × N 的格子地图，可以将其视作一个只包含字符‘0’（代表海水）和 ‘1’（代表陆地）的二维数组，地图之外可以视作全部是海水，每个岛屿由在上/下/左/右四个方向上相邻的 ‘1’ 相连接而形成。在岛屿 A 所占据的格子中，如果可以从中选出 k 个不同的格子，使得他们的坐标能够组成一个这样的排列：(x0, y0),(x1, y1), . . . ,(xk−1, yk−1)，其中(x(i+1)%k, y(i+1)%k) 是由 (xi, yi) 通过上/下/左/右移动一次得来的 (0 ≤ i ≤ k − 1)，此时这 k 个格子就构成了一个 “环”。如果另一个岛屿 B 所占据的格子全部位于这个 “环” 内部，此时我们将岛屿 B 视作是岛屿 A 的子岛屿。若 B 是 A 的子岛屿，C 又是 B 的子岛屿，那 C 也是 A 的子岛屿。请问这个地图上共有多少个岛屿？在进行统计时不需要统计子岛屿的数目。**

#### **【输入格式】**

**第一行一个整数 T，表示有 T 组测试数据。**
**接下来输入 T 组数据。对于每组数据，第一行包含两个用空格分隔的整数**
**M、N 表示地图大小；接下来输入 M 行，每行包含 N 个字符，字符只可能是**
**‘0’ 或 ‘1’。**

#### **【输出格式】**

**对于每组数据，输出一行，包含一个整数表示答案。**

#### **【样例输入】**

>2
>5 5
>01111
>11001
>10101
>10001
>11111
>5 6
>111111
>100001
>010101
>100001
>111111

#### **【样例输出】**

> 1
> 3

#### 【样例说明】

**对于第一组数据，包含两个岛屿，下面用不同的数字进行了区分：**

> **01111**
> **11001**
> **10201**
> **10001**
> **11111**

**岛屿 2 在岛屿 1 的 “环” 内部，所以岛屿 2 是岛屿 1 的子岛屿，答案为 1。**
**对于第二组数据，包含三个岛屿，下面用不同的数字进行了区分：**

> **111111**
> **100001**
> **020301**
> **100001**
> **111111**

**注意岛屿 3 并不是岛屿 1 或者岛屿 2 的子岛屿，因为岛屿 1 和岛屿 2 中均没有**
**“环”。**

#### 【解析】

**本题找岛屿容易，关键是找子岛屿，我们考虑，既然是子岛屿，那么每个子岛屿外围一定有1包围，那么如果我们从海水开始向8个方向搜索，无论如何都搜索不到子岛屿，想到这题目就变简单了，我们先从最外围搜索海水，将没有到达的海水全部标记为1，这样我们就将子岛屿和外层的岛屿直接相连接了，那么后续的统计也就不是大问题。**

#### 【代码】

```c++
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N=100;
int n,m,k,ans;
char a[N][N];

char b[N][N];
int dx[8]={1,-1,0,0,1,-1,1,-1};
int dy[8]={0,0,1,-1,1,-1,-1,1};
bool v1[N][N];
bool v[N][N];
//查找海水
void dfs1(int x,int y){
	a[x][y]='2';
	v1[x][y]=1;
	for(int i=0;i<8;i++){
		int xx=x+dx[i];
		int yy=y+dy[i];
		if(xx<0||xx>n+1||yy<0||yy>m+1) continue;
		if(a[xx][yy]!='0') continue;
		if(v1[xx][yy]) continue;
		dfs1(xx,yy);
	}
}
//查找岛屿
void dfs(int x,int y){
	a[x][y]='2';
	v[x][y]=1;
	for(int i=0;i<4;i++){
		int xx=x+dx[i];
		int yy=y+dy[i];
		if(xx<1||yy<1||xx>n||yy>m) continue;
		if(v[xx][yy]) continue;
		if(a[xx][yy]!='1') continue;
		dfs(xx,yy);
	}
}
void solve(){
	cin>>n>>m;
	ans=0;
    memset(v,0,sizeof(v));
    memset(v1,0,sizeof(v));
	string s;
	for(int i=1;i<=n;i++){
		cin>>s;
		for(int j=1;j<=m;j++){
			a[i][j]=s[j-1];
		}
	}
	for(int i=0;i<=m+1;i++){
		a[0][i]='0';
        a[n+1][i]='0';
	}
	for(int i=0;i<=n+1;i++){
		a[i][0]='0';
        a[i][m+1]='0';
	}
	dfs1(0,0);
	for(int i=1;i<=n;i++){
		for(int j=1;j<=m;j++){
			if(a[i][j]=='0') a[i][j]='1';
		}
	}
	for(int i=1;i<=n;i++){
		for(int j=1;j<=m;j++){
			if(a[i][j]=='1'){
				dfs(i,j);
				ans++;
			}
		}
	}
	cout<<ans<<'\n';
}

signed main(){
	ios::sync_with_stdio(false);
	int t=1;
	cin>>t;
	while(t--){
		solve();
	}
	return 0;
}
```

## G 子串简写

------

#### 【问题描述】

**程序猿圈子里正在流行一种很新的简写方法：对于一个字符串，只保留首尾字符，将首尾字符之间的所有字符用这部分的长度代替。例如 internation-alization 简写成 i18n，Kubernetes （注意连字符不是字符串的一部分）简写成 K8s, Lanqiao 简写成 L5o 等。在本题中，我们规定长度大于等于 K 的字符串都可以采用这种简写方法（长度小于 K 的字符串不配使用这种简写）。给定一个字符串 S 和两个字符 c1 和 c2，请你计算 S 有多少个以 c1 开头c2 结尾的子串可以采用这种简写？**

#### **【输入格式】**

**第一行包含一个整数 K。**
**第二行包含一个字符串 S 和两个字符 c1 和 c2。**

#### **【输出格式】**

**一个整数代表答案。**

#### **【样例输入】**

>4
>abababdb a b

#### **【样例输出】**

> 6

#### 【样例说明】

**符合条件的子串如下所示，中括号内是该子串：**

> [abab]abdb
> [ababab]db
> [abababdb]
> ab[abab]db
> ab[ababdb]
> abab[abdb]

#### 【解析】

**前缀和思想，当我们遇到a时，用cnt[i]记录a出现的数量，当遇到b时，此时需要累加答案，此时的b能够匹配的a的数量即为cnt[i-k+1]**

#### 【代码】

```c++
#include <bits/stdc++.h>
using namespace std;
long long cnt[500010];
int main() {
	int k;
	cin >> k;
	string s;
	cin >> s;
	long long ans = 0;
	char a, b;
	cin >> a >> b;
	int len = s.size();
	int t = 0;
	for (int i = 0; i < len; i++) {
		if (s[i] == a) t++;
		cnt[i] = t;
		if (s[i] == b && i >= k - 1) ans += cnt[i - k + 1];
	}
	cout << ans << '\n';
	return 0;
}
```

