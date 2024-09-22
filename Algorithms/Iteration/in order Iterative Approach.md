L
V
R
1-احنا عملنا stack عشان نحاكي فكره recursion وعملنا pointer called cur عشان نمشي بيه علي ال root 
2-عملنا 2 while loop الاولي بتوقف البرنامج بعد اما نخلص tree 
التانيه بت check ان cur مش ب null بس ده بسبب اننا بنخلي cur = stack .top
طيب لو مش ب null بندخل اللوب وبعدني ب push  لل stack وبعدين بنروح شمال 
لحد اما نوصل لاخر نود وتبقى cur=null وقتها هنخرج من اللوب دي ونخلي 
cur =stack.top why?becuse it is last vaild value and we print cur
then make the cur=right 
طلما خلصنا الجزئ الشمال هنروح على اليمين  ومتنساش ال stack شغال ازاي 

