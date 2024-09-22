```c++
bool   search_helper(treeNode<tData>*node,tData target){  
    if (!node){  
        return false;  
    }  
    if (node->data==target){  
        return true;  
    }  
    if (target<node->data){  
       return search_helper(node->left,target);  
    }  
  
       return search_helper(node->right,target);  
  
}
```
![[Pasted image 20240825183456.png]]
