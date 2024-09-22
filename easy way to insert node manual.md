```c++
void addNode(tData value,treeNode<tData>*parent, bool isLeft){  
    treeNode<tData>*newNode=new treeNode<tData>(value);  
    if (isLeft){  
        parent->left=newNode;  
    } else{  
        parent->right=newNode;  
    }  
    nodesCounter++;  
}  
treeNode<tData>*getRoot(){  
    return root;  
}
```

	انت بتقوله كل مره هتنادي ال fun هنعمل ايه هنخزن value في new node وبعدين نحدد على حسب ما هتقوله هل هتروح شمال ولا يمين 

```
main()
tree.addNode(3, tree.getRoot(), true); // Insert 3 as the left child of 2 tree.addNode(13, tree.getRoot(), false); // Insert 13 as the right child of 2 tree.addNode(5, tree.getRoot()->left, true); // Insert 5 as the left child of 3 tree.addNode(8, tree.getRoot()->left, false); // Insert 8 as the right child of 3 tree.addNode(7, tree.getRoot()->right, false); // Insert 7 as the right child of 13 // Print the tree structure or perform other operations to validate cout << "Tree created successfully!" << endl;
```