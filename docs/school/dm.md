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
好的，下面是 **DM1.3 PPT（Propositional Equivalences 命题等价）** 的知识点梳理和例题整理，保持我们之前的结构和语言要求。  

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
        - \(\forall x (A(x) ∧ B(x)) ≡ (\forall x A(x)) ∧ (\forall x B(x))\)  
        - \(\exists x (A(x) ∨ B(x)) ≡ (\exists x A(x)) ∨ (\exists x B(x))\)  

### 5. 嵌套量词 (Nested Quantifiers)
- **嵌套量词 nested quantifiers**：一个量词在另一个量词的作用域内。  
- 顺序不同可能导致语义不同：  
  - \(\forall x \exists y P(x,y)\)：对每个 x，存在一个 y。  
  - \(\exists y \forall x P(x,y)\)：存在一个 y，使得对所有 x 成立。  

### 6. 翻译与应用 (Translation and Applications)
- **英语转逻辑表达式**：识别量词、引入谓词、翻译。  
- **逻辑表达式转英语**：解释量词范围和谓词含义。  
- **典型应用**：数学定义（如极限）、Lewis Carroll 的逻辑句子、朋友关系建模。  

---

## 📑 例题检验

### Example 1: Universal Quantifier
**Problem:** What is the truth value of \(\forall x (x^2 ≥ x)\) when the domain is integers?  
**解析（中文）：** 对所有整数，平方大于等于自身。负数平方后变正数，仍 ≥ 原数；0 和 1 也满足。因此为真。  
**Solution (English):**  
For integers, \(x^2 ≥ x\) holds for all x. Thus, \(\forall x (x^2 ≥ x)\) is true.

---

### Example 2: Existential Quantifier
**Problem:** Express “Some real numbers are rational numbers” as a logical expression.  
**解析（中文）：** 在实数域中，存在某个数是有理数。  
**Solution (English):**  
Let \(Q(y): y\) is rational.  
Expression: \(\exists y Q(y)\).

---

### Example 3: Nested Quantifier
**Problem:** Translate \(\forall x \exists y C(x,y)\), where \(C(x,y)\) means “x has taken course y.”  
**解析（中文）：** 对每个学生 x，存在一门课程 y，使得 x 修过 y。即“每个学生都修过某门课”。  
**Solution (English):**  
For every student x, there exists a course y such that x has taken y.

---

### Example 4: Negating Nested Quantifiers
**Problem:** Negate \(\forall x \exists y (xy = 1)\).  
**解析（中文）：** 否定全称量词，得到存在一个 x，使得对所有 y，xy ≠ 1。  
**Solution (English):**  
¬\(\forall x \exists y (xy = 1)\)  
≡ \(\exists x \forall y (xy ≠ 1)\).

好的，下面是 **DM1.6 PPT（Rules of Inference 推理规则）** 的知识点梳理和例题整理，保持我们之前的结构。  

---

## 📘 知识点梳理（Chapter 1.6）

### 1. 有效论证 (Valid Arguments)
- **论证 argument**：一系列命题，最后一个是结论，其余是前提。  
- **有效 valid**：如果所有前提为真，则结论必为真。  
- **论证形式 argument form**：用命题变量表示的复合命题序列。  
- **判定方法**：若 \(P_1 ∧ P_2 ∧ … ∧ P_n → q\) 是永真式，则论证有效。  

### 2. 命题逻辑的推理规则 (Rules of Inference for Propositional Logic)
- **肯定前件 Modus Ponens**：  
  - 前提：\(p, p → q\)  
  - 结论：\(q\)  
- **否定后件 Modus Tollens**：  
  - 前提：¬q, \(p → q\)  
  - 结论：¬p  
- **假言三段论 Hypothetical Syllogism**：  
  - 前提：\(p → q, q → r\)  
  - 结论：\(p → r\)  
- **析取三段论 Disjunctive Syllogism**：  
  - 前提：\(p ∨ q, ¬p\)  
  - 结论：\(q\)  
