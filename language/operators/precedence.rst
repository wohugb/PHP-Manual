运算符优先级
============================

运算符优先级指定了两个表达式绑定得有多“紧密”。例如，表达式 1 + 5 * 3 的结果是 16 而不是 18 是因为乘号（“*”）的优先级比加号（“+”）高。必要时可以用括号来强制改变优先级。例如：(1 + 5) * 3 的值为 18。如果运算符优先级相同，则使用从左到右的左联顺序。

下表从高到低列出了运算符的优先级。同一行中的运算符具有相同优先级，此时它们的结合方向决定求值顺序。

运算符优先级
结合方向	运算符	附加信息
非结合	clone new	clone 和 new
左	[	array()
非结合	++ --	递增／递减运算符
非结合	~ - (int) (float) (string) (array) (object) (bool) @	类型
非结合	instanceof	类型
右结合	!	逻辑操作符
左	* / %	算术运算符
左	+ - .	算术运算符 和 字符串运算符
左	<< >>	位运算符
非结合	< <= > >= <>	比较运算符
非结合	== != === !==	比较运算符
左	&	位运算符 和 引用
左	^	位运算符
左	|	位运算符
左	&&	逻辑运算符
左	||	逻辑运算符
左	? :	三元运算符
右	 = += -= *= /= .= %= &= |= ^= <<= >>=	赋值运算符
左	and	逻辑运算符
左	xor	逻辑运算符
左	or	逻辑运算符
左	,	多处用到
左联表示表达式从左向右求值，右联相反。

Example #1 结合方向
<?php
$a = 3 * 3 % 5; // (3 * 3) % 5 = 4
$a = true ? 0 : true ? 1 : 2; // (true ? 0 : true) ? 1 : 2 = 2

$a = 1;
$b = 2;
$a = $b += 3; // $a = ($b += 3) -> $a = 5, $b = 5
?>
使用括号可以增强代码的可读性。
Note:

尽管 = 比其它大多数的运算符的优先级低，PHP 仍旧允许类似如下的表达式：if (!$a = foo())，在此例中 foo() 的返回值被赋给了 $a。


