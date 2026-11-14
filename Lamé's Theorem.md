---
created: 2026-04-15 21:19
tags:
  - 离散数学
---
# Lamé's Theorem
---

## 目的
用来计算[[算法学习笔记(8)：拓展欧几里得]]中欧几里得算法的复杂度。
其实这个部分在课程中仅仅作为一个示例，作为递推的例子。

## 内容
![[Pasted image 20260415211325.png]]
### Proof
 # Proof Sketch of Lamé's Theorem

*   Let $n$ be the number of divisions.
*   The remainders $r_i$ satisfy $r_i \ge r_{i+1} + r_{i+2}$.
*   Comparing this to the Fibonacci recurrence, we find $r_n \ge 1 = f_2, r_{n-1} \ge 2 = f_3, ..., b = r_1 \ge f_{n+1}$.
*   Using $f_{n+1} > \alpha^{n-1}$ [^1]and taking logs:
    $$n - 1 < 5 \log_{10} b$$
*   If $b$ has $k$ digits, $b < 10^k$, so $n \le 5k$.

[^1]: [[斐波那契数列的下界性质]]
# 3. 证明主体： Lamé 定理 (Lamé's Theorem)

## 欧几里得算法步骤

考虑欧几里得算法的一系列除法步骤，设 $a > b$：

$$
\begin{aligned}
a &= q_1 b + r_1, & 0 \le r_1 < b \\
b &= q_2 r_1 + r_2, & 0 \le r_2 < r_1 \\
r_1 &= q_3 r_2 + r_3, & 0 \le r_3 < r_2 \\
&\vdots & \\
r_{n-2} &= q_n r_{n-1} + r_n, & r_n \neq 0 \\
r_{n-1} &= q_{n+1} r_n + 0 & 
\end{aligned}
$$

这里 $n$ 是算法的步数（即除法执行的次数），$r_n = \gcd(a, b)$ 是最后一个非零余数。

---

## 步骤 1：构造余数序列的下界

由于商 $q_i \ge 1$（除非余数为 0），我们有：
$$
\begin{aligned}
r_1 &< b \\
r_2 &< r_1 \\
&\vdots \\
r_n &< r_{n-1}
\end{aligned}
$$

更关键的是，从最后一个非零余数开始反向推导，可以建立余数与斐波那契数列的联系。

**核心观察**：余数序列满足 $r_i \ge r_{i+1} + r_{i+2}$。
**推导**：这是因为 $q_{i+2} \ge 1$，所以：
$$r_i = r_{i+1} q_{i+2} + r_{i+2} \ge r_{i+1} \cdot 1 + r_{i+2} = r_{i+1} + r_{i+2}$$

---

## 步骤 2：与斐波那契数列比较

利用上述不等式，我们可以对每个余数进行下界估计（设斐波那契数列 $f_1=1, f_2=1, f_3=2, \dots$）：

1.  $r_n \ge 1 = f_2$
2.  $r_{n-1} \ge r_n + r_{n+1}$ (注意 $r_{n+1}=0$，此处直接比较大小)
    *   实际上，$r_{n-1} > r_n \ge 1 \implies r_{n-1} \ge 2 = f_3$
3.  $r_{n-2} \ge r_{n-1} + r_n \ge 2 + 1 = 3 = f_4$
4.  $\dots$
5.  一般地，通过归纳可得：
    $$b \ge r_1 \ge f_{n+2}$$
    *(注：笔记中记为 $b = r_1 \ge f_{n+1}$，此处根据标准定义修正索引，核心逻辑一致)*

---

## 步骤 3：引入对数与位数

我们知道 $b \ge f_{n+1}$（按笔记记号）。结合核心引理 $f_{n+1} > \alpha^{n-1}$（其中 $\alpha = \frac{1+\sqrt{5}}{2} \approx 1.618$ 是黄金比例），得到：

$$b > \alpha^{n-1}$$

两边取以 10 为底的对数：
$$\log_{10} b > (n-1) \log_{10} \alpha$$

代入 $\log_{10} \alpha \approx 0.20899$，计算其倒数：
$$\frac{1}{\log_{10} \alpha} \approx 4.785$$

因此：
$$n-1 < \frac{1}{\log_{10} \alpha} \cdot \log_{10} b \approx 4.785 \cdot \log_{10} b < 5 \log_{10} b$$

---

## 步骤 4：与位数挂钩

如果 $b$ 是一个 $k$ 位数，那么 $b < 10^k$，即：
$$\log_{10} b < k$$

代入上式：
$$n-1 < 5k$$

由于 $n$ 和 $k$ 都是整数，故：
$$n \le 5k$$

---
