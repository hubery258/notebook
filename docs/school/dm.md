# 离散数学

!!! info
    由于本身对这门课的意义感受不大，不会详细体系地记录笔记，只记录一些必要的必考的知识。

## chapter1

1. 命题 (Proposition)
    - **命题 proposition**：一个陈述句，要么真 (True)，要么假 (False)，不能同时为真和假。  
    - **命题变量 propositional variable**：常用小写字母 (p, q, r, s)。  
    - **真值 truth value**：T (真)，F (假)。  

2. 逻辑运算 (Logical Operators)
    - **否定 negation (¬p)**：真变假，假变真。  
    - **合取 conjunction (p ∧ q)**：只有当 p 和 q 都为真时为真。  
    - **析取 disjunction (p ∨ q)**：至少一个为真时为真（inclusive OR）。  
    - **异或 exclusive OR (p ⊕ q)**：仅当 p 和 q 中恰好一个为真时为真。  
    - **条件 conditional (p → q)**：只有 p 为真且 q 为假时为假。  
    - **双条件 biconditional (p ↔ q)**：p 与 q 真值相同则为真。  

3. 条件语句的变形 (Conditional Variants)
    - **逆命题 converse**：\(q → p\)。  
    - **否命题 inverse**：\(¬ p → ¬ q\)。  
    - **逆否命题 contrapositive**：\(¬q → ¬p\)。  
    - 条件语句与其逆否命题等价。  

4. 运算优先级 (Precedence of Operators)
    - 括号最高，其次是 **¬**，再是 **∧, ∨**，最后是 **→, ↔**。 

1. 复合命题分类 (Classification of Compound Propositions)
    - **永真式 tautology**：始终为真。  
    - **永假式 contradiction**：始终为假。  
    - **偶然式 contingency**：既不是永真也不是永假。  

2. 命题等价 (Logical Equivalence)
    - **逻辑等价 logically equivalent**：若 \(p <-> q\) 是永真式，则称 \(p\) 与 \(q\) 等价。  
    - **记号 notation**：\(p ≡ q\) 或 \(p <-> q\)。  
    - **证明方法**：  
        1. **真值表 truth table**：逐行比较。  
        2. **已知等价式 equivalences**：利用已证明的等价式逐步替换。  

3. 常见等价律 (Common Equivalences)
    - 恒等律 Identity laws：\(p ∧ T ≡ p ; p ∨ F ≡ p\)  
    - 支配律 Domination laws：\(p ∨ T ≡ T ; p ∧ F ≡ F\)  
    - 幂等律 Idempotent laws：\(p ∨ p ≡ p ; p ∧ p ≡ p\)  
    - 双重否定 Double negation：¬(¬p) ≡ p  
    - 交换律 Commutative laws：\(p ∨ q ≡ q ∨ p ; p ∧ q ≡ q ∧ p\)  
    - 结合律 Associative laws：\((p ∨ q) ∨ r ≡ p ∨ (q ∨ r)\)  
    - **分配律 Distributive laws**：\(p ∨ (q ∧ r) ≡ (p ∨ q) ∧ (p ∨ r)\)  
    - **德摩根律 De Morgan’s laws**：¬(p ∧ q) ≡ ¬p ∨ ¬q ；¬(p ∨ q) ≡ ¬p ∧ ¬q  
    - **吸收律 Absorption laws**：\(p ∨ (p ∧ q) ≡ p ; p ∧ (p ∨ q) ≡ p\)  
    - 否定律 Negation laws：\(p ∨ ¬p ≡ T,\; p ∧ ¬p ≡ F\)  
    - **蕴涵律 Implication law**：\(p → q ≡ ¬p ∨ q\)  
    - 双条件律 Equivalence law：\(p ↔ q ≡ (p → q) ∧ (q → p)\)  


4. 可满足性 (Satisfiability)
    - **可满足 satisfiable**：存在某种真值赋值使复合命题为真。  
    - **不可满足 unsatisfiable**：无论如何赋值都为假。  
    - **关系**：命题不可满足 ⇔ 其否定是永真式。  

1. 谓词 (Predicate)
    - **谓词 predicate**：含有变量的陈述句，变量取值后才能确定真值。  
    - **命题函数 propositional function**：如 P(x), Q(x,y)。  
    - 示例：  
        - P(x): x > 3  
        - Q(x,y): x < y 

