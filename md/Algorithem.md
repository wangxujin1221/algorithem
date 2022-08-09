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

