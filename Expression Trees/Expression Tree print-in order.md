### Summary and Key Points

**1. `isOperand` Function:**
   - **Purpose:** Checks if a character is a numeric operand (digit).
   - **Implementation:** `bool isOperand(char c) { return c >= '0' && c <= '9'; }`
   - **Returns:** `true` if the character is a digit, `false` otherwise (i.e., if it is an operator).

**2. `!isOperand` Usage:**
   - **Purpose:** Determines if a character is **not** a numeric operand, i.e., if it is an operator.
   - **In Function:** Used to decide if parentheses should be added around operators.
   - **Example:** `!isOperand(node->left->data)` returns `true` if the left child’s data is an operator, which means parentheses should be added around it.

**3. `print_inorder_expression_helper` Function:**
   - **Purpose:** Prints the expression tree in infix notation with proper parentheses to maintain correct operator precedence.
   - **Logic:**
     - **Left Subtree:**
       - If the left child is an operator (not an operand), print an opening parenthesis before printing the left subtree and a closing parenthesis after.
     - **Current Node:**
       - Print the node’s data (operator or operand).
     - **Right Subtree:**
       - If the right child is an operator (not an operand), print an opening parenthesis before printing the right subtree and a closing parenthesis after.

**4. Example Explanation:**
   - **Expression Tree for `2 + 3 * 4`:**
     - **Infix Notation:** `(2 + (3 * 4))`
     - **Operand Nodes:** `2`, `3`, `4` (no parentheses needed around them).
     - **Operator Nodes:** `+`, `*` (parentheses needed to indicate precedence).

**5. Code Implementation:**
   - **`print_inorder_expression_helper` Function:**
     ```cpp
     void print_inorder_expression_helper(treeNode<tData>* node) {
         if (node == nullptr)
             return;

         if (node->left) {
             if (!isOperand(node->left->data))
                 cout << '(';
             print_inorder_expression_helper(node->left);
             if (!isOperand(node->left->data))
                 cout << ')';
         }

         cout << node->data << " ";

         if (node->right) {
             if (!isOperand(node->right->data))
                 cout << '(';
             print_inorder_expression_helper(node->right);
             if (!isOperand(node->right->data))
                 cout << ')';
         }
     }
     ```
   - **`isOperand` Function:**
     ```cpp
     bool isOperand(char c) {
         return c >= '0' && c <= '9';
     }
     ```
   - **`binaryTree` Constructor:**
     ```cpp
     binaryTree(string &s) {
         stack<treeNode<tData>*> st;
         for (char c : s) {
             if (isOperand(c)) {
                 st.push(new treeNode<tData>(c));
             } else {
                 treeNode<tData>* newNode = new treeNode<tData>(c);
                 newNode->right = st.top(); st.pop();
                 newNode->left = st.top(); st.pop();
                 st.push(newNode);
             }
         }
         root = st.top();
     }
     ```

# Example Expression: `23*4+`

### Steps to Build the Expression Tree:

1. **Postfix Expression:** `23*4+`
2. **Build the Tree:**

   - Read `2` and `3`: Push as leaf nodes.
   - Read `*`: Pop `2` and `3` from the stack, create a new node with `*`, and set `2` as the left child and `3` as the right child. Push the `*` node back to the stack.
   - Read `4`: Push as a leaf node.
   - Read `+`: Pop `4` and the `*` node from the stack, create a new node with `+`, and set `*` as the left child and `4` as the right child. Push the `+` node back to the stack.

### Resulting Expression Tree:

```
    +
   / \
  *   4
 / \
2   3
```

### Infix Expression with Parentheses:

The in-order traversal of the tree with proper parentheses would be: `(2 * 3) + 4`

### Visualization:

1. **Initial Stack Operations:**
   - Push `2` → Stack: `[2]`
   - Push `3` → Stack: `[2, 3]`
   - Process `*` → Create node `*` with left child `2` and right child `3`
     ```
       *
      / \
     2   3
     ```
     → Stack: `[*]`
   - Push `4` → Stack: `[* , 4]`
   - Process `+` → Create node `+` with left child `*` and right child `4`
     ```
       +
      / \
     *   4
    / \
   2   3
     ```
     → Stack: `[+]`

### Summary of Steps:

1. **Postfix Expression:** `23*4+`
2. **Build Tree:**
   - Push operands (`2`, `3`, `4`) as leaf nodes.
   - For operators (`*`, `+`), create internal nodes and combine subtrees.
3. **Infix Expression:** `(2 * 3) + 4`

This process ensures that the operators and operands are placed correctly according to operator precedence and parentheses are used to group expressions properly.
![[Pasted image 20240816013414.png]]
