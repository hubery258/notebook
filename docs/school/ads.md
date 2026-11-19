# ads个人笔记

> 先只整理维护一份文件，如果内容太多了再做文件管理。我的目的主要是构建自己能用的管理系统，不需要摘抄别人的内容，别人写了直接引用链接即可

## 001. AVL Trees

- BST的左右子树高低差大于1时就不再是AVL，否则就是。
- `Trouble Maker` & `Trouble Finder`: maker就是插入导致AVL tree不平衡的点，Finder就是离maker最近的首次出现不平衡的点,不平衡可以被分为`LL`,`RR`,`LR`,`RL`四类
    - `LR`表示的是 Trouble Maker 在 Trouble Finder 的 L 孩子节点的 R 孩子树中，其余的类似。

- 重新调平的方式可以参考[换根视角](https://note.isshikih.top/cour_note/D2CX_AdvancedDataStructure/Lec01/#%E6%8D%A2%E6%A0%B9%E8%A7%86%E8%A7%92)

## 002. Splay Trees 伸展树

> 为使 AVL 保持平衡，我们需要维护从根节点到 Trouble Maker 这条路径上所有点的平衡因子。而 Splay 则不再维护这些信息，这意味着我们无法保证 Splay 树的状态都是平衡的，但是我们希望它尽可能平衡。[具体讲](https://note.isshikih.top/cour_note/D2CX_AdvancedDataStructure/Lec01/#splay-%E6%A0%91:~:text=%E5%85%B7%E4%BD%93%E6%9D%A5%E8%AF%B4%E5%B0%B1%E6%98%AF,%E3%80%82)可以再多加理解一下

