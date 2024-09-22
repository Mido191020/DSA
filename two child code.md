```c++
void deleteNodeWithTwoChildren_helper(tData value) {  
    treeNode<tData>* cur = find(value);  
    if (!cur) {  
        cout << "The node was not found!" << endl;  
        return;  
    }  
  
    // Find the in-order successor  
    treeNode<tData>* successor = findMinNode(cur->right);  
    tData successorValue = successor->data;  
  
    // Replace the value of the current node with the successor's value  
    cur->data = successorValue;  
  
    // Delete the successor node (which will have at most one child)  
    deleteNodeHasChild_helper(successorValue);  
}  
treeNode<tData>* findMinNode(treeNode<tData>* node) {  
    if (node == nullptr) return nullptr;  
    while (node->left != nullptr) {  
        node = node->left;  
    }  
    return node; // Return the node itself, not just the value  
}
```
	