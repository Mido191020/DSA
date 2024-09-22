```
void InOrder() {
    internalInOrder(root);
    cout << endl;
}

void internalInOrder(TreeNode<Tdata> *node) {
    if (node == nullptr) return; // Base case: if node is null, return
    internalInOrder(node->Left);  // Recur on the left subtree
    cout << node->Data << " -> "; // Print the data of the current node
    internalInOrder(node->Right); // Recur on the right subtree
}

```