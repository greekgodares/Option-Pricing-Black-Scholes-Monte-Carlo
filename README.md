# Option Pricing: Black-Scholes PDE & Monte Carlo

<p align="center">
  <strong>Mathematical Modeling of European Option Pricing</strong>
</p>

<p align="center">
  Black-Scholes PDE • Differential Equations • Monte Carlo Simulation • Volatility Smile
</p>

---

## 📌 Overview

This project studies the mathematical modeling of **European option pricing** using two complementary approaches:

* **Black-Scholes PDE** — an analytical approach that derives the option pricing formula using differential equation techniques.
* **Monte Carlo Simulation** — a numerical approach that estimates option prices by simulating a large number of possible future stock-price paths.

The project connects concepts from **differential equations, stochastic processes, probability, and mathematical finance**.

A key objective is not only to derive the classical Black-Scholes formula, but also to understand its assumptions, limitations, and the motivation for using numerical methods such as Monte Carlo simulation.

---

## 🎯 Objectives

The main objectives of this project are:

* Model stock prices using **Geometric Brownian Motion**.
* Derive the **Black-Scholes PDE** using Itô's Lemma.
* Construct a risk-free hedged portfolio using the **no-arbitrage principle**.
* Transform the Black-Scholes PDE into the **heat equation**.
* Apply the **method of undetermined coefficients**.
* Use the **Laplace transform** to solve the transformed equation.
* Derive the classical **Black-Scholes formula**.
* Calculate the theoretical price of a European call option.
* Understand the **volatility smile** and the limitations of constant volatility.
* Introduce **Monte Carlo simulation** as a numerical pricing method.
* Compare analytical and simulation-based approaches to option pricing.

---

# 📐 Mathematical Framework

## 1. Stock Price Model

The underlying stock price is modeled using **Geometric Brownian Motion**:

$$
dS_t
====

\mu S_t,dt
+
\sigma S_t,dW_t
$$

where:

* $S_t$ = stock price at time $t$
* $\mu$ = expected return or drift
* $\sigma$ = volatility
* $W_t$ = Wiener process

The first term represents the deterministic component of the stock return, while the second term represents the random component.

---

## 2. From SDE to the Black-Scholes PDE

Let $V(S,t)$ denote the value of an option.

Applying **Itô's Lemma** gives:

$$
dV
==

\left(
\frac{\partial V}{\partial t}
+
\mu S\frac{\partial V}{\partial S}
+
\frac{1}{2}\sigma^2S^2
\frac{\partial^2V}{\partial S^2}
\right)dt
+
\sigma S
\frac{\partial V}{\partial S}
dW_t
$$

A hedged portfolio can be constructed to eliminate the stochastic term.

Using the **no-arbitrage principle**, the resulting Black-Scholes partial differential equation is:

$$
\frac{\partial V}{\partial t}
+
\frac{1}{2}\sigma^2S^2
\frac{\partial^2V}{\partial S^2}
+
rS\frac{\partial V}{\partial S}
-------------------------------

# rV

0
$$

For a European call option, the terminal condition is:

$$
V(S,T)
======

\max(S-K,0)
$$

where:

* $K$ = strike price
* $T$ = maturity
* $r$ = risk-free interest rate

---

# 🔥 3. Transformation to the Heat Equation

The Black-Scholes PDE contains variable coefficients involving $S$ and $S^2$.

A suitable change of variables transforms the equation into a form related to the classical heat equation.

The transformation begins with:

$$
S=Ke^x
$$

and

$$
t=T-\frac{2\tau}{\sigma^2}
$$

The option value is then expressed in terms of transformed variables.

After applying an exponential transformation using the **method of undetermined coefficients**, the equation becomes:

$$
\frac{\partial u}{\partial \tau}
================================

\frac{\partial^2u}{\partial x^2}
$$

This is the standard **heat equation**.

This transformation provides a connection between option pricing and classical techniques from differential equations.

---

