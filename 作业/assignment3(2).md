# Assignment #3: March月考

Updated 1537 GMT+8 March 6, 2024

2024 spring, Complied by王业成 生命科学学院



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:
- Learn about Time and Space complexities
- Learn the basics of individual Data Structures
- Learn the basics of Algorithms
- Practice Problems on DSA

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：Windows 11 家庭中文版 22631.3235

Python编程环境：Spyder IDE 5.2.2, PyCharm 2023.1.4 (Professional Edition)

C/C++编程环境：Mac terminal vi (version 9.0.1424), g++/gcc (Apple clang version 14.0.3, clang-1403.0.22.14.1)



## 1. 题目

**02945: 拦截导弹**

http://cs101.openjudge.cn/practice/02945/



思路：找出最长递减子序列的长度，注意输出max（dp），而不是dp【-1】



##### 代码

```python
# n=int(input())
lst=list(map(int,input().split()))
def dao_que(lst):
    dp=[1 for i in range(len(lst))]
    for i in range(n):
        for j in range(i):
            if lst[j]>=lst[i]:
                dp[i]=max(dp[j]+1,dp[i])
    return max(dp)
print(dao_que(lst))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240310225341403](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240310225341403.png)



**04147:汉诺塔问题(Tower of Hanoi)**

http://cs101.openjudge.cn/practice/04147



思路：递归



##### 代码

```python
# lst=list(input().split())
n=int(lst[0])
a,b,c=lst[1],lst[2],lst[3]
def ta_que(n,start,by,to):
    if n==1:
        print(f"{n}:{start}->{to}")
    else:
        ta_que(n-1,start,to,by)
        print(f"{n}:{start}->{to}")
        ta_que(n-1,by,start,to)
ta_que(n,a,b,c)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240310231952282](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240310231952282.png)



**03253: 约瑟夫问题No.2**

http://cs101.openjudge.cn/practice/03253



思路：直接数学计算序号



##### 代码

```python
# while True:
    n,p,m=map(int,input().split())
    if n==m==p==0:
        break
    else:
       lst=[i for i in range(1,n+1)]
       lstoutput=[]
       length=n
       a=(p-1+m)%n-1
       lstoutput.append(lst[a])
       while length>1:
           lst.remove(lst[a])
           length-=1
           a=(a-1+m)%length
           lstoutput.append(lst[a])
       if lst[0]not in lstoutput:
           lstoutput.append(lst[0])
    print(",".join(map(str,lstoutput)))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240311001653960](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240311001653960.png)



**21554:排队做实验 (greedy)v0.2**

http://cs101.openjudge.cn/practice/21554



思路：通过字典储存每个人的时间顺序，再进行排序



##### 代码

```python
# n=int(input())
lst=list(map(int,input().split()))
dic={}
for i in range(1,n+1):
    dic[i]=lst[i-1]
lst1=sorted(dic.items(),key=lambda x:(x[1],x[0]))
lst2=[i[0] for i in lst1]
sum=0
for i in range(n):
    sum+=lst1[i][1]*(n-1-i)
print(" ".join(map(str,lst2)))
a=sum/n
print(f"{a:.2f}")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240311110326792](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240311110326792.png)



**19963:买学区房**

http://cs101.openjudge.cn/practice/19963



思路：排序找中位数，依次比较输出



##### 代码

```python
# n=int(input())
juli1=[eval(x)[0]+eval(x)[1] for x in input().split()]
jiage=list(map(int,input().split()))
xingjiabi=[]
for i in range(n):
    a=int(juli1[i])/int(jiage[i])
    xingjiabi.append(a)
dic={}
for i in range(n):
    dic[i]=(xingjiabi[i],jiage[i])
xingjiabi.sort()
jiage.sort()
if n%2==1:
    c=xingjiabi[int((n-1)/2)]
    b=jiage[int((n-1)/2)]
else:
    c=(xingjiabi[n//2]+xingjiabi[n//2-1])/2
    b=(int(jiage[n//2])+int(jiage[n//2-1]))/2
sum=0
for i in range(n):
    if dic[i][0]>c and dic[i][1]<b:
        sum+=1
print(sum)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240311113405855](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240311113405855.png)



**27300: 模型整理**

http://cs101.openjudge.cn/practice/27300



思路：用字典储存排序



##### 代码

```python
# from collections import defaultdict
n=int(input())
dic=defaultdict(list)
for _ in range(n):
    name,s=input().split("-")
    if s[-1]=="M":
        dic[name].append((s,float(s[:-1])))
    else:
        dic[name].append((s,float(s[:-1])*1000))
dic1=sorted(dic)
for i in dic1:
    a = sorted(dic[i],key=lambda x: x[1])
    value = ', '.join([i[0] for i in a])
    print(f'{i}: {value}')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240311122712235](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240311122712235.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

本周作业感觉难度挺大的，不过也学到了许多东西，自己也花时间自学了dp，后续也会自己找一些dp的题目练练熟悉一下，也重新回顾了一下汉诺塔的写法和约瑟夫的相关写法，也更熟练的使用一些字典的操作和collections库里的一些函数，最后的模型整理跟题解写的几乎一样，也是小有成就感，也算收获颇丰把。



