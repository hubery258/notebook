# chapter 4: Trees

??? note "重点单词"
    - **Traversal**: 遍历
        - **Preorder**: 前序遍历(根放最前面)
        - **inorder**: 中序遍历(二叉树特有)
        - **postorder**: 后序遍历(根在最后)
        - **Levelorder**: 层序遍历
        - **predecessor**: 前驱
        - **successor**: 后继
    - **key**: 节点储存的值
 
## 基本概念


2. **根（Root）**: 树的最顶层节点，唯一。
3. **父节点（Parent）**与**子节点（Child）**: 有子树的节点是 parent, 子树的根是 child
4. **兄弟（Sibling）**: 同一个父节点的多个子节点互为兄弟。
5. **度（Degree）**:
    - **节点的度**：它有多少个子节点  
    - **树的度**：所有节点度的最大值
6. **叶子（Leaf）**: 度为 0 的节点（没有孩子）。
7. **路径（Path）与路径长度（Length）**
    - 路径：从一个节点到另一个节点的节点序列  
    - 路径长度：路径上的边数,换句话说，`经过的节点个数-1`的值(包括起终点)
8. **深度（Depth）**: 从根到该节点的路径长度（根的深度 = 0）
9. **高度（Height）**: 从该节点到最深叶子的最长路径长度(叶子的高度 = 0)
10. **子树（Subtree）**: 每个节点都可以看成一棵子树的根。

??? note "度数和"
    度数和(度数为n的节点个数乘上n求和) = 所有孩子的总数 = 边数和 = 节点数 - 1

<hr>

### 树的两种表示方式

#### List Representation

每个节点包含：

- 数据
- 一个“孩子列表”（可能是数组、链表等）

例如：

```
A
├── B
├── C
└── D
```

表示为：

```
A: [B, C, D]
B: [...]
C: [...]
D: [...]
```

##### 缺点  
每个节点的孩子数不同 → 节点大小不一致 → 不好实现。

<hr>

#### **FirstChild–NextSibling**

重点，能把**任意树转成二叉树**。

每个节点有两个指针：

- `FirstChild`：指向第一个孩子  
- `NextSibling`：指向右边的兄弟  

结构：

```c
struct TreeNode {
    ElementType Element;
    TreeNode* FirstChild;
    TreeNode* NextSibling;
};
```

例如：

```
A
├── B
│   ├── E
│   └── F
├── C
└── D
```

变成：

```
A
↓FirstChild
B → C → D
↓FirstChild
E → F
```

##### 优点  
- 每个节点大小一致  
- 可以用二叉树结构存任意树  
- 后续所有遍历都能复用二叉树的遍历方式

<hr>

## Directory Tree(目录树)

### 定义

就是你电脑里的文件系统结构：

```
/
├── home
│   ├── user
│   │   ├── docs
│   │   └── pics
│   └── guest
└── etc
```

每个目录（文件夹）都是一个节点，每个节点可以有多个子节点。

这就是一个 **树**。

### 表示？

用**FirstChild–NextSibling（孩子兄弟表示法）**。

因为目录的子节点数量不固定：

- 有的目录有 0 个文件  
- 有的目录有 1000 个文件  

所以不能用固定大小的数组。

孩子兄弟表示法非常适合：

```c
typedef struct TreeNode {
    char* name;                 // 文件名或目录名
    struct TreeNode* firstChild; // 第一个子目录/文件
    struct TreeNode* nextSibling; // 下一个兄弟节点
} TreeNode;
```

结构示意：

```
A
├── B
│   ├── E
│   └── F
├── C
└── D
```

变成：

```
A
↓firstChild
B → C → D
↓firstChild
E → F
```

<hr>

### 目录树最重要的操作：**递归遍历**

目录树最经典的操作就是：

- 打印目录结构  
- 计算目录大小  
- 搜索文件  
- 删除目录  
- 复制目录  

这些全部都用 **递归**。

<hr>

#### 打印目录树

