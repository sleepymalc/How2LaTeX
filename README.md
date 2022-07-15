# How2LaTeX
This is a quick guide to help you write $\LaTeX$ in a **professional** way. Throughout this tutorial, I assume you're familiar with the basic $\LaTeX$ syntax and know how to do all the basic stuff, e.g., compiling, using `itemize`, `enumerate` environments, etc.

For a more advanced $\LaTeX$ setup, please see my [VSCode-LaTeX-Inkscape](https://github.com/sleepymalc/VSCode-LaTeX-Inkscape) to typeset your $\LaTeX$ documents efficiently and also draw professionally.

## Table of Content

* [The Basic](#the-basic)
  + [Newline `\\`](#newline-----)
* [Math Environment](#math-environment)
  + [Math mode](#math-mode)
  + [Text in Math mode](#text-in-math-mode)
  + [Symbols](#symbols)
    - [Semantic](#semantic)
    - [Misused](#misused)
    - [Else](#else)
  + [Sizing](#sizing)
    - [Automatic Sizing](#automatic-sizing)
    - [Manual Sizing](#manual-sizing)
    - [Else](#else-1)
  + [Spacing](#spacing)
  + [Limits](#limits)
* [Reference and Citation](#reference-and-citation)
* [Else](#else-2)

## The Basic

### Newline `\\`

I often see things like

```latex
This is one paragraph.\\

This is another.
```

When writing paragraphs, $\LaTeX$ will wrap text in adjacent lines as if they were *part of the same paragraph*, while treating `\n` (i.e., newline symbol) as a sign for starting a new paragraph.

```latex
This is 
one paragraph

This is another.
```

Output will be like 

```bash
This is one paragraph.

This is another.
```

Hence, while `\\` will create a new line and start a new paragraph, as we now know, if you already have a blank line between paragraphs, `\\` is redundant.

## Math Environment

### Math mode

As you know, `$...$` and `$$...$$` are two commonly used commands to write mathematical expression. For example, `$e^{i\pi} + 1 = 0$` produces $e^{i\pi} + 1 = 0$, while `$$e^{i\pi} + 1 = 0$$` produces

$$e^{i\pi} + 1 = 0.$$

Both `$...$` and `$$...$$` are fine but this is why you should avoid them: they are $\TeX$ commands, which is too old in some sense. A better way to write math equations is to use `\(...\)` and `\[...\]`, which is supported by modern $\LaTeX$.

> While `equation*` environment is also an good option for unnumbered equations, but I tend to keep things simple and unified. For numbered equation, `equation` and `align` environment should be used. We'll talk about referencing numbered equations later.

### Text in Math mode

When you need to have some texts in your math equation, **please** use `\text{...}` to wrap the texts around. For example,

```latex
\[
	x_i \geq 0 \text{ for all } i,
\]
```
which produces

$$x_i \geq 0 \text{ for all }i$$

is a good example. Notice that you should always indent both sides of your text inside `\text{}`, otherwise you'll have something like 

$$x_i\geq 0\text{for all}i,$$

which is not desirable since $\LaTeX$ will neglect any spacing in math mode.

> If you write somehting like `$x y$`, you'll just get $x y$ instead of $x\\; y$. More about spacing in Math mode later.

Also, you should always think twice when choosing between `\text{}` or `\mathrm{}`. They render the same output, but it's always a good habit to keep your source code clean and **semantically correct**. A quick guide is that when writing **text**, use `\text{}`, when writing **math shorthand**, use `\mathrm{}` instead. For example, if a variable $u_{\text{up}}$ has a flag `up`, you should write `u_{\text{up}}` instead of `u_{\mathrm{up}}` since `up` is a text. But if you're doing an integral, say 

$$\int x\\,\mathrm{d}x,$$

you should write `\int x \,\mathrm{d}x` instead of `\int x \,\text{d}x`.

### Symbols

Most of the time, when you're writing a math symbol with your direct keyboard input, there's a corresponding command in $\LaTeX$ as well. Here is a short list of them:

* `:` (`\colon`): Instead of writing `f: X \to Y` for $f:X\to Y$, write `f\colon X \to Y` instead.

* `...` (`\ldots`): This is a straightforward one. Instead of writing `a_1, a_2, ...` for $a_1, a_2, \ldots$, write `a_2, a_2, \ldots` instead.

  > There's something called `\cdots` also, which is my personal preferred one. If you really want to know about `...`, there are actually five types of them:
  > <div align="center">
  > 
  > | Code                  | Output                | Comment                                      |
  > | --------------------- | --------------------- | -------------------------------------------- |
  > | `A_1, A_2, \dotsc`    | $A_1, A_2, \dotsc$    | for **dots with commas**                     |
  > | `A_1 + \dotsb + A_N`  | $A_1 + \dotsb + A_N$  | for **dots with binary operators/relations** |
  > | `A_1 \dotsm A_N`      | $A_1 \dotsm A_N$      | for **multipication dots**                   |
  > | `\int_{a}^{b} \dotsi` | $\int_{a}^{b} \dotsi$ | for **dots with integrals**                  |
  > | `A_1\dotso A_N`       | $A_1\dotso A_N$       | for **other dots**                           |
  >
  > </div>
  > 
  > The above is the conventions suggested by American Mathematical Society. If you don't want to follow them strictly, just choose one of them and stick with it.

* `'` (`\prime`): When you need to render $x^\prime$, write `x^\prime` instead of simply `x'`.

* `*` (`\ast`): When you need to render $x^\ast$, write `x^\ast` instead of simply `x*`.

  > There are also something called `\star`, which produces $\star$. In some cases, $x^\star$ may be desired.

* `~` (`\sim`): This is often used when you want to say something like $x\sim \mathcal{N}(0 ,1)$, i.e., $x$ is sampled from a normal distribution. In this case, write `x \sim \mathcal{N}(0, 1)` instead of `x ~ \mathcal{N}(0, 1)`.

* `:=`, `=:` (`\coloneqq`, `\eqqcolon`): A direct one. When you define a new symbol such as let $y\coloneqq x_1-x_2$, write `y \coloneqq x_1 - x_2` instead of `y := x_1 - x_2`.

  > This need `\usepackage{mathtools}` in your header, namely you need `mathtools` package.

* `>>`, `<<` (`\gg`, `\ll`): Use `\gg` for much greater than and `\ll` for much less than instead of directly using `>>` and `<<`. The former ones produce $\gg$, $\ll$, while the latter ones produce $>>$ and $<<$.

#### Semantic

There are also commands which produce exactly the same output, but with different semantics. To keep the source code clean, we mention some of them.

* `\rightarrow` v.s. `\to` ($\rightarrow$): I use `\to` for mapping, e.g. $f\colon X\to Y$, while `\rightarrow` for all other cases.

* `\leftarrow` v.s. `\gets` ($\leftarrow$): I use `\gets` when writing pseudocode, while `\leftarrow` for all other cases.

* `\Rightarrow` v.s. `\implies` ($\Rightarrow$ v.s. $\implies$): I use `\implies` when writing proofs, while `\Rightarrow` for all other cases.

* `\Leftarrow` v.s. `\impliedby` ($\Leftarrow$ v.s. $\impliedby$): I use `\impliedby` when writing proofs, while `\Leftarrow` for all other cases.

* `\Leftrightarrow` v.s. `\iff` ($\Leftrightarrow$ v.s. $\iff$): Similarly, I use `\iff` when writing proofs, while `\Leftrightarrow` for all other cases.

  > Since `\implies`, `\impliedby`, and also `\iff` are quite long, so I redefined them into their corresponding ones for a more compact look. But in the code, I still type `\implies` when writing proof. To redefine them, put
  >
  > ```latex
  > \let\implies\Rightarrow
  > \let\impliedby\Leftarrow
  > \let\iff\Leftrightarrow
  > ```
  >
  > into your preamble.

#### Misused

I sometimes saw something like $\cup_{i=1}^{\infty} X_i$ instead of $\bigcup\nolimits_{i=1}^\infty X_i$. Clearly, the latter one is preferred since `\cup` is a binary operator, so it should only be used when you want to write something like $A\cup B$. If you want to perform such operation multiple time as our example, use `\bigcup` instead. Below are some examples.

<div align="center">

| Operation      | Standard form code | Output    | Big form code | Output       |
| -------------- | ------------------ | --------- | ------------- | ------------ |
| Intersection   | `\cap`             | $\cap$    | `\bigcap`     | $\bigcap$    |
| Disjoint union | `\sqcup`           | $\sqcup$  | `\bigsqcup`   | $\bigsqcup$  |
| Tensor product | `\otimes`          | $\otimes$ | `\bigotimes`  | $\bigotimes$ |
| Disjunction    | `\vee`             | $\vee$    | `\bigvee`     | $\bigvee$    |
| Conjunction    | `\wedge`           | $\wedge$  | `\bigwedge`   | $\bigwedge$  |

</div>

#### Else

There are two symbols I want to mention, the **empty set** symbol and **l** (ell). You can either write `\emptyset` or `\varnothing` to denote an empty set, which produces $\emptyset$ and $\varnothing$. I prefer the latter one, but choose whatever you want. On the other hand, it seems like not everyone knows the command `\ell` for producing a nice looking $\ell$, and instead, they simply type `l`, which produces $l$.

### Sizing

The most painful thing when I read a $\LaTeX$ document is when seeing something like 

$$N \coloneqq \vert\sum\limits_{j=1}^\infty(\sum\limits_{i=1}^\infty X_{ij})\vert$$

with the source code being 

```latex
\[
	N \coloneqq \vert \sum\limits_{j=1}^\infty ( \sum\limits_{i=1}^\infty X_{ij} ) \vert.
\]
```

The size of the absolute value and the parenthesis are still in the default size, while the formula being wrapped is much higher than the default size. Before we talk about how to resolve this sizing issue, we should first see the common commands which will cause this kind of problem.

* `|...|` (`\vert ... \vert`): This is a fun one, since we often use this to denote the absolute value like $\vert x \vert$. In this case, write `\vert x \vert` instead of `|x|`. 

* `||...||` (`\lVert ... \rVert` or `\| ... \|`): For norm, write `\|x\|` instead of `||x||` for $\lVert x\rVert$.

  > We'll talk about this later. Notice that you can also write `\Vert x \Vert` for $\Vert x\Vert$, though I still prefer `\lVert x \rVert`.

* `[...]` (`\lbrack ... \rbrack` or `[ ... ]`): They are indeed equivalent, so I prefer `[ ... ]` for simplicity.

* `<...>` (`\langle ... \rangle`)

* `{...}` (`\{ ... \}`)

Let's see how we can fix this. 

#### Automatic Sizing
To automatically resize the brackets, and parentheses, we use `\left...\right...` to do this. For the above example, the resized formula should be

```latex
\[
	N \coloneqq \left\vert \sum\limits_{j=1}^\infty \left( \sum\limits_{i=1}^\infty X_{ij} \right) \right\vert
\]
```

  which produces

$$N \coloneqq \left\vert\sum\limits_{j=1}^\infty\left(\sum\limits_{i=1}^\infty X_{ij}\right)\right\vert.$$

Interesting enough, though this is already powerful, but there are more commands can be utilized. They are `\left.`/`\right.` and `\middle`. A typical usage for `\left.` or `\right.` is when you want to automatically resize an operator which only appears on one side. For example:

$$\left.\frac{x^2}{2}\right\vert_0^1$$
with the source code being

```latex
\left. \frac{x^2}{2} \right|_0^1
```

And for `\middle`, you might have encountered the following situation:

$$\Delta^n\coloneqq \left\\{(t_0, \ldots, t_n)\in\mathbb{R}^{n+1} | t_i\geq 0, \sum_{i=0}^{n}t_i=1\right\\}$$

We se that $|$ is not being resized together with $\\{ \\}$. To do this, we add a `\middle` before `|` and get

$$\Delta^n\coloneqq \left\\{(t_0, \ldots, t_n)\in\mathbb{R}^{n+1}\middle| t_i\geq 0, \sum_{i=0}^{n}t_i=1\right\\}$$

as we desired.

#### Manual Sizing

Sometimes the automatic sizing may tend to be too big since it's trying to wrap everything inside, for example, $\vert \hat{x}^{(n)}_i\vert$ is way better than $\left\vert \hat{x}^{(n)}_i \right\vert$ while the latter uses `\left\vert ... \right\vert` and the former simply uses `\vert ... \vert`. In this case, uses `\big`, `\Big`, `\bigg` and `\Bigg` instead of `\left` and `\right` as modifiers. For example, 

```latex
\[
	( \big( \Big( \bigg( \Bigg(
\]
```

produces

$$( \big( \Big( \bigg( \Bigg($$

A typical use case is that, `\left( k g(x) \right)` produces $\left( k g(x) \right)$, while `\left` and `\right` produce the same size delimiters as those nested within it. In this case, we can use `\big( k g(x) \big)`, which produces $\big( k g(x) \big)$ to further distinguish the nested parentheses.

> A particularly important use case is that, when you uses `\underbrace`, the automatic resizing will be larger than expected. For example,
>
> $$\mathbb{E}\left\lbrack \underbrace{\prod_{i=0}^\infty X_i}\right\rbrack\text{ v.s. }\mathbb{E}\bigg[ \underbrace{\prod_{i=0}^{\infty} X_i}\bigg],$$ 
>
> where I use `\left[ ... \right]` on the left and `\bigg[ ... \bigg]` on the right. Notice that we even haven't written anything under the braces, and the left one is already ugly.

#### Else

Another thing relates to the sizing is the way of handling **continued fractions**. If we use `\frac{}{}` throughout, we'll have something like

$$x = a_0 + \frac{1}{a_1 + \frac{1}{a_2 + \frac{1}{a_3 + \frac{1}{a_4} } } }$$

with code being

```latex
\[
	x = a_0 + \frac{1}{a_1 + \frac{1}{a_2 + \frac{1}{a_3 + \frac{1}{a_4} } } }
\]
```

which is ugly. Instead, we use `\cfrac{}{}`, where that extra `c` stands for `continued`. In this case, we have

$$x = a_0 + \cfrac{1}{a_1 + \cfrac{1}{a_2 + \cfrac{1}{a_3 + \cfrac{1}{a_4} } } },$$

with the code being

```latex
\[
	x = a_0 + \cfrac{1}{a_1 + \cfrac{1}{a_2 + \cfrac{1}{a_3 + \cfrac{1}{a_4} } } }.
\]
```

### Spacing

As we have seen before, when I type an indefinite integral, we have something like

$$\int x\\,\mathrm{d}x$$

with the source code being `\int x\,\mathrm{d}x`. Notice that there's a `\,` before $\mathrm{d}x$, which gives us a small indent. since if we don't have this `\,`, we will end up with

$$\int x\mathrm{d}x,$$

where $x^2\mathrm{d}x$ is now a single entity rather than two independent ones. $\LaTeX$ provides several such commands to give you a small indent.

<div align="center">

| Command | Description    | Size                 |
| ------- | -------------- | -------------------- |
| `\,`    | small space    | $3/18$ of a `\quad`  |
| `\:`    | medium space   | $4/18$ of a `\quad`  |
| `\;`    | large space    | $5/18$ of a `\quad`  |
| `\!`    | negative space | $-3/18$ of a `\quad` |

</div>

> While `\quad` and `\qquad` are commonly used for spacing in every scenario, the above only works in math environments.

### Limits

When using inline math environment, you'll often see $\sum\nolimits_{i=1}^\infty x_i$, which is the default behavior when typing `\sum_{i=1}^\infty x_i`. But if you type the same thing in display math mode, you'll get 

$$\sum_{i=1}^\infty x_i$$

instead. You can indeed put the subscript and supscript below/on the summation symbol in inline math mode by using `\limits`. For example, $\sum\limits_{i=1}^\infty x_i$ by using `\sum\limits_{i=1}^\infty x_i`. This `\limits` command can be used in various scenarios, for examples, $\prod$, $\lim$, $\coprod$, or $\bigcup$ and $\bigcap$.

> This indeed works for all **big** commands like $\int$, $\iint$, $\iiint$, $\iiiint$, $\oint$, $\idotsint$, $\bigodot$, $\bigoplus$, $\bigotimes$, $\bigvee$, $\bigwedge$, $\bigsqcup$, $\biguplus$. For example, $\bigoplus\nolimits_{i=1}^\infty G_i$ v.s. $\bigoplus\limits_{i=1}^\infty G_i.$ 
>
> But notice that `\limits` works differently with integral signs: It'll put the upper-bound directly on top of the integral sign, and the same is done for the lower-bound. For example: 
>
> $$\int_{a}^{b} x\\,\mathrm{d}x\text{ v.s. }\int\limits_{a}^{b} x\\,\mathrm{d}x.$$
>
> Notice that if you want to apply this to all your integral, please use `\usepackage[intlimits]{amsmath}` when loading `amsmath` package. This will only be applied when using integrals, since as mentioned, `\limits` with integral is treated differently.

## Reference and Citation

> TODO

## Else

Sometimes you may want to define your operators. For example, while there is a default `\ker` for producing the kernel of a function like $\ker(f)$, there is no default `\im` for the image of a function. To do this, we should use

```latex
\DeclareMathOperator{\im}{Im}
```

instead of

```latex
\newcommand{\im}{\mathrm{Im}}
```

since we'll have some spacing issues if we go with the latter one.
