# shell知识补全

> 基础的知识不说了,推荐使用tldr解决大多问题，可以`tldr -L zh`变为中文(如果有人翻译成中文的话就有缓存)

## 001 alias

`ls`是`Get-ChildItem`的别名，我们在查询别名时可以: `Get-Alias ls`即可得到：

```shell
CommandType     Name                                               Version    Source   
-----------     ----                                               -------    ------   
Alias           ls -> Get-ChildItem                                                    
```

`select`是`Select-Object`的别名，用于选择对象或属性

特别注意: 同样的命令在`PowerShell` 和 `Linux/类 Unix` shell 里完全不一定是同一个东西，比如`select`

!!! example 
    ```shell
    ls -r -File -Include *.sln,*.slnx,*.csproj |
    Select-Object -First 30 FullName
    ```
    `-r`都很熟悉了，`-File`则是只返回文件不返回目录，`Include`后面就跟**希望匹配的名称模式**; `-First 30`表示最多取前30个对象.

## 002 查询

- `find`: 在指定目录树下递归查找文件或目录，下面记录常用修饰符，别的自己查tldr与help。
    - 通过扩展名查找文件：`find 指定目录 -name '*.ext'`
    - 查找匹配指定名称的目录，不区分大小写：`find 指定目录 -type d -iname '*lib*'`
    - 查找匹配指定模式的文件，排除特定路径：`find 指定目录 -name '*.py' -not -path '*/site-packages/*'`

- `grep`:  在文件中查找内容
    - 在文件中查找模式：`grep "模式字符串" 路径/到/文件1 路径/到/文件2`
    - 查找精确的字符串（禁用 `regex` 式）：`grep [-F|--fixed-strings] "字符串" 路径/到/文件`
    - 在目录中递归查找所有文件中的模式，忽略二进制文件：`grep [-rI|--recursive --binary-files=without-match] "模式字符串" 路径/到/目录`
    - 打印每个匹配项周围、之前或之后的 3 行上下文：`grep --context|--before-context|--after-context 3 "模式字符串" 路径/到/文件`

- `fd`: 升级版`find`,可以自动在当前目录下递归查找
    - 在当前目录中递归查找匹配特定模式的文件：`fd "正则表达式"`
    - 在特定目录中查找文件：`fd "正则表达式" 路径/到/文件`
    - 查找具有特定扩展名的文件：`fd [-e|--extension] 扩展名`
    - 仅查找匹配特定模式的文件夹：`fd "正则表达式" [-t|--type] [d|directory]`
    - 排除匹配特定通配符（glob）模式的文件：`fd "正则表达式" [-E|--exclude] 通配符`
    - 仅在当前目录中查找文件(限制递归深度)：`fd "正则表达式" [-d|--max-depth] 1`

!!! example "一个fd实例"
    我们不妨玩起来，现在有一堆md文档我们不想放到根目录，然而又想保留README在根目录，我们新建了一个`./docs`文件夹，那么指令就是:`fd -e md -d 1 -E "README*" -X mv -t ./docs `即可实现操作，这里比较重要的点:
    - `E`使用**glob**语法,即**专门用来匹配文件名的简易通配符规则**
        - `*`匹配任意长度的字符(包括零个字符)，`?`表示匹配一个字符，`[abc]`表示匹配括号内任意字符,但如果你在上面的README什么都不加的话并不能匹配到`README.md`文件，我们懒得写`.md`就可以直接通配一下
    - `-t`很多时候都表示目标目录
    - `-X`可以一次性把fd的所有结果作为一组参数传递给后面的指令，如果使用`-x`想要指定当前查到的文件要在后面加`{}`表示查到文件的参数位置，然后会查到一次处理一次

- `rg`: Ripgrep，一款递归的行导向搜索工具, 旨在成为 `grep` 的更快替代品。
    - 在当前目录中递归搜索匹配模式的内容：`rg 模式`
    - 在指定文件或目录中递归搜索匹配模式的内容：`rg 模式 路径/到/文件或目录`
    - 包含隐藏文件以及 `.gitignore` 中列出的条目：`rg [-.|--hidden] --no-ignore 模式`
    - 仅搜索文件名匹配通配符（glob）模式的文件（如 `README.*`）：`rg 模式 [-g|--glob] 文件名通配符模式`
    - 仅列出匹配的文件（适用于管道传递给其他命令）：`rg [-l|--files-with-matches] 模式`

!!! inline end tips
    建议用tldr查一下`xargs`,可以实现很多功能。
