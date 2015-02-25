
# Assignment 02

**Due:** 2015-02-26, 11:59 PM, as an IPython notebook submitted via your repo in
the course GitHub organization.  Edit the provided Solution02 notebook with your
solutions.  All subproblems are worth 1 point unless otherwise noted.

## 1. Logic problems

We will not be using propositional logic extensively in this course, but it's
important to grasp basic logic in order to understand the goals and
interpretation of Bayesian inference.

In class we discussed three fundamental logical operations, the unary (operating
on a single proposition) **NOT** (denial) operation, and the binary (operating
on two propositions) **AND** (conjuction) and **OR** (disjunction) operations.
For propositions $A$ and $B$, with 0 denoting *False* and 1 denoting *True*, the
following truth tables describe these operations (I've separated inputs from
outputs with an empty column; note that the IPy notebook's table renderer may
split "$A\land B$", etc., across a line):

| $A$ |   | $\overline{A}$ |
|-----|:-:|----------------|
| 0   |   | 1              |
| 1   |   | 0              |

| $A$ | $B$ |   | $A \land B$ | $A \lor B$ |
|:---:|:---:|---|:-----------:|:----------:|
| 0   | 0   |   | 0           | 0          |
| 0   | 1   |   | 0           | 1          |
| 1   | 0   |   | 0           | 1          |
| 1   | 1   |   | 1           | 1          |

Of course, there are other useful truth-functional operations (unary, binary,
and higher order).  For example, **OR** is defined to correspond to *inclusive*
"or" in English, but we could also define an *exclusive* "or" operation ("either
$A$ or $B$, but not both"), denoted by $\veebar$ and called **XOR**, according
to the following truth table:

| $A$ | $B$ |   | $A \veebar B$ |
|:---:|:---:|---|:-------------:|
| 0   | 0   |   | 0             |
| 0   | 1   |   | 1             |
| 1   | 0   |   | 1             |
| 1   | 1   |   | 0             |

Similarly, propositional logic uses a *material implication* operator, denoted
by $\Rightarrow$, to capture the weakest meaning of statements like "if $A$ is
true, then $B$ must be," with this truth table:

| $A$ | $B$ |   | $A \Rightarrow B$ |
|:---:|:---:|---|:-----------------:|
| 0   | 0   |   | 1                 |
| 0   | 1   |   | 1                 |
| 1   | 0   |   | 0                 |
| 1   | 1   |   | 1                 |

$A \Rightarrow B$ captures a weak interpretation of "if... then..." in the sense
that it is false to claim $A \Rightarrow B$ *only* if $A$ is true when $B$ is
false; in all other cases the implication is considered true.  Don't puzzle too
much over the meaning of material implication; here it's just meant to be
another example of a binary operation.

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

## 2. Base rate fallacy

Daniel Kahneman and Amos Tversky did groundbreaking work on the psychology of
judgment and decision-making in the 1970s; Kahneman won the 2002 Nobel Memorial
Prize in Economic Sciences for this work (Tversky died in 1996 and thus could
not share the prize).  They performed numerous ingenious survey-based
experiments designed to uncover the heuristics people use to reason amidst
uncertainty.  One of their most famous experiments featured the following
problem:

> A cab was involved in a hit and run accident at night. Two cab companies, the
Green and the Blue, operate in the city. The following facts are known:

> * 85% of the cabs in the city are Green and 15% are Blue.
> * A witness identified the cab as Blue.
> * The court tested the reliability of the witness under the same circumstances
that existed on the night of the accident and concluded that the witness
correctly identified each one of the two colors 80% of the time and failed 20%
of the time.

> What is the probability that the cab involved in the accident was actually
Blue?

Kahneman and Tversky found that the typical answer was around 80%.  They used
this finding (among many others) to show that humans reason using *heuristics*,
mental shortcuts that may give a usable result or decision quickly in some
circumstances, but not always the *correct* or *optimal* answer.  For this cab
problem, the evidence for use of heuristics came from realizing that the typical
answer is *wrong*, i.e., that most people do not reason correctly in this
problem.

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

## The beta distribution

This problem explores properties of the beta distribution; it's also a
Markdown/MathJax exercise.

Recall the definition of the *beta distribution* PDF for $x\in [0,1]$:
$$
{\rm Beta}(x|a,b) = \frac{1}{B(a,b)} x^{a-1} (1-x)^{b-1},
$$
where $B(a,b)$ is the *beta function*,
$$
B(a,b) = \frac{\Gamma(a) \Gamma(b)}{\Gamma(a+b)}.
$$
Recall also that the gamma function generalizes factorials to non-integers; in
particular, analogous to the result that $n! = n \times (n-1)!$, the gamma
function obeys
$$
\Gamma(z+1) = z\times\Gamma(z).
$$

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


## 4. The normal-normal conjugate model

In Lecture 08 we covered basic inference with the normal (Gaussian)
distribution.  Without derivation, I claimed that a normal prior is the
conjugate prior for a likelihood function based on data with a normal
distribution for the additive noise or error terms.  Verify this claim
numerically.  The following instructions use the notation in the Lecture 08
slides, for the problem of inferring $\mu$ with $\sigma$ considered *known*.

For this problem, write a separate script (say, "NormNorm.py") implementing your
solution.  At the end of your notebook, use "`%matplotlib inline`" and run the
script in the notebook (using IPython's `run` command).  Then run the
`nosetests` command-line program in your notebook using "`!nosetests
NormNorm.py`".

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
