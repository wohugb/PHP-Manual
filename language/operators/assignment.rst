赋值运算符
============================

基本的赋值运算符是“=”。一开始可能会以为它是“等于”，其实不是的。它实际上意味着把右边表达式的值赋给左边的运算数。

赋值运算表达式的值也就是所赋的值。也就是说，“$a = 3”的值是 3。这样就可以做一些小技巧：

<?php

$a = ($b = 4) + 5; // $a 现在成了 9，而 $b 成了 4。

?>
在基本赋值运算符之外，还有适合于所有二元算术，数组集合和字符串运算符的“组合运算符”，这样可以在一个表达式中使用它的值并把表达式的结果赋给它，例如：

<?php

$a = 3;
$a += 5; // sets $a to 8, as if we had said: $a = $a + 5;
$b = "Hello ";
$b .= "There!"; // sets $b to "Hello There!", just like $b = $b . "There!";

?>
注意赋值运算将原变量的值拷贝到新变量中（传值赋值），所以改变其中一个并不影响另一个。这也适合于在很密集的循环中拷贝一些值例如大数组。也可以使用引用赋值，用 $var = &$othervar; 语法。引用赋值意味着两个变量都指向同一个数据，没有任何数据的拷贝。有关引用的更多信息见引用的说明。在 PHP 5中，对象总是通过引用赋值的，除非明确使用新的 clone关键字。
