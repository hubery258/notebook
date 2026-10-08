# SQL

!!! info "相关链接"
    [过去笔记](https://note.ramenboy.cc/cs/cs50x/sql/)  
    [docs](https://www.sqlite.org/docs.html)  
    [sqlite的datatype](https://www.sqlite.org/datatype3.html)
    [sqlite的外键约束](https://sqlite.org/foreignkeys.html)
    [sqlite中文文档](https://www.dba.cn/book/sqlite/)

简单地说SQL就是支持对数据库进行CRUD操作的语言，我们掌握SQL是为了操作数据库，`sqlite3`则是一个轻量化sql数据库。

??? note "兴趣了解:SQL里的宏观结构"

    ```
    SQL
    ├─ 1. 语句/命令层：SELECT、INSERT、UPDATE、CREATE、GRANT、COMMIT...
    │
    └─ 2. 语句内部结构层
        ├─ 子句 clause：SELECT、FROM、WHERE、GROUP BY、HAVING、ORDER BY...
        ├─ 关键字 keyword：DISTINCT、AS、AND、OR、JOIN、ON...
        ├─ 表达式 expression：列名、常量、运算符、函数调用、CASE...
        │   ├─ 函数 function
        │   │   ├─ 标量函数：LOWER、UPPER、ROUND...
        │   │   ├─ 聚合函数：AVG、COUNT、MAX、MIN、SUM...
        │   │   └─ 窗口函数：ROW_NUMBER、RANK、SUM() OVER...
        │   ├─ 运算符 operator：+、-、=、>、AND、OR...
        │   └─ 标识符 identifier：表名、列名、别名、schema...
        └─ 谓词 predicate：WHERE 里的条件，如 LIKE、IN、BETWEEN、IS NULL...
    ```

    > **语句/命令是最外层；子句是语句的组成部分；函数只是表达式里的零件；关键字是语法标记。**

    再具体一点：

    - **SQL 语句/命令**：这是最外层。比如 `SELECT` 是查询语句，`INSERT` 是插入语句，`CREATE` 是定义语句。平时说“SQL 指令”大致对应这一层，但更标准的说法是“SQL 语句”或“命令”。
    - **子句**：一个语句由多个子句组成。比如 `SELECT ... FROM ... WHERE ... GROUP BY ... HAVING ... ORDER BY ...`，这些是 `SELECT` 语句内部的子句。
    - **关键字**：像 `SELECT`、`FROM`、`WHERE`、`DISTINCT`、`AS`、`AND`，它们是语法标记，决定句子结构。`DISTINCT` 就属于这一类，不是函数。
    - **函数**：函数不是语句，它通常出现在表达式里。比如 `LOWER(name)`、`AVG(salary)`。函数可以再分：
      - 标量函数：一个输入出一个输出，如 `LOWER`、`UPPER`。
      - 聚合函数：多行输入出一个结果，如 `AVG`、`COUNT`、`MAX`、`MIN`。
      - 窗口函数：多行输入但每行输出一个结果，如 `ROW_NUMBER() OVER (...)`。
    - **表达式**：函数、列名、常量、运算符组合起来就是表达式。比如 `AVG(salary) + 100` 是表达式。
    - **谓词/条件**：`WHERE` 里的 `age > 18`、`name LIKE 'A%'` 是谓词。

## DML 数据操作(表内)

### 查询(Read)

主要依托`SELECT`语法: `SELECT <columns> FROM <tablename>`(大写不是必须，方便区分，然后`<>`不是说要填入，意思是我记录这里要填什么东西) ，而`*`可作为通配符，显示所有columns

`SELECT` 的书写顺序通常是：

```sql
SELECT [DISTINCT] 列/表达式 AS 别名 # 同时可以select好几个东西，用逗号分开，会产出临时表
FROM 表
JOIN 其他表 ON 条件
WHERE 行过滤条件 # 多条件时用 AND连接，引用字符串要用''，而栏名不是按字符串存的，不需要
GROUP BY 分组列 # 把表分成几组，每组都会按要求计算一行出来
HAVING 组过滤条件
ORDER BY 排序列
LIMIT 数量;
```


但数据库逻辑执行顺序不是这样，而是接近：

```text
FROM / JOIN
→ WHERE # 因此where里不能用select别名，顺序不对
→ GROUP BY
→ 聚合计算
→ HAVING
→ SELECT
→ DISTINCT
→ ORDER BY # order by 后面就可以跟别名,多项排序比如ORDER BY a,b就是先看a遇到相同再比b
→ LIMIT
```

!!! note 
    写查询时不要按书写顺序想，按这个顺序想：**从哪张表来 → 怎么连接 → 过滤哪些行 → 怎么分组 → 过滤哪些组 → 选什么列 → 去不去重 → 怎么排序 → 取多少。**

???+ example
    - `SELECT language, COUNT(*) FROM favorites GROUP BY language;`. This would offer a temporary table that would show the language and count.
    - `SELECT COUNT(*) FROM favorites WHERE language = 'C' AND problem = 'Hello, World';`
    - `SELECT COUNT(*) FROM favorites WHERE language = 'C' AND (problem = 'Hello, World' OR problem = 'Hello, It''s Me');` 可以注意到这里由OR表示if
    - `SELECT COUNT(*) FROM favorites WHERE language = 'C' AND problem LIKE 'Hello, %';` **LIKE**用于模糊查询，这里的%是空格都可以

#### 与join有关的错误


### 新建(Create)

使用`INSERT`: 

```sql
INSERT INTO favorites (language, problem)
VALUES ('SQL', 'Fiftyville');
```
- `INSERT INTO 表 (列...) VALUES (值...)`。

也可以一次插多行：
```sql
INSERT INTO favorites (language, problem)
VALUES ('SQL', 'Fiftyville'), ('Python', 'CS50');
```

### 更新(Update)

```sql
UPDATE favorites
SET language = 'SQL',
    problem = 'Fiftyville';
```

- `SET` 就是“把某列设置成新值”。上面这条没有 `WHERE`，会更新**所有行**。
- 更安全的写法：
```sql
UPDATE favorites
SET language = 'SQL',
    problem = 'Fiftyville'
WHERE language = 'C';
```

### 删除(Delete)

```sql
DELETE FROM favorites
WHERE Timestamp IS NULL;
```
- 删除满足条件的行。判断 NULL 必须用 `IS NULL` 或 `IS NOT NULL`，不能写 `= NULL`。原因是：NULL 不是“某个值”，它代表“未知”。`= NULL` 的结果不是 true，而是 unknown，所以不会匹配任何行。这个确实很骚气，但本质是 SQL 的三值逻辑。

如果没有 `WHERE`：
```sql
DELETE FROM favorites;
```
会删除表里所有行，但表还在。


实际工作中，**执行 `UPDATE` 或 `DELETE` 前，最好先用同样的 `WHERE` 写一条 `SELECT` 看看会命中哪些行**。


### 表达式中存在的函数

#### 1. AVG：求平均

```sql
SELECT AVG(salary) FROM employees;
```
- 只对数值列有意义。
- **忽略 NULL**。
- 如果所有行都是 NULL，结果是 NULL，不是 0。

#### 2. COUNT：计数

```sql
SELECT COUNT(*) FROM employees;              -- 总行数，包含 NULL
SELECT COUNT(salary) FROM employees;         -- salary 非 NULL 的行数
SELECT COUNT(DISTINCT dept_id) FROM employees; -- 不同部门数
```
重点：
- `COUNT(*)` 数“行”。
- `COUNT(列)` 数“该列非 NULL 的值”。
- `COUNT(DISTINCT 列)` 数“该列非 NULL 且去重后的值”。

#### 3. DISTINCT：去重

```sql
SELECT DISTINCT dept_id FROM employees;
SELECT DISTINCT dept_id, salary FROM employees;
```
- `DISTINCT` 作用于整个 `SELECT` 结果行。
- `SELECT DISTINCT dept_id, salary` 是“部门+工资”的组合去重，不是只对 `dept_id` 去重。
- 它不是函数，不要写成 `DISTINCT(dept_id)` 这种思维。

#### 4. LOWER / UPPER：转小写 / 大写

```sql
SELECT LOWER(email), UPPER(name) FROM employees;
SELECT * FROM employees WHERE LOWER(email) = 'a@x.com';
```
- 只影响查询结果或比较，不修改原表。
- 想修改表要 `UPDATE`。
- 对列使用函数可能导致普通索引失效，数据量大时要注意。

#### 5. MAX / MIN：最大 / 最小

```sql
SELECT MAX(salary), MIN(salary) FROM employees;
SELECT MAX(hire_date) FROM employees;
SELECT MAX(name) FROM employees; -- 字符串也能比，按排序规则
```
- 可用于数字、日期、字符串。
- 忽略 NULL。
- 没有数据时返回 NULL。

#### 6. SUM: 求和

对于数字类生效

---

## DDL 数据定义(对表操作)

### CREATE：创建表、数据库、索引等

最常见的是创建表。

```sql
CREATE TABLE favorites (
    id INTEGER PRIMARY KEY,
    language TEXT NOT NULL,
    problem TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

含义：
- `CREATE TABLE favorites`：创建一张叫 `favorites` 的表。
- `id INTEGER PRIMARY KEY`：id 是整数，主键，唯一标识一行。
- `language TEXT NOT NULL`：language 是文本，不能为空。
- `problem TEXT`：problem 是文本，可以为空。
- `created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP`：默认用当前时间。

还可以创建数据库：

```sql
CREATE DATABASE cs50;
```

创建索引：
```sql
CREATE INDEX idx_favorites_language
ON favorites (language);
```

索引的作用是加快查询，但会占空间，也会让插入、更新稍微变慢。


### ALTER：修改表结构

`ALTER` 不是改数据，而是改表的结构。

#### 加一列

```sql
ALTER TABLE favorites
ADD COLUMN difficulty TEXT;
```

#### 删除一列

```sql
ALTER TABLE favorites
DROP COLUMN difficulty;
```

#### 重命名列

有些数据库支持：
```sql
ALTER TABLE favorites
RENAME COLUMN problem TO problem_name;
```

- `ALTER TABLE` 很强大，但不同数据库语法差异较大。
- SQLite 对 `ALTER TABLE` 支持比较有限。

### 五、DROP：删除表、数据库、索引

`DROP` 删除的是整个对象，不只是数据。

#### 删除表
```sql
DROP TABLE favorites;
```
表结构和数据都没了。

更安全一点：
```sql
DROP TABLE IF EXISTS favorites;
```
如果表不存在，也不会报错。

#### 删除数据库
```sql
DROP DATABASE cs50;
```
非常危险。

#### 删除索引
```sql
DROP INDEX idx_favorites_language;
```

## 实际运用常查手册

### 值类型(sqlite)

Each value stored in an SQLite database (or manipulated by the database engine) has one of the following storage classes:

- **NULL**. The value is a NULL value.
- **INTEGER**. The value is a signed integer, stored in 0, 1, 2, 3, 4, 6, or 8 bytes depending on the magnitude of the value.
- **REAL**. The value is a floating point value, stored as an 8-byte IEEE floating point number.
- **TEXT**. The value is a text string, stored using the database encoding (UTF-8, UTF-16BE or UTF-16LE).
- **BLOB**. The value is a blob of data, stored exactly as it was input.

sqlite没有针对time的类型，所以可以用TEXT 作为 ISO8601 字符串（“YYYY-MM-DD HH:MM:SS.SSS”），然后可以用函数转化:
- `date()` 函数以这种格式返回日期作为文本：YYYY-MM-DD。
- `time()` 函数以格式化后的 HH:MM:SS 或 HH:MM:SS.SSS（如果使用了subsec 修饰符）的形式返回时间作为文本。
- `datetime()` 函数以 YYYY-MM-DD HH:MM:SS 或 YYYY-MM-DD HH:MM:SS.SSS（如果使用了subsec 修饰符）的形式返回日期和时间。

另外，建表时可以直接跟`is_archived INTEGER NOT NULL DEFAULT 0`即可使用默认了

### 外键

不是datatype，是对这张表里的某些列的约束，让它的值必须在另一张表的主键或唯一列里找到

```sql
CREATE TABLE departments (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL
);

CREATE TABLE employees (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    dept_id INTEGER REFERENCES departments(id)
);

或

CREATE TABLE employees (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    dept_id INTEGER,
    FOREIGN KEY (dept_id) REFERENCES departments(id)
);
```

在sqlite中，外键约束默认情况下处于禁用状态，需要在sqlite中输入`PRAGMA foreign_keys = ON;`启用外键约束

> `PRAGMA foreign_keys` 是**“每个连接”**的设置，不是数据库文件永久设置。
>
> 在 `sqlite shell` 里设置了 `foreign_keys = 1`，只对当前 shell 连接有效。Flutter 里每次打开数据库连接，都要确保它被开启，否则外键不会生效。