```c
void listDir(TreeNode* root, int depth) {
    if (root == NULL) return;

    // 打印缩进
    for (int i = 0; i < depth; i++)
        printf("  ");

    printf("%s\n", root->name);

    // 递归打印子目录
    listDir(root->firstChild, depth + 1);

    // 打印兄弟节点
    listDir(root->nextSibling, depth);
}
```

!!! note "递归思想"
    - **firstChild → 往下走（更深层）**
    - **nextSibling → 往右走（同层）**
    > **树结构 + 递归 = 天然搭档**


#### 计算目录大小

```c
int getSize(TreeNode* root) {
    if (root == NULL) return 0;

    int size = root->size;  // 文件大小（目录大小可设为 0）

    // 加上所有子节点的大小
    size += getSize(root->firstChild);

    // 加上所有兄弟节点的大小
    size += getSize(root->nextSibling);

    return size;
}
```

<hr>

## Binary Tree（二叉树）

### 定义  
- 每个节点最多有 **两个孩子**：Left、Right  
- 二叉树不要求“满”或“平衡”，只是结构限制

### binary tree 的遍历

```c
// 结构定义
typedef struct TreeNode {
    int element;
    struct TreeNode* left;
    struct TreeNode* right;
} TreeNode;

typedef TreeNode* BinaryTree; 

// 遍历（Traversal），遍历是二叉树最重要的操作。

/* 1. 前序遍历（Preorder）
顺序：根 → 左 → 右 */

void preorder(BinaryTree T) {
    if (T != NULL) {
        visit(T->element); // visit 要实现什么依据需要而不同
        preorder(T->left);
        preorder(T->right);
    }
}

/*2. 中序遍历（Inorder）
顺序：左 → 根 → 右*/

void inorder(BinaryTree T) {
    if (T != NULL) {
        inorder(T->left);
        visit(T->element);
        inorder(T->right);
    }
}

/* 3. 后序遍历（Postorder）
顺序：左 → 右 → 根 */

void postorder(BinaryTree T) {
    if (T != NULL) {
        postorder(T->left);
        postorder(T->right);
        visit(T->element);
    }
}

/* 4. 层序遍历（Levelorder）
需要队列（Queue），queue的实现见chap3*/

void levelorder(BinaryTree T) {
    queue Q = CreateQueue(100);
    enqueue(T, Q);

    while (!IsEmpty(Q)) {
        BinaryTree node = dequeue(Q);
        visit(node->element);

        if (node->left) enqueue(node->left, Q);
        if (node->right) enqueue(node->right, Q);
    }
}
```

!!! note "遍历序列的价值"
    遍历序列本质是 **区间信息**:
    - postorder的最后一位visit是root，而其左右区间可用inoder判断
    - 根在inoder中把左右区间分出来了
<hr>

??? example

    给定二叉树：
    ```
            A
           / \
          B   C
         / \
        D   E
    ```
    中序遍历顺序：

    ```
    D → B → E → A → C
    ```

    过程：

    1. 访问 A 的左子树 → B  
    2. 访问 B 的左子树 → D  
    3. D 无左 → visit(D)  
    4. 回到 B → visit(B)  
    5. 访问 B 的右子树 → E  
    6. visit(E)  
    7. 回到 A → visit(A)  
    8. 访问 A 的右子树 → C  
    9. visit(C)

<hr>

### 性质

设：

- n = 总结点数
- n<sub>0</sub>​ = 叶子结点数（度为 0）
- n<sub>1</sub>​ = 只有一个孩子的结点数（度为 1）
- n<sub>2</sub>​ = 有两个孩子的结点数（度为 2）

则:
**n<sub>0</sub>​\=n<sub>2</sub>​+1**且n= n<sub>0</sub>​+n<sub>1</sub>​+n<sub>2</sub>

!!! example "一般树转binary tree"

使用**左孩子–右兄弟表示法**，left放的是孩子，而自己right放的是兄弟,原:
```
R
├── N1
│   ├── A
│   └── B
├── N2
│   └── C
└── N3
    ├── D
    ├── E
    └── F
        └── G
```
末:
```
          R
         /
       N1
      /  \
     A    N2
      \   / \
       B C   N3
             /
            D
             \
              E
               \
                F
               /
              G
```

