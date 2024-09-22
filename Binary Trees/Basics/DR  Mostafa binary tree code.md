```c++
#include <iostream>  
#include <queue>  
#include <cassert>  
#include <cmath>  
  
using namespace std;  
  
template <typename tData>  
class treeNode {  
public:  
    tData data{};  
    treeNode<tData>* left{};  
    treeNode<tData>* right{};  
    treeNode(tData data) : data(data) {}  
};  
  
template <typename tData>  
class binaryTree {  
private:  
    treeNode<tData>* root{};  
    static int nodesCounter;  
    // Helper method for level-order insertion  
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
    tData tree_max_helper(treeNode<tData>*node){  
  
        if (node== nullptr)  
            return -1;  
        tData maxL=tree_max_helper(node->left);  
        tData maxR=tree_max_helper(node->right);  
        return max(node->data, max(maxL,maxR));  
    }  
    int  tree_height_rec_helper(treeNode<tData>*newNode){  
        if (newNode== nullptr)  
            return -1;  
        int leftHeight=tree_height_rec_helper(newNode->left);  
        int rightHeight=tree_height_rec_helper(newNode->right);  
        return max(leftHeight,rightHeight)+1;  
    }  
    int total_nodes_rec_helper(treeNode<tData>*newNode){  
        if (newNode==nullptr)  
            return 0;  
        int res=1;  
        res+= total_nodes_rec_helper(newNode->left);  
        res+= total_nodes_rec_helper(newNode->right);  
        return res;  
    }  
    int  Count_leaf_nodes_helper(treeNode<tData>*newNode){  
        if (newNode== nullptr)  
            return 0;  
        if (newNode->left== nullptr&&newNode->right== nullptr){  
            return 1;  
        }  
        return  Count_leaf_nodes_helper(newNode->left)+Count_leaf_nodes_helper(newNode->right);  
    }  
    bool search_the_tree_rec_helper(treeNode<tData>*newNode,int value){  
        if (newNode == nullptr)  
            return false;  
        if (newNode->data==value){  
            return true;  
        }  
        if (search_the_tree_rec_helper(newNode->left,value)){  
            return true;  
        }  
        if (search_the_tree_rec_helper(newNode->right,value)){  
            return true;  
        }  
        return false;  
    }  
    bool is_perfect_rec_helper(treeNode<tData>* node, int depth, int currentLevel) {  
        if (node == nullptr) {  
            // An empty node (subtree) is perfect  
            return true;  
        }  
  
        if (node->left == nullptr && node->right == nullptr) {  
            // We are at a leaf node  
            // Check if this leaf node is at the correct depth            return (depth == currentLevel + 1);  
        }  
  
        if (node->left == nullptr || node->right == nullptr) {  
            // An internal node must have both left and right children  
            return false;  
        }  
  
        // Recursively check if both left and right subtrees are perfect  
        bool leftPerfect = is_perfect_rec_helper(node->left, depth, currentLevel + 1);  
        bool rightPerfect = is_perfect_rec_helper(node->right, depth, currentLevel + 1);  
  
        // The current tree is perfect if both subtrees are perfect  
        return leftPerfect && rightPerfect;  
    }  
public:  
    binaryTree(tData root_value) {  
        root = new treeNode<tData>(root_value);  
        nodesCounter = 1;  
    }  
  
    void Insert(tData value) {  
        treeNode<tData>* newNode = new treeNode<tData>(value);  
        insertLevelOrder(newNode);  
    }  
    void print_inorder() {  
        print_inorder(root);  
        cout << "\n" << nodesCounter << "\n";  
    }  
    void print_inorder(treeNode<tData>* cur) {  
        if (cur == nullptr)  
            return;  
        print_inorder(cur->left);  
        cout << cur->data << " ";  
        print_inorder(cur->right);  
    }  
    int total_nodes() {  
        return nodesCounter;  
    }  
    tData tree_max() {  
        return tree_max_helper(root);  
    }  
    int  tree_height_rec(){  
        return tree_height_rec_helper(root);  
    }  
    int total_nodes_rec(){  
       return total_nodes_rec_helper(root);  
    }  
    int  Count_leaf_nodes(){  
        return Count_leaf_nodes_helper(root);  
    }  
   bool Search_the_tree_it(int value){  
       treeNode<tData>*newNode=root;  
       if (newNode->data==value){  
           return true;  
       }  
       else {  
           treeNode<tData>*cur=newNode;  
           while (cur!= nullptr){  
               if (cur->left->data==value){  
                   return true;  
               } else{  
                   cur=cur->left;  
               }  
               if (cur->right->data==value){  
                   return true;  
               } else{  
                   cur=cur->right;  
               }  
  
           }  
  
       }  
       return false;  
    }  
    bool search_the_tree_rec(int value){  
  
        return search_the_tree_rec_helper(root,value);  
    }  
    bool is_perfect(){  
       int depth=tree_height_rec();  
        return is_perfect_rec_helper(root,depth,0);  
    }  
  
};  
  
// Define and initialize the static member outside the class  
template <typename tData>  
int binaryTree<tData>::nodesCounter = 0;  
  
int main() {  
    binaryTree<int> tree(2);  
    tree.Insert(3);  
    tree.Insert(13);  
    tree.Insert(7);  
    tree.Insert(9);  
    //tree.Insert(10);  
    tree.Insert(15);  
    tree.print_inorder();  
    //cout << "Max Value: " << tree.tree_max() << endl;  
    //cout << "Total Nodes: " << tree.total_nodes() << endl;cout<<tree.is_perfect();  
    return 0;  
}
```