
**Definition**: The diameter (or width) of a binary tree is the length of the longest path between any two nodes in the tree. This path can pass through the root or any other node.
<mark style="background: #BBFABBA6;"><mark style="background: #CACFD9A6;">depth for each node </mark></mark>
this the idea behind the 
problem
so to make this we will dealing 
with each node as it may be
root that has left, right
then calculate the depth of it 
find the LH ,then find RH then
make LH+RH 
that mean we use post-order DFS
so after we find the Sum of them we store them
because we wont to find the max of them not 
the first path so we need to store them in varible
this should be global or based by reference 
then now we should make the step of calucate
the max between (RH,LF +1) i dont understand this 
as this mean we go to find the hight or what
we get the max depth to know the depth between 
each one as if we have this tree the max depth=2.
look easy way to calculate depth is to calculate it by
level but from the leaf to the root this more easy. 
```c

int depth(TreeNode* node) {
    if (node == nullptr)
        return 0;  // Base case: If the node is null, its depth is 0 (we've reached a leaf's child).
    
    int left_depth = depth(node->left);  // Recursively calculate the depth of the left subtree.
    int right_depth = depth(node->right);  // Recursively calculate the depth of the right subtree.
    
    int current_diameter = left_depth + right_depth;  // Diameter at the current node.
    maxDiameter = max(maxDiameter, current_diameter);  // Update the maximum diameter if necessary.
    
    return 1 + max(left_depth, right_depth);  // Return the depth of the current node.
}
int diameterOfBinaryTree(TreeNode* root) {

        depth(root); // Start the depth-first search from the root

        return maxDiameter; // Return the maximum diameter found

    }
    
```

### Why Return Depth Instead of Diameter?
	ببساطة عشان انا لو جبت right depth وجبت left depth كل الهيكون باقيلي اني اجمعهم وارجع max بتاعهم بس كده .
	By returning the depth, you can calculate the diameter without needing a separate computation for it.


![[Pasted image 20240917001521.png]]
