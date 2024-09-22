```c++
bool deleteNodeHasChild_helper(tData value) {  
    treeNode<tData>* cur = find(value);  
    if (!cur) {  
        cout << "The node was not found!" << endl;  
        return false;  
    }  
    treeNode<tData>* parent = findParent(value);  
    if (cur->left == nullptr && cur->right != nullptr) {  
        if (parent) {  
            if (parent->left == cur) {  
                parent->left = cur->right;  
            } else if (parent->right == cur) {  
                parent->right = cur->right;  
            }  
        }  
        delete cur;  
        cout << "The node with one child has been deleted!" << endl;  
    } else if (cur->left != nullptr && cur->right == nullptr) {  
        if (parent) {  
            if (parent->left == cur) {  
                parent->left = cur->left;  
            } else if (parent->right == cur) {  
                parent->right = cur->left;  
            }  
        }  
        delete cur;  
        cout << "The node with one child has been deleted!" << endl;  
    } else {  
        cout << "Node has two children; deletion not implemented for this case." << endl;  
        return false;  
    }  
    return true;  
}
```
find father
```c++
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
