```c++
tData findMin_it_helper(treeNode<tData>*node){  
    treeNode<tData>*ans=node;  
    while (ans->left!= nullptr){  
        ans=ans->left;  
    }  
    return ans->data;  
}
```
second
```c++
 tData findMin_rec_helper(treeNode<tData>*node){  
     if (node->left== nullptr){  
         return node->data;  
     }  
     return findMin_rec_helper(node->left);  
}
```
![[Pasted image 20240825211632.png]]
why because left is small elements