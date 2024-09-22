	بص يبشا انت بتمشي ب ايه ب sub trees حلو 
بص يا حبيب اخوك دلوقتي انا عاوز اضيف 20 دي 
![[Pasted image 20240825190456.png]]
هعمل ايه اول حاجة محتاج احدد 
![[Pasted image 20240825190601.png]]
تمام يا بيه حددت دلوقتي انا رايح يمين حلو ايه بعد كده المفروض ابقى عارف شغال على انهي sub tree
![[Pasted image 20240825190728.png]]
والله انا شغال على دي حلو هنا محتاج احدد برضه حاجة مهمة 
![[Pasted image 20240825190918.png]]
طيب حددت بعد كده بشوف هل يمين ال 16 في حاجة قالي لا قولتله حلو خلاص يمينك دلوقتي بقى 20 بس كده 

```c++
void insert_helper(treeNode<tData>*node,int target){  
    if (node== nullptr){  
        node=new treeNode<tData>(target);  
        return;  
    }  
    if (target<node->data){  
        insert_helper(node->left,target);  
    }  
    else if (target>node->data){  
        insert_helper(node->right,target);  
    }  
}
```