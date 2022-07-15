# How2LaTeX
This is a quick guide of writing $\LaTeX$ **CORRECTLY.** Throughout this tutorial, I assume you're familiar with basic $\LaTeX$ syntex and know how to do all the basic stuffs, e.g., compiling, using `itemize`, `enumerate` environments.

## The Basic

### Newline `\\`

I frequently saw the following:

```latex
This is one paragraph.\\

This is another.
```

---

When writing paragraphs, $\LaTeX$ will wrap text in adjacent lines as if they were *part of the same paragraph*, while treat `\n` (i.e., newline symbol) as a sign for starting a new paragraph.

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

Hence, while `\\` will create a new line, hence start a new paragraph, but as we now know, if you already have a blank line between paragraphs, `\\` is redundant.

## Math Environment

### Math mode

As you know, `$...$` and `$$...$$` are two commonly used commands to write mathematical expression. For example, `$e^{i\pi} + 1 = 0$` produces $e^{i\pi} + 1 = 0$, while `$$e^{i\pi} + 1 = 0$$` produces

$$e^{i\pi} + 1 = 0$$

While the former is fine, but the latter one will cause some problems. The reason is that `$...$` and `$$...$$` are $\TeX$ commands, which is too old in some sense. A better way to write math equation is to use `\(...\)` and `\[...\]`, which is supported by modern $\LaTeX$.

> While `equation*` environment is also an good option for not numbered equations, but I tend to keep things simple and unified. For numbered equation, `equation` and `align` environment should be used. We'll talk about referencing numbered equations later.

### Text in Math mode

When you need to have some texts in your math equation, **please** use `\text{...}` wrapping your texts around. For examples,

```latex
\[
	x_i \geq 0 \text{ for all }i
\]
```

is a good example. Notice that you should always indent your text inside `\text{}`, otherwise you'll have something like 

$$x_i\geq 0\text{for all}i,$$

which is not desireable. 

Also, you should always think twice when choosing between `\text{}` or `\mathrm{}`. They render the same output, but it's always a good habit (for others) to keep your source code clean. A quick guide is that when writing **text**, use `\text{}`, when writing **math shorthand**, use `\mathrm{}` instead. For example, if a variable $u_{\text{up}}$ has a flag `up`, you should write `u_{\text{up}}` instead of `u_{\mathrm{up}}` since `up` is a text. But if you're doing an integral, say 

$$\int x^2\mathrm{d}x,$$

you should write `\int x^2 \mathrm{d}x` instead of `\int x^2 \text{d}x`.

### Symbols

Most of the time, when you're writing a math symbol with your direct keyboard input, there's a command in $\LaTeX$ instead. Here is a short list of them:

* `:` (`\colon`): Instead of writing `f:X\to Y` for $f:X\to Y$, write `f\colon X\to Y` instead.

* `...` `(\ldots`): This is a straightforward one. Instead of writing `a_1, a_2, ...` for $a_1, a_2, \ldots$, write `a_2, a_2, \ldots` instead.

  > There's something called `\cdots` also, which is my personal perferred one. If you really want to know about `...`, there are actually five types of them:
  >
  > | Code                  | Output                | Comment                                      |
  > | --------------------- | --------------------- | -------------------------------------------- |
  > | `A_1, A_2, \dotsc`    | $A_1, A_2, \dotsc$    | for **dots with commas**                     |
  > | `A_1 + \dotsb + A_N`  | $A_1 + \dotsb + A_N$  | for **dots with binary operators/relations** |
  > | `A_1 \dotsm A_N`      | $A_1 \dotsm A_N$      | for **multipication dots**                   |
  > | `\int_{a}^{b} \dotsi` | $\int_{a}^{b} \dotsi$ | for **dots with integrals**                  |
  > | `A_1\dotso A_N`       | $A_1\dotso A_N$       | for **other dots**                           |
  >
  > The above is the conventions suggested by American Mathematical Society. If you don't want to follow them strictly, just choose one of them and stick with it.

* `'` (`\prime`): When you need to render $x^\prime$, write `x^\prime` instead of simply `x'`.

* `*` (`\ast`): When you need to render $x^\ast$, write `x^\ast` instead of simply `x*`.

* `~` (`\sim`): This is often used when you want to say something like $x\sim \mathcal{N}(0 ,1)$, i.e., $x$ is sampled from a normal distribution. In this case, write `x\sim \mathcal{N}(0, 1)` instead of `x~ \mathcal{N}(0, 1)`.

* `:=`, `=:` (`\coloneqq`, `\eqqcolon`): A direct one. When you define a new symbol such as let $y\coloneqq x_1-x_2$, write `y\coloneqq x_1 - x_2` instead of `y:= x_1 - x_2`.

  > This need `\usepackage{mathtools}` in your header, namely you need `mathtools` package.

* `>>`, `<<` (`\gg`, `\ll`): Use `\gg` for much greater than and `\ll` for much less than instead of directly using `>>` and `<<`. The former ones produce $\gg$, $\ll$, while the latter ones produce $>>$ and $<<$.

#### Semantic

There are also commands which produce exactly the same output, but with different semantics. To keep the source code clean, we mention some of them.

