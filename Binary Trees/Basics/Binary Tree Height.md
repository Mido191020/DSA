![[Pasted image 20240807110238.png]]
```
if (newNode== nullptr)  
    return -1;  
int leftHeight=tree_height_rec_helper(newNode->left);  
int rightHeight=tree_height_rec_helper(newNode->right);  
return max(leftHeight,rightHeight)+1;
```