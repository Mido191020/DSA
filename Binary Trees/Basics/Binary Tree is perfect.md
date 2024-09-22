### Formula-Based Approach

- **Objective:** Verify if the tree is perfect using the number of nodes and tree height.

- **Steps:**
  1. **Calculate Tree Height:** Use a helper function to find the height of the tree.
  2. **Count Nodes:** Use a helper function to count the total number of nodes in the tree.
  3. **Verify Perfection:** Check if the number of nodes equals \(2^{height + 1} - 1\).

- **Code:**

  ```cpp
  bool is_perfect() {
      int height = tree_height_rec();
      int nodes = total_nodes_rec();
      
      // Calculate 2^(height + 1) - 1
      int expectedNodes = pow(2, height + 1) - 1;
      
      return (nodes == expectedNodes); // Check if nodes == 2^height - 1
  }
  ```

**Explanation:**
- `pow(2, height + 1)` computes \(2^{height + 1}\).
- Subtracting 1 gives \(2^{height + 1} - 1\), which is the expected number of nodes for a perfect binary tree of given height.




### Recursive Method to Check if a Tree is Perfect

#### **Notes:**

1. **Definition of a Perfect Binary Tree:**
   - A binary tree is perfect if all internal nodes have exactly two children and all leaf nodes are at the same level.

2. **Recursive Approach:**
   - **Base Case:** If the tree is empty, it's considered perfect.
   - **Leaf Node Check:** All leaf nodes must be at the same depth.
   - **Internal Node Check:** Every internal node must have exactly two children.

3. **Steps:**
   1. **Calculate Depth:** Calculate the depth of the leftmost leaf node.
   2. **Check Each Node:** Recursively verify if each node fulfills the perfection conditions.

#### **Code:**

```cpp
bool is_perfect_rec_helper(treeNode<tData>* node, int depth, int level) {
    if (node == nullptr) {
        // An empty node (subtree) is perfect
        return true;
    }

    if (node->left == nullptr && node->right == nullptr) {
        // We are at a leaf node
        // Check if this leaf node is at the correct depth
        return (depth == level);
    }

    if (node->left == nullptr || node->right == nullptr) {
        // An internal node must have both left and right children
        return false;
    }

    // Recursively check if both left and right subtrees are perfect
    bool leftPerfect = is_perfect_rec_helper(node->left, depth, level + 1);
    bool rightPerfect = is_perfect_rec_helper(node->right, depth, level + 1);

    // The current tree is perfect if both subtrees are perfect
    return leftPerfect && rightPerfect;
}

bool is_perfect() {
    int depth = tree_height_rec();
    return is_perfect_rec_helper(root, depth, 0);
}
```

#### **Explanation:**

- **`is_perfect_rec_helper` Function:**
  - **Parameters:**
    - `node`: The current node being checked.
    - `depth`: The depth of the tree, used to validate leaf nodes.
    - `level`: The current level of the node in the tree.
  - **Base Case:** If `node` is `nullptr`, return `true` (an empty subtree is perfect).
  - **Leaf Node Check:** If both left and right children are `nullptr`, verify if the current level matches the expected depth.
  - **Internal Node Check:** Ensure the current node has both left and right children, then recursively check its subtrees.

- **`is_perfect` Function:**
  - Computes the depth of the tree.
  - Calls the recursive helper function to check if the tree is perfect.
  - 