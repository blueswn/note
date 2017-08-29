## 比较运算符

### 三元运算符（Ternary Operator）

另一个条件运算符是“?:”（或三元）运算符 。

Example #3 赋默认值

    <?php
    // Example usage for: Ternary Operator
    $action = (empty($_POST['action'])) ? 'default' : $_POST['action'];

    // The above is identical to this if/else statement
    if (empty($_POST['action'])) {
        $action = 'default';
    } else {
        $action = $_POST['action'];
    }

    ?>

表达式 (expr1) ? (expr2) : (expr3) 在 expr1 求值为 TRUE 时的值为 expr2，在 expr1 求值为 FALSE 时的值为 expr3。
自 PHP 5.3 起，可以省略三元运算符中间那部分。表达式 expr1 ?: expr3 在 expr1 求值为 TRUE 时返回 expr1，否则返回 expr3。

>Note: 注意三元运算符是个语句，因此其求值不是变量，而是语句的结果。如果想通过引用返回一个变量这点就很重要。在一个通过引用返回的函数中语句 return $var == 42 ? $a : $b; 将不起作用，以后的 PHP 版本会为此发出一条警告。

>Note:
建议避免将三元运算符堆积在一起使用。当在一条语句中使用多个三元运算符时会造成 PHP 运算结果不清晰：
Example #4 不清晰的三元运算符行为

    <?php
    // 乍看起来下面的输出是 'true'
    echo (true?'true':false?'t':'f');

    // 然而，上面语句的实际输出是't'，因为三元运算符是从左往右计算的

    // 下面是与上面等价的语句，但更清晰
    echo ((true ? 'true' : 'false') ? 't' : 'f');

    // here, you can see that the first expression is evaluated to 'true', which
    // in turn evaluates to (bool)true, thus returning the true branch of the
    // second ternary expression.
    ?>
