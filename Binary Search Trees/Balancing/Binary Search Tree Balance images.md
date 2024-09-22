![[Screenshot 2024-07-25 155454.png]]

![[Screenshot 2024-07-25 154821.png]]
### Explanation

#### Image 1:

- **Scratches (Notes)**:
  - **In-order traversal**: It lists all nodes in a sorted way. We can save all nodes' data in an array using this method.
  - **Recursive division**: The array is divided into left and right parts. The recursive function accepts the start and end indices of a part of the array and returns a subtree. For each node:
    - Calculate the mid index and create a new node with the data from this index.
    - Divide the part of the array into two parts: one before the mid and one after the mid.
    - `node.left` will equal a new recursive call with the left part of the array.
    - `node.right` will equal a new recursive call with the right part of the array.

- **Functions**:
  - `Balance()`: 
    - Creates an empty list `nodes[]`.
    - Calls `InorderToArray(root, nodes)` to fill the list with sorted node values.
    - Sets `root` to `recursiveBalance(0, nodes.length - 1, nodes)` which rebalances the BST.

  - `InorderToArray(node, nodes)`:
    - If `node` is null, return.
    - Recursively add left node data to `nodes`, add current `node.data` to `nodes`, and then add right node data to `nodes`.

  - `recursiveBalance(start, end, nodes)`:
    - If `start > end`, return null.
    - Calculate `mid` as `(start + end) / 2`.
    - Create a new node `newNode` with `nodes[mid]`.
    - Set `newNode.left` to the result of `recursiveBalance(start, mid - 1, nodes)`.
    - Set `newNode.right` to the result of `recursiveBalance(mid + 1, end, nodes)`.
    - Return `newNode`.

#### Image 2:

- **Scratches (Notes)**:
  - In-order traversal saves nodes' data sorted in an array.
  - Calculate the mid index and make it the new root.
  - Recursively divide the array into left and right parts. For each node:
    - Divide the part of the array into two parts.
    - `node.left` will equal a new recursive call with the left part of the array.
    - `node.right` will equal a new recursive call with the right part of the array.