1. 量词(Quantifier):
    - 全称量词 (Universal Quantifier)
        - **全称量词 universal quantifier**：`∀xP(x)`，表示“对所有 x，P(x) 成立”。  
        - **反例 counterexample**： `∀xP(x)` 为假的元素。  
        - 常见表达：for all, for every, for each, given any。  
    - 存在量词 (Existential Quantifier)
        - **存在量词 existential quantifier**：`∃xP(x)`，表示“存在某个 x 使得 P(x) 成立”。  
        - 常见表达：there exists, for some, at least one。  
        - **唯一量词 uniqueness quantifier**：∃!xP(x)，表示“存在唯一的 x 使得 P(x) 成立”。  

4. 量词的逻辑等价 (Logical Equivalences with Quantifiers)
    - **德摩根律 De Morgan’s laws for quantifiers**：  
        - ¬∃xP(x) ≡ ∀x¬P(x)  
        - ¬∀xP(x) ≡ ∃x¬P(x)  
    - **结合逻辑运算 equivalences**：  
        - ∀x(A(x) ∧ B(x)) ≡ (∀xA(x)) ∧ (∀xB(x))  
        - ∃x(A(x) ∨ B(x)) ≡ (∃xA(x)) ∨ (∃xB(x))  


5. 嵌套量词 (Nested Quantifiers)
  - **嵌套量词 nested quantifiers**：一个量词在另一个量词的作用域内。    

<hr>

1. 有效论证 (Valid Arguments)
  - **论证 argument**：一系列命题，最后一个是结论，其余是前提。  
  - **有效 valid**：如果所有前提为真，则结论必为真。  
  - **论证形式 argument form**：用命题变量表示的复合命题序列。  
  - **判定方法**：若 **P<sub>1</sub> ∧ P<sub>2</sub> ∧ … ∧ P<sub>n</sub> → q** 是永真式，则论证有效。  

2. 命题逻辑的推理规则 (Rules of Inference for Propositional Logic)
  - **肯定前件 Modus Ponens**：  
    - 前提：p, p → q 
    - 结论：q  
  - **否定后件 Modus Tollens**：  
    - 前提：¬q, p → q 
    - 结论：¬p  
  - **假言三段论 Hypothetical Syllogism**：  
    - 前提：p → q, q → r  
    - 结论：p → r  
  - **析取三段论 Disjunctive Syllogism**：  
    - 前提：p ∨ q, ¬p  
    - 结论：q
  - **加法 Addition**：  
    - 前提：p  
    - 结论：p ∨ q  
  - **化简 Simplification**：  
    - 前提：p ∧ q  
    - 结论：p  
  - **合取 Conjunction**：  
    - 前提：p, q  
    - 结论：p ∧ q  
  - **归结 Resolution**：  
    - 前提：p ∨ q, ¬p ∨ r  
    - 结论：q ∨ r  

3. 量词推理规则 (Rules of Inference for Quantified Statements)
  - **全称实例化 Universal Instantiation (UI)**：∀xP(x) ⊢ P(c)。  
  - **全称推广 Universal Generalization (UG)**：若对任意 c 成立，则 ⊢ ∀xP(x)。  
  - **存在实例化 Existential Instantiation (EI)**：∃xP(x) ⊢ P(c)（某个 c）。  
  - **存在推广 Existential Generalization (EG)**：若 `P(c)` 成立，则 ⊢ ∃xP(x)。  

5. 综合推理 (Combining Inference Rules)
  - **全称肯定 Universal Modus Ponens**: ∀x(P(x) → Q(x)), P(a) ⊢ Q(a)。  
  - **全称否定 Universal Modus Tollens**：∀x(P(x) → Q(x)), ¬Q(a) ⊢ ¬P(a)。  

1. 基本术语 (Terminology)
  - **证明 proof**：建立数学命题真实性的有效论证。  
  - **定理 theorem**：可以被证明为真的陈述。  
  - **公理 axiom / postulate**：假定为真的陈述。  
  - **引理 lemma**：辅助证明其他结果的次要定理。  
  - **推论 corollary**：由已证明定理直接推出的结论。  
  - **猜想 conjecture**：尚未证明但被认为可能为真的陈述。  

2. 证明类型 (Types of Proofs)
  - **直接证明 direct proof**：假设前提成立，推导出结论。  
  - **逆否证明 proof by contraposition**：证明 ¬Q → ¬P。  
  - **真空证明 vacuous proof**：若前提 P 为假，则 P → Q 恒为真。  
  - **平凡证明 trivial proof**：若结论 Q 已知为真，则 P → Q 恒为真。  
  - **反证法 proof by contradiction**：假设命题为假，推出矛盾。  
  - **分类讨论 proof by cases**：将前提分解为若干情况，逐一证明。  
  - **穷举证明 exhaustive proof**：通过有限枚举所有可能情况。  
  - **存在性证明 existence proof**：  
    - 构造性 constructive：给出具体例子。  
    - 非构造性 nonconstructive：通过矛盾证明存在性。  
  - **唯一性证明 uniqueness proof**：证明存在并且只有一个满足条件的元素。  

