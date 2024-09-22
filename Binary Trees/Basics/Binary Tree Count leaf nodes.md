![[Pasted image 20240807120314.png]]
```
int  Count_leaf_nodes_helper(treeNode<tData>*newNode){  
    if (newNode== nullptr)  
        return 0;  
    if (newNode->left== nullptr&&newNode->right== nullptr){  
        return 1;  
    }  
    return  Count_leaf_nodes_helper(newNode->left)+Count_leaf_nodes_helper(newNode->right);  
}
```