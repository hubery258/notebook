## 1. 环境变量

环境变量可以理解成：

> Windows 给程序看的一张“全局便签”。

比如你设置：

```text
ANDROID_HOME = C:\Users\20192\AppData\Local\Android\Sdk
```

意思是在告诉 Flutter、Gradle、Android 工具：

> Android SDK 放在这个目录里，你要找东西就来这里找。

`ANDROID_HOME` 和 `ANDROID_SDK_ROOT` 都是这种“指路便签”。不同工具、不同版本可能读不同的名字，所以最省事的做法是两个都设成同一个路径。

## 2. PATH

`PATH` 也是一个环境变量，但它很特殊：

> Windows 用它来决定：当你输入一个命令时，应该去哪些目录里找对应的 `.exe`。

例如你现在输入：

```powershell
adb
```

Windows 会去 `PATH` 里的一个个目录中找：

```text
adb.exe
adb.bat
adb.cmd
```

如果没找到，就会报：

```text
adb : 无法将“adb”项识别为 cmdlet、函数、脚本文件或可运行程序的名称
```

所以我们要把：

```text
C:\Users\20192\AppData\Local\Android\Sdk\platform-tools
```

加入 `PATH`，这样你才能在任意目录下使用 `adb`。

## 3. 两者的关系

| 东西 | 作用 |
|---|---|
| `ANDROID_HOME` | 告诉工具 SDK 在哪里 |
| `ANDROID_SDK_ROOT` | 同样是告诉工具 SDK 在哪里，兼容不同工具 |
| `PATH` | 让 `adb`、`sdkmanager` 成为全局命令 |
| `PATH` 里的 `platform-tools` | 让 `adb` 可以直接输入 |
| `PATH` 里的 `cmdline-tools\latest\bin` | 让 `sdkmanager`、`avdmanager` 可以直接输入 |

简单说：

- `ANDROID_HOME` 是地址。
- `PATH` 是命令搜索目录列表。
- 两者不是一回事，通常都要配。

## 4. 用户变量、系统变量、当前进程变量

Windows 里环境变量大致分三层：

1. **当前进程变量**  
   只在当前 PowerShell 窗口有效，关掉就消失。  
   例如：

   ```powershell
   $env:ANDROID_HOME = "..."
   ```

2. **用户变量**  
   只对当前 Windows 用户生效，不需要管理员权限。  
   推荐你使用这一层。

3. **系统变量**  
   对所有用户生效，需要管理员权限。  
   个人开发环境一般不动系统变量。

设置完成后，**已经打开的终端不会自动刷新**。你要关掉旧 PowerShell，重新打开一个新的，变量才会生效。


