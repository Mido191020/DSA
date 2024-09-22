انا عملت دي جوه insertion كل ما بضيف عنصر بزود counter
![[Pasted image 20240807110830.png]]
![[Pasted image 20240807111945.png]]
```
if (newNode== nullptr)  
    return 0;  
int res=1;  
res+= total_nodes_rec_helper(newNode->left);  
res+= total_nodes_rec_helper(newNode->right);  
return res;
```