- **加法 Addition**：  
  - 前提：\(p\)  
  - 结论：\(p ∨ q\)  
- **化简 Simplification**：  
  - 前提：\(p ∧ q\)  
  - 结论：\(p\)  
- **合取 Conjunction**：  
  - 前提：\(p, q\)  
  - 结论：\(p ∧ q\)  
- **归结 Resolution**：  
  - 前提：\(p ∨ q, ¬p ∨ r\)  
  - 结论：\(q ∨ r\)  

### 3. 常见谬误 (Fallacies)
- **否定前件 Denying the Hypothesis**：\(p → q, ¬p ⊢ ¬q\)（错误）。  
- **肯定结论 Affirming the Conclusion**：\(p → q, q ⊢ p\)（错误）。  

### 4. 量词推理规则 (Rules of Inference for Quantified Statements)
- **全称实例化 Universal Instantiation (UI)**：\(\forall x P(x) ⊢ P(c)\)。  
- **全称推广 Universal Generalization (UG)**：若对任意 c 成立，则 ⊢ \(\forall x P(x)\)。  
- **存在实例化 Existential Instantiation (EI)**：\(\exists x P(x) ⊢ P(c)\)（某个 c）。  
- **存在推广 Existential Generalization (EG)**：若 \(P(c)\) 成立，则 ⊢ \(\exists x P(x)\)。  

### 5. 综合推理 (Combining Inference Rules)
- **全称肯定 Universal Modus Ponens**：\(\forall x (P(x) → Q(x)), P(a) ⊢ Q(a)\)。  
- **全称否定 Universal Modus Tollens**：\(\forall x (P(x) → Q(x)), ¬Q(a) ⊢ ¬P(a)\)。  

---

## 📑 例题检验

### Example 1: Modus Ponens
**Problem:** Premises: “If you have a current password, then you can log onto the network.” “You have a current password.” Conclusion: “You can log onto the network.”  
**解析（中文）：** 前提是 \(p → q, p\)，因此结论必然是 \(q\)。  
**Solution (English):**  
Let p = “You have a current password”, q = “You can log onto the network”.  
Premises: \(p → q, p\).  
Conclusion: \(q\). Valid by Modus Ponens.

---

### Example 2: Modus Tollens
**Problem:** Premises: “If it snows today, then we will go skiing.” “We will not go skiing.” Conclusion: “It does not snow today.”  
**解析（中文）：** 前提是 \(p → q, ¬q\)，因此结论是 ¬p。  
**Solution (English):**  
Let p = “It snows today”, q = “We will go skiing”.  
Premises: \(p → q, ¬q\).  
Conclusion: ¬p. Valid by Modus Tollens.

---

### Example 3: Quantified Inference
**Problem:** Premises: “Everyone in the discrete math class has taken a CS course.” “Marla is a student in the discrete math class.” Conclusion: “Marla has taken a CS course.”  
**解析（中文）：** 使用全称实例化和 Modus Ponens。  
**Solution (English):**  
Let D(x): “x is in discrete math class”, C(x): “x has taken a CS course”.  
Premises: \(\forall x (D(x) → C(x)), D(Marla)\).  
By UI: \(D(Marla) → C(Marla)\).  
By Modus Ponens: \(C(Marla)\).  

好的，下面是 **DM1.7–1.8 PPT（Introduction to Proofs 证明导论 & Proof Methods and Strategy 证明方法与策略）** 的知识点梳理和例题整理，保持我们之前的结构。  

---

## 📘 知识点梳理（Chapter 1.7–1.8）

### 1. 基本术语 (Terminology)
- **证明 proof**：建立数学命题真实性的有效论证。  
- **定理 theorem**：可以被证明为真的陈述。  
- **公理 axiom / postulate**：假定为真的陈述。  
- **引理 lemma**：辅助证明其他结果的次要定理。  
- **推论 corollary**：由已证明定理直接推出的结论。  
- **猜想 conjecture**：尚未证明但被认为可能为真的陈述。  

### 2. 证明类型 (Types of Proofs)
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

