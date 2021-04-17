#### [107. 二叉树的层序遍历 II](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/)

难度：中等

给定一个二叉树，返回其节点值自底向上的层序遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

例如：
给定二叉树 `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其自底向上的层序遍历为：

```
[
  [15,7],
  [9,20],
  [3]
]
```



C++：迭代算法

```
思路：
	1、层序遍历可以利用队列来实现
	2、根节点先入队，当队列为空时，遍历结束
	3、当遍历完一层后，队列中就只剩下一层的节点，可以通过查询队列中的节点数控制一层的迭代数
	4、最终翻转结果序列，得到自底向上的遍历结果
	
	
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if(!root) return result;
        queue<TreeNode*> queue;
        queue.push(root); //根节点先入队
        while(!queue.empty()){
            int count = queue.size();//这一层有多少个节点
            vector<int> levelValue;
            for(int i = 0; i < count; i++){
                TreeNode* p = queue.front();//取出队头
                if(p->left != nullptr) 
                    queue.push(p->left);//将队头的左右孩子入队
                if(p->right != nullptr) 
                    queue.push(p->right);
                levelValue.push_back(p->val);
                queue.pop();//弹出队头
            }
            result.push_back(levelValue);//遍历完一层
        }
        reverse(result.begin(), result.end());//翻转遍历结果
        return result;
    }
};
```

