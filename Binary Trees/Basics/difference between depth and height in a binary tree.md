**"In a binary tree:**

- **Depth** of a node is defined as the number of edges from the root node to that node. For example, the root has a depth of 0, and each subsequent level increases the depth by 1.
    
- **Height** of a node is defined as the number of edges on the longest path from that node to a leaf. A leaf node has a height of 0, and the height of the tree is the height of the root node, which is equal to the maximum depth of any node in the tree.
    
- **In most coding problems**, especially those involving recursion, the height of the tree is often calculated using the formula `1 + max(left_height, right_height)` from the leaf nodes up to the root, which can be seen as the maximum depth of the tree from the perspective of the root."