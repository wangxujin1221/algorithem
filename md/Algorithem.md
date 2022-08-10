### 二叉树镜像（简单）

+ 层序遍历加交换

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    LinkedBlockingQueue<TreeNode> nodes = new LinkedBlockingQueue<>();
    public TreeNode mirrorTree(TreeNode root) {
        if(root == null){
            return null;
        }
        nodes.offer(root);
        while(nodes.size() != 0){
            switchNode(nodes.poll());
        }
        return root;
    }

    public void switchNode(TreeNode node){
        if(node == null){
            return;
        }
        TreeNode tmp = node.left;
        node.left = node.right;
        node.right = tmp;
        if(node.left != null){
            nodes.offer(node.left);
        }
        if(node.right != null){
            nodes.offer(node.right);
        }
    }
}
```
时间复杂度：O(n)
空间复杂度：O(n)

+ 递归

```java
class Solution {
    public TreeNode mirrorTree(TreeNode root) {
        if(root == null){
            return null;
        }
        switchNode(root);
        mirrorTree(root.left);
        mirrorTree(root.right);
        return root;
    }

    public TreeNode switchNode(TreeNode node){
        TreeNode tmp = node.left;
        node.left = node.right;
        node.right = tmp;
        return node;
    }
}
```
时间复杂度：O(n)
空间复杂度：O(n)

### 不同的二叉搜索树 2
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<TreeNode> generateTrees(int n) {
        if(n == 0){return new ArrayList<TreeNode>();}
        return generateOneTree(1,n);

    }

    public List<TreeNode> generateOneTree(int start,int end){
        List<TreeNode> res = new ArrayList<>();
        // 递归退出条件
        if(start > end){
            res.add(null);
            return res; // 这里不能直接返回null，否则递归的结果一层层都是null
        }
        // 枚举所有可能的根节点
        for(int i = start; i <= end; i++){ // 这里是可以等于end的
            // 类似于后序遍历的结构
            List<TreeNode> leftTrees = generateOneTree(start,i-1);
            List<TreeNode> rightTrees = generateOneTree(i+1,end);
            // 构建所有可能的组合
            for(TreeNode leftTree:leftTrees){
                for(TreeNode rightTree:rightTrees){
                    TreeNode root = new TreeNode(i);
                    root.left = leftTree;
                    root.right = rightTree;
                    res.add(root);
                }
            }
        }
        return res;    
    }
}
```
时间复杂度：O(n*Gn)
空间复杂度：O(n)
