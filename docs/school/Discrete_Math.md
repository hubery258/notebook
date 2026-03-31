# 离散数学及其运用 | Discrete Mathematics and Its Applications

## Chapter1

- **Proposition(命题)**: declarative sentence  ； either true or false,but not both. 

![符号](https://s41.ax1x.com/2026/03/12/peAADcF.md.png)
<br>
`↓`：NOR operator, 或非，全为F时才为T

注意 **真值表(truth table)** 很常用,可以关注`p -> q`的真值情况:
![p->q的针织表](https://s41.ax1x.com/2026/03/12/peAAIje.md.png)

- **consistent**: 存在至少一组命题值使得所有需要的命题值都为真

??? note "错题本"
    To use the wireless network in the airport you must pay the daily fee unless you are a subscriber to the service.Express your answer in terms of w: “You can use thewireless network in the airport,” d:“You pay the daily fee,” and s: “You are a subscriber to the service.” 应当是`w→(s∨d)`而不能反过来，对于`to do A , you have to B`，只能说你做了A一定就做到了B，但做到了B不一定就能做A。

### De Morgan’s Laws & Logical Equivalences(逻辑等价式)

- 命题类型:
    - **Tautology** : 重言式，永远为真
    - **Contradiction**: 矛盾式
    - **Contingency** : 偶然式，可真可假


### quantifiers(量词) &  predicates (谓词)

??? note "错题"
    Let P(x), Q(x), and R(x) be the statements “x is a clear explanation,” “x is satisfactory,” and “x is an excuse,”respectively. Suppose that the domain for x consists of all English text. Express each of these statements using quantifiers, logical connectives, and P(x), Q(x), and R(x).
    a) All clear explanations are satisfactory.
    b) Some excuses are unsatisfactory.
    c) Some excuses are not clear explanations.
    d) Does (c) follow from (a) and (b)?

    - All A are B ⇒ 用 →
    - Some A are B ⇒ 用 ∧