### 3. 证明策略 (Proof Strategies)
- **正向推理 forward reasoning**：从前提出发逐步推导结论。  
- **逆向推理 backward reasoning**：从结论出发，寻找能推出结论的前提。  
- **等价证明 proofs of equivalence**：证明双向蕴涵或多个命题的循环蕴涵。  

### 4. 其他方法 (Additional Methods)
- 数学归纳法 mathematical induction  
- 结构归纳法 structural induction  
- 康托对角线法 Cantor diagonalization  
- 组合证明 combinatorial proofs  

---

## 📑 例题检验

### Example 1: Direct Proof
**Problem:** Prove: If n is odd, then \(n^2\) is odd.  
**解析（中文）：** 假设 n 为奇数，写成 \(n = 2k+1\)，平方后得到 \(n^2 = 2(2k^2+2k)+1\)，仍为奇数。  
**Solution (English):**  
Assume \(n = 2k+1\). Then  
\(n^2 = (2k+1)^2 = 4k^2+4k+1 = 2(2k^2+2k)+1\).  
Thus, \(n^2\) is odd. Q.E.D.

---

### Example 2: Proof by Contradiction
**Problem:** Prove: There is no largest prime number.  
**解析（中文）：** 假设存在最大素数 s，构造所有素数的乘积 r，再考虑 r+1，它必然有大于 s 的素因子或本身为素数，矛盾。  
**Solution (English):**  
Assume s is the largest prime. Let \(r = 2·3·5·…·s\).  
Then \(r+1\) is either prime > s or has a prime factor > s.  
Contradiction. Hence, no largest prime exists. Q.E.D.

---

### Example 3: Proof by Cases
**Problem:** Prove: If n is an integer not divisible by 3, then \(n^2 ≡ 1 \pmod{3}\).  
**解析（中文）：** 分两种情况：n ≡ 1 (mod 3) 或 n ≡ 2 (mod 3)，平方后都得到余数 1。  
**Solution (English):**  
Case 1: \(n ≡ 1 \pmod{3}\), then \(n^2 ≡ 1 \pmod{3}\).  
Case 2: \(n ≡ 2 \pmod{3}\), then \(n^2 ≡ 4 ≡ 1 \pmod{3}\).  
Thus, \(n^2 ≡ 1 \pmod{3}\). Q.E.D.

---

### Example 4: Uniqueness Proof
**Problem:** Show that if \(a ≠ 0\), then there is a unique real number r such that \(ar+b=0\).  
**解析（中文）：** 存在性：令 \(r = -b/a\)，满足方程。唯一性：若 s 也满足，则 as+b=0=ar+b ⇒ as=ar ⇒ s=r。  
**Solution (English):**  
Existence: \(r = -b/a\).  
Uniqueness: If \(as+b=0\), then \(as=ar\). Since \(a ≠ 0\), \(s=r\).  
Thus, r is unique. Q.E.D.

---

这样你就能掌握 **证明的基本术语、常见方法、策略与应用**，并通过例题检验理解。到这里，**Chapter 1** 的逻辑与证明部分就完整了。下一步我们可以进入 **Chapter 2（Basic Structures: Sets, Functions, Sequences, and Sums）** 的总结，你要不要我直接接着整理 DM2.1–2.2？

好的，下面是 **DM2.1–2.2 PPT（Sets 集合 & Set Operations 集合运算）** 的知识点梳理和例题整理，保持我们之前的结构。  

---

## 📘 知识点梳理（Chapter 2.1–2.2）

### 1. 集合基础 (Sets)
- **集合 set**：无序的对象集合。  
- **元素 element / member**：集合中的对象。  
- **表示方法**：  
  - 列举法 roster method：如 \(\{1,3,5,7,9\}\)。  
  - 省略号 ellipses：如 \(\{1,2,3,…,99\}\)。  
  - 描述法 set-builder notation：\(\{x | P(x)\}\)。  
- **维恩图 Venn diagram**：用矩形表示全集 U，用圆表示子集。  
- **空集 empty set**：\(\varnothing\)，是所有集合的子集。  

