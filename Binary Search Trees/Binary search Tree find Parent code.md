```
template <typename T>class nodeAndParent{  
public:  
    treeNode<T>*node;  
    treeNode<T>*Parent;  
    bool isLeft;  
};
nodeAndParent<tData>*FindNodeAndParent(tData value){  
    treeNode<tData>*cur= this->root;  
    treeNode<tData>*parent= nullptr;  
    nodeAndParent<tData>*nodeAndParentInfo= nullptr;  
    bool left= false;  
    while (cur!= nullptr){  
        if (cur->data==value){  
            nodeAndParentInfo=new nodeAndParent<tData>();  
            nodeAndParentInfo->node=cur;  
            nodeAndParentInfo->Parent= parent;  
            nodeAndParentInfo->isLeft=left;  
        } else if (cur->data>value){  
            parent=cur;  
            left= true;  
            cur=cur->left;  
        }else{  
            parent=cur;  
            left= false;  
            cur=cur->right;  
        }  
    }  
    return nodeAndParentInfo;  
}
```