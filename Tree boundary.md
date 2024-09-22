```
void traverse_left_boundry(treeNode<tData>*node){  
    if (node == nullptr) return;  
  
    cout << node->data << " ";  
  
    if (node->left)  
        traverse_left_boundry(node->left);  
    else if (node->right)  
        traverse_left_boundry(node->right);  
}
tData   traverse_boundry(){  
    return traverse_left_boundry(root);  
}
```
another way
```
void get_boundry(){  
    cout<<data<<" ";  
    if (left){  
        left->get_boundry();  
    }  
    else if (right){  
        right->get_boundry();  
    }  
}
```
