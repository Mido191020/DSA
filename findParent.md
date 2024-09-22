```c++
treeNode<tData>* find_helper(treeNode<tData>* node, tData target) {  
    if (!node) {  
        return nullptr;  
    }  
    if (node->data == target) {  
        return node;  
    }  
    if (target < node->data) {  
        return find_helper(node->left, target);  
    }  
    return find_helper(node->right, target);  
}  
  
treeNode<tData>* findParent_helper(treeNode<tData>* node, tData target) {  
    if (!node) {  
        return nullptr;  
    }  
    if ((node->left && node->left->data == target) || (node->right && node->right->data == target)) {  
        return node;  
    }  
    if (target < node->data) {  
        return findParent_helper(node->left, target);  
    } else {  
        return findParent_helper(node->right, target);  
    }  
}
```