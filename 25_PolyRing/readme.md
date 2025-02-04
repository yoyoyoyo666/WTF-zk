---
title: 25. 多项式环
tags:
  - zk
  - abstract algebra
  - polynomials
  - polynomial ring
---

# WTF zk 教程第 25 讲：多项式环

在抽象代数中，多项式环是一种重要的代数结构，它在密码学和零知识证明中有广泛的应用。这一讲，我们将介绍多项式环的定义、性质以及一些基本操作。

## 1. 多项式环

上一讲我们学习了多项式，它包含加法和乘法运算。群只包含一种运算，因此我们没法使用群来研究多项式；而环正好包含这两种运算，可以很好的和多项式结合。

多项式环是由一个变量的多项式集合构成的环，其中所有系数都来自一个环。

**多项式环的定义** 如果 $R$ 是一个环，那么 $R[x]$ 表示由 $R$ 中的元素构成的所有形如：

$$
P(x) = \sum_{j=0}^{n}{a_jx^j} = a_nx^n + a_{n-1}x^{n-1} + \ldots + a_1x + a_0
$$

的多项式构成的集合，其中 $a_j \in R$ 为系数，$n$ 为多项式的次数， $x$ 为变量。而环 $R$ 被称为 $R[x]$ 的基础环。

多项式环中的加法和乘法和多项式之间的一样。具体来说，对于两个多项式 $P(x) = \sum_{j=0}^{n}{a_jx^j}$ 和 $Q(x) = \sum_{j=0}^{m}{b_jx^j}$，有

**多项式加法：** 

$$
P(x) + Q(x) = \sum_{j=0}^{n}{a_jx^j} + \sum_{j=0}^{m}{b_jx^j} = \sum_{j=0}^{\max{(n,m)}}{(a_j+b_j)x^j}
$$

**多项式乘法：** 
$$
P(x) \cdot Q(x)  = (\sum_{j=0}^{n}{a_jx^j}) \cdot (\sum_{j=0}^{m}{b_jx^j}) = \sum_{i=0}^{n+m}\sum_{j=0}^{i}{(a_jb_{i-j})x^i}
$$

因为若 $a_j, b_j \in R$，有 $(a_j+b_j), \sum_{j=0}^{i}{(a_jb_{i-j})} \in R$。因此，我们容易验证 $R[x]$ 和加法构成Abel群，其中加法单位元为零多项式； $R[x]$ 和乘法构成幺半群（封闭性，结合律，单位元存在），其中乘法单位元为一多项式。因此 $(R[x], +, \cdot)$ 构成环。

## 2. 多项式环的例子

### 整数环上的多项式环 $\mathbb{Z}[x]$

当取环 $R$ 为整数环 $\mathbb{Z}$ 时，多项式环 $\mathbb{Z}[x]$ 就是整数系数的多项式集合。例如：

$$ 
f(x) = 2x^2 - 3x + 1
$$

是 $\mathbb{Z}[x]$ 中的一个多项式。

### 有限域上的多项式环 $\mathbb{Z}_2[x]$

当取环 $R$ 为整数模2环 $\mathbb{Z}_2$（系数只能是 $0$ 或 $1$）时，多项式环 $\mathbb{Z}_2[x]$ 就是二元有限域上的多项式集合。例如：

$$
g(x) = x^3 + x + 1
$$

是 $\mathbb{Z}_2[x]$ 中的一个多项式。

## 3. 多项式环的性质

**性质1.** 若环 $R$ 为交换环，那么多项式环 $R[x]$ 也是交换环。

<details><summary>点我展开证明👀</summary>

设多项式 $P(x) = \sum_{j=0}^{n}{a_jx^j}$ 和 $Q(x) = \sum_{j=0}^{m}{b_jx^j}$ 为 $R[x]$ 中任意2个多项式。

那么 $P(x) \cdot Q(x) = \sum_{i=0}^{n+m}\sum_{j=0}^{i}{(a_jb_{i-j})x^i}$，其中第 $i$ 项的系数为 $\sum_{j=0}^{i}{(a_jb_{i-j})}$。

