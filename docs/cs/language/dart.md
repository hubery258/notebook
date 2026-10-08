# dart

> 暂时只是为了项目粗学内容，后续完善

!!! info "相关链接"
    [Dart 语言](https://dart.dev/language)
    [DartPad codespace ](https://dartpad.dev/)
    [dart cheatsheet](https://dart.dev/resources/dart-cheatsheet)

1. 使用`var`,dart里的变量可以不自己指定类型，它们会类型推理自动把类型**设置为初始值的类型**:
```dart
var name = 'Voyager I';
var year = 1977;
var antennaDiameter = 3.7;
var flybyObjects = ['Jupiter', 'Saturn', 'Uranus', 'Neptune'];
var image = {
  'tags': ['saturn'],
  'url': '//path/to/saturn.jpg',
};
```

---

2. dart的loop规则比较常规，小特性是可以多层退出loop，一般默认break/continue都只在一层中运行，但:
```dart
outerLoop:
for (var i = 1; i <= 3; i++) {
  for (var j = 1; j <= 3; j++) {
    if (i == 2 && j == 2) {
      break outerLoop; // 直接跳出两层循环
    }
  }
}
```

---

3. dart的branch当然支持常规ifelse，但新东西比较多:

> `if-case` = 单模式匹配 + 解构 + if/else  
> `switch` = 多模式匹配 + 分派，还能作为表达式返回值。  
> 匹配成功后，模式里的变量只在对应分支里可用。

首先是case可以匹配的变多了:

```dart
case >= digit0 && <= digit9:
case slash || star || plus || minus:
```

我们可以拿`if-case`测试针对单个模式匹配和解绑变量的操作，而测试多个模式可以用`switch`:

!!! example 

    ```dart
    if (pair case [int x, int y]) {
      return Point(x, y);
    } else {
      throw FormatException('Invalid coordinates.');
    }
    ```

`if (<某种值> case <一种模式>) {A} else {B}`如果值匹配模式，则执行A，否则B，在上面例子中也就要求pair要是一个list，长度2，第一个第二个元素都是int，分别绑定到x，y上

??? example "more example on if-case"

    ```dart
    void main() {
      var test = 20;
      if ( test case (int x) ){
        print("yes,${x}");
      } else {
        print("no,${x}");
      }
    }
    ```
    这个情况下代码是有问题的，因为else就说明不符合模式，那么就不可能绑定出x，这里的`"no,${x}"`就属于出现了undefined name，无法编译。而可以尝试把test的定义删掉，把if条件里的test改成`30`,我们也会得到`yes.30`
list.map((x) => x * 2)

// 等价于
list.map((x) {
  return x * 2;
})
而`switch`的特点就是可以匹配多个模式:
```dart
switch (pair) {
  case [int x, int y]:
    return Point(x, y);
  case [int x]:
    return Point(x, 0);
  default:
    throw FormatException('Invalid coordinates.');
}
```
稍加注意，dart中如果switch-case里case xx有语句，那么就会执行完后自动结束，不会再往下执行case。

---

3. 关于异常(exception)

> 说来惭愧，大二了其实我对异常也只处于"知道"的阶段，这里算是第一次真正了解异常。
>
> 异常就是程序出问题时“扔出一个错误”，你可以选择接住处理，也可以不接。Dart 不强迫你接；不接的话，当前 isolate 会停，通常程序就挂了。

我们可以`throw`异常与错误，存在两个自带的可以用的子类，`Exception`与`Error`，Exception是可以处理的异常，而Error则是本不该发生的错误,就像取钱时余额不足是Exception，而取一个负数金额应该是Error。

简单理解dart下的异常处理:
```dart
try {
  // 可能出错的代码
} on FormatException catch (e) {
  // 只抓 FormatException，并拿到错误对象 e
} catch (e, s) {
  // 抓所有错误，e 是错误对象，s 是堆栈
} finally {
  // 不管出不出错，最后都执行，常用于清理
}
```

`assert`是开发时启用的东西，第一个参数必须是可以判断bool值表达式，如果bool值为1，则继续，否则停止运行，若还跟了字符串参数可以弹出字符串

??? example "详细例子"

    ```dart
    void main() {
      try {
        withdraw(100, 30);   // 成功
        withdraw(100, 200);  // 余额不足，抛 Exception
      } on ArgumentError catch (e) {
        print('参数错误：$e');
      } catch (e, s) {
        print('其他错误：$e');
        print('堆栈：$s');
      } finally {
        print('无论如何，收尾');
      }
    }
    ```

    运行结果大致是：

    ```
    取款成功，剩余 70.0
    其他错误：Exception: 余额不足
    堆栈：...
    无论如何，收尾
    ```

    读法：

    1. `try` 里代码从上往下跑。
    2. 第一次 `withdraw(100, 30)` 成功。
    3. 第二次 `withdraw(100, 200)` 扔出 `Exception('余额不足')`。
    4. 找匹配的 `catch`：
       - `on ArgumentError` 不匹配。
       - `catch (e, s)` 匹配，接住。
    5. 打印错误和堆栈。
    6. `finally` 一定执行。

---

5. function: 最好参数的type还是要准确的，然后有一个新语法`=>`
```dart
int add(int a, int b) => a + b;

// 等价于
int add(int a, int b) {
  return a + b;
}

//匿名函数

list.map((x) => x * 2)

// 等价于
list.map(
    (x) {
        return x * 2;
    })
```

---

6. 
