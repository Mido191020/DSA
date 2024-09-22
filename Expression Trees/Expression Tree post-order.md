بص احنا محتاجين نقسم المسئلة لتلت اجزاء 
	print post order, check is number, insert the elements
	 post order->LRV
	 تاني حاجة محتاج اشوف ال input ده num or operator 
	 لو num ه push في stack هفضل a push untile i find operator 
	 اول ما الاقي operator هدخل على else
	 هنا محتاجين نفتكر مبدا LIFO بتاع stack عشان كده انا بدخل على right الاول

first part
```
void print_post_order_helper(treeNode<tData>*node){  
    if (node== nullptr)  
        return;  
    print_post_order_helper(node->left);  
    print_post_order_helper(node->right);  
    cout<<node->data<<" ";  
}
```
second
```
bool isOperand(char c) {  
    // Returns true if 'c' is not an operator, meaning it's an operand  
    return !(c == '+' || c == '-' || c == '*' || c == '/');  
}
```
third
```
binaryTree(string &s) {  
    stack<char> st;  
    for(auto c:s){  
        if (isOperand(c)){  
            st.push(new treeNode<tData>(c));  
        } else{  
            treeNode<tData>*newNode=new treeNode<tData>(c);  
            //the resoan is we are using stack so we should revers  
            newNode->right=st.top();st.pop();  
            newNode->left=st.top();st.pop();  
            st.push(newNode);  
        }  
    }  
    root=st.top();  
}
```
![[Pasted image 20240816010803.png]]