3. 证明策略 (Proof Strategies)
  - **正向推理 forward reasoning**：从前提出发逐步推导结论。  
  - **逆向推理 backward reasoning**：从结论出发，寻找能推出结论的前提。  
  - **等价证明 proofs of equivalence**：证明双向蕴涵或多个命题的循环蕴涵。  

4. 其他方法 (Additional Methods)
  - 数学归纳法 mathematical induction  
  - 结构归纳法 structural induction  
  - 康托对角线法 Cantor diagonalization  
  - 组合证明 combinatorial proofs  

<hr>

## chapter2

1. 集合基础 (Sets)
  - **集合 set**：无序的对象集合。  
  - **元素 element / member**：集合中的对象。  
  - **表示方法**：  
    - 列举法 roster method：如 {1,3,5,7,9}。  
    - 省略号 ellipses：如 {1,2,3,…,99\}。  
    - 描述法 set-builder notation：{x | P(x)\}。  
  - **维恩图 Venn diagram**：用矩形表示全集 U，用圆表示子集。  
  - **空集 empty set**：\(\varnothing\)，是所有集合的子集。  

2. 集合关系 (Relations Between Sets)
  - **子集 subset**：\(A ⊆ B\)。  
  - **真子集 proper subset**：\(A ⊂ B\)。  
  - **相等 equal sets**：若元素完全相同。  
  - **基数 cardinality**：集合中元素个数，记作 |S|。有限集与无限集。  

3. 幂集 (Power Set)
  - **定义 definition**：集合 S 的所有子集构成的集合，记作 P(S)。  
  - **性质**：若 `|S|=n`，则 |P(S)|=2<sup>n</sup>。  

4. 笛卡尔积 (Cartesian Product)
  - **定义 definition**：A × B = {(a,b) | a ∈ A, b ∈ B}。  
  - **性质**：若 |A|=m, |B|=n，则 |A × B| = mn。  
  - **注意**：A × B != B × A。  

5. 真值集 (Truth Sets of Quantifiers)
  - 给定谓词 P 和定义域 D，真值集为 \{x ∈ D | P(x)\}。  

6. 集合运算 (Set Operations)
  - **并 union**：\(A \cup B = \{x | x \in A \vee x \in B\}\)。  
  - **交 intersection**：\(A \cap B = \{x | x \in A \wedge x \in B\}\)。  
  - **差 difference**：\(A - B = \{x | x \in A \wedge x \notin B\}\)。  
  - **补 complement**：\(\overline{A} = \{x | x \notin A, x \in U\}\)。  
  - **对称差 symmetric difference**：\(A \oplus B = (A \cup B) - (A \cap B)\)。  
  - **基数公式**：\(|A \cup B| = |A| + |B| - |A \cap B|\)。  

7. 集合恒等式 (Set Identities)
  - 恒等律 Identity laws：\(A \cup \varnothing = A, A \cap U = A\)。  
  - 支配律 Domination laws：\(A \cup U = U, A \cap \varnothing = \varnothing\)。  
  - 幂等律 Idempotent laws：\(A \cup A = A, A \cap A = A\)。  
  - 交换律 Commutative laws：\(A \cup B = B \cup A\)。  
  - 结合律 Associative laws：\((A \cup B) \cup C = A \cup (B \cup C)\)。  
  - 分配律 Distributive laws：\(A \cup (B \cap C) = (A \cup B) \cap (A \cup C)\)。  
  - 德摩根律 De Morgan’s laws：\(\overline{A \cup B} = \overline{A} \cap \overline{B}\)。  
  - 吸收律 Absorption laws：\(A \cup (A \cap B) = A\)。  
  - 补集律 Complement laws：\(A \cup \overline{A} = U, A \cap \overline{A} = \varnothing\)。  

8. 计算机表示 (Computer Representation)
  - 用位串 bit string 表示集合，1 表示元素在集合中，0 表示不在。  
  - 并 → 位或 OR，交 → 位与 AND，差 → 位运算。  

