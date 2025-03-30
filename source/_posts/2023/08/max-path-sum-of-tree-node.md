---
title: 二叉树的最大路径和
date: 2023-08-24 16:40:11
updated: 2023-08-24 16:40:11
tags:
- 算法
categories:
- 技术
---



今天看到一个题，[二叉树求最大路径和](https://leetcode.cn/problems/binary-tree-maximum-path-sum/solutions/)，leecode上还是hard模式，觉得这个题还是很有代表性。

复习下，看看怎么解。因为涉及到二叉树，一般都可分解为子问题去递归处理。

`递归框架`：

~~~markdown
```c++
void traverse(Node *node) {
//前序
	traverse(node->left);
// 中序
	traverse(node->right);
// 后序
}  
```
~~~

最重要的还是要理解这个`子问题`，怎么定义。

想象下自己在这颗二叉树进行遍历，先进入root节点， 接下来有很多选择，要选最大的子树边距去走。

子树有自己的左子树和右子树。这颗子树对于父亲节点而言，需要交付给父亲节点是：

包含自己(subNode->val)的最大边距是多少？

> 子问题：subMaxPath = subNode->val+max(subNode->left, subNode->right)



整体的结构：

~~~markdown
```c++
		int res = INT_MIN;
		
    //后序遍历可以先知道左节点和右节点
    //这个递归函数返回的是当前这个节点最大的路径和
    int def(TreeNode* root) {

        if(root == nullptr) return 0;

        //左右两边节点最大值
        int left = max(0, def(root->left));
        int right = max(0, def(root->right));

        //节点的最大路径取决于该节点的值，左右节点的最大路径
        res = max(res, left+right+root->val);

        //因为总要选一边所以是max，左右子树，选最大的那颗树
        //想象下自己在游走这颗二叉树
        return max(left, right)+root->val;
    }
    
    int maxPathSum(TreeNode* root) {
        def(root);
        return res;
    }  
```
~~~

递归里面，需要想清楚子问题的定义，和return出口的定义。

整个框架结构就清晰了。



算法是软肋，之前面试，有好几个不错的机会，在算法这一轮挂了。
尤其是那些从硅谷回来的CTO，喜欢跟你聊算法，测验你的最基础的技术功底如何。
也是万万没想到，最后一轮还要搞算法，当时汗都快下来了。
有时间应该多补补这块，算是给脑子健健脑。

即使不干技术这行了，也是有意义的。
