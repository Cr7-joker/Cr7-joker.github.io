---
title: Markdown mathematical formula
tags: Math Markdown
edit: 2019-02-07
categories: Markdown
status: Completed
description: This article aims to record the coding rules of some commonly used mathematical expressions in MarkDown. In fact, LaTeX coding rules are used. These rules can also be used in some functions and expressions of matlab to bring convenience to their work.
---

# 基本语法

## 呈现位置

- 所有公式定义格式为

```
$ . . . $
```

- 具体语句例如

```
$\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t$
```

$\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t​$

- 居中并放大显示

```
$$\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t$$
```

$$
\sum_{i=0}^N\int_{a}^{b}g(t,i)\text{d}t
$$

# 希腊字母

| 显示 |    命令     |    显示    |    命令     |
| :--: | :---------: | :--------: | :---------: |
|  α   |  \$\alpha$  |     β      |  \$\beta$   |
|  γ   |  \$\gamma$  |     δ      |  \$\delta$  |
|  ϵ   | \$\epsilon$ |     ζ      |  \$\zeta$   |
|  η   |   \$\eta$   |     θ      |  \$\theta$  |
|  ι   |  \$\iota$   |  $\kappa$  |  \$\kappa$  |
|  λ   | \$\lambda$  |     μ      |   \$\mu$    |
|  ν   |   \$\nu$    |     ξ      |   \$\xi$    |
|  π   |   \$\pi$    |     ρ      |   \$\rho$   |
|  σ   |  \$\sigma$  |     τ      |   \$\tau$   |
|  υ   | \$\upsilon$ |     ϕ      |   \$\phi$   |
|  χ   |   \$\chi$   |     ψ      |   \$\psi$   |
|  ω   |  \$\omega$  | $\omicron$ | \$\omicron$ |

- 如果需要大写的希腊字母，只需将命令的首字母大写即可(有的字母没有大写)，如

```
$\gamma$ & $\Gamma$
```

$\gamma$ & $\Gamma$

- 若需要斜体希腊字母，在命令前加上var前缀即可(大写可斜)，如

```
$\Gamma$ & $\varGamma$
```

$\Gamma$ & $\varGamma$



# 字母修饰

## 上下标

- 上标：^
- 下标：_

```
$C_n^2$
```

$C_n^2$



## 矢量

- 例1

```
$\vec a$
```

$\vec a$

- 例2

```
$\overrightarrow a$
```

$\overrightarrow a​$



## 字体

Typewriter:

```
$\mathtt {ABCDEFGHIJKLMNOPQRSTUVWXYZ}$
```

$\mathtt {ABCDEFGHIJKLMNOPQRSTUVWXYZ}​$


<br/>Blackboard Bold:

```
$\mathbb {ABCDEFGHIJKLMNOPQRSTUVWXYZ}$
```

$\mathbb {ABCDEFGHIJKLMNOPQRSTUVWXYZ}$



<br/>Sans Serif:

```
$\mathsf {ABCDEFGHIJKLMNOPQRSTUVWXYZ}$
```

$\mathsf {ABCDEFGHIJKLMNOPQRSTUVWXYZ}$



## 分组

{}有分组功能，如

```
$10^{10}$ & $10^10$
```

$10^{10}$ & $10^10$



## 括号

小括号：\$()\$显示()

中括号：\$[]\$显示[]

尖括号：\$\langle\rangle\$显示⟨⟩

使用​\$\left(​$ 和\$\right)\$使符号大小与邻近的公式相适应，括号类型可换，如

```
$(\frac{x}{y})$ & $\left(\frac{x}{y}\right)$
```

$(\frac{x}{y})$ & $ \left(\frac{x}{y}\right)$



## 累加和累乘

- \sum_{ }^{ }
- 累加号的上标下标的前后顺序可以互换。

|    名称    |      数学表达式      |     markdown公式      |
| :--------: | :------------------: | :-------------------: |
|   求和号   |     $\sum{3x^n}$     |     \$\sum{3x^n}$     |
| 带范围求和 | $\sum_{n=1}^N{3x^n}$ | \$\sum_{n=1}^N{3x^n}$ |

<br/>

- \prod_{ }^{ }
- 累乘号的上标下标的前后顺序可以互换。

|    名称    |      数学表达式       |      markdown公式      |
| :--------: | :-------------------: | :--------------------: |
|   求积号   |     $\prod{3x^n}$     |     \$\prod{3x^n}$     |
| 带范围求乘 | $\prod_{n=1}^N{3x^n}$ | \$\prod_{n=1}^N{3x^n}$ |

<br/>

## 极限和积分

极限\lim，如

```
$\lim_{x\to 0}$
```

$\lim_{x\to 0}$

<br/>积分\int，如

```
$\int_0^\infty{fxdx}$
```

$\int_0^\infty{fxdx}$



## 分式与根式

- 分式\frac，如

```
$\frac{公式一}{公式二}$
```

$\frac{公式一}{公式二}$

<br/>- 根式\sqrt，如

```
$\sqrt[x]{y}$
```