### Expression Tree（表达式树）  

#### 定义

表达式树是一种**特殊的二叉树**，用于表示算术表达式。

规则：
- **叶子节点（Leaf）**：操作数（数字、变量）
- **内部节点（Internal Node）**：运算符（+、-、*、/）

例如表达式：

```
(3 + 4) * 5
```

对应的表达式树是：

```
        *
       / \
      +   5
     / \
    3   4
```

表达式树的作用：

1. 清晰表达运算顺序: 用树结构决定优先级。
2. 轻松转换表达式形式:   
    - 前序遍历 → 前缀表达式(Prefix)  
    - 中序遍历 → 中缀表达式(Infix)  
    - 后序遍历 → 后缀表达式(Postfix)  
3. 轻松计算表达式: 递归求值即可。
4. 是编译器的基础: 编译器就是用表达式树来生成中间代码的。

<hr>

#### 表达式树的构建（从后缀表达式构建）

选取从后缀入手是因为后缀表达式没有括号，构建最简单。

扫描后缀表达式：

- 如果是 **操作数**：创建节点，**push** 到栈  
- 如果是 **运算符**：  
  - **pop两个节点**作为右、左子树  
  - 创建新节点  
  - push回栈  

最终栈顶就是整棵树。

---

##### 示例：后缀表达式 `3 4 + 5 *`

步骤如下：

1. 读到 `3` → push

栈：  
```
[3]
```

2. 读到 `4` → push

栈：  
```
[3, 4]
```

3. 读到 `+` → pop 两个节点

```
    +
   / \
  3   4
```

push 回栈：

```
[ + ]
```

4. 读到 `5` → push

```
[ + , 5 ]
```

5. 读到 `*` → pop 两个节点

```
        *
       / \
      +   5
     / \
    3   4
```

push 回栈：

```
[ * ]
```

结束，栈顶就是表达式树。

<hr>

#### 表达式树与遍历的关系

表达式树最经典的性质：

| 遍历方式 | 得到的表达式 |
|---------|--------------|
| **前序遍历** | 前缀表达式（Prefix） |
| **中序遍历** | 中缀表达式（Infix） |
| **后序遍历** | 后缀表达式（Postfix） |

以刚才的树为例：

```
        *
       / \
      +   5
     / \
    3   4
```

##### 前序

```
* + 3 4 5
```

##### 中序

```
3 + 4 * 5
```

（注意：实际中序需要加括号）

##### 后序

```
3 4 + 5 *
```

<hr>

#### 从后缀表达式实现

```c
// 结构定义
typedef struct TreeNode {
    char element;              // 运算符或操作数
    struct TreeNode* left;
    struct TreeNode* right;
} TreeNode;
typedef TreeNode* ExpressionTree;

// 构建tree
ExpressionTree buildTree(char postfix[]) {
    stack S = CreateStack();   // stack的实现见chap3

    for (int i = 0; postfix[i] != '\0'; i++) {
        char c = postfix[i];

        if (isdigit(c)) {
            // 操作数：创建节点并 push
            ExpressionTree node = malloc(sizeof(TreeNode));
            node->element = c;
            node->left = node->right = NULL;
            stack_push(node, S);
        } else {
            // 运算符：pop 两个节点
            ExpressionTree right = stack_pop(S);
            ExpressionTree left  = stack_pop(S);

            ExpressionTree node = malloc(sizeof(TreeNode));
            node->element = c;
            node->left = left;
            node->right = right;

            stack_push(node, S);
        }
    }

    return stack_pop(S);
}
```

#### 表达式树求值

```c
int eval(ExpressionTree T) {
    if (T->left == NULL && T->right == NULL)
        return T->element - '0';   // 字符转数字

    int left = eval(T->left);
    int right = eval(T->right);

    switch (T->element) {
        case '+': return left + right;
        case '-': return left - right;
        case '*': return left * right;
        case '/': return left / right;
    }
}
```

