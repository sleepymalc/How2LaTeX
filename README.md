# How2LaTeX
This is a quick guide of writing $\LaTeX$ **CORRECTLY.** Throughout this tutorial, I assume you're familiar with basic $\LaTeX$ syntex and know how to do all the basic stuffs, e.g., compiling, using `itemize`, `enumerate` environments.

## The Basic

When writing paragraphs, $\LaTeX$ will wrap text in adjacent lines as if they were *part of the same paragraph*, while treat `\n` as a sign for starting a new paragraph.

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