而 $Q(x) \cdot P(x) = \sum_{i=0}^{n+m}\sum_{j=0}^{i}{(b_ja_{i-j})x^i}$，其中第 $i$ 项的系数为 $\sum_{j=0}^{i}{(b_ja_{i-j})}$。

因为 $R$ 为交换环，有 $P(x) \cdot Q(x) = \sum_{j=0}^{i}{(a_jb_{i-j})} = \sum_{j=0}^{i}{(b_{i-j}a_j)}$。我们可以设索引 $j = i - j$ 而 $i = j$，有 $\sum_{j=0}^{i}{(b_{i-j}a_j)} = \sum_{j=0}^{i}{(b_ja_{i-j})} = Q(x) \cdot P(x)$。因此有 $P(x) \cdot Q(x) = Q(x) \cdot P(x)$，多项式环 $R[x]$ 是交换环。证毕。

</details>

**性质2.** 若环 $R$ 为整环，那么多项式环 $R[x]$ 也是整环。

<details><summary>点我展开证明👀</summary>

我们证明这个命题的逆反命题成立：若多项式环 $R[x]$ 不是整环，则 $R$ 不是整环。

因为 $R[x]$ 不是整环，那么存在非零多项式 $P(x) = \sum_{j=0}^{n}{a_jx^j}$ 和 $Q(x) = \sum_{j=0}^{m}{b_jx^j}$，其中 $a_n, b_m \neq 0$，有 $P(x) \cdot Q(x) = 0$。也就是说 $P(x) \cdot Q(x) = \sum_{i=0}^{n+m}\sum_{j=0}^{i}{(a_jb_{i-j})x^i}$ 第 $n+m$ 项的系数 $a_nb_m = 0$。因此，环 $R$ 中存在零因子 $a_n$ 和 $b_m$，它不是整环。证毕

</details>

**性质3.** 若环 $R$ 为域，那么多项式环 $R[x]$ 是整环，但并不一定是域。

<details><summary>点我展开证明👀</summary>

因为域也是整环，环 $R$ 为域，那么 $R$ 也是整环，根据性质2，多项式环 $R[x]$ 也是整环。

证毕。

</details>

## 4. 域上多项式

虽然当 $R$ 为域时，多项式环 $R[x]$ 不一定构成域。但是由于域 $R$ 支持除法（乘法逆运算），使得 $R[x]$ 和整数环 $Z$ 的性质很像。

在介绍域上多项式的性质之前，我们要介绍**首一多项式**的概念：设多项式 $P(x) \in R[x]$，如果它的首项系数为单位元 $1$，我们就称 $P(x)$ 为**首一多项式**。比如 $x^2 + x + 3$ 就是一个首一多项式。

**性质4.** 对于域上多项式环 $F[x]$，设多项式 $P(x) \in F[x]$ 的首项系数为 $a_n$，那么 $Q(x) = a_n^{-1} P(x)$ 为首一多项式，并且它们的度相同 $\text{deg}(P(x)) = \text{deg}(Q(x))$。

设 $P(x) = 2x^2 - 3x + 1 \in Z_3(x)$，那么它对应的首一多项式为 $Q(x) = 2P(x) = 4x^2 - 6x + 2 = x^2 + 2 \pmod{3}$。

**性质5. 域上多项式的欧几里得除法** 对于域上多项式环 $F[x]$，设 $P(x), G(x) \in F[x]$，其中 $G(x)$ 不是零多项式，那么存在唯一的 $Q(x), R(x) \in F[x]$，使得

$$
P(x) = Q(x)G(x) + R(x)
$$

成立，其中 $0 \leq \deg(R(x)) < \deg(G(x))$。这和整数的欧几里得除法很相似，只是把整数换成了多项式。

你可以利用多项式的长除法计算欧几里得除法，比如 $x^3 -12x -42 = (x^2 -9x -27)(x-3) -123$。

**性质6. $F[x]$ 不可约多项式的性质取决于 $F$。** 不可约多项式在域上多项式中的作用类似于素数在整数中的作用。

举个例子，当 $F$ 为整数环时，多项式 $x^2 - 2$ 是不可约多项式；但当 $F$ 为实数域时， $x^2 - 2 = (x + \sqrt{2})(x - \sqrt{2})$，因此它是可约的。