$\sqrt[x]{y}$



## 特殊函数

- \函数名，如

```
$\sin x$ & $\ln x$ & $\max(A,B,C)$ & $\log_2{18}$
```

$\sin x$ & $\ln x$ & $\max(A,B,C)$ & $\log_2{18}$



# 特殊符号

| 显示 |      命令      |       显示        |        命令        |
| :--: | :------------: | :---------------: | :----------------: |
|  ∞   |   \$\infty$    |         ∪         |      \$\cup$       |
|  ∩   |    \$\cap$     |         ⊂         |     \$\subset$     |
|  ⊆   |  \$\subseteq$  |         ⊃         |     \$\supset$     |
|  ∈   |     \$\in$     |         ∉         |     \$\notin$      |
|  ∅   | \$\varnothing$ |         ∀         |     \$\forall$     |
|  ∃   |   \$\exists$   |         ¬         |      \$\lnot$      |
|  ∇   |   \$\nabla$    |         ∂         |    \$\partial$     |
|  ≥   |    \$\geq$     |         ≤         |      \$\leq$       |
|  ±   |     \$\pm$     |         ⋅         |      \$\cdot$      |
|  ×   |   \$\times$    |         ÷         |      \$\div$       |
|  ≠   |    \$\not=$    |         ≮         |      \$\not<$      |
|  ⊅   | \$\not\supset$ |   $\not\subset$   |   \$\not\supset$   |
|  ⊥   |    \$\bot$     |         ∠         |     \$\angle $     |
|  ∘   |    \$\circ$    |         ↑         |    \$\uparrow$     |
|  ↓   | \$\downarrow$  |         ←         |   \$\leftarrow$    |
|  →   | \$\rightarrow$ | $\longrightarrow$ | \$\longrightarrow$ |

<br/>

## 空格

- LaTex会忽略空格
- 小空格 \ ，如

```
$a\ b$
```

$a\ b$

<br/>

- 4个空格\quad，如

```
$a\quad b$
```

$a\quad b$



# 矩阵

## 基本语法

- 起始标记begin{matrix}
- 结束标记end{matrix}
- 每行末尾标记\\
- 行间元素之间以&分隔
- 如

```
$$\begin{matrix}
1&0&0\\
0&1&0\\
0&0&1\\
\end{matrix}$$
```

$$\begin{matrix}
1&0&0\\
0&1&0\\
0&0&1\\
\end{matrix}​$$ 

## 矩形边框

- 将matrix换成下列词语

|  命令   |    样式    |
| :-----: | :--------: |
| matrix  |   无样式   |
| pmatrix | 小括号边框 |
| bmatrix | 中括号边框 |
| Bmatrix | 大括号边框 |
| vmatrix | 单竖线边框 |
| Vmatrix | 双竖线边框 |

## 省略元素

- 横省略号\cdots

- 竖省略号\vdots

- 斜省略号\ddots

  如

```
$$\begin{vmatrix}
{a_{11}}&{a_{12}}&{\cdots}&{a_{1n}}\\
{a_{21}}&{a_{22}}&{\cdots}&{a_{2n}}\\
{\vdots}&{\vdots}&{\ddots}&{\vdots}\\
{a_{m1}}&{a_{m2}}&{\cdots}&{a_{mn}}\\
\end{vmatrix}$$
```

$$
\begin{vmatrix}
{a_{11}}&{a_{12}}&{\cdots}&{a_{1n}}\\
{a_{21}}&{a_{22}}&{\cdots}&{a_{2n}}\\
{\vdots}&{\vdots}&{\ddots}&{\vdots}\\
{a_{m1}}&{a_{m2}}&{\cdots}&{a_{mn}}\\
\end{vmatrix}
$$

## 阵列

- 起始、结束处以{array}声明

- 对齐方式：在{array}后以{}逐行统一声明<br/> 
  左对齐：1；居中：c；右对齐：r； <br/>
  竖直线：在声明对齐方式时，插入|建立竖直线

- 插入水平线：\hline

  如

  ```
  $$\begin{array}{c|111}
  {any}&{a}&{b}&{c}\\
  \hline
  {R_1}&{c}&{b}&{a}\\
  {R_2}&{b}&{c}&{a}\\
  \end{array}$$
  ```

  $$
  \begin{array}{c|111}
  {any}&{a}&{b}&{c}\\
  \hline
  {R_1}&{c}&{b}&{a}\\
  {R_2}&{b}&{c}&{a}\\
  \end{array}
  $$

  ## 方程组

  - 起始、结束处以{cases}声明

    如

    ```
    $$\begin{cases}
    a_1x+b_1y+c_1z=d_1\\
    a_2x+b_2y+c_2z=d_2\\
    a_3x+b_3y+c_3z=d_3\\
    \end{cases}$$
    ```

    $$
    \begin{cases}
    a_1x+b_1y+c_1z=d_1\\
    a_2x+b_2y+c_2z=d_2\\
    a_3x+b_3y+c_3z=d_3\\
    \end{cases}
    $$

    

  