# 🧮 4. Laplace Transform Solution

Applying the Laplace transform with respect to $\tau$ gives:

$$
\hat{u}(x,s)
============

\int_0^\infty
e^{-s\tau}
u(x,\tau)
,d\tau
$$

The heat equation is transformed into the second-order ordinary differential equation:

$$
\frac{d^2\hat{u}}{dx^2}
-----------------------

# s\hat{u}

-u(x,0)
$$

The corresponding homogeneous solution has the form:

$$
\hat{u}_h(x,s)
==============

A(s)e^{-\sqrt{s}x}
+
B(s)e^{\sqrt{s}x}
$$

After applying the appropriate boundary conditions and taking the inverse Laplace transform, the classical Black-Scholes pricing formula is obtained.

---

# 📊 5. Black-Scholes Formula

For a European call option, the Black-Scholes price is:

$$
C
=

## SN(d_1)

Ke^{-r(T-t)}N(d_2)
$$

where:

$$
d_1
===

\frac{
\ln(S/K)
+
\left(
r+\frac{\sigma^2}{2}
\right)(T-t)
}{
\sigma\sqrt{T-t}
}
$$

and:

$$
d_2
===

## d_1

\sigma\sqrt{T-t}
$$

Here, $N(x)$ represents the cumulative distribution function of the standard normal distribution.

---

# 💰 6. Worked Example

Consider a European call option with the following parameters:

| Parameter                 |  Value |
| ------------------------- | -----: |
| Current stock price ($S$) |    100 |
| Strike price ($K$)        |    100 |
| Time to maturity ($T-t$)  | 1 year |
| Risk-free rate ($r$)      |     5% |
| Volatility ($\sigma$)     |    20% |

### Step 1 — Calculate $d_1$

$$
d_1
===

\frac{
\ln(100/100)
+
\left(
0.05+\frac{0.20^2}{2}
\right)(1)
}{
0.20\sqrt{1}
}
$$

Therefore:

$$
d_1
===

0.35
$$

### Step 2 — Calculate $d_2$

$$
d_2
===

d_1-\sigma\sqrt{T-t}
$$

Therefore:

$$
d_2
===

# 0.35-0.20

0.15
$$

### Step 3 — Calculate the normal CDF values

$$
N(d_1)
======

N(0.35)
\approx
0.6368
$$

$$
N(d_2)
======

N(0.15)
\approx
0.5596
$$

### Step 4 — Calculate the option price

Using:

$$
C
=

## SN(d_1)

Ke^{-r(T-t)}N(d_2)
$$

we obtain:

$$
C
=

## 100(0.6368)

100e^{-0.05}(0.5596)
$$

Therefore:

$$
\boxed{C\approx10.45}
$$

The theoretical Black-Scholes price of the European call option is therefore approximately **10.45**.

---

# 🎲 7. Monte Carlo Simulation

Monte Carlo simulation provides a numerical approach to option pricing by generating a large number of possible future stock-price paths.

Under the risk-neutral dynamics, the stock price can be simulated using:

$$
S_{t+\Delta t}
==============

S_t
\exp
\left[
\left(
r-\frac{\sigma^2}{2}
\right)\Delta t
+
\sigma\sqrt{\Delta t},Z
\right]
$$

where:

* $S_t$ = stock price at time $t$
* $r$ = risk-free interest rate
* $\sigma$ = volatility
* $\Delta t$ = time step
* $Z$ = standard normal random variable

with:

$$
Z\sim N(0,1)
$$

---

## 🔄 Monte Carlo Simulation Procedure

### Step 1 — Initialize Parameters

Set the model parameters:

* Initial stock price: $S_0$
* Strike price: $K$
* Time to maturity: $T$
* Risk-free interest rate: $r$
* Volatility: $\sigma$
* Number of simulations: $N$

---

### Step 2 — Simulate Stock-Price Paths

Generate independent random variables:

$$
Z_i\sim N(0,1)
$$

