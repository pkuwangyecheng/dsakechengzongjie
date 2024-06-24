# Assignment #4: 排序、栈、队列和树

Updated 0005 GMT+8 March 11, 2024

2024 spring, Complied by 王业成 生命科学学院



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:

Learn about Time complexities, learn the basics of individual Data Structures, learn the basics of Algorithms, and practice Problems.

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：Windows 11 家庭中文版 22631.3235

Python编程环境：Spyder IDE 5.2.2, PyCharm 2023.1.4 (Professional Edition)

C/C++编程环境：Mac terminal vi (version 9.0.1424), g++/gcc (Apple clang version 14.0.3, clang-1403.0.22.14.1)



## 1. 题目

### 05902: 双端队列

http://cs101.openjudge.cn/practice/05902/



思路：直接使用collections库里的deque函数进行求解



代码

```python
# from collections import deque
for _ in range(int(input())):
    a=deque()
    for _ in range(int(input())):
        b=list(map(int,input().split()))
        if b[0]==1:
            a.append(b[1])
        else:
            if b[1]==0:
                a.popleft()
            else:
                a.pop()
    if a:
        print(" ".join(map(str,a)))
    else:
        print("NULL")

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240317232434505](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240317232434505.png)



### 02694: 波兰表达式

http://cs101.openjudge.cn/practice/02694/



思路：利用栈从后往前遍历数据进行处理



代码

```python
s=list(input().split(" "))
yunsuan="+-*/"
stack=[]
for i in s[::-1]:
    if i not in yunsuan:
        stack.append(float(i))
    else:
        a = float(stack.pop())
        b = float(stack.pop())
        if i == "+":
            stack.append(a + b)
        elif i == "-":
            stack.append(a - b)
        elif i == "*":
            stack.append(b * a)
        elif i == "/":
            stack.append(a / b)
print(f"{stack[0]:.6f}")# 

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240318000358376](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240318000358376.png)



### 24591: 中序表达式转后序表达式

http://cs101.openjudge.cn/practice/24591/



思路：利用调度场算法进行处理



代码

```python
# for _ in range(int(input())):
    dict={"+":1,"-":1,"*":2,"/":2}
    stack=[]
    output=[]
    num=""
    for i in input():
        if i.isnumeric() or i==".":
            num+=i
        else:
            if num:
                output.append(float(num) if "." in num else int(num))
                num=""
            if i in "+-*/":
                while stack and stack[-1] in "+-*/" and dict[i]<=dict[stack[-1]]:
                    output.append(stack.pop())
                stack.append(i)
            elif i =="(":
                stack.append(i)
            elif i==")":
                while stack and stack[-1]!="(":
                    output.append(stack.pop())
                stack.pop()
    if num:
        output.append(float(num) if "." in num else int(num))
    while stack:
        output.append(stack.pop())
    print(" ".join(map(str,output)))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240318150855386](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240318150855386.png)



### 22068: 合法出栈序列

http://cs101.openjudge.cn/practice/22068/



思路：通过栈模拟操作过程



代码

```python
# s=input()
while True:
    try:
        a=input()
    except EOFError:
        break
    if len(a)!=len(s):
        print("NO")
        continue
    else:
        k=0
        b=0
        stack=[]
        for i in a:
            if stack and stack[-1]==i:
                stack.pop()
            else:
                while k<len(s) and s[k]!=i:
                    stack.append(s[k])
                    k+=1
                if k==len(s):
                    print("NO")
                    b+=1
                    break
                k+=1
        if stack and b==0:
            print("NO")
            continue
        if not stack and b==0:
            print("YES")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240318150944990](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240318150944990.png)



### 06646: 二叉树的深度

http://cs101.openjudge.cn/practice/06646/



思路：建树处理



代码

```python
# class Treenode:
    def __init__(self):
        self.left=None
        self.right=None
    def depth(self,node):
        if node is None:
            return 0
        else:
            return max(self.depth(node.left),self.depth(node.right))+1
n=int(input())
nodes=[Treenode() for _ in range(n)]
for i in range(n):
    left,right=map(int,input().split())
    if left!=-1:
        nodes[i].left=nodes[left-1]
    if right!=-1:
        nodes[i].right=nodes[right-1]
root=nodes[0]
a=root.depth(root)
print(a)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240318151039129](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240318151039129.png)



### 02299: Ultra-QuickSort

http://cs101.openjudge.cn/practice/02299/



思路：进行归并排序



代码

```python
# def merge_sort(lst):
    if len(lst)<=1:
        return lst,0
    else:
        middle=len(lst)//2
        left,count_left=merge_sort(lst[:middle])
        right,count_right=merge_sort(lst[middle:])
        merged,count_merge=merge(left,right)
        return merged,count_left+count_right+count_merge
def merge(left,right):
    merged=[]
    count_merge=0
    i,j=0,0
    while i<len(left) and j <len(right):
        if left[i]<=right[j]:
            merged.append(left[i])
            i+=1
        else:
            merged.append(right[j])
            j+=1
            count_merge+=len(left)-i
    merged+=left[i:]
    merged+=right[j:]
    return merged,count_merge
while True:
    n=int(input())
    if n==0:
        break
    else:
        lst=[]
        for _ in range(n):
            lst.append(int(input()))
        b,a=merge_sort(lst)
        print(a)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240318153730699](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240318153730699.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

本周作业感觉难度明显上来了，除了1，2，4完全自己搞定外，后面四题都参考了群佬们的思路或者课件。其中第三题认真学习并理解了调度场算法，二叉树的深度参考了课件，在自己理解，也算第一次写树这种代码，感觉好多细节还不甚熟悉，还需再后面的练习中巩固。第六题调了好久仍然超时，后来看群才发现得用归并（悲）。本周做作业就花了整整一天，每日选做拉下了好多，争取后半学期实验课结束再来慢慢补上吧。