1. 函数 (Functions)
  - **定义 definition**：函数 \(f: A \to B\)，将集合 A 中每个元素映射到集合 B 中唯一的元素。  
    - A：定义域 domain  
    - B：陪域 codomain  
    - f(A)：值域 range  
  - **图像 graph**：函数的图像是有序对集合 \(\{(a,f(a)) | a \in A\}\)。  
  - **函数性质**：  
    - 单射 injective (一一函数 one-to-one)：不同输入对应不同输出。  
    - 满射 surjective (onto)：陪域中每个元素都有原像。  
    - 双射 bijection：既是单射又是满射。  
    - 单调 monotonic：严格递增或严格递减。  
    - 反函数 inverse function：仅双射函数可逆，记作 \(f^{-1}\)。  
    - 复合函数 composition：\((f \circ g)(a) = f(g(a))\)。  

2. 特殊函数 (Special Functions)
  - **取整函数 floor function**：\(\lfloor x \rfloor\)，不大于 x 的最大整数。  
  - **上取整函数 ceiling function**：\(\lceil x \rceil\)，不小于 x 的最小整数。  
  - **性质 properties**：  
    - \(\lfloor -x \rfloor = -\lceil x \rceil\)，\(\lceil -x \rceil = -\lfloor x \rfloor\)。  
    - \(\lfloor x+m \rfloor = \lfloor x \rfloor + m\)，其中 m 为整数。  

3. 序列 (Sequences)
  - **定义 definition**：序列是从整数集合到某集合 S 的函数。  
  - **几何序列 geometric progression**：\(a, ar, ar^2, …\)。  
  - **算术序列 arithmetic progression**：\(a, a+d, a+2d, …\)。  
  - **常见序列**：平方数 \(n^2\)，立方数 \(n^3\)，阶乘 \(n!\)，幂序列 \(2^n, 3^n\)。  

4. 求和 (Summations)
  - **符号 notation**：\(\sum_{i=m}^n a_i\)。  
  - **常用公式**：  
    - \(\sum_{k=1}^n k = \frac{n(n+1)}{2}\)  
    - \(\sum_{k=1}^n k^2 = \frac{n(n+1)(2n+1)}{6}\)  
    - \(\sum_{k=1}^n k^3 = \left(\frac{n(n+1)}{2}\right)^2\)  
    - 等比数列求和：\(\sum_{k=0}^n ar^k = a\frac{r^{n+1}-1}{r-1}\)  

5. 集合的基数 (Cardinality of Sets)
  - **有限集 finite set**：元素个数有限。  
  - **无限集 infinite set**：元素无限。  
  - **基数相等 equal cardinality**：若存在双射 \(f: A \to B\)，则 \(|A|=|B|\)。  
  - **可数集 countable set**：有限或与正整数集合 \(\mathbb{Z}^+\) 等势。  
  - **不可数集 uncountable set**：如实数区间 (0,1)。  
  - **典型结果**：  
    - 正整数与偶数集合等势。  
    - 有理数集合是可数的。  
    - 实数集合是不可数的（康托对角线法 Cantor diagonalization）。  
    - 幂集的基数大于原集合。  

1. 函数完备性 (Functionally Complete)
  - **定义 definition**：若一组逻辑算子能表达所有复合命题，则称其为函数完备。  
  - 常见完备集合：  
    - {¬, ∧, ∨}  
    - {¬, ∨}  
    - {¬, ∧}  

2. 命题标准形式 (Propositional Normal Forms)
  - **文字 literal**：命题变量 \(p\) 或其否定 ¬p。  
  - **子句 clause**：文字的析取或合取。  
    - 析取子句 disjunctive clause：如 \(p ∨ ¬q\)。  
    - 合取子句 conjunctive clause：如 \(p ∧ ¬q\)。  

3. 合取范式 CNF (Conjunctive Normal Form)
  - **定义 definition**：若公式是若干析取子句的合取，则为 CNF。  
  - 例子：\((p ∨ ¬q) ∧ (¬p ∨ r)\)。  

4. 析取范式 DNF (Disjunctive Normal Form)
  - **定义 definition**：若公式是若干合取子句的析取，则为 DNF。  
  - 例子：\((p ∧ q) ∨ (¬p ∧ r)\)。  

5. 完全析取范式 Full DNF
  - **最小项 minterm**：每个变量都出现一次（正或负）的合取。  
  - **完全析取范式 full DNF**：公式写成所有使其为真的最小项的析取。  
  - 可通过真值表直接得到。  

6. 前束范式 Prenex Normal Form
  - **定义 definition**：谓词逻辑公式若所有量词都移到最前面，则为前束范式。  
  - 转化步骤：  
    1. 消除 → 和 ↔。  
    2. 将否定移到文字层面。  
    3. 必要时重命名变量。  
    4. 将量词前移。  