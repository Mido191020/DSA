![[Pasted image 20240807125223.png]]
```c++
bool search_the_tree_rec_helper(treeNode<tData>*newNode,int value){  
    if (newNode == nullptr)  
        return false;  
    if (newNode->data==value){  
        return true;  
    }  
    if (search_the_tree_rec_helper(newNode->left,value)){  
        return true;  
    }  
    if (search_the_tree_rec_helper(newNode->right,value)){  
        return true;  
    }  
    return false;  
}
```
