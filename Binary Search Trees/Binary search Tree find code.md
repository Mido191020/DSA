```c++
    bool IsExist(tData data){
        return BSFind(data)!=NULL;
    }
    treeNode<tData>*BSFind(tData value){
        treeNode<tData>*cur=this->root;
        while (cur!= nullptr){
            if (cur->data==value){
                return cur;
            } else if (value<cur->data){
                cur=cur->left;
            } else{
                cur=cur->right;
            }
        }
        return NULL;
      }
```
