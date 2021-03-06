在新版本的 PHP 中使用旧的 PHP 代码
===================================

现在，PHP 已经发展成为一种流行的脚本语言，可以在很多公共的资源里找到可以在自己的脚本中重新利用的代码。PHP 语言的开发者为向下兼容性下了很多功夫，因此在新版本的 PHP 下，老版本的代码应该可以在不作任何改动的情况下（理想地）运行。不过实际上，还是必须对老的代码做一些改动。

有可能影响到老版本的代码的最重要的两点改动分别是：

* 取消了旧的 $HTTP_*_VARS 数组（在函数或者方法中原本是全局变量）。PHP » 4.1.0 版本引入了如下超全局数组变量：$_GET、$_POST、$_COOKIE、$_SERVER、$_FILE、$_ENV、$_REQUEST 以及 $_SESSION。老的 $HTTP_*_VARS 数组，诸如 $HTTP_POST_VARS 等，从 PHP 3 就已经开始使用，它们仍然存在。自 PHP 5.0.0 起, 用 register_long_arrays 设置选项可禁用 长类型的 PHP 预定义变量数组。
* 外部变量不再被默认注册为全局变量。也就是说，从 PHP » 4.2.0 版开始，php.ini 中的设置选项 register_globals 默认值变成了 off。建议用以上提到的超全局数组变量来访问这些值。但可能老的脚本、书籍以及教程都可能建立在该设置为 on 的基础上。如果该选项被设置为 on，则可以在 URL http://www.example.com/foo.php?id=42 中直接使用变量 $id。但不管被设置为 on 还是 off，$_GET['id'] 一直有效。

如果希望了解关于这些改动的细节，请参阅“预定义变量”一章以及其中的连接。