and use the stock-price equation to generate future stock prices.

For multiple time steps, the simulation is repeated until maturity $T$.

---

### Step 3 — Calculate the Option Payoff

For a European call option, the payoff from simulation $i$ is:

$$
P_i
===

\max\left(S_T^{(i)}-K,0\right)
$$

where:

* $S_T^{(i)}$ = terminal stock price from simulation $i$
* $K$ = strike price
* $P_i$ = payoff from simulation $i$

If the terminal stock price is below the strike price, the payoff is zero.

---

### Step 4 — Repeat the Simulation

Repeat the simulation for a large number of independent paths.

For example:

$$
N=100{,}000
$$

This produces:

$$
S_T^{(1)},
S_T^{(2)},
\ldots,
S_T^{(N)}
$$

and a corresponding payoff for each simulated path.

---

### Step 5 — Average the Payoffs

The average simulated payoff is:

$$
\overline{P}
============

\frac{1}{N}
\sum_{i=1}^{N}
\max\left(S_T^{(i)}-K,0\right)
$$

This gives an estimate of the expected payoff before discounting.

---

### Step 6 — Discount to the Present

The Monte Carlo estimate of the option price is:

$$
\hat{C}
=======

e^{-rT}
\frac{1}{N}
\sum_{i=1}^{N}
\max\left(S_T^{(i)}-K,0\right)
$$

where:

* $\hat{C}$ = Monte Carlo estimate of the option price
* $r$ = risk-free interest rate
* $T$ = time to maturity
* $N$ = number of simulated paths

As the number of simulations increases, the Monte Carlo estimate converges toward the theoretical price under the same model assumptions.

---

## 💡 Key Idea

The central idea behind Monte Carlo option pricing is:

$$
\text{Option Price}
===================

\text{Discounted Expected Payoff}
$$

Instead of solving the pricing equation analytically, Monte Carlo simulation approximates the expected payoff by averaging the outcomes of many simulated future scenarios.

---

# 📈 8. Volatility Smile

The standard Black-Scholes model assumes that volatility is **constant**.

If this assumption were perfectly consistent with market prices, implied volatility would remain approximately constant across different strike prices.

In real markets, implied volatility varies with strike price, producing a pattern commonly known as the **volatility smile** or volatility skew.

The volatility smile indicates that observed option prices cannot be completely explained by the constant-volatility assumption of the basic Black-Scholes model.

---

## Why Does the Volatility Smile Matter?

When volatility depends on the underlying asset price, time, or other stochastic factors, the standard Black-Scholes framework becomes more difficult to apply analytically.

This motivates the study of more flexible models, including:

* Local volatility models
* Stochastic volatility models
* Jump-diffusion models
* Numerical simulation methods

Monte Carlo simulation is particularly useful because it can be adapted to more complex stochastic models.

---

# ⚖️ 9. Black-Scholes vs Monte Carlo

| Feature             | Black-Scholes                       | Monte Carlo         |
| ------------------- | ----------------------------------- | ------------------- |
| Approach            | Analytical                          | Numerical           |
| Main technique      | PDE solution                        | Random simulation   |
| Output              | Closed-form price                   | Estimated price     |
| Computational cost  | Low for standard European options   | Higher              |
| Model flexibility   | Limited by assumptions              | Highly flexible     |
| Complex dynamics    | More difficult                      | Can be incorporated |
| Sampling error      | None                                | Present             |
| Confidence interval | Not required for closed-form result | Can be estimated    |

---

# 📊 10. Key Results

For the parameters:

$$
S=100
$$

$$
K=100
$$

$$
T=1
$$

$$
r=0.05
$$

$$
\sigma=0.20
$$

the Black-Scholes analytical price is approximately:

$$
\boxed{C\approx10.45}
$$

Under the same model assumptions, a sufficiently large Monte Carlo simulation should produce an estimate close to this value.

This demonstrates the connection between the analytical Black-Scholes solution and the numerical Monte Carlo approach.

