```
void insertLevelOrder(treeNode<tData>* newNode) {  
    if (root == nullptr) {  
        root = newNode;  
        nodesCounter++;  
        return;  
    }  
  
    queue<treeNode<tData>*> q;  
    q.push(root);  
  
    while (!q.empty()) {  
        treeNode<tData>* currentNode = q.front();  
        q.pop();  
  
        if (currentNode->left == nullptr) {  
            currentNode->left = newNode;  
            nodesCounter++;  
            return;  
        } else {  
            q.push(currentNode->left);  
        }  
  
        if (currentNode->right == nullptr) {  
            currentNode->right = newNode;  
            nodesCounter++;  
            return;  
        } else {  
            q.push(currentNode->right);  
        }  
    }  
}
```