### 2. 集合关系 (Relations Between Sets)
- **子集 subset**：\(A \subseteq B\)。  
- **真子集 proper subset**：\(A \subset B\)。  
- **相等 equal sets**：若元素完全相同。  
- **基数 cardinality**：集合中元素个数，记作 \(|S|\)。有限集与无限集。  

### 3. 幂集 (Power Set)
- **定义 definition**：集合 S 的所有子集构成的集合，记作 \(P(S)\)。  
- **性质**：若 \(|S|=n\)，则 \(|P(S)|=2^n\)。  

### 4. 笛卡尔积 (Cartesian Product)
- **定义 definition**：\(A \times B = \{(a,b) | a \in A, b \in B\}\)。  
- **性质**：若 \(|A|=m, |B|=n\)，则 \(|A \times B| = mn\)。  
- **注意**：\(A \times B \neq B \times A\)。  

### 5. 真值集 (Truth Sets of Quantifiers)
- 给定谓词 P 和定义域 D，真值集为 \(\{x \in D | P(x)\}\)。  

### 6. 集合运算 (Set Operations)
- **并 union**：\(A \cup B = \{x | x \in A \vee x \in B\}\)。  
- **交 intersection**：\(A \cap B = \{x | x \in A \wedge x \in B\}\)。  
- **差 difference**：\(A - B = \{x | x \in A \wedge x \notin B\}\)。  
- **补 complement**：\(\overline{A} = \{x | x \notin A, x \in U\}\)。  
- **对称差 symmetric difference**：\(A \oplus B = (A \cup B) - (A \cap B)\)。  
- **基数公式**：\(|A \cup B| = |A| + |B| - |A \cap B|\)。  

### 7. 集合恒等式 (Set Identities)
- 恒等律 Identity laws：\(A \cup \varnothing = A, A \cap U = A\)。  
- 支配律 Domination laws：\(A \cup U = U, A \cap \varnothing = \varnothing\)。  
- 幂等律 Idempotent laws：\(A \cup A = A, A \cap A = A\)。  
- 交换律 Commutative laws：\(A \cup B = B \cup A\)。  
- 结合律 Associative laws：\((A \cup B) \cup C = A \cup (B \cup C)\)。  
- 分配律 Distributive laws：\(A \cup (B \cap C) = (A \cup B) \cap (A \cup C)\)。  
- 德摩根律 De Morgan’s laws：\(\overline{A \cup B} = \overline{A} \cap \overline{B}\)。  
- 吸收律 Absorption laws：\(A \cup (A \cap B) = A\)。  
- 补集律 Complement laws：\(A \cup \overline{A} = U, A \cap \overline{A} = \varnothing\)。  

### 8. 计算机表示 (Computer Representation)
- 用位串 bit string 表示集合，1 表示元素在集合中，0 表示不在。  
- 并 → 位或 OR，交 → 位与 AND，差 → 位运算。  

---

## 📑 例题检验

### Example 1: Power Set
**Problem:** Find \(P(\{a,b,c\})\).  
**解析（中文）：** 子集包括空集、单元素集、双元素集和全集。总数 \(2^3=8\)。  
**Solution (English):**  
\(P(\{a,b,c\}) = \{\varnothing, \{a\}, \{b\}, \{c\}, \{a,b\}, \{a,c\}, \{b,c\}, \{a,b,c\}\}\).

---

### Example 2: Cartesian Product
**Problem:** Let \(A=\{a,b\}, B=\{0,1,2\}\). Find \(A \times B\).  
**解析（中文）：** 每个 A 的元素与 B 的元素配对，共 \(2 \times 3 = 6\) 个。  
**Solution (English):**  
\(A \times B = \{(a,0),(a,1),(a,2),(b,0),(b,1),(b,2)\}\).

---

