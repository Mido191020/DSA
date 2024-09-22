# Pre-Order Traversal of a Binary Tree (Iterative Approach)

## Code Breakdown

```cpp
void pre_order(tree* root) {
    if (root == nullptr) return;
    stack<tree*> stack;
    stack.push(root);
    while (!stack.empty()) {
        tree* cur = stack.top();
        stack.pop();
        cout << cur->value << " ";
        if (cur->right) {
            stack.push(cur->right);
        }
        if (cur->left) {
            stack.push(cur->left);
        }
    }
}
```

## Explanation

1. We start by checking if the root is null. If it is, we return immediately.
2. We create a stack and push the root node onto it.
3. We enter a while loop that continues as long as the stack is not empty.
4. In each iteration:
   a. We pop a node from the stack and immediately print its value.
   b. We push the right child (if it exists) onto the stack.
   c. We push the left child (if it exists) onto the stack.
5. This process ensures we visit the nodes in the order: root, left subtree, right subtree.

## Visual Representation

```
    1
   / \
  2   3
 / \
4   5

Step-by-step:

1. Push 1
2. Pop and print 1, push 3, push 2
3. Pop and print 2, push 5, push 4
4. Pop and print 4
5. Pop and print 5
6. Pop and print 3

Output: 1 2 4 5 3
```

## Key Points

- The stack is used to keep track of the nodes we need to visit.
- We push the right child before the left child so that the left child is processed first (LIFO - Last In, First Out).
- This method is more memory-efficient than recursion for very deep trees, as it doesn't risk stack overflow.
- The time complexity is O(n) where n is the number of nodes in the tree.
- The space complexity is O(h) where h is the height of the tree. In the worst case (for a skewed tree), this could be O(n).

## Comparison with In-Order Traversal

- Pre-order: Root, Left, Right
- In-order: Left, Root, Right

The main difference in implementation is:
- In pre-order, we process (print) the node before pushing its children.
- In in-order, we push all left children first, then process the node, then move to the right child.