* `\rightarrow` v.s. `\to` ($\rightarrow$): I use `\to` for mapping, e.g. $f\colon X\to Y$, while `\rightarrow` for all other usages.

* `\leftarrow` v.s. `\gets` ($\leftarrow$): I use `\gets` when writing pseudocode, while `\leftarrow` for all other useages.

* `\Rightarrow` v.s. `\implies` ($\Rightarrow$ v.s. $\implies$): I use `\implies` when writing proof, while `\Rightarrow` for all other usages.

* `\Leftarrow` v.s. `\impliedby` ($\Leftarrow$ v.s. $\impliedby$): Similarly, I use `\impliedby` when writing proof, while `\Leftarrow` for all other usages.

* `\Leftrightarrow` v.s. `\iff` ($\Leftrightarrow$ v.s. $\iff$): Similarly, I use `\iff` when writing proof, while `\Leftrightarrow` for all other usages.

  > Since `\implies`, `\impliedby`, and also `\iff` are quite long, so I redefined them into their corresponding ones for a more compact look. But in the code, I still type `\implies` when writing proof for a good semantic meaning. To redefine them, put
  >
  > ```latex
  > \let\implies\Rightarrow
  > \let\impliedby\Leftarrow
  > \let\iff\Leftrightarrow
  > ```
  >
  > into your premable.

#### Misused

I sometimes saw somehting like $\cup_{i=1}^{\infty} X_i$ instead of $\bigcup_{i=1}^\infty X_i$. Clearly, the latter one is perferred since `\cup` is a binary operator, so it should only be used when you want to write something like $A\cup B$. If you want to perform such operation multiple time as our example, use `\bigcup` instead. Some other examples are:

* `\cap` v.s. `\bigcap` ($\cap$ v.s. $\bigcap$)
* `\sqcup` v.s. `\bigsqcup` ($\sqcup$ v.s. $\bigsqcup$)
* `\uplus` v.s. `\biguplus` ($\uplus$ v.s. $\biguplus$)
* `\otimes` v.s. `\bigotimes` ($\otimes$ v.s. $\bigotimes$)
* `\odot` v.s. `\bigodot` ($\odot$ v.s. $\bigodot$)
* `\vee` v.s. `\bigvee` ($\vee$ v.s. $\bigvee$)
* `\wedge` v.s. `\bigwedge` ($\wedge$ v.s. $\bigwedge$)

#### Else

Finally, there are a tricky one, the **empty set** symbol. you can either write `\emptyset` or `\varnothing`, which produces $\emptyset$ and $\varnothing$. Personally I prefer the latter one, but choose whatever you want.

Also, it seems that not everyone knows the command `\ell` for producing a nice looking $\ell$, and instead, they simply type `l`, which produces $l$ instead.

### Sizing

#### Brackets, Braces

We first note that there are some commonly misused symbols for different kinds of brackets and braces as follows.

* `||` (`\vert`)

  This is a fun one, since we often use this to denote the absolute value like $\vert x \vert$. In this case, write `\vert x \vert` instead of `|x|`. 

* `|| ||` (`\Vert` or `\|`)

  For norm, write `\|x\|` instead of `||x||` for $\|x\|$.

  > We'll talk about this later. Notice that you can also write `\Vert x\Vert` for $\Vert x\Vert$, which is my preferred one.

* `[]` (`\lbreak` and `\rbreak`)

* `<>` (`\langle` and `\rangle`)

#### Automatic Sizing



#### Manual Sizing

### Limits

When using inline math environment, you'll often see $\sum_{i=1}^\infty x_i$, which is the default behavior when typing `\sum_{i=1}^\infty x_i`. But if you type the same thing in display math mode, you'll get 

$$\sum_{i=1}^\infty x_i$$

instead. You can indeed put the subscript and supscript below/on the summation symbol in inline math mode by using `\limits`. For example, $\sum\limits_{i=1}^\infty x_i$ by using `\sum\limits_{i=1}^\infty x_i`. This `\limits` command can be used in various scenarios, for examples, $\prod$, $\lim$, $\coprod$, or $\bigcup$ and $\bigcap$.

> This indeed works for all **big** commands like $\int$, $\iint$, $\iiint$, $\iiiint$, $\oint$, $\idotsint$, $\bigodot$, $\bigoplus$, $\bigotimes$, $\bigvee$, $\bigwedge$, $\bigsqcup$, $\biguplus$. For example, $\bigoplus_{i=1}^\infty G_i$ v.s. $\bigoplus\limits_{i=1}^\infty G_i.$ 
>
> But notice that `\limits` works differently with integral signs: It'll put the upper-bound directly on top of the integral sign, and the same is done for the lower-bound. For example: 
>
> $$\int_{a}^{b} x\mathrm{d}x\text{ v.s. }\int\limits_{a}^{b} x\mathrm{d}x.$$
>
> Notice that if you want to apply this to all your integral, please use `\usepackage[intlimits]{amsmath}` when loading `amsmath` package. This will only be applied when using integrals, since as mentioned, `\limits` with integral is treated differently.

## Reference
