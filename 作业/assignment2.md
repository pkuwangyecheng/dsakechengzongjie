# Assignment #2: 编程练习

Updated 0953 GMT+8 Feb 24, 2024

2024 spring, Complied by 王业成 生命科学学院



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:
- Learn about Time and Space complexities
- Learn the basics of individual Data Structures
- Learn the basics of Algorithms
- Practice Problems on DSA

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知3月1日导入选课名单后启用。**作业写好后，保留在自己手中，待3月1日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：Windows 11 家庭中文版 22631.3155

Python编程环境：Spyder IDE 5.2.2, PyCharm 2023.1.4 (Professional Edition)

C/C++编程环境：Mac terminal vi (version 9.0.1424), g++/gcc (Apple clang version 14.0.3, clang-1403.0.22.14.1)



## 1. 题目

### 27653: Fraction类

http://cs101.openjudge.cn/2024sp_routine/27653/



思路：定义分数类，直接计算所得结果分数的分子与分母，并通过找最大公约数的方法对结果进行化简



##### 代码

```python
# class Fraction:
    def __init__(self,a,b,c,d):
        self.a=a
        self.b=b
        self.c=c
        self.d=d

    def add(self):
        self.e=self.a*self.d+self.b*self.c
        self.f=self.b*self.d
        shu = self.gongyueshu(self.f,self.e)
        self.e = self.e // shu
        self.f = self.f // shu
        return f"{self.e}/{self.f}"
    def gongyueshu(self,a,b):
        while b!= 0:
            a,b=b,a%b
        return a
n=list(map(int,input().split()))
fraction=Fraction(n[0],n[1],n[2],n[3])
print(fraction.add())

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240303215626089](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240303215626089.png)



### 04110: 圣诞老人的礼物-Santa Clau’s Gifts

greedy/dp, http://cs101.openjudge.cn/practice/04110



思路：利用元组储存每组数据，并用比值排序，比较输出最大值



##### 代码

```python
# n,m=map(int,input().split())
lst=[]
num=0
for i in range(n):
    a,b=map(int,input().split())
    c=(a,b)
    lst.append(c)
lst.sort(key=lambda x:x[1]/x[0])
for i in lst:
    if i[1]<=m:
        m-=i[1]
        num+=i[0]
    else:
        num+=i[0]*m/i[1]
        break
print(f"{num:.1f}")

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240303222302609](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240303222302609.png)



### 18182: 打怪兽

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/



思路：将所有时间和技能做成列表并进行排序，一个一个进行比较，注意时间num不是从零开始，而且最后num应该直接等于i，而不是简单加1，不然会跳数据



##### 代码

```python
# s=int(input())
for _ in range(s):
    n,m,b=map(int,input().split())
    lst=[]
    for _ in range(n):
        a,d=map(int,input().split())
        c=(a,d)
        lst.append(c)
    lst.sort(key=lambda x:(x[0],-x[1]))
    num=lst[0][0]
    e=1
    for i,j in lst:
        if i==num and e<=m:
            b-=j
            e+=1
            if b<=0:
                print(num)
                break
        elif i!=num:
            num =i
            e = 2
            b -= j
            if b <= 0:
                print(num)
                break
    if b>0:
        print("alive")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240303234000902](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240303234000902.png)



### 230B. T-primes

binary search/implementation/math/number theory, 1300, http://codeforces.com/problemset/problem/230/B



思路：即找质数的平方数，利用欧拉筛法



##### 代码

```python
n=100000
lst=[1]*1000000
a=set()
for i in range(2,n):
    if lst[i]:
        a.add(i*i)
        for j in range(i*i,n,i):
            lst[j]=0
n=int(input())
lst1=list(map(int,input().split()))
for i in lst1:
    print("YES" if i in a else"NO")# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240304114252664](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240304114252664.png)



### 1364A. XXXXX

brute force/data structures/number theory/two pointers, 1200, https://codeforces.com/problemset/problem/1364/A



思路：通过左右双指针定一移一找数组，注意不要在循环里用sum



##### 代码

```python
# s=int(input())
for _ in range(s):
    n,x=map(int,input().split())
    lst=list(map(int,input().split()))
    a=0
    c=sum(lst)
    d=c
    if c%x!=0:
        print(len(lst))
        continue
    for left in range(1,len(lst)):
        c-=lst[left-1]
        if c%x!=0:
            a=len(lst)-left
            break
    for right in range(len(lst)-1,0,-1):
        d-=lst[right]
        if d%x!=0:
            b=right
            if b>a:
                a=b
                break
    if a==0:
        print(-1)
    else:
        print(a)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240304121555173](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240304121555173.png)



### 18176: 2050年成绩计算

http://cs101.openjudge.cn/practice/18176/



思路：通过埃氏筛法找出所有符合条件的数进行计算



##### 代码

```python
# n=10000
lst=[1]*10000
a=set()
for i in range(2,n):
    if lst[i]:
        a.add(i*i)
        for j in range(i*i,n,i):
            lst[j]=0
m,n=map(int,input().split())
for _ in range(m):
    lst=list(map(int,input().split()))
    lst1=[x for x in lst if x in a]
    if len(lst1)==0:
        print(0)
    else:
        print(f"{sum(lst1)/len(lst):.2f}")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240304123243330](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240304123243330.png)



## 2. 学习总结和收获

本周作业花费时间较长，主要被时间复杂度卡的比较难受，之前计概对被卡时间恶心的时候不多，这次算是真正的见识到了，也学得到了一些优化算法和优化时间的方法，以后要尽可能改掉一些时间复杂度高的代码习惯了



