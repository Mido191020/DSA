```
void clear_hlepr(treeNode<tData>*node){  
    if(node== nullptr){  
        return;  
    }  
    clear_hlepr(node->left);  
    clear_hlepr(node->right);  
    cout<<"delete node with value: "<<node->data<<"\n";  
    delete node;  
}
void clear(){  
    clear_hlepr(root);  
    root= nullptr;  
    std::cout << "The root has been deleted!\n";  
}
```
	زي ما متعودين بنقسم الدنيا ل sub tree وبعد كده بنشتغل هنا المفروض امسح كل حاجة الاول قبل ما امسح ال root عشان بنكتب c++ طيب هنمسح ال left وبعدين ال right وبعدين في الاخر مش هيكون باقي غير root انا مسحت كل nodes المرتبطة بيه فخلاص كده تقدر دلوقتي تخليه ب null عادي زي ما عملنا في clear