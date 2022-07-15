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

## Reference
