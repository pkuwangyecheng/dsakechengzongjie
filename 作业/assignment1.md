# Assignment #1: 拉齐大家Python水平

Updated 0940 GMT+8 Feb 19, 2024

2023 fall, Complied by王业成 生命科学学院



**说明：**

1）数算课程的先修课是计概，由于计概学习中可能使用了不同的编程语言，而数算课程要求Python语言，因此第一周作业练习Python编程。如果有同学坚持使用C/C++，也可以，但是建议也要会Python语言。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知3月1日导入选课名单后启用。**作业写好后，保留在自己手中，待3月1日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：Windows 11 家庭中文版 22631.3007

Python编程环境：Spyder IDE 5.2.2, PyCharm 2023.1.4 (Professional Edition)

C/C++编程环境：Mac terminal vi (version 9.0.1424), g++/gcc (Apple clang version 14.0.3, clang-1403.0.22.14.1)



## 1. 题目

### 20742: 泰波拿契數

http://cs101.openjudge.cn/practice/20742/



思路：因为时间和空间限制比较宽松，所以采取打表的方式直接输出



##### 代码

```python
# 
n=int(input())
lst=list(range(31))
lst[0]=0
lst[1]=1
lst[2]=1
for i in range(3,31):
    lst[i]=lst[i-1]+lst[i-2]+lst[i-3]
print(lst[n])
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240223194504831](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240223194504831.png)



### 58A. Chat room

greedy/strings, 1000, http://codeforces.com/problemset/problem/58/A



思路：从输入的字符串中逐个寻找目标字符



##### 代码

```python
# a="hello"
s=input()
i=0
for b in s:
    if b==a[i]:
        i+=1
        if i==5:
            print("YES")
            break
if i!=5:
    print("NO")

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240223203410024](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240223203410024.png)



### 118A. String Task

implementation/strings, 1000, http://codeforces.com/problemset/problem/118/A



思路：起初试图通过删除的方法做，结果被浅拷贝小小折磨了一下，后来换了种思路很快搞定



##### 代码

```python
# s=input()
a=list(s.lower())
c=[]
for i in range(0,len(a)):
    if a[i] not in ["a","e","i","o","u","y"]:
        c.append(a[i])
b=".".join(c)
b="."+b
print(b)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240223210139072](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240223210139072.png)



### 22359: Goldbach Conjecture

http://cs101.openjudge.cn/practice/22359/



思路：



##### 代码

```python
# import math
def sushu(n):
    for i in range(2,math.ceil(math.sqrt(n))):
        if n%i==0:
            return False
    return True
n=int(input())
for i in range(2,n//2+2):
    if sushu(i) and sushu(n-i):
        print(f"{i} {n-i}")
        break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240223210819057](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240223210819057.png)



### 23563: 多项式时间复杂度

http://cs101.openjudge.cn/practice/23563/



思路：遍历找次方号



##### 代码

```python
# s=input()
a=0
b=''
for i in range(0,len(s)):
    if s[i]=="^":
        j = i + 1
        while j < len(s) and s[j].isdigit():
            b += s[j]
            j += 1
        if int(b) > a:
            if  s[i-2]=="0" and s[i-3]=="+":
                c=1
            else:
                a = int(b)
        b = ""
if a==0:
    if "n" in s:
        a=1
print(f"n^{a}")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240223212718427](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240223212718427.png)



### 24684: 直播计票

http://cs101.openjudge.cn/practice/24684/



思路：用集合找出不同元素，再找最大值



##### 代码

```python
# 
lst=list(map(int,input().split()))
a=set(lst)
b={}
lst1=[]
for i in a:
    b[i]=lst.count(i)
c=max(b.values())
for i,j in b.items():
    if j==c:
        lst1.append(i)
lst1.sort()
lst1=map(str,lst1)
print(" ".join(lst1))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240223221108563](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240223221108563.png)



## 2. 学习总结和收获

感觉计概的一些语法和思路忘得有点多，后续得持续更进



