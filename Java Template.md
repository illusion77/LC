# Basic DataStructure

- [Basic DataStructure](#basic-datastructure)
  - [String](#string)
  - [StringBuilder](#stringbuilder)
  - [Array](#array)
  - [Collection](#collection)
  - [List](#list)
  - [Stack](#stack)
  - [Queue](#queue)
    - [LinkedList](#linkedlist)
    - [PriorityQueue](#priorityqueue)
  - [Deque](#deque)
  - [Map](#map)
    - [TreeMap](#treemap)
  - [Set](#set)
    - [TreeSet](#treeset)
  - [outer](#outer)
- [格式转换](#格式转换)
- [坑](#坑)
- [二分查找](#二分查找)
  - [API](#api)
  - [入门写法](#入门写法)
  - [lower_bound](#lower_bound)
  - [upper_bound](#upper_bound)
  - [eps<1e-6](#eps1e-6)
- [Stream](#stream)
- [图论](#图论)
  - [并查集（Union Find）](#并查集union-find)
  - [带权二分图最大完美匹配](#带权二分图最大完美匹配)
    - [匈牙利算法（KM算法）](#匈牙利算法km算法)
- [DP](#dp)
  - [01背包](#01背包)
  - [多重背包](#多重背包)
  - [完全背包](#完全背包)
- [数学](#数学)
  - [排序](#排序)
  - [交换](#交换)
  - [极值](#极值)
  - [对数](#对数)
  - [组合数](#组合数)
    - [O(n^2)杨辉三角](#on2杨辉三角)
    - [O(n)公式法](#on公式法)
  - [随机数](#随机数)
  - [几何](#几何)
    - [三角形面积 行列式计算公式](#三角形面积-行列式计算公式)
    - [三角函数](#三角函数)
  - [二进制](#二进制)
  - [日期](#日期)
    - [判断闰年](#判断闰年)
  - [二维差分/前缀和](#二维差分前缀和)
  - [IterablePermutation](#iterablepermutation)
- [字符串](#字符串)
  - [哈希](#哈希)
  - [Trie](#trie)
  - [KMP](#kmp)
  - [后缀数组SA](#后缀数组sa)

## String
```java
String s = "asdefgasdefg";
// indexOf
s.indexOf("s") //retrun 1
s.indexOf("sd") //retrun 1
s.indexof("s",2) //return 7
s.lastIndexOf('s') //return 7
s.lastIndexOf('s',6)//return 1

// String to char 
String s = "abc";
char c = s.charAt(0); // 'a'

String s = s.substring((int)start,(int)end) //[start,end)
String s = s.trim(); 
String s = String.valueOf(object);

// char[] to String
char[] stringArray = { 'H', 'e', 'l', 'l', 'o' };
String s = new String(stringArray);
// String to char[]
for(char x : s.toCharArray())

// join, can be used in list<String> and String[]
String.join(",", list);
String.join(",", arr);
String.join("/", stack); // /abc/cde/ef

Character.isLetterOrDigit(s.charAt(i))
Character.isDigit(char c)
Character.isLowerCase(char c)||Character.isUpperCase(char c)
Character.toLowerCase(s.charAt(i))
Character.toUpperCase(s.charAt(i))
[implementation with bit]
toLower: c|=32
toUpper: c&=-33
exchange: c^=32

// split, split只获取分隔符前面的元素，最后一个分隔符右边如果有元素就拿，没元素就空
String[] ss = s.split("#");
"#,#,#" -> "#","#","#"
",#,#" -> "","#","#"
",#,#," -> "","#","#"
    
// repeat
"U".repeat(x) // 'U' repeat x times

// format
String.format("$%.2f", num); // "$1.23"
String.format("$%02d", num); // when num=3, "$03"

```
## StringBuilder
```java
StringBuilder sb = new StringBuilder("String");
sb.append(""); // int float double String char boolean都可以append
sb.reverse();
sb.indexOf("abc")
sb.delete((int)start,(int)end); //[start,end)
sb.deleteCharAt(int index);	// O(n)
sb.insert((int)offset,"String");
sb.toString();
sb.setCharAt((int)index,(char)c);

String.contians(StringBuilder) // return true or false
```
## Array
```java
String[] a = new String[100];
Arrays.sort(a);
// 与list转换
// List<Integer> 和 int[] 因类型不同不可直接转换
List<String> list = Arrays.asList(a);
String[] b = (String[])list.toArray(new String[size]);
//复制
Arrays.copyOfRange(arr, (int)start, (int)to)//[start,to)
Arrays.copyOf(arr, k); // [0, k)
//填充
Arrays.fill(a,"fill");
Arrays.fill(arr, 0);

// 相等
Arrays.equals(arr, targetArr) // 非嵌套 int[]
Arrays.deepEquals(arr, targetArr) // 嵌套 int[][]...
    
// toString
Arrays.deepToString
```
## Collection
```java
add(Object o);
addAll(Collection c);
clear();
contains(Object o);
remove(Object o);
size();
toArray();
Collections.sort(Collection c);
Collections.reverse(Collection c);
```
## List
```java
List<Object> list = new ArrayList<>();
list.add((int)index,Object o);
list.get((int)index);
list.remove((int)index);
list.indexOf(Object o);
list.subList(int start,int end); [start,end);
list.set(int index, E element);
// 创建时赋值
ans.add(Arrays.asList(i, j));
```
## Stack
```java
Stack<Integer> stack = new Stack<>();
stack.push();
stack.pop(); // 移除并返回
stack.peek(); // 返回

// Stack转二维数组
stack.toArray(new int[0][])
```
## Queue
```java
// LinkedList 和 PriorityQueue 共用
q.offer(Object o); // join in the tail
q.poll(); // return and pop the head
q.peek(); // return the head
```
### LinkedList
```java
// 用作队列
Queue<Object> q = new LinkedList<>();

// 定义为LinkedList时可以使用addLast和addFirst
LinkedList<Object> q = new LinkedList<>();
q.addLast(val);
q.addFirst(val);
```
### PriorityQueue
```java
Queue<Integer> pq = new PriorityQueue<>(); // 默认升序
```
## Deque
```java
Deque<Integer> dq = new ArrayDeque<>();
dq.offerLast(1);
dq.offerFirst(2);
int removedNumber1 = dq.pollLast();
int removedNumber2 = dq.pollFirst();
int lastElement = dq.peekLast();
int firstElement = dq.peekFirst();
```
## Map
```java
Map<String,String> map = new HashMap<>();
map.put("key","value");
map.getOrDefault("key","default");
map.get("key"); //return "value";
map.containsKey("key");
for(int k : map.keySet())
for(int v : map.values())

// putIfAbsent and computeIfAbsent
map.putIfAbsent(k, v); // 没有k的时候，把v放进去，无返回值
map.computeIfAbsent(k, o -> v) // 没有k的时候，把v放进去，返回v或者已存在的值

// 嵌套HashMap
Map<String, HashMap<Integer, Integer>> mp = new HashMap<>();
mp.put("A", new HashMap<>(){{put(1,2);put(3,4);}});
mp.put("B", new HashMap<>(){{put(5,6);put(7,8);}});
mp.forEach((k,v)->{
    v.forEach((k1,v1)->{
        System.out.println(k1 + " " + v1);
    });
});

```
### TreeMap
```java
TreeMap<Integer, Integer> map = new TreeMap<>();
map.firstKey() // 获取第一个
map.lastKey() // 获取最后一个
map.remove(obj) // 删除指定元素
    
// return Integer or null if no exist
map.higherKey(x)    // > x
map.lowerKey(x)     // < x
map.ceilingKey(x)   // >= x
map.floorKey(x)     // <= x
```
## Set
```java
Set<Object> set = new HashSet<>();
```
### TreeSet
```java
TreeSet<Object> set = new TreeSet<>();

set.first()
set.last()
set.pollFirst()
set.pollLast()

// return Integer or null if no exist
set.higher(x) // > x
set.lower(x)  // < x
set.ceiling(x)// >= x
set.floor(x)  // <= x
```
## outer
```java
int ans = 0;
outer:
for(int[] a : artifacts){
    for(int i = a[0];i <= a[2];i++){
        for(int j = a[1];j <= a[3];j++){
            if(!dug[i][j]){
                continue outer; // continue/break
            }
        }
    }
    ans++;
}
```
# 格式转换
```java
// List<Integer> to int[]
ans.stream().mapToInt(o->o).toArray();

// int[] to List<Integer>
Arrays.stream(ans).boxed().collect(Collectors.toList());

// List<int[]> to int[][]
ans.toArray(new int[0][]);

// int[][] to List<int[]>
Arrays.asList(ans);

// char[] to String
new String(ans);

// int[] to String
Arrays.stream(ans).mapToObj(String::valueOf).collect(Collectors.joining());

// List<Character>/List<Integer> to String
ans.stream().map(String::valueOf).collect(Collectors.joining());

```
# 坑

1. 两个Integer之间比较大小，可以用<和>，但不能用==，要用equals。同理所有包装类都要用equals
# 二分查找
## API
```java
Arrays.binarySearch(Object[] a, Object key) // 找到返回i，没找到 在左边 -1，在右边 -(n+1)
```
## 入门写法
```cpp
// find target
int l = 0, r = n-1;
while(l <= r){
    int mid = l+(r-l)/2;
    if (a[mid] == target) return mid;
    if (a[mid] > target) r = mid-1;
    else l = mid+1;
}
```
## lower_bound
```java
// 存在返回[0,n-1], 不存在返回n
public int lower_bound(int[] a, int target) {
    int l = 0, r = a.length;
    while(l < r) {
        int mid = l+(r-l)/2;
        if(a[mid] >= target) r = mid;
        else l = mid+1;
    }
    return l;
}
```
## upper_bound
```java
// 存在返回[0,n-1], 不存在返回n
public int upper_bound(int[] a, int target) {
    int l = 0, r = a.length;
    while(l < r) {
        int mid = l+(r-l)/2;
        if(a[mid] <= target) l = mid+1;
        else r = mid;
    }
    return l;
}

```
## eps<1e-6
```cpp
// 结果返回l
double l = 0, r = n;
while(r-l >= 1e-6){
    double mid = l+(r-l)/2;
    if(check(mid)) l = mid;  //l和r依据题意互换
    else r = mid;
}
return l;
```
# Stream
```java
Arrays.stream(nums).sum();

```
# 图论
## 并查集（Union Find）
```cpp
// TC: 只做了路径压缩，未按秩合并，因此每次Find是O(logn)。做了按秩合并则是一个常数（<5）
int[] f = new int[n+1];

// 普通并查集
// 初始化
for(int i = 1; i <= n; i++) f[i] = i;
public int Find(int x){return f[x]==x ? x : (f[x]=Find(f[x]));}
public void Union(int x, int y){
    x = Find(x); y = Find(y);
    if(x != y) f[y] = x;
}

// 带权并查集
// 初始化f为-1
public int find(int x) {
    return f[x] < 0 ? x : (f[x]=find(f[x]));
}
public boolean union(int x, int y){
    x = find(x); y = find(y);
    if(x != y) {
        f[x] += f[y];
        f[y] = x;
    }
    return x != y;
}
// x节点所在的树有多大：-f[find(x)]
```
[并查集oi-wiki](https://oi-wiki.org/ds/dsu/)
[zerotrac总结](https://leetcode-cn.com/problems/number-of-provinces/solution/jie-zhe-ge-wen-ti-ke-pu-yi-xia-bing-cha-0unne/)
[路径压缩时间为logn](https://www.cnblogs.com/Canopus-wym/p/10376053.html)
## 带权二分图最大完美匹配
### 匈牙利算法（KM算法）
```java
class IntegerKM {
    private static final int INF = Integer.MAX_VALUE / 2;

    private int[][] table = null;     // 权重矩阵（方阵）
    private int[] leftLabel = null;          // X标号值
    private int[] rightLabel = null;          // Y标号值
    private int[] leftPartner = null;      // X点对应的匹配点
    private int[] rightPartner = null;      // Y点对应的匹配点
    private int n;                // 矩阵维度

    public IntegerKM(int[][] table) {
        this.table = table;
        this.n = table.length;
        this.leftLabel = new int[n];
        this.rightLabel = new int[n];
        Arrays.fill(leftLabel, -INF);
        for (int x = 0; x < n; x++) {
            for (int y = 0; y < n; y++) {
                if (table[x][y] > leftLabel[x]) {
                    leftLabel[x] = table[x][y];
                }
            }
        }
        this.leftPartner = new int[n];
        this.rightPartner = new int[n];
        Arrays.fill(leftPartner, -1);
        Arrays.fill(rightPartner, -1);
    }

    public int getLeftPartner(int i) {
        return leftPartner[i];
    }

    public int getRightPartner(int i) {
        return rightPartner[i];
    }

    public int getLeftLabel(int i) {
        return leftLabel[i];
    }

    public int getRightLabel(int i) {
        return rightLabel[i];
    }

    public int solve() { // 入口，输入权重矩阵
        for (int x = 0; x < n; x++) {
            bfs(x);
        }
        int value = 0;
        for (int x = 0; x < n; x++) {
            value += table[x][leftPartner[x]];
        }
        return value;
    }

    private void bfs(int startX) {    // 为一个x点寻找匹配
        boolean find = false;
        int endY = -1;
        int[] yPre = new int[n];      // 标识搜索路径上y点的前一个点
        boolean[] S = new boolean[n], T = new boolean[n]; // S集合，T集合
        int[] slackY = new int[n];    // Y点的松弛变量
        Arrays.fill(yPre, -1);
        Arrays.fill(slackY, INF);
        int[] queue = new int[n];     // 队列
        int qs = 0, qe = 0;           // 队列开始结束索引
        queue[qe++] = startX;
        while (!find) {       // 循环直到找到匹配
            while (qs < qe && !find) {   // 队列不为空
                int x = queue[qs++];
                S[x] = true;
                for (int y = 0; y < n; y++) {
                    if (T[y]) {
                        continue;
                    }
                    int tmp = leftLabel[x] + rightLabel[y] - table[x][y];
                    if (tmp == 0) {  // 相等子树中的边
                        T[y] = true;
                        yPre[y] = x;
                        if (rightPartner[y] == -1) {
                            endY = y;
                            find = true;
                            break;
                        } else {
                            queue[qe++] = rightPartner[y];
                        }
                    } else if (slackY[y] > tmp) { // 不在相等子树中的边，看是否能够更新松弛变量
                        slackY[y] = tmp;
                        yPre[y] = x;
                    }
                }
            }
            if (find) {
                break;
            }
            int a = INF;
            for (int y = 0; y < n; y++) {  // 找到最小的松弛值
                if (!T[y]) {
                    a = Math.min(a, slackY[y]);
                }
            }
            for (int i = 0; i < n; i++) {  // 根据a修改标号值
                if (S[i]) {
                    leftLabel[i] -= a;
                }
                if (T[i]) {
                    rightLabel[i] += a;
                }
            }
            qs = qe = 0;
            for (int y = 0; y < n; y++) {        // 重要！！！控制修改标号之后需要检查的x点
                if (!T[y] && slackY[y] == a) {   // 查看那些y点新加入到T集合，注意，这些y点的前向x点都记录在了yPre里面，所以这些x点不用再次入队
                    T[y] = true;
                    if (rightPartner[y] == -1) {       // 新加入的y点没有匹配，那么就找到可扩路了
                        endY = y;
                        find = true;
                        break;
                    } else {   // 新加入的y点已经有匹配了，将它匹配的x加到队列
                        queue[qe++] = rightPartner[y];
                    }
                }
                slackY[y] -= a;   // 所有松弛值减去a。(对于T集合中的松弛值已经没用了，对于不在T集合里面的y点，
            }                     // 它们的松弛值是通过S集合中的x点求出的，S集合中的x点的标号值在上面都减去了a，所以这里松弛值也要减去a)
        }
        while (endY != -1) {    // 找到可扩路最后的y点后，回溯并扩充
            int preX = yPre[endY], preY = leftPartner[preX];
            leftPartner[preX] = endY;
            rightPartner[endY] = preX;
            endY = preY;
        }
    }
}
```
例题：lc1947
# DP
## 01背包
## 多重背包
## 完全背包

# 数学
## 排序
```java
// int[] a 升序
Arrays.sort(a)
// int[] 降序
a = Arrays.stream(a).boxed().sorted((o1,o2)->o2-o1).mapToInt(o->o).toArray();
// int[][] 按a[0]升序 a:[[2,3],[1,2],[2,5]] 2 5   2 3
Arrays.sort(a, (o1,o2)->o1[0]-o2[0]);
// int[][] 先按a[0], 再按a[1]
Arrays.sort(rect, (a,b)->(a[0]!=b[0] ? a[0]-b[0] : a[1]-b[1]));

// List<Integer> list
Collections.sort(list, (a,b)->(b-a)); // a < b  b-a
// List<int[]> 按a[2]排序
Collections.sort(arr, (a,b)->(a[2]-b[2]));

// PriorityQueue<Integer> 升序
Queue<Integer> pq = new PriorityQueue<>();
// PriorityQueue<Integer> 降序，只用于int
Queue<Integer> pq = new PriorityQueue<>((o1,o2)->(o2-o1));
// 降序，int和double都适用
Queue<Integer> pq = new PriorityQueue<>(Comparator.reverseOrder());

// PriorityQueue<int[]> 按a[0]排序
Queue<int[]> pq = new PriorityQueue<>((o1,o2)->o1[0]-o2[0]);
// PriorityQueue<int[]> 先按a[1]排序，再按a[0]排序
Queue<int[]> pq = new PriorityQueue<>((o1,o2)->(o1[1]!=o2[1] ? o1[1]-o2[1] : o1[0]-o2[0]));

// PriorityQueue<ListNode> 升序
Queue<ListNode> pq = new PriorityQueue<>((o1,o2)->o1.val-o2.val);
// PriorityQueue<ListNode> 降序
Queue<ListNode> pq = new PriorityQueue<>((o1,o2)->o2.val-o1.val);


```
## 交换
```java
int a = 1, b = 2;
a = b + 0*(b=a);
System.out.println(a+" "+b);    // 2 1
a = b + 0*(b=a);
System.out.println(a+" "+b);    // 1 2
```
## 极值
```java
Math.max((int)a,(int)b);
Math.min((int)a,(int)b);

//Float Double Byte Character Short Integer Long
max = Integer.MAX_VALUE; // 2147483647
min = Integer.MIN_VALUE; // -2147483648

// 为了防止最大值做加法，用0x3f3f3f3f更稳，它同样是10^9数量级，比一般数字要大
System.out.println(0x3f3f3f3f); //  1061109567
System.out.println((int)1e9);   //  1000000000
System.out.println(0x7fffffff); //  2147483647
System.out.println(~0x7fffffff);// -2147483648	~操作：+1再*-1

// 数组最小值
int min = Arrays.stream(a).min().getAsInt();
```
## 对数
```java
System.out.println(Math.log(9e8)); // 10为底
System.out.println(Math.log(9e8)/Math.log(2)); // 2为底
```
## 组合数
### O(n^2)杨辉三角
定理1：![](https://cdn.nlark.com/yuque/__latex/5c59f8c6013de3153e22c6d15c439ff7.svg#card=math&code=C_%7Bn%7D%5E%7Bm%7D%20%3D%20C_%7Bn%7D%5E%7Bn-m%7D&id=jLlql) 
定理2：由定理1推得 ![](https://cdn.nlark.com/yuque/__latex/5c79ffd065a76bb21b633effaa744d24.svg#card=math&code=C_%7Bn%7D%5E%7Bm%7D%20%3D%20C_%7Bn-1%7D%5E%7Bm-1%7D%20%2B%20C_%7Bn-1%7D%5E%7Bm%7D&id=zmuHy) 即上一轮中选到的是或不是m中的一个，便会产生的两种情况
定理3：![](https://cdn.nlark.com/yuque/__latex/2c1446df643bd976fab2f690bbe32f35.svg#card=math&code=C_%7Bn%7D%5E%7B0%7D%20%2B%20C_%7Bn%7D%5E%7B1%7D%20%2B%20C_%7Bn%7D%5E%7B2%7D%20%2B%20...%20%2BC_%7Bn%7D%5E%7Bn%7D%20%3D%202%5En&id=oLSlA)
```java
// f[i][j]代表从i个元素取j个
int n = 100;
int[][] f = new int[n + 1][n + 1];
f[0][0] = f[1][0] = f[1][1] = 1;
for (int i = 2; i <= n; i++) {
    f[i][0] = 1;
    for (int j = 1; j <= i; j++) {
        f[i][j] = f[i - 1][j - 1] + f[i - 1][j];
    }
}
```
### O(n)公式法
定理4：![](https://cdn.nlark.com/yuque/__latex/e00e384875916d22e07fbe5bd3e3bde1.svg#card=math&code=C_%7Bn%7D%5E%7Bm%7D%20%3D%20%5Cfrac%7Bn%21%7D%7Bm%21%2A%28n-m%29%21%7D%20%3D%20%5Cfrac%7Bn%2A%28n-1%29%2A%28n-2%29%2A...%2A%28n-%28m-1%29%29%7D%7Bm%21%7D&id=Vtj9f)（常用）
```java
// 按每一对分子和分母，拆开来先除好，避免溢出
// 计算Cnm：
long ans = 1;
for (int x = n, y = 1; y <= m; x--, y++) {
    ans = ans * x / y;
}
return (int)ans;

// 可能溢出long
int n = 6, m = 2;
long a = 1, b = 1;
for(int i = 0; i < m; i++) {
    a *= n-i;
    b *= i+1;
}
return (int)(a/b);
```
[参考链接](https://blog.csdn.net/Shenpibaipao/article/details/109608970?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1.no_search_link&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1.no_search_link)
## 随机数
```java
Random random = new Random();
int x = random.nextInt(n); // generate x in [0, n)
```
## 几何
### [三角形面积 行列式计算公式](https://www.bilibili.com/video/BV183411r7Zd/?spm_id_from=333.788.recommend_more_video.-1&vd_source=249ace3c47f456b1ad193f62bea119c3)
```java
double area = 0.5*Math.abs(p1[0]*p2[1]-p2[0]*p1[1]+
              p2[0]*p3[1]-p3[0]*p2[1] + p3[0]*p1[1]-p1[0]*p3[1]);
// x1 y1  x2 y2  x3 y3
// x2 y2  x3 y3  x1 y1

```
### 三角函数
```java
point(x, y)
【弧度制】Double a = Math.atan2(y, x);
【角度制】Double b = Math.atan2(y, x)*180/Math.PI
```
## 二进制
```java
// int num 转 unsigned long n
// int改成无符号可能会溢出int，所以需要用long接住
long n = Integer.toUnsignedLong(num);
```
## 日期
### 判断闰年
```java
闰年比平年多1天。闰年判断 if(year%400 == 0 || (year%4 == 0 && year%100 != 0))
```
## 二维差分/前缀和
```java
// 差分数组g
// 标记
int[][] g = new int[n+2][n+2];
for (int[] x : a) {
    int x1=x[0]+1, y1=x[1]+1, x2=x[2]+1, y2=x[3]+1;
    g[x1][y1]++;
    g[x2+1][y2+1]++;
    g[x2+1][y1]--;
    g[x1][y2+1]--;
}
// 生成
g[i][j] = g[i][j]+g[i-1][j]+g[i][j-1]-g[i-1][j-1];

// 前缀和
// 累加
g[i][j] = g[i][j]+g[i-1][j]+g[i][j-1]-g[i-1][j-1];
// 获取
area = g[i][j]-g[i-1][j]-g[i][j-1]+g[i-1][j-1];
```
## IterablePermutation
```java
public class IterablePermutation implements Iterable<int[]>, Iterator<int[]> {
    int[] a;
    boolean first = true;

    public IterablePermutation(int n) {
        assert n >= 1;
        a = new int[n];
        for(int i = 0;i < n;i++)a[i] = i;
    }

    public IterablePermutation(int... a) {
        this.a = Arrays.copyOf(a, a.length);
    }

    @Override
    public boolean hasNext() {
        if(first)return true;
        int n = a.length;
        int i;
        for(i = n - 2;i >= 0 && a[i] >= a[i+1];i--);
        return i != -1;
    }

    @Override
    public int[] next() {
        if(first) {
            first = false;
            return a;
        }
        int n = a.length;
        int i;
        for(i = n - 2;i >= 0 && a[i] >= a[i+1];i--);
        assert i != -1;
        int j;
        for(j = i + 1;j < n && a[i] < a[j];j++);
        int d = a[i]; a[i] = a[j - 1]; a[j - 1] = d;
        for(int p = i + 1, q = n - 1;p < q;p++,q--){
            d = a[p]; a[p] = a[q]; a[q] = d;
        }
        return a;
    }

    @Override
    public Iterator<int[]> iterator() {
        return this;
    }
}
```
# 字符串
## 哈希
```java
long[] h = new long[n+1], p = new long[n+1];
long base = 131; // 13131
p[0] = 1;
for(int i = 1; i <= n; i++){
    h[i] = h[i-1]*base + s.charAt(i-1);
    p[i] = p[i-1]*base;
}

get [i, j] (1-indexed): h[j]-h[i-1]*p[j-i+1]
```

## Trie
```java
class Trie {
    
    class Node {
        Map<Character, Node> child = new HashMap<>();
        boolean isWord;
        // String word;
    }
    
    Node root = new Node();

    public Trie() {

    }
    
    public void insert(String word) {
        Node cur = root;
        for(char c : word.toCharArray()) {
            cur = cur.child.computeIfAbsent(c, o->new Node());
        }
        cur.isWord = true;
        // word = cur;
    }
    
    public boolean search(String word) {
        Node cur = root;
        for(char c : word.toCharArray()) {
            if(!cur.child.containsKey(c)) return false;
            cur = cur.child.get(c);
        }
        return cur.isWord;
    }
    
    public boolean startsWith(String prefix) {
        Node cur = root;
        for(char c : prefix.toCharArray()) {
            if(!cur.child.containsKey(c)) return false;
            cur = cur.child.get(c);
        }
        return true;
    }
}
```
## KMP
```java
// O(n+m)
public static void Match(String s, int[] match) {
    int i;
    int m = s.length();
    match[0] = -1;
    for(int j = 1; j < m; j++) {
        i = match[j-1];
        while(i >= 0 && s.charAt(i+1) != s.charAt(j)) {
            i = match[i];
        }
        if(s.charAt(i+1) == s.charAt(j)) {
            match[j] = i+1;
        } else {
            match[j] = -1;
        }
    }
}

public static int KMP(String a, String b) {
    int n = a.length(), m = b.length();
    if(n < m) return -1;
    int[] match = new int[m];
    Match(b, match);
    int i = 0, j = 0;
    while(i < n && j < m) {
        if(a.charAt(i) == b.charAt(j)) {
            i++;
            j++;
        } else if(j > 0) {
            j = match[j-1]+1;
        } else {
            i++;
        }
    }
    return j == m ? i - m : -1;
}
```
[参考链接](https://www.icourse163.org/learn/ZJU-93001?tid=1450069451#/learn/content?type=detail&id=1214143659&cid=1217772610&replay=true)
## 后缀数组SA
生成的后缀数组sa可以使得 s[sa[i-1]:] < s[sa[i]:]，即后缀字符串按字典序排列后的起点数组
```java
private static final int SIZE = 100005;	// length of String

private static int[] SA(String s) {
    char[] ch = s.toCharArray();
    int i, p, step, m = SIZE, len = ch.length;
    int[] sa = new int[len],x = new int[len+1],y = new int[len+1],wv = new int[len],ws = new int[SIZE],t;

    for (i = 0 ; i < m ; i ++) ws[i] = 0;
    for (i = 0; i < len; i++) ws[x[i] = ch[i]]++;
    for (i = 1; i < m; i++) ws[i] += ws[i-1];
    for (i = len-1; i >= 0; i--) sa[--ws[ch[i]]] = i;

    for (step = 1,p = 0; p < len && step <= len ; step *= 2,m = p) {
        for (p = 0,i = len - step; i < len; i++) y[p++] = i;
        for (i = 0; i < len; i++)
            if (sa[i] >= step) y[p++] = sa[i] - step;

        for (i = 0; i < len; i++) wv[i] = x[y[i]];
        for (i = 0 ; i < m ; i++) ws[i] = 0;
        for (i = 0; i < len; i++) ws[wv[i]]++;
        for (i = 1; i < m; i++) ws[i] += ws[i-1];
        for (i = len - 1; i >= 0; i--) sa[--ws[wv[i]]] = y[i];

        for (t = x,x = y,y = t,i = 1,y[len] = -1,x[sa[0]] = 0,p = 1; i < len; i++)
            x[sa[i]] = (y[sa[i]] == y[sa[i-1]] && y[sa[i]+step] == y[sa[i-1]+step]) ? p-1 : p++;
    }
    return sa;
}
```
例题：lc1163
