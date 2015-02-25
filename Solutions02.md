
# Assignment 02 Solutions

**Due:** 2015-02-26, 11:59 PM, as an IPython notebook submitted via your repo in
the course GitHub organization.  Edit the provided Solution02 notebook with your
solutions, placing your solution in cells following each subproblem cell.  All
subproblems are worth 1 point unless otherwise noted.

### Problem 1.1 (1/2 point):

> *How many possible binary logical operations are there?*  Don't just report a
number; briefly explain your reasoning.

### Problem 1.2 (1/2 point):

An important result in propositional logic is that **all** possible logical
operations can be expressed in terms of **NOT**, **AND**, and **OR**; one says
this set of operations is *functionally complete*.  In particular, whatever your
answer was for Problem 1.1, all of those binary operations can be expressed as
some combination of **NOT**, **AND**, and **OR**.  This is important for
probability theory, which is built on expressions for probabilities for these
three operations on propositions.

> *Express **XOR** in terms of **NOT**, **AND**, and **OR** (you may not need
all of them).*

> Present your result as a truth table similar to this:

| $A$ | $B$ |   | OP1 | OP2 | ... |   | **Answer** |
|:---:|:---:|---|:---:|:---:|:---:|---|:----------:|
| 0   | 0   |   | ?   | ?   |     |   | 0          |
| 0   | 1   |   | ?   | ?   |     |   | 1          |
| 1   | 0   |   | ?   | ?   |     |   | 1          |
| 1   | 1   |   | ?   | ?   |     |   | 0          |

> Replace **OP1**, etc., with whatever operations you are composing to construct
**XOR** (i.e., showing the ingredients comprising your expression), and replace
**Answer** with your final expression (e.g., something like $(A\land B)\lor
(\overline{A\lor B}) \land B$, but not exactly that!).

[To quickly create nice Markdown markup for the tables above, I used the
[Markdown TablesGenerator](http://www.tablesgenerator.com/markdown_tables) that
we used in Lab.  Feel free to use it to help with your solutions.]

### Problem 1.3:

There are other small sets of functionally complete operations.  In fact, all
possible logical operations can be expressed in terms of a **single** binary
operator, which may be taken to be either **NAND** ("*NOT* *AND*" or "not both,"
i.e., $\overline{A\land B}$) or **NOR** ("*NOT* *OR*," i.e., $\overline{A\lor
B}$, "neither $A$ nor $B$"), as defined in the following truth table:

| $A$ | $B$ |   | $A$ NAND $B$ | $A$ NOR $B$ |
|:---:|:---:|---|:------------:|:-----------:|
| 0   | 0   |   | 1            | 1           |
| 0   | 1   |   | 1            | 0           |
| 1   | 0   |   | 1            | 0           |
| 1   | 1   |   | 0            | 0           |

> *Pick one of these operators, and express $\overline{A}$, $A\land B$, and
$A\lor B$ in terms of it.*  You need only present three expressions (use MathJax
LaTeX); no truth tables are necessary.

### Problem 1.4:

Digital computers are essentially propositional logic computing devices, built
using "logic gate" circuit elements that implement basic logic (and memory)
functions.  A key component of a CPU chip in a computer is an *arithmetic logic
unit* (ALU) that performs arithmetic and bitwise logic operations on bytes and
larger groups of binary digits (bits).  The ALU is built from simple gates that
implement desired operations via truth table representations.  For example, the
addition of the lowermost bits, $A$ and $B$, of two numbers can be expressed by
the following truth table:

| $A$ | $B$ |   | Sum | Carry |
|:---:|:---:|---|:---:|:-----:|
| 0   | 0   |   | 0   | 0     |
| 0   | 1   |   | 1   | 0     |
| 1   | 0   |   | 1   | 0     |
| 1   | 1   |   | 0   | 1     |

Here **Sum** denotes the first (lowermost) binary digit of the sum of $A$ and
$B$, and **Carry** denotes a carry bit, indicating that $1+1=2$, or 10 in binary
(the carry bit will affect the outcome of adding the next highest bits of the
numbers being processed by the ALU).  Two logic functions implementing this
table comprise a *half adder* (a *full adder* is a trinary operation that
handles an additional carry bit input).

> *Express the Sum and Carry operations in terms of **NOT**, **AND**, and
**OR**.*  Show the intermediate operations in a truth table, along the lines of
Problem 1.2.

### Problem 2.1:

> *Using Bayes's theorem, answer the question posed in the Kahneman/Tversky
exercise quoted above, verifying that the typical answer is incorrect.*
> * Specify the hypothesis space.
> * Specify the data proposition.
> * Calculate the posterior probabilities for the hypotheses, presenting a table
that shows the prior, likelihood, prior$\times$likelihood, and posterior
probabilities for the hypotheses.

### Problem 2.2:

> Briefly explain what you think the heuristic is that most people used to
justify their conclusion.  Criticize it in light of the result of the
calculation in Problem 2.1.

### Problem 3.1:

> *Derive the formula given in lecture for the expectation value of $x$, denoted
$\Bbb{E}(x)$ or $\langle x\rangle$, in terms of $a$ and $b$, where*
$$
\Bbb{E}(x) = \int dx\; x \times {\rm Beta}(x|a,b).
$$

Present your derivation in the IPython notebook using MathJax LaTeX notation for
the math (make sure to also use text to briefly explain your reasoning).

### Problem 3.2:

> *Derive the formula given in lecture for the mode of the beta distribution,
$\hat x$, in terms of $a$ and $b$.  (The mode is the value of $x$ with maximum
probability density).*


### Problem 4.1:

> Calculate and plot the posterior PDF using the analytic formula from lecture:
> * Use the scipy.stats.norm distribution object to generate a single sample of
$N$ observations, $d_i$, following the model in the lecture.  Pick your own
"true" values of the parameters $\mu$ and $\sigma$ for the observations.
> * Pick a prior mean, $\mu_0$, and standard deviation, $w_0$, defining a normal
prior.  Plot the posterior PDF for $\mu$ using the formula presented in class
for the conjugate posterior (the formula with the quantity $B$ specifying how
much the posterior shrinks toward the prior).  Use the numpy `linspace` function
to make an array of $\mu$ values over which you'll evaluate the PDF.  You may
use either the scipy.stats `norm` object, or explicit calculation (with `exp`,
etc.), to evaluate the PDF.  Use a thick solid curve for the plot (say, with
lw=2 or 3 in the matplotlib `plot` function).

### Problem 4.2:

> Now explicitly calculate and plot the posterior PDF from the prior and
likelihood:
* Use the same grid of $\mu$ values used for Problem 4.1.
*Evaluate the normal prior and the likelihood function on the grid.
* Calculate the prior $\times$ likelihood, and normalize it using the trapezoid
rule (code the trapezoid rule explicitly; don't use `numpy.trapz`).
* Plot the resulting normalized PDF on the same axes as Problem 4.1.  Use a
dashed line style (and optionally transparency, via the `alpha` argument to
`plot`) so that both curves are visible (they should overlap!).

### Problem 4.3:

> Create test cases that verify elements of your computation:
* Create a case that checks whether your trapezoid rule integration matches the
result given by `numpy.trapz`.
* Create a case that checks whether the two posterior PDFs match over the grid
of $\mu$ values.
* Include a `nosetests` run in your notebook that verifies the tests pass.


    %matplotlib inline
