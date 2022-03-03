# Report Formatting

This guide will provide some advide on how to format and structure your technical reports.

The [su](../files/su.sty)
LaTeX package provides a template for your LaTeX reports in Software Development.

The description of how to set up the package on Overleaf or your local computer can be found after `Using su.sty`.

# Using su.sty
### **When using su.sty you must never change su.sty and how the paper is set up. In the case that let us say the margins or the font size gets smaller than allowed, then you will fail your assignment.**

You can start with a `main.tex` as follows:

```
\documentclass[a4paper]{article}

\usepackage{su}

\header{%
  assignment={Exercise 1: Introduction to C#},%
  authors={Donald E. Knuth <\texttt{knuth@stanford.edu}>},%
  shortAuthors={\texttt{knuth}},%
  date={Friday, February 10, 15:00},%
  year={2019}
}

\begin{document}

\maketitle

\end{document}
```

If you are writing in Danish, you should instead write:

```
\usepackage[danish]{su}
```

When including code snippets we recommend using the `minted` package. It is a
very nice environment for viewing code, as it allows for a lot of customization.

For your convenience we provide a configuration for `minted` in
`su.sty` This configuration is not mandatory, but we expect that all included
code snippets are included through LaTeX code-packages and not as images.
Furthermore we expect both syntax highlighting and line numbers. If you chose to
use our configuration, including code is as easy as the following example:

```
\documentclass[a4paper]{article}

\usepackage{su}

\begin{document}

\maketitle

\inputminted{csharp}{src/code.cs}

\end{document}
```

This example includes an external code file `src/code.cs`. The benefit is that
you get syntax highlighting, and this could be your solution to the programming
exercise in question. Here is some sample code to put into `src/code.cs`:

```
class MyClass : BaseClass {
    // Properties are always capitalized
    public int MyProperty { get; private set; }

    public void MyFunc(int a, int b) {
        for (int i = 0; i < 15; i++) {
            ...
        }
    }
}

```

# Setting su.sty up on Overleaf

If you want to use the su.sty report formatting with **Overleaf** you need to download the .sty file above.
Then you proceed to upload this .sty file to your Overleaf. 

You can then write `\usepackage{su}` at the top of your main.tex. Installing Python and Pygments are only required if you want to use this `.sty` file on your local machine with LaTex.

Do keep in mind that to use the `\inputminted` you do need to upload the files you want input to your overleaf and then provide the path (in the example a folder src and a file inside the folder code.cs)

# Setting su.sty up on your Local Machine

To use it on your local machine, you will have to install [Python 3](https://www.python.org/download/releases/3.0/),
the Python package manager [pip](https://pip.pypa.io/en/stable/installing/),
as well as the [Pygments](http://pygments.org/) package for Python:

```
$ pip install Pygments
```

### Compilation

The technical report can be compiled in a number of different ways:

#### Using `pdflatex`

```
$ pdflatex -shell-escape master.tex
```

That is, provided you've placed `su.sty` either in the same
directory, or in your `~/texmf/tex/latex/` directory.

#### Using `latexrun`

Latexrun is a tool that is designed to make it really nice to compile latex
documents. Instead of +50 lines of random messages you only get errors or
warnings printed in your terminal.
```
$ ./latexrun --latex-args='-shell-escape' master.tex
```

P.S. `latexrun` can be downloaded here:
[latexrun](../files/latexrun) or at
the original [repository](https://github.com/aclements/latexrun).

Remember to make sure that `latexrun` is an executable (`sudo chmod +x latexrun`)!

### Final notes

If `su.sty` or any other files from this repository are changed during the course,
the changes will be announced on Absalon as well as on this repository. We will try our best to ensure backwards compatibility, so using a new version will not break your existing LaTeX-files.
