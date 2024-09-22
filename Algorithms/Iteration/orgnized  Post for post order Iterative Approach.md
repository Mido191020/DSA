# Post-Order Traversal of a Binary Tree (Iterative Approach)

## Code Breakdown

```cpp
void post_order(tree* root) {
    if (root == nullptr) return;
    stack<tree*> stack;
    stack.push(root);
    stack<tree*> output;
    
    while (!stack.empty()) {
        tree* cur = stack.top();
        stack.pop();
        output.push(cur);
        if (cur->left) {
            stack.push(cur->left);
        }
        if (cur->right) {
            stack.push(cur->right);
        }
    }
    
    while (!output.empty()) {
        cout << output.top()->value << " ";
        output.pop();
    }
}
```

## Explanation

1. We start by checking if the root is null. If it is, we return immediately.
2. We create two stacks: `stack` for traversal and `output` for storing the result.
3. We push the root node onto the `stack`.
4. We enter the first while loop that continues as long as the `stack` is not empty:
   a. We pop a node from the `stack` and push it onto the `output` stack.
   b. We push the left child (if it exists) onto the `stack`.
   c. We push the right child (if it exists) onto the `stack`.
5. After the first loop, the `output` stack contains the nodes in reverse post-order.
6. We enter the second while loop to print the nodes from the `output` stack, giving us the correct post-order traversal.

## Visual Representation

```
    1
   / \
  2   3
 / \
4   5

Step-by-step:

1. Push 1 to stack
2. Pop 1, push to output, push 3 and 2 to stack
3. Pop 2, push to output, push 5 and 4 to stack
4. Pop 4, push to output
5. Pop 5, push to output
6. Pop 3, push to output

Output stack (top to bottom): 3, 5, 4, 2, 1
Printed output: 4 5 2 3 1
```

## Key Points

- This method uses two stacks: one for traversal and one for storing the result.
- The first loop performs a modified pre-order traversal (root, right, left).
- The second loop reverses the order, giving us the post-order traversal (left, right, root).
- This method is more memory-efficient than recursion for very deep trees, as it doesn't risk stack overflow.
- The time complexity is O(n) where n is the number of nodes in the tree.
- The space complexity is O(n) as in the worst case, all nodes might be in the stack at once.

## Comparison with Pre-Order and In-Order Traversals

- Post-order: Left, Right, Root
- Pre-order: Root, Left, Right
- In-order: Left, Root, Right

The main differences in implementation are:
- Post-order uses two stacks to reverse the order of visited nodes.
- Pre-order processes the node before pushing its children.
- In-order pushes all left children first, then processes the node, then moves to the right child.
### Why Reverse Printing?

The iterative approach using a stack processes nodes in a manner that resembles a reverse of the desired post-order sequence (`root, right, left` instead of `left, right, root`). This happens because of the LIFO (Last-In-First-Out) nature of stacks:

- **Push Order**: Nodes are pushed onto `stack` in a specific order (root, left child, right child), which inherently reverses the order relative to the desired post-order sequence.
- **Pop and Print Order**: When nodes are popped from `stack`, they are printed immediately. This direct printing would result in nodes being printed in a reversed order relative to the desired post-order sequence.