### Threaded Binary Tree（线索二叉树）

#### 定义

**普通二叉树的中序遍历需要用递归或栈。**，因为你需要“回到父节点”，但普通二叉树没有指向父节点的指针。而线索二叉树**把二叉树中原本为 NULL 的指针利用起来，指向中序遍历的前驱或后继。**

也就是说：
- 如果一个节点的 left 本来是 NULL  
  → 改成指向它的 **中序前驱**
- 如果一个节点的 right 本来是 NULL  
  → 改成指向它的 **中序后继**

这样：不需要栈，不需要递归，可以直接沿着“线索”找到下一个节点，中序遍历可以 O(n) 时间、O(1) 空间完成

#### 结构

每个节点需要两个额外的标志位：

```c
typedef struct ThreadNode {
    int element;
    struct ThreadNode* left;
    struct ThreadNode* right;
    int leftTag;   // 0 = left 指向左孩子, 1 = left 是线索（前驱）
    int rightTag;  // 0 = right 指向右孩子, 1 = right 是线索（后继）
} ThreadNode;
```

#### 中序线索化（Inorder Threading）

以中序遍历为例,中序遍历顺序：

```
Left → Root → Right
```

线索化规则：

1. 如果节点没有左孩子  
`leftTag = 1`  
`left = 中序前驱`

2. 如果节点没有右孩子  
`rightTag = 1`  
`right = 中序后继`

#### 图示

原树：

```
      A
     / \
    B   C
   /
  D
```

中序遍历：D → B → A → C

线索化后：

```
      A
     / \
    B   C
   /
  D

(D.left 无前驱，所以是null)
D.right → B
B.left  → D
B.right → A
A.right → C
```

所有 NULL 指针都被利用起来了。

---

**线索二叉树必须有一个 head node。**,因: 

- head.left 指向整棵树的根  
- head.right 指向中序遍历的最后一个节点  
- 方便从头到尾遍历  
- 也方便从尾到头遍历（双向）

结构：

```
   head
   /  \
 root  last
```


#### 中序遍历线索二叉树

算法非常优雅：

1. 找到中序序列的第一个节点（一直往左走）
2. visit
3. 如果 rightTag == 1  
   → 直接沿着线索走到后继  
4. 否则  
   → 进入右子树，再找最左节点

#### 实现

```c
ThreadNode* createNode(int x) {
    ThreadNode* T = malloc(sizeof(ThreadNode));
    T->element = x;
    T->left = T->right = NULL;
    T->leftTag = T->rightTag = 0;
    return T;
}

/*2. 中序线索化*/
ThreadNode* pre = NULL;  // 全局变量，记录前驱

void inorderThread(ThreadNode* T) {
    if (T == NULL) return;

    inorderThread(T->left);

    // 左指针为空 → 指向前驱
    if (T->left == NULL) {
        T->leftTag = 1;
        T->left = pre;
    }

    // 前驱的右指针为空 → 指向后继
    if (pre != NULL && pre->right == NULL) {
        pre->rightTag = 1;
        pre->right = T;
    }

    pre = T;

    inorderThread(T->right);
}



/*3. 中序遍历线索二叉树*/
void inorderTraverse(ThreadNode* head) {
    ThreadNode* p = head->left;  // root

    while (p != head) {
        // 找到最左节点
        while (p->leftTag == 0)
            p = p->left;

        visit(p->element);

        // 沿着线索走
        while (p->rightTag == 1 && p->right != head) {
            p = p->right;
            visit(p->element);
        }

        p = p->right;
    }
}
```

<hr>

### Binary Search Tree（二叉搜索树,BST）

#### 定义  
- 每个节点有一个唯一的 key（整数）  
- 左子树**所有节点**的 key < 根节点的 key  
- 右子树**所有节点**的 key > 根节点的 key  
- 左右子树也必须是 BST  

#### 基本操作（ADT）  