### Example 3: Set Identity
**Problem:** Show that \((A-B) \cup B = A \cup B\).  
**解析（中文）：** 利用集合恒等式化简，结果等于 \(A \cup B\)。  
**Solution (English):**  
\((A-B) \cup B = (A \cap \overline{B}) \cup B = (A \cup B) \cap (\overline{B} \cup B) = (A \cup B) \cap U = A \cup B\). Q.E.D.

---

这样你就能掌握 **集合与集合运算的核心知识点**，并通过例题检验理解。下一份 PPT 我可以继续帮你总结 **DM2.3（Functions 函数）**，保持同样的结构。

好的，下面是 **DM2.3–2.5 PPT（Functions 函数、Sequences and Summations 序列与求和、Cardinality of Sets 集合的基数）** 的知识点梳理和例题整理。  

---

## 📘 知识点梳理（Chapter 2.3–2.5）

### 1. 函数 (Functions)
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

### 2. 特殊函数 (Special Functions)
- **取整函数 floor function**：\(\lfloor x \rfloor\)，不大于 x 的最大整数。  
- **上取整函数 ceiling function**：\(\lceil x \rceil\)，不小于 x 的最小整数。  
- **性质 properties**：  
  - \(\lfloor -x \rfloor = -\lceil x \rceil\)，\(\lceil -x \rceil = -\lfloor x \rfloor\)。  
  - \(\lfloor x+m \rfloor = \lfloor x \rfloor + m\)，其中 m 为整数。  

### 3. 序列 (Sequences)
- **定义 definition**：序列是从整数集合到某集合 S 的函数。  
- **几何序列 geometric progression**：\(a, ar, ar^2, …\)。  
- **算术序列 arithmetic progression**：\(a, a+d, a+2d, …\)。  
- **常见序列**：平方数 \(n^2\)，立方数 \(n^3\)，阶乘 \(n!\)，幂序列 \(2^n, 3^n\)。  

### 4. 求和 (Summations)
- **符号 notation**：\(\sum_{i=m}^n a_i\)。  
- **常用公式**：  
  - \(\sum_{k=1}^n k = \frac{n(n+1)}{2}\)  
  - \(\sum_{k=1}^n k^2 = \frac{n(n+1)(2n+1)}{6}\)  
  - \(\sum_{k=1}^n k^3 = \left(\frac{n(n+1)}{2}\right)^2\)  
  - 等比数列求和：\(\sum_{k=0}^n ar^k = a\frac{r^{n+1}-1}{r-1}\)  

### 5. 集合的基数 (Cardinality of Sets)
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

---

## 📑 例题检验

### Example 1: Inverse Function
**Problem:** Let \(f(x)=x+1\) from integers to integers. Find its inverse.  
**解析（中文）：** f 是双射，逆函数为 \(f^{-1}(y)=y-1\)。  
**Solution (English):**  
\(f^{-1}(y)=y-1\).

---

### Example 2: Composition
**Problem:** \(f(x)=2x+3, g(x)=3x+2\). Find \(f \circ g\) and \(g \circ f\).  
**解析（中文）：** 代入计算即可。  
**Solution (English):**  
\(f(g(x))=2(3x+2)+3=6x+7\).  
\(g(f(x))=3(2x+3)+2=6x+11\).

---

### Example 3: Summation
**Problem:** Compute \(\sum_{k=1}^n k^2\).  
**解析（中文）：** 使用公式，结果为 \(\frac{n(n+1)(2n+1)}{6}\)。  
**Solution (English):**  
\(\sum_{k=1}^n k^2 = \frac{n(n+1)(2n+1)}{6}\).

---

### Example 4: Cardinality
**Problem:** Show that the set of positive integers and the set of positive even integers have the same cardinality.  
**解析（中文）：** 构造双射 f(n)=2n。  
**Solution (English):**  
Define \(f: \mathbb{Z}^+ \to E\) by \(f(n)=2n\).  
This is bijective, hence \(|\mathbb{Z}^+|=|E|\).

---

这样你就能掌握 **函数、序列与求和、集合基数** 的核心知识点，并通过例题检验理解。下一步我们可以进入 **Chapter 3（Algorithms 算法）** 的总结，你要不要我直接接着整理 DM3.1？