**性质7. 唯一因式分解** 域上多项式环 $F[x]$ 中非零多项式都可以唯一地分解成一些不可约多项式的乘积。这类似于整数的唯一质因子分解定理。

**性质8. 最大公约式存在** 对于域上多项式环 $F[x]$，设非零多项式 $P(x), G(x) \in F[x]$，它们的最大公约式 $\gcd{P(x), G(x)}$ 被定义为能够同时整除 $P(x)$ 和 $G(x)$ 的多项式中度最大的那个。这类似于整数的最大公约数。

我们可以用因式分解法或扩展欧几里得法来求两个多项式的最大公约式。

**性质9. 最小公倍式存在** 对于域上多项式环 $F[x]$，设非零多项式 $P(x), G(x) \in F[x]$，它们的最小公倍式 $\text{lcd(P(x), G(x))}$ 被定义为能够同时被整除 $P(x)$ 和 $G(x)$ 的多项式中度最小的那个。这类似于整数的最小公倍数。

我们可以在求得最大公约式后，使用最大公约式和最小公倍式的关系来求它 $\text{lcd(P(x), G(x))} \text{gcd(P(x), G(x))} = P(x) G(x)$

> 通过性质4-9，我们可以发现域上多项式环和整数很像，支持欧几里得除法，有类似素数的不可约多项式，可以被唯一的因式分解，存在最大公约式和最小公倍式。

**性质10. 域上多项式环是主理想整环** 域上多项式环 $F[x]$ 中的任意理想 $I$ 都可以由其中一个元素生成。设这个元素为 $f(x)$，有理想 $I = (f(x))$，形如这样的理想被称为主理想。若环中任意理想都是主流想，这个环被称为主理想环。

## 5. 代码示例

我们可以使用`sympy`包在python中进行多项式环的运算：

```python
from sympy import symbols, Poly, GF, gcd

# 定义符号变量
x = symbols('x')

# 定义多项式，系数在整数模5环中
p1 = Poly(2*x**3 + 3*x**2 + x + 1, x, domain=GF(5))
p2 = Poly(x**2 + 4*x + 4, x, domain=GF(5))

# 打印多项式
print("多项式p1:", p1)
print("多项式p2:", p2)


# 多项式加法
add_result = p1 + p2
print("加法结果:", add_result)

# 多项式减法
sub_result = p1 - p2
print("减法结果:", sub_result)

# 多项式乘法
mul_result = p1 * p2
print("乘法结果:", mul_result)

# 注意：在整数模n环中，不能总是进行多项式除法
# 但可以进行模运算
mod_result = p1 % p2
print("取余运算:", mod_result)

# 求商
quotient_result = p1 // p2
print("商:", quotient_result)

# 求最大公约数
gcd_result = gcd(p1, p2)
print("最大公约数:", gcd_result)

# 代入值求解
value_result = p1.subs(x, 2)
print("在多项式 p1 中代入 x = 2 的结果:", value_result)

## 输出示例
# 多项式p1: Poly(2*x**3 - 2*x**2 + x + 1, x, modulus=5)
# 多项式p2: Poly(x**2 - x - 1, x, modulus=5)
# 加法结果: Poly(2*x**3 - x**2, x, modulus=5)
# 减法结果: Poly(2*x**3 + 2*x**2 + 2*x + 2, x, modulus=5)
# 乘法结果: Poly(2*x**5 + x**4 + x**3 + 2*x**2 - 2*x - 1, x, modulus=5)
# 取余运算: Poly(-2*x + 1, x, modulus=5)
# 商: Poly(2*x, x, modulus=5)
# 最大公约数: Poly(x + 2, x, modulus=5)
# 在多项式 p1 中代入 x = 2 的结果: 1
```

## 6. 总结

这一讲，我们简要介绍了多项式环的定义、性质以及域上多项式环。其中，域上多项式在密码学和零知识证明中经常用到，它和整数非常相似，支持欧几里得除法，有类似素数的不可约多项式，可以被唯一的因式分解，并且存在最大公约式和最小公倍式。