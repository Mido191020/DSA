```c++
void Balance() {  
vector<tData>nodes;  
    InOrderToArray(this->root,nodes);  
    this->root= RecursiveBalance(0,nodes.size()-1,nodes);  
}  
void InOrderToArray(treeNode<tData>*node,vector<tData>&nodes){  
    if (node== nullptr)  
        return;  
    InOrderToArray(node->left,nodes);  
    nodes.push_back(node->data);  
    InOrderToArray(node->right,nodes);  
}  
treeNode<tData>*RecursiveBalance(int start,int end,vector<tData> &nodes){  
    if (start>end){  
        return nullptr;  
    }  
    int mid=(start+end)/2;  
    treeNode<tData>*newNode=new treeNode(nodes[mid]);  
    newNode->left= RecursiveBalance(start,mid-1,nodes);  
    newNode->right= RecursiveBalance(mid+1,end,nodes);  
    return newNode;  
}
```