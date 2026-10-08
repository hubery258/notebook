# C#学习笔记00

> 这篇学习笔记主要是为了在做oa的场地审核前真的让自己了解仓库以及能看得懂代码与全程逻辑，可能包含c#,blazor以及一些仓库基本信息。

## 相关链接

[c#能干嘛](https://learn.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/what-you-can-build)
[c#数据类型总论](https://learn.microsoft.com/zh-cn/dotnet/csharp/fundamentals/types/)

## 学习规划

| 顺序 | 当天怎么学、怎么用 | 完成标准 |
|---|---|---|
| **第 1 天：先读懂“数据长什么样”** | 花 30 分钟读 [C# 导览](https://learn.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/overview)中的类型、类和方法；接着打开 [ProjectMember](D:/Koala/koala-dir-contract/Src/Koala.Dir.ProjectManagementService/Models/ProjectMember.cs)、[HumanUser](D:/Koala/koala-dir-contract/Src/Koala.Dir.UserService/Models/HumanUser.cs) 和 [用户领域对象](D:/Koala/koala-dir-user-service/Src/Koala.Dir.UserService.Domain/User/User.cs:5)。只弄懂 `class`、`record`、属性、方法、`string?`、`private set`。最后用自己的话写下：这三个类型各表示什么，为什么手机号可以为空，为什么用户资料不能随便改属性。 | 不看解释也能读出一个 C# 数据类型有哪些字段、哪些可能缺失。 |
| **第 2 天：读懂“代码怎样筛数据”** | 打开 [GetProjects.cs](D:/Koala/koala-dir-project-management-service/Src/Koala.Dir.ProjectManagementService.Application/RequestHandlers/GetProjects.cs:8)。逐行理解方法参数、`async Task<...>`、`await`、`Where`、`OrderByDescending`、`Skip`、`Take`。不会的地方只查 [异步](https://learn.microsoft.com/en-us/dotnet/csharp/asynchronous-programming/async-scenarios)和 [LINQ](https://learn.microsoft.com/en-us/dotnet/csharp/linq/get-started/write-linq-queries)对应小节。用纸笔拿 5 个虚构项目，手算这段代码会返回哪两个。 | 能解释它为什么只返回已批准项目，分页怎么算，数据库查询在哪一步真正执行。 |
| **第 3 天：读懂“页面怎样调用它”** | 打开 [ProjectList.razor](D:/Koala/koala-dir-webui/Src/Koala.Dir.WebUI.UI/Pages/ProjectManagementService/ProjectList.razor:290)。先认 `@page`、`@inject`、`@code`、按钮事件和页面状态，再找到 `GetProjectsAsync` 的调用与成功、失败处理。按需看 [Blazor 组件文档](https://learn.microsoft.com/en-us/aspnet/core/blazor/components/?view=aspnetcore-10.0)。 | 能指出“点击刷新 → 哪个方法运行 → 页面数据如何更新”。 |
| **第 4 天：把 NOF 接上** | 对照 [IProjectService](D:/Koala/koala-dir-contract/Src/Koala.Dir.ProjectManagementService/IProjectService.cs:24)、[ProjectRpcServer](D:/Koala/koala-dir-project-management-service/Src/Koala.Dir.ProjectManagementService.Application/ProjectManagementServiceRpcServer.cs:5) 和第 2 天的 handler。读 [NOF 公共 API 说明](D:/Koala/NOF/docs/design/public-api.md)的接口与处理器部分。此时学 `interface`、继承、特性 `[HttpEndpoint]` 和泛型；弄清为何接口写 `GetProjects`，页面却调用 `GetProjectsAsync`。 | 能画出“页面 → 生成的客户端 → 契约 → handler → 数据库”的一条线。 |
| **第 5 天：自己模拟一次 review** | 再读 [UserPicker](D:/Koala/koala-dir-webui/Src/Koala.Dir.WebUI.UI/Components/Selectors/UserPicker.razor)，找出搜索、取消旧请求、空结果怎么处理。然后检查项目列表的 `PageSize = 100`：如果门禁要“选择全部项目成员”，只用这个页面结果会发生什么？ | 写一页审查笔记：数据是否完整、空值怎样处理、权限在哪、失败怎样显示、列表是否漏页。 |

## C#工程流程

1. `Main`方法一般放在一个叫`Program`的类里，文件一般叫`Program.cs`
2. C# 9+之后可以直接在文件顶部写代码，不再需要class Program与Main，编译器会自动生成入口点，但一个项目里只能有一个文件用顶层语句

???+ example "示例流程"
```bash
# 1. 创建控制台项目
dotnet new console -n MyMessageApp

# 2. 进入目录
cd MyMessageApp

# 3. 把类型声明文件复制进来，比如命名为 MessageTypes.cs
#    或者直接新建文件粘贴代码

# 4. 编辑 Program.cs，写入 Main 或顶层语句

# 5. 运行
dotnet run

```

## 数据类型

和dart类似，我们在程序中声明变量也可以用`var`来让编译器自己通过输入的value判断类型，类型很多，大概可以分为：

- **值类型**: 变量里直接装数据，赋值时是复制而非修改引用
- **引用类型**: 变量里装的是“对象在哪里”的引用,存地址(有点像C里的指针相关的知识)。

### 内置基本类型

`int`,`double`,`decimal`(用于小数点精准计算),`bool`,`char`,`string`

字符串文本记录: 常规 (`"hello"`)和内插 (`$"value: {x}"`)。

### 类class — 用于处理复杂行为、多态性或可变状态

> 上面提到的内置基本类型都是，大多数自定义类型(type)都是类。

类是一个对象蓝图，包含很多想要定义的东西，每次 new 就是依照蓝图 + 输入参数，构造出一个新的对象(object),因此说对象是类的实例。

一个类通常可以包含：

| 成员 | 作用 |
|---|---|
| 字段 field | 存数据，通常私有 |
| 属性 property | 封装字段，提供 get(查)/set(update) |
| 方法 method | 定义行为 |
| 构造函数 constructor | 创建对象时初始化 |
| 静态成员 static | 属于类，不属于某个对象 |
| 事件 event | 通知机制 |
| 索引器 indexer | 像数组一样访问 |
| 嵌套类型 | 类里再定义类 |

构造函数的名**一定与类的名字相同**；**不能写返回类型** 

!!! example "示例"

    ```csharp
    using System;

    public class Person
    {
        // 属性
        public string Name { get; set; }
        public int Age { get; private set; }
        private int just_example {set;}

        // 构造函数: 一定要与类的名字相同
        public Person(string name, int age)
        {
            Name = name;
            Age = age;
        }

        // 方法
        public void SayHello()
        {
            Console.WriteLine($"你好，我是 {Name}，今年 {Age} 岁。");
        }
    }
    ```

用 `new ClassName()`创建新的对象。

#### 类中常见修饰符

- `public`：公开；
- `private`：私有，只有类内部能访问；
- `protected`: 保护，自己和子类能看;
- `internal`：内部，同一项目能看。

- `virtual`：会写这个方法的默认实现，子类可以用`override`覆盖 
- `override`: 可以覆盖父类的`virtual`方法以及抽象父类里的抽象方法

- `base`: 主要是对父类作读取后的一些操作
    - `base.Method()`： 调用父类的方法
    - `base(...)`：调用父类的构造函数

???+ example "base的具体示例"

    ```csharp
    public class Animal
    {
        public string Name { get; private set; }

        public Animal(string name)
        {
            Name = name;
        }
    }

    public class Dog : Animal
    {
        public string Breed { get; private set; }

        public Dog(string name, string breed)
            : base(name)   // ← 调用父类构造函数 Animal(string name)
        {
            Breed = breed;
        }
    }
    ```

    如果没有 `: base(name)`，编译器会报错，因为 `Animal` 没有无参构造函数。

#### abstract class 抽象类

有时候很多类有类似的属性与方法，但方法又有微小的不同，抽象类可以提供一个 **模板**，其主要特点是

- **不能直接new，必须先被继承**
- 其中可以放**抽象方法，但不能放实现**，且不需要**virtual**子类即可用**override**

拿动物举例，不同动物叫的声音不同，但都要叫，那么简单写:
```csharp
// 下面对继承的笔记也由这个例子展开，可以在需要时回来读读
public abstract class Animal{
    public string name {get; private set;}

    public void Eat()
    {
        Console.WriteLine($"{name} 在吃东西");
    }
    
    public abstract void MakeSound();    
} 

public class Dog : Animal   // Dog 继承 Animal,关于继承见下，一会也会用这个例子
{
    public Dog(string name)
    {
        Name = name // 继承时自动保有父类的属性与方法等等
    }

    public override void MakeSound()
    {
        Console.WriteLine($"{Name} 汪汪叫");
    }
    public void example()
    {
        Console.WriteLine("主要只是为了说明子类可以比父类多更多属性/方法")
    } 
}

public class Cat : Animal
{
    public Cat(string Name)
    {
        name = Name // 继承时自动保有父类的属性与方法等等
    }
    public override void MakeSound()
    {
        Console.WriteLine($"{Name} meow ~");
    }
}
```

#### static class 静态类

- 不能 `new`；
- 所有成员必须是 `static`；
- 不能被继承；
- 常用于工具类、扩展方法容器。

常见：

- Math（Math.Sqrt、Math.Abs）
- **Console**（Console.WriteLine）

相当于一个没有实例化需求的工具箱，我们只是集成调用里面的方法

#### sealed class 密封类

密封类不能被继承，它是继承链的终点。

#### 继承

- 子类自动拥有父类的属性与方法；
- 一个类只能继承一个父类
- 写法见抽象类中的例子

#### 可空引用类型

```csharp
string name = "小明";     // 非空，编译器保证
string? nickname = null; // 可能为 null，用的时候要检查
```

减少空引用问题，减少`NullReferenceException`

#### `using`与`namespace`

`namespace`有点像文件夹，他们可以分类存放各种类，可以组织代码，避免命名冲突

??? example

    ```csharp
    namespace ZooSystem
    {
        public class Dog { }
    }

    namespace SchoolSystem
    {
        public class Dog { }   // 同名不冲突，因为在不同 namespace
    }
    ```

C#10后可以在开头写一行加分号，整个文件就都属于这个命名空间。

而`using`就是快捷使用namespace的方法，没有using每次引用别的namespace的方法都要输入全名，有了using可以减去一部分的输入，我们也可以给namespace起别名:`using Zoo = ZooSystem;`然后输入也可以变得简短

### `record`

> 当你主要关心“里面装了什么数据”，而不是“这个对象有什么复杂行为”时，优先考虑 `record`。

`record` 默认是 record class，也就是引用类型。它自动帮你生成：

- 值相等性（==、Equals、GetHashCode）：不同于class，只要值相同record就能相同
- `ToString()`： 会自动按string输出信息
- `with` 表达式支持

在C# 9引入 `record` 之后，很多团队的风格变成了：

> “只要是数据模型，默认用 record；只有需要复杂行为或身份语义时，才用 class。”也就是说，record 在这些团队里不是“特殊类型”，而是默认选择。原因：

- 代码短，少写一堆样板；
- 自带 ToString，调试和日志方便；
- 支持 with，方便做“复制并修改”；
- 值相等，便于测试和比较。
- 所以有的时候用record只是为了方便

### 数据类型上的实践

- 基本上`models/`存的都是各种数据类型，需要的时候可以去看看类型是什么样的。
- `public string UserId { get; set; } = string.Empty;`, 此处的`= string.Empty`就是赋予默认值为空字符串

## `.NET`常用命令

### 项目创建

```bash
# 查看所有可用模板
dotnet new list

# 控制台应用
dotnet new console -n MyApp

# 类库（编译成 .dll，给别人引用）
dotnet new classlib -n MyLib
```

### 常用

```bash
# 运行当前目录项目
dotnet run

# 编译（不运行）
dotnet build

# 编译并指定 Release 配置
dotnet build -c Release

# 清理编译产物
dotnet clean

# 还原 NuGet 包
dotnet restore

# 查看 .NET 版本信息
dotnet --info
dotnet --version

# 运行某个项目
dotnet run --project MyApp/MyApp.csproj

# 传给程序的参数（Main 的 args）
dotnet run -- arg1 arg2 arg3
```

