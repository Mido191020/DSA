```c++
tData findMax_it_helper(treeNode<tData>*node){  
    treeNode<tData>*ans=node;  
    while (ans->right!= nullptr){  
        ans=ans->right;  
    }  
    return ans->data;  
}
```
second
```c++
tData findMax_rec_helper(treeNode<tData>*node){  
    if (node->right== nullptr){  
        return node->data;  
    }  
    return findMax_rec_helper(node->right);  
}
```