# Assignment #5: "树"算：概念、表示、解析、遍历

Updated 2124 GMT+8 March 17, 2024

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

### 27638: 求二叉树的高度和叶子数目

http://cs101.openjudge.cn/practice/27638/



思路：建树模拟



代码

```python
# class Treenode:
    def __init__(self):
        self.left=None
        self.right=None
    def tree_height(self,node):
        if node is None:
            return -1
        else:
            return max(self.tree_height(node.left),self.tree_height(node.right))+1
    def numleaf(self,node):
        if node is None:
            return 0
        if node.left is None and node.right is None:
            return 1
        return self.numleaf(node.left)+self.numleaf(node.right)
n=int(input())
nodes=[Treenode()for _ in range(n)]
has_parent=[False]*n
for i in range(n):
    a,b=map(int,input().split())
    if a!=-1:
        nodes[i].left=nodes[a]
        has_parent[a]=[True]
    if b!=-1:
        nodes[i].right=nodes[b]
        has_parent[b]=[True]
index=has_parent.index(False)
root=nodes[index]
c=Treenode()
height=c.tree_height(root)
cunt=c.numleaf(root)
print(f"{height} {cunt}")

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240325151002944](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240325151002944.png)



### 24729: 括号嵌套树

http://cs101.openjudge.cn/practice/24729/



思路：建树模拟操作过程



代码

```python
# class Treenode:
    def __init__(self,value):
        self.value=value
        self.children=[]
def parse_Tree(s):
    stack=[]
    node=None
    for i in s:
        if i.isalpha():
            node=Treenode(i)
            if stack:
                stack[-1].children.append(node)
        elif i=="(":
            if node:
                stack.append(node)
                node=None
        elif i==")":
            if stack:
                node=stack.pop()
    return node
def qianorder(node):
    output=[node.value]
    for child in node.children:
        output.extend(qianorder(child))
    return "".join(output)
def houorder(node):
    output=[]
    for child in node.children:
        output.extend(houorder(child))
    output.append(node.value)
    return "".join(output)
s=input()
node=parse_Tree(s)
print(qianorder(node))
print(houorder(node))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240325154206056](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240325154206056.png)



### 02775: 文件结构“图”

http://cs101.openjudge.cn/practice/02775/



思路：实在调不好输出，只能借鉴课件的代码了



代码

```python
# from sys import exit
class Treenode:
    def __init__(self, value):
        self.value =value
        self.dirs = []
        self.files = []

    def getGraph(self):
        g = [self.value]
        for d in self.dirs:
            subg= d.getGraph()
            g.extend(["|     " + s for s in subg])
        for f in sorted(self.files):
            g.append(f)
        return g
n = 0
while True:
    n += 1
    stack = [Treenode("ROOT")]
    while (s := input()) != "*":
        if s == "#": exit(0)
        if s[0] == 'f':
            stack[-1].files.append(s)
        elif s[0] == 'd':
            stack.append(Treenode(s))
            stack[-2].dirs.append(stack[-1])
        else:
            stack.pop()
    print(f"DATA SET {n}:")
    print(*stack[0].getGraph(), sep='\n')
    print()

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240325171530841](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240325171530841.png)



### 25140: 根据后序表达式建立队列表达式

http://cs101.openjudge.cn/practice/25140/



思路：建树模拟



代码

```python
# from collections import  deque
class Treenode():
    def __init__(self,value):
        self.value=value
        self.left=None
        self.right=None
def parse_tree(s):
    stack=[]
    for i in s:
        node=Treenode(i)
        if i.isupper():
            node.right=stack.pop()
            node.left=stack.pop()
        stack.append(node)
    return stack[0]
def shuchu(root):
    deque=[root]
    output=[]
    while deque:
        node=deque.pop(0)
        output.append(node.value)
        if node.left:
            deque.append(node.left)
        if node.right:
            deque.append(node.right)
    return output
n=int(input())
for _ in range(n):
    s=input()
    root=parse_tree(s)
    a=shuchu(root)[::-1]
    print("".join(a))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240325160827187](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240325160827187.png)



### 24750: 根据二叉树中后序序列建树

http://cs101.openjudge.cn/practice/24750/



思路：先根据中后序列建树，在前序输出



代码

```python
# class Treenode():
    def __init__(self,value):
        self.value=value
        self.left=None
        self.right=None
def build_tree(inorder,postorder):
    if not inorder or not postorder:
        return None
    root=Treenode(postorder.pop())
    root_index=inorder.index(root.value)
    root.right=build_tree(inorder[root_index+1:],postorder)
    root.left = build_tree(inorder[:root_index], postorder)
    return root
def parse_tree(root):
    output=[]
    if root:
        output.append(root.value)
        output.extend(parse_tree(root.left))
        output.extend(parse_tree(root.right))
    return output
inorder=list(input())
postorder=list(input())
root=build_tree(inorder,postorder)
a=parse_tree(root)
print("".join(a))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240325163802013](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240325163802013.png)



### 22158: 根据二叉树前中序序列建树

http://cs101.openjudge.cn/practice/22158/



思路：与上一题类似，先按前中序列建树，再按照后序输出



代码

```python
# while True:
    try:
        class Treenode():
            def __init__(self,value):
                self.value=value
                self.left=None
                self.right=None
        def build_tree(inorder,preorder):
            if not inorder or not preorder:
                return None
            root=Treenode(preorder.pop(0))
            root_index=inorder.index(root.value)
            root.left = build_tree(inorder[:root_index], preorder)
            root.right = build_tree(inorder[root_index + 1:], preorder)
            return root
        def parse_tree(root):
            output=[]
            if root:
                output.extend(parse_tree(root.left))
                output.extend(parse_tree(root.right))
                output.append(root.value)
            return output
        preorder=list(input())
        inorder=list(input())
        root=build_tree(inorder,preorder)
        a=parse_tree(root)
        print("".join(a))
    except EOFError:
        break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240325164433750](C:\Users\27173\AppData\Roaming\Typora\typora-user-images\image-20240325164433750.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

对树的理解逐渐加深了吧，但自己写还是会出现各种各样的问题，作业基本还是只能写出个大概框架，再根据课件上的代码慢慢微调，还是很有体会的吧，学到了挺多东西的，但还是觉得有点乱，后续争取找个时间把树有关的知识点再从头到尾理顺一遍



