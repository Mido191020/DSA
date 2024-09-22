```
void PostOrder() {
    internalPostOrder(root);
    cout << endl;
}

void internalPostOrder(TreeNode<Tdata> *node) {
    if (node == nullptr) return; // Base case: if node is null, return
    internalPostOrder(node->Left);  // Recur on the left subtree
    internalPostOrder(node->Right); // Recur on the right subtree
    cout << node->Data << " -> ";   // Print the data of the current node
```}