- `MakeEmpty(T)`：清空树  
- `Find(X, T)`：查找元素  
- `FindMin(T)`：查找最小值  
- `FindMax(T)`：查找最大值  
- `Insert(X, T)`：插入元素  
- `Delete(X, T)`：删除元素  
- `Retrieve(P)`：返回节点值  

#### 实现  

```c
// 结构定义
typedef struct TreeNode {
    int element;                // 节点值（key）
    struct TreeNode* left;      // 左子树
    struct TreeNode* right;     // 右子树
} TreeNode;

typedef TreeNode* SearchTree;
typedef TreeNode* Position; 

// 1. 查找（Find）

// 递归版
Position Find(int X, SearchTree T) {
    if (T == NULL) return NULL;              // 空树
    if (X < T->element) return Find(X, T->left);   // 左子树
    else if (X > T->element) return Find(X, T->right); // 右子树
    else return T;                           // 找到
}
// 迭代版
Position Iter_Find(int X, SearchTree T) {
    while (T != NULL) {
        if (X == T->element) return T;
        else if (X < T->element) T = T->left;
        else T = T->right;
    }
    return NULL;
}

// 2. 查找最小值 / 最大值  

Position FindMin(SearchTree T) {
    if (T == NULL) return NULL;
    else if (T->left == NULL) return T;
    else return FindMin(T->left);
}

Position FindMax(SearchTree T) {
    if (T == NULL) return NULL;
    while (T->right != NULL) T = T->right;
    return T;
}

// 3. 插入（Insert）
SearchTree Insert(int X, SearchTree T) {
    if (T == NULL) { // 创建新节点
        T = malloc(sizeof(TreeNode));
        T->element = X;
        T->left = T->right = NULL;
    } else if (X < T->element) {
        T->left = Insert(X, T->left);
    } else if (X > T->element) {
        T->right = Insert(X, T->right);
    }
    // 如果 X == T->element，不插入（不允许重复）
    return T;
}

/* 4. 删除（Delete）
分三种情况：
1. **叶子节点**：直接删除  
2. **度为 1**：用子节点替代  
3. **度为 2**：用右子树最小值（或左子树最大值）替代，再删除该节点*/
SearchTree Delete(int X, SearchTree T) {
    Position TmpCell;
    if (T == NULL) return NULL;

    if (X < T->element) T->left = Delete(X, T->left);
    else if (X > T->element) T->right = Delete(X, T->right);
    else { // 找到要删除的节点
        if (T->left && T->right) { // 两个孩子
            TmpCell = FindMin(T->right);
            T->element = TmpCell->element;
            T->right = Delete(T->element, T->right);
        } else { // 一个或零个孩子
            TmpCell = T;
            if (T->left == NULL) T = T->right;
            else if (T->right == NULL) T = T->left;
            free(TmpCell);
        }
    }
    return T;
}
```

<hr>

??? example

    假设插入顺序：30, 20, 40, 10, 25, 35, 50  

    构建的 BST：

    ```
            30
           /  \
         20    40
        / \    / \
      10  25  35  50
    ```

    - `Find(25)` → 30 → 20 → 25 → 找到  
    - `FindMin()` → 一直往左 → 10  
    - `FindMax()` → 一直往右 → 50  
    - `Insert(22)` → 插到 25 左边  
    - `Delete(20)` → 用右子树最小值 25 替代，再删除 25  


#### 平均情况分析  

- 插入顺序好（平衡） → 树高约 \(\log n\)，操作效率 O(log n)  
- 插入顺序差（递增或递减） → 退化成链表，树高 = n，操作效率 O(n), 比如只有一条线等等...  

??? note "平衡"
    平衡二叉树: 对任意节点，**左子树高度-右子树高度的绝对值<=1**

???+ note "decision tree for binary search?"
    出现在作业题中，这种tree的要求是**必须是完全二叉树**且是平衡二叉树，平衡二叉树的定义见上;<br>
    完全二叉树:除了最后一层，其他层都是满的；最后一层的节点从左到右连续，没有空隙。
