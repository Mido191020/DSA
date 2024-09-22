```c++
bool delete_child_helper(tData value) {  
    treeNode<tData>* cur = find(value);  
    if (!cur) {  
        cout << "The node was not found!" << endl;  
        return false;  
    }  
    if (cur == root) {  
        delete cur;  
        root = nullptr;  
        cout << "The root node has been deleted!" << endl;  
        return true;  
    }  
    treeNode<tData>* parent = findParent(value);  
    if (parent) {  
        if (parent->left == cur) {  
            parent->left = nullptr;  
        } else if (parent->right == cur) {  
            parent->right = nullptr;  
        }  
    }  
    delete cur;  
    cout << "The node has been deleted!" << endl;  
    return true;  
}
```
i should find what i want to delete first 
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
```
