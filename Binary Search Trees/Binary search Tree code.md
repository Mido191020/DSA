````cpp fold

template <typename tData>class treeNode{  
public:  
  tData data;  
  treeNode<tData>*left;  
    treeNode<tData>*right;  
    treeNode(tData data):data(data),left(nullptr),right(nullptr){  
  
    }  
};  
template <typename T>class nodeAndParent{  
public:  
    treeNode<T>*node;  
    treeNode<T>*Parent;  
    bool isLeft;  
};  
template <typename tData>class BinaryTree{  
private:  
    treeNode<tData>*root;  
    int internalHeight(treeNode<tData>*node){  
        if (node== nullptr){  
            return 0;  
        }  
        return 1+max(internalHeight(node->left),internalHeight(node->right));  
    }  
    void internalPreOrder(treeNode<tData>*node){  
      if(node== nullptr){  
          return;  
      }  
      cout<<node->data<<"->";  
        internalPreOrder(node->left);  
        internalPreOrder(node->right);  
    }  
   void internalInOrder(treeNode<tData>*node) {  
       if (node== nullptr){  
           return;  
       }  
       internalInOrder(node->left);  
       cout<<node->data<<"->";  
       internalInOrder(node->right);  
   }  
   void internalPostOrder(treeNode<tData>*node){  
       if (node== nullptr){  
           return;  
       }  
       internalPostOrder(node->left);  
       internalPostOrder(node->right);  
       cout<<node->data<<"->";  
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
    void BSDelete_Has_Childs(treeNode<tData>*nodeToDelete){  
        treeNode<tData>*cur=nodeToDelete->right;  
        treeNode<tData>*parent= nullptr;  
        while (cur->left!= nullptr){  
            parent=cur;  
            cur=cur->left;  
        }  
        //what is this  
        if (parent!= nullptr){  
            //why  
            parent->left=cur->right;  
        } else{  
            nodeToDelete->right=cur->right;  
        }  
        nodeToDelete->data=cur->data;  
        delete cur;  
    }  
    void BSDelete_Has_One_Child(treeNode<tData> *nodeToDelete){  
        treeNode<tData>*nodeToReplace= nullptr;  
        if (nodeToDelete->left!= nullptr){  
            nodeToReplace=nodeToDelete->left;  
        } else{  
            nodeToReplace=nodeToDelete->right;  
        }  
        nodeToDelete->data=nodeToReplace->data;  
        nodeToDelete->left=nodeToReplace->left;  
        nodeToDelete->right=nodeToReplace->right;  
        delete nodeToReplace;  
    }  
    void BSDelete_leaf(nodeAndParent<tData>*nodeAndParentInfo){  
        if (nodeAndParentInfo->Parent== nullptr){  
            this->root= nullptr;  
        } else{  
            if (nodeAndParentInfo->isLeft){  
                nodeAndParentInfo->Parent->left= nullptr;  
            } else{  
                nodeAndParentInfo->Parent->right= nullptr;  
            }  
        }  
    }  
public:  
    BinaryTree(){  
        root= nullptr;  
    }  
    ~BinaryTree(){  
        delete root;  
    }  
    void Insert(tData value){  
        treeNode<tData>*newNode=new treeNode<tData>(value);  
       //Checks if the tree is empty (root is null)  
        //If empty, sets the new node as the root and returns        if (this->root== nullptr){  
            this->root=newNode;  
            return;  
        }  
    queue<treeNode<tData>*>q;  
        q.push(this->root);  
        while (!q.empty()){  
            treeNode<tData>*currentNode=q.front();  
            q.pop();  
            if (currentNode->left== nullptr){  
                currentNode->left=newNode;  
                break;  
            } else{  
                q.push(currentNode->left);  
            }  
            if (currentNode->right== nullptr){  
                currentNode->right=newNode;  
                break;  
            } else{  
                q.push(currentNode->right);  
            }  
        }  
    }  
    int Height(){  
        //rember in kinked list we give the head  
        //here we give the root        return this->internalHeight(this->root);  
    }  
   void PostOrder() {  
       internalPostOrder(root);  
       cout<<"\n";  
    }  
    void InOrder(){  
        internalInOrder(root);  
        cout<<"\n";  
    }  
    void PreOrder(){  
        internalPreOrder(root);  
        cout<<"\n";  
    }  
## Binary search TREE



    void BSInsert(tData value){  
        treeNode<tData>*newNode=new treeNode<tData>(value);  
        //Checks if the tree is empty (root is null)  
        //If empty, sets the new node as the root and returns        if (this->root== nullptr){  
            this->root = newNode;  
            return;}  
  treeNode<tData>*cur=root;  
            while (cur!= nullptr){  
                if (value<cur->data){  
                    if (cur->left== nullptr){  
                        cur->left=newNode;  
                        break;  
                    } else{  
                        cur=cur->left;  
                    }  
                }else{  
                    if (cur->right== nullptr){  
                        cur->right=newNode;  
                        break;  
                    } else{  
                        cur=cur->right;  
                    }  
                }  
            }  
    }  
    bool IsExist(tData data){  
        return BSFind(data)!=NULL;  
    }  
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
    void BsDelete(tData value){  
        nodeAndParent<tData>*nodeAndParentInfo= FindNodeAndParent(value);  
        if (nodeAndParentInfo== nullptr){  
            return;  
        }  
        if (nodeAndParentInfo->node->left!= nullptr  
        &&nodeAndParentInfo->node->right!= nullptr){  
            BSDelete_Has_Childs(nodeAndParentInfo->node);  
        } else if (nodeAndParentInfo->node->left!= nullptr  
        ^nodeAndParentInfo->node->right!= nullptr){  
            BSDelete_Has_One_Child(nodeAndParentInfo->node);  
        } else{  
            BSDelete_leaf(nodeAndParentInfo);  
        }  
    }  
  
};
```