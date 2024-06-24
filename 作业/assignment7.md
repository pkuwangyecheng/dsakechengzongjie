# Assignment #7: April 月考

Updated 1557 GMT+8 Apr 3, 2024

2024 spring, Complied by 王业成 生命科学学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：Windows 11 家庭中文版 22631.3296

Python编程环境：Spyder IDE 5.2.2, PyCharm 2023.1.4 (Professional Edition)

C/C++编程环境：Mac terminal vi (version 9.0.1424), g++/gcc (Apple clang version 14.0.3, clang-1403.0.22.14.1)



## 1. 题目

### 27706: 逐词倒放

http://cs101.openjudge.cn/practice/27706/



思路：



代码

```python
# n=list(map(str,input().split(" ")))
print(" ".join(n[::-1]))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240408163058553](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240408163058553.png)



### 27951: 机器翻译

http://cs101.openjudge.cn/practice/27951/



思路：



代码

```python
from collections import deque
n,m=map(int,input().split())
neicun=deque()
lst=list(map(int,input().split()))
count=0
for i in lst:
    if i in neicun:
        continue
    else:
        count+=1
        neicun.append(i)
        if len(neicun)>n:
            neicun.popleft()
print(count)# 

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240408163843049](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240408163843049.png)



### 27932: Less or Equal

http://cs101.openjudge.cn/practice/27932/



思路：



代码

```python
# n,k=map(int,input().split())
lst=list(map(int,input().split()))
lst.sort()
if k==0 and lst[0]>1:
    print(lst[0]-1)
elif k==0 and lst[0]==1:
    print(-1)
elif k==n:
    print(lst[n-1])
else:
    if lst[k-1]==lst[k]:
        print(-1)
    else:
        print(lst[k-1])

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240408165203447](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240408165203447.png)



### 27948: FBI树

http://cs101.openjudge.cn/practice/27948/



思路：



代码

```python
# def zhuanhuan(lst):
    if "0" in lst and "1" in lst:
        return "F"
    elif "0" in lst and "1" not in lst:
        return "B"
    else:
        return "I"
class Treenode():
    def __init__(self,value):
        self.left=None
        self.right=None
        self.value=value
def buildtree(lst):
    rot=zhuanhuan(lst)
    root=Treenode(rot)
    if len(lst)>=2:
        root.left=buildtree(lst[:len(lst)//2])
        root.right=buildtree(lst[len(lst)//2:])
    return root
def postorder(root):
    output=[]
    if root:
        output.extend(postorder(root.left))
        output.extend(postorder(root.right))
        output.append(root.value)
    return output
n=int(input())
lst=input()
root=buildtree(lst)
output=postorder(root)
print("".join(map(str,output)))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240408171555279](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240408171555279.png)



### 27925: 小组队列

http://cs101.openjudge.cn/practice/27925/



思路：可以将整个队列分为若干个小组队列，队列中只有小组队列的代表元素，要输出的时候找到代表元素，然后从其对应的小组队列中输出



代码

```python
# from collections import deque
n=int(input())
groups={}
group_member={}
for i in range(n):
    members=list(map(int,input().split()))
    representation=members[0]
    groups[representation]=deque()
    for j in members:
        group_member[j]=representation
queue=deque()
while True:
    order=list(input().split())
    if order[0]=="STOP":
        break
    elif order[0]=="ENQUEUE":
        person=int(order[1])
        group=group_member.get(person)
        if group is None:
            group=person
            groups[person]=deque([person])
            group_member[person]=person
        else:
            groups[group].append(person)
        if group not in queue:
            queue.append(group)
    elif order[0] == 'DEQUEUE':
        if queue:
            group = queue[0]
            x = groups[group].popleft()
            print(x)
            if not groups[group]:
                queue.popleft()

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240408175338652](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240408175338652.png)



### 27928: 遍历树

http://cs101.openjudge.cn/practice/27928/



思路：



代码

```python
# class Treenode():
    def __init__(self,value):
        self.value=value
        self.children=[]
n=int(input())
node=[]
child=[]
for _ in range(n):
    lst=list(map(int,input().split()))
    root=Treenode(lst[0])
    if len(lst)>1:
        root.children=lst[1:]
        child.extend(lst[1:])
    node.append(root)
for i in node:
    if i.value not in child:
        root=i
def parsetree(root):
    lst=root.children
    lst.append(root.value)
    if len(lst)==1:
        print(root.value)
    else:
        lst.sort()
        for i in lst:
            for j in node:
                if j.value==i and j.value!=root.value:
                    parsetree(j)
                    break
                elif j.value==i and j.value==root.value:
                    print(root.value)
    return
parsetree(root)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240408215449691](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240408215449691.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

感觉月考题目难度比上周小很多，花费约一个多小时把，这周期末周比较忙，后续再继续跟进数算课程的学习