---

# ⚠️ 11. Model Assumptions and Limitations

The standard Black-Scholes model relies on several simplifying assumptions:

* Volatility is constant.
* The risk-free interest rate is constant.
* Stock prices follow geometric Brownian motion.
* Markets are frictionless.
* There are no transaction costs.
* Trading is continuous.
* The underlying asset can be traded continuously.
* The option is European and can only be exercised at maturity.
* The model does not directly account for jumps in asset prices.

These assumptions make the model mathematically tractable but limit its ability to perfectly represent real financial markets.

The volatility smile is one of the important market observations that challenges the constant-volatility assumption.

---

# 🔬 12. Mathematical Finance Perspective

This project demonstrates an important principle in quantitative finance:

> A mathematical model is useful not only because it produces a solution, but also because it helps us understand the assumptions behind that solution.

The Black-Scholes framework provides an elegant closed-form solution under a set of simplifying assumptions.

Monte Carlo simulation provides a flexible numerical framework that can be extended to more complicated models and payoff structures.

The distinction between **analytical tractability** and **model flexibility** is an important concept in quantitative finance.

---

# 📁 13. Project Structure

```text
Option-Pricing-Black-Scholes-Monte-Carlo/
│
├── README.md
│
└── Mathematical_Modeling_of_Option_Pricing.pdf
```

Future versions of the repository can include Python implementations, Jupyter notebooks, and visualization files.

---

# 📄 14. Project Report

The complete mathematical derivation and discussion are available in the project report:

**[📄 View the Full Project Report](./Mathematical_Modeling_of_Option_Pricing.pdf)**

The report covers:

* Introduction to options
* Geometric Brownian Motion
* Itô's Lemma
* Black-Scholes PDE
* Risk-free hedging
* Heat-equation transformation
* Method of undetermined coefficients
* Laplace transform
* Black-Scholes formula
* Worked numerical example
* Implied volatility
* Volatility smile
* Feynman-Kac theorem
* Monte Carlo simulation
* Comparison of analytical and numerical approaches

---

# 📚 15. References

1. Black, F., & Scholes, M. (1973). *The Pricing of Options and Corporate Liabilities*. Journal of Political Economy, 81(3), 637–654.

2. Heston, S. L. (1993). *A Closed-Form Solution for Options with Stochastic Volatility*. The Review of Financial Studies, 6(2), 327–343.

3. Shreve, S. E. (2004). *Stochastic Calculus for Finance II: Continuous-Time Models*. Springer.

---

# 👤 Author

**Rahul Kumar**

Indian Statistical Institute, Kolkata

**Interests:** Quantitative Finance • Mathematical Finance • Algorithmic Trading • Financial Modeling

---

# 🚀 Future Work

Possible extensions of this project include:

* [ ] Implement Monte Carlo option pricing in Python.
* [ ] Compare Monte Carlo prices with Black-Scholes prices.
* [ ] Study Monte Carlo convergence.
* [ ] Calculate Monte Carlo standard error and confidence intervals.
* [ ] Plot simulated stock-price paths.
* [ ] Plot the convergence of the Monte Carlo estimator.
* [ ] Estimate implied volatility from market option prices.
* [ ] Study stochastic volatility models such as the Heston model.
* [ ] Explore jump-diffusion models.
* [ ] Extend the framework to exotic options.
* [ ] Compare different numerical option-pricing methods.

---

## ⭐ Conclusion

This project demonstrates how mathematical modeling can be used to approach a practical financial problem from both analytical and numerical perspectives.

The **Black-Scholes PDE** provides an elegant analytical solution, while **Monte Carlo simulation** provides a flexible numerical alternative.

The study of the **volatility smile** further illustrates an important lesson in quantitative finance: models are powerful tools, but their assumptions must always be examined against real market behavior.

---

<p align="center">
  <strong>Mathematical Finance • Quantitative Finance • Option Pricing</strong>
</p>
