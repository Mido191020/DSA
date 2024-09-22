# In-Order Traversal of a Binary Tree (Iterative Approach)

## Code Breakdown

```cpp
void in_order(tree* root) {
    stack<tree*> stack;
    tree* cur = root;
    
    while (cur != nullptr || !stack.empty()) {
        while (cur != nullptr) {
            stack.push(cur);
            cur = cur->left;
        }
        cur = stack.top();
        stack.pop();
        cout << cur->value << " ";
        cur = cur->right;
    }
}
```
## Visual Representation

```
    1
   / \
  2   3
 / \
4   5

Step-by-step:

هو بيطبع ازاي؟
 Push 1, 2, 4
 تمام حلو بيطبع 4 
 وبعيدن بيروح right بتاع ال 4 الهو (null)
 stack->1,2
 طالما هوcur= null
 كده مش هيدخل loop الجوه وهيروح يطبع ال top بتاعه ويقف على cur->2
 هنا وقتها هروح right وادخل inner loop 
 هعملها push 
  stack->1,5
 ملهاش حاجة شمال صح؟اه خلاص هخرج واطبع 5
   stack->1
   هروح يمين 5 مفيش خلاص هطبع ال 1 واروح يمين ال1 
 
```