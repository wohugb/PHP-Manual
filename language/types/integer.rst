.. _int:

整型
=====================

一个 integer 是集合 Z = {..., -2, -1, 0, 1, 2, ...} 中的一个数。

.. seealso::

 * 任意长度整数 / GMP
 * 浮点数
 * 任意精度数学库 / BCMath

语法
----

整型值可以使用十进制，十六进制或八进制表示，前面可以加上可选的符号（- 或者 +）。

八进制表示数字前必须加上 0（零），十六进制表示数字前必须加上 0x。

例 #1 整数文字表达

.. code-block:: php

 <?php
   $a = 1234; // 十进制数
   $a = -123; // 负数
   $a = 0123; // 八进制数 (等于十进制 83)
   $a = 0x1A; // 十六进制数 (等于十进制 26)
 ?>

整型(integer)的形式描述:

.. code-block:: ini

 decimal     : [1-9][0-9]*
             | 0

 hexadecimal : 0[xX][0-9a-fA-F]+

 octal       : 0[0-7]+

 integer     : [+-]?decimal
             | [+-]?hexadecimal
             | [+-]?octal

整型数的字长和平台有关，尽管通常最大值是大约二十亿（32 位有符号）。PHP 不支持无符号整数。Integer值的字长可以用常量 ``PHP_INT_SIZE`` 来表示，自 PHP 4.4.0 和 PHP 5.0.5后，最大值可以用常量PHP_INT_MAX来表示。

.. warning:: 如果向八进制数传递了一个非法数字（即 8 或 9），则后面其余数字会被忽略。

例 #2 八进制数的怪事

.. code-block:: php

 <?php
   var_dump(01090); // 八进制 010 = 十进制 8
 ?>

整数溢出
--------

如果给定的一个数超出了 integer 的范围，将会被解释为 float。同样如果执行的运算结果超出了 integer 范围，也会返回 float。

.. code-block:: php

 <?php
  $large_number =  2147483647;
  var_dump($large_number);
 // 输出为：int(2147483647)

 $large_number =  2147483648;
 var_dump($large_number);
 // 输出为：float(2147483648)

 // 同样也适用于十六进制表示的整数： 从 2^31 到 2^32-1:
 var_dump( 0xffffffff );
 // 输出: float(4294967295)

 // 不适用于大于 2^32-1　的十六进制表示的数:
 var_dump( 0x100000000 );
 // 输出: int(2147483647)
 
 $million = 1000000;
 $large_number =  50000 * $million;
 var_dump($large_number);
 // 输出: float(50000000000)
 ?>

.. warning:: 不幸的是 PHP 中有个 bug，因此当有负数参与时结果并不总是正确。例如当运算 -50000 * $million 时结果是 -429496728。不过当两个运算数都是正数时就没问题。

这个问题已经在 PHP 4.1.0 中解决了。

PHP 中没有整除的运算符。1/2 产生出 float 0.5。可以总是舍弃小数部分，或者使用 round() 函数。

.. code-block:: php

 <?php
  var_dump(25/7);         // float(3.5714285714286) 
  var_dump((int) (25/7)); // int(3)
  var_dump(round(25/7));  // float(4) 
 ?>

转换为整型
----------

要明确地将一个值转换为 integer，用 (int) 或 (integer) 强制转换。不过大多数情况下都不需要强制转换，因为当运算符，函数或流程控制需要一个 integer 参数时，值会自动转换。还可以通过函数 intval() 来将一个值转换成整型。

.. seealso:: 类型转换的判别.

从布尔值转换
------------

FALSE 将产生出 0（零），TRUE 将产生出 1（壹）。

从浮点数转换
------------

当从浮点数转换成整数时，将向零取整。

如果浮点数超出了整数范围（通常为 +/- 2.15e+9 = 2^31），则结果不确定，因为没有足够的精度使浮点数给出一个确切的整数结果。在此情况下没有警告，甚至没有任何通知！

.. warning:: 决不要将未知的分数强制转换为 integer，这样有时会导致不可预料的结果。

.. code-block:: php

 <?php
  echo (int) ( (0.1+0.7) * 10 ); // 显示 7!
 ?>

.. seealso:: 关于浮点数精度的警告。

从字符串转换
------------

.. seealso:: 字符串转换为数字

从其它类型转换
--------------

.. caution:: 没有定义从其它类型转换为整型的行为。不要依赖任何可见的行为，因为它会未加通知地改变。