好的，下面是 **Normal Forms PPT（命题逻辑的标准形式）** 的知识点梳理和例题整理，保持我们之前的结构。  

---

## 📘 知识点梳理（Normal Forms）

### 1. 函数完备性 (Functionally Complete)
- **定义 definition**：若一组逻辑算子能表达所有复合命题，则称其为函数完备。  
- 常见完备集合：  
  - {¬, ∧, ∨}  
  - {¬, ∨}  
  - {¬, ∧}  

### 2. 命题标准形式 (Propositional Normal Forms)
- **文字 literal**：命题变量 \(p\) 或其否定 ¬p。  
- **子句 clause**：文字的析取或合取。  
  - 析取子句 disjunctive clause：如 \(p ∨ ¬q\)。  
  - 合取子句 conjunctive clause：如 \(p ∧ ¬q\)。  

### 3. 合取范式 CNF (Conjunctive Normal Form)
- **定义 definition**：若公式是若干析取子句的合取，则为 CNF。  
- 例子：\((p ∨ ¬q) ∧ (¬p ∨ r)\)。  

### 4. 析取范式 DNF (Disjunctive Normal Form)
- **定义 definition**：若公式是若干合取子句的析取，则为 DNF。  
- 例子：\((p ∧ q) ∨ (¬p ∧ r)\)。  

### 5. 完全析取范式 Full DNF
- **最小项 minterm**：每个变量都出现一次（正或负）的合取。  
- **完全析取范式 full DNF**：公式写成所有使其为真的最小项的析取。  
- 可通过真值表直接得到。  

### 6. 前束范式 Prenex Normal Form
- **定义 definition**：谓词逻辑公式若所有量词都移到最前面，则为前束范式。  
- 转化步骤：  
  1. 消除 → 和 ↔。  
  2. 将否定移到文字层面。  
  3. 必要时重命名变量。  
  4. 将量词前移。  

---

## 📑 例题检验

### Example 1: CNF 转化
**Problem:** Convert \(-((p ∨ ¬q) ∧ ¬r)\) into CNF.  
**解析（中文）：** 使用德摩根律和分配律逐步化简。  
**Solution (English):**  
\(-((p ∨ ¬q) ∧ ¬r)\)  
≡ (p ∨ ¬q) ∨ r  
≡ (¬p ∨ r) ∧ (q ∨ r).  
Thus, CNF is \((¬p ∨ r) ∧ (q ∨ r)\).

---

### Example 2: Full DNF from Truth Table
**Problem:** Find the full DNF of \(f(p,q,r) = (p ∧ q) ∨ (¬p ∧ r)\).  
**解析（中文）：** 列真值表，找出所有使 f 为真的赋值，写成最小项的析取。  
**Solution (English):**  
Truth table shows f is true for:  
- (p=T,q=T,r=T) → \(p ∧ q ∧ r\)  
- (p=T,q=T,r=F) → \(p ∧ q ∧ ¬r\)  
- (p=F,q=T,r=T) → \(¬p ∧ q ∧ r\)  
- (p=F,q=F,r=T) → \(¬p ∧ ¬q ∧ r\)  
So full DNF is \((p ∧ q ∧ r) ∨ (p ∧ q ∧ ¬r) ∨ (¬p ∧ q ∧ r) ∨ (¬p ∧ ¬q ∧ r)\).

---

### Example 3: Prenex Normal Form
**Problem:** Convert \(\forall x (P(x) ∧ ∃y Q(y))\) into prenex normal form.  
**解析（中文）：** 将量词前移，注意变量作用域。  
**Solution (English):**  
\(\forall x ∃y (P(x) ∧ Q(y))\).  
This is prenex normal form.

---

这样整理后，你就能快速掌握 **CNF、DNF、Full DNF、Prenex Normal Form** 的定义、转化步骤和应用。它们在逻辑推理、自动定理证明、SAT 求解等领域都是基础工具。  

要不要我接着帮你整理 **Chapter 3（Algorithms 算法）** 的 PPT？