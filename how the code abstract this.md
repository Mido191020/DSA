```c++
void delte_fromTree(tData value) {  
    treeNode<tData>* cur = find(value);  
    if (!cur) {  
        cout << "The node was not found!" << endl;  
        return;  
    }  
  
    if (cur->left == nullptr && cur->right == nullptr) {  
        delete_child_helper(value);  
    } else if ((cur->left != nullptr && cur->right == nullptr) || (cur->left == nullptr && cur->right != nullptr)) {  
        deleteNodeHasChild_helper(value);  
    } else {  
        deleteNodeWithTwoChildren_helper(value);  
    }  
}
```
