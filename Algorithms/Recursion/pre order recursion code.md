```c++
void PreOrder() {
    internalPreOrder(root);
    cout << endl;
}

void internalPreOrder(TreeNode<Tdata> *node) {
    if (node == nullptr) return; // Base case: if node is null, return
    cout << node->Data << " -> "; // Print the data of the current node
    internalPreOrder(node->Left);  // Recur on the left subtree
    internalPreOrder(node->Right); // Recur on the right subtree
}
```
