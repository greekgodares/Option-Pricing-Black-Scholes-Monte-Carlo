# Option Pricing: Black-Scholes PDE & Monte Carlo

<p align="center">
  <b>Mathematical Modeling of European Option Pricing</b>
</p>

<p align="center">
  Analytical Black-Scholes PDE Approach • Monte Carlo Simulation • Volatility Smile
</p>

---

## 📌 Overview

This project studies the mathematical modeling of **European option pricing** using two complementary approaches:

1. **Black-Scholes PDE** — an analytical approach that derives the option pricing formula using differential equations and mathematical transformations.
2. **Monte Carlo Simulation** — a numerical approach that estimates option prices by simulating a large number of possible future stock-price paths.

The project connects concepts from **differential equations, stochastic processes, probability, and mathematical finance**.

A major focus of the project is understanding not only how the Black-Scholes model produces an elegant closed-form solution, but also **where its assumptions fail in real financial markets**.

---

## 🎯 Objectives

The main objectives of this project are:

* Derive the **Black-Scholes PDE** from the underlying stock-price model.
* Use **Itô's Lemma** to obtain the dynamics of the option price.
* Construct a risk-free hedged portfolio using the **no-arbitrage principle**.
* Transform the Black-Scholes PDE into the **heat equation**.
* Apply the **method of undetermined coefficients**.
* Use the **Laplace transform** to obtain the analytical solution.
* Derive the classical **Black-Scholes formula** for a European call option.
* Calculate an option price using realistic model parameters.
* Understand the **volatility smile** and the limitations of constant volatility.
* Introduce **Monte Carlo simulation** as a numerical pricing method.
* Compare the analytical Black-Scholes price with the Monte Carlo estimate.

---

# 📐 Mathematical Framework

## 1. Stock Price Model

Under the Black-Scholes framework, the stock price is modeled using **Geometric Brownian Motion**:

$$
dS_t = \mu S_t,dt + \sigma S_t,dW_t
$$

where:

* $S_t$ = stock price at time $t$
* $\mu$ = expected return or drift
* $\sigma$ = volatility
* $W_t$ = Wiener process

The model assumes that the stock return contains both a deterministic component and a random component.

---

## 2. From the SDE to the Black-Scholes PDE

Let $V(S,t)$ denote the value of an option.

Applying **Itô's Lemma** gives:

$$
dV =
\left(
\frac{\partial V}{\partial t}
+
\mu S\frac{\partial V}{\partial S}
+
\frac{1}{2}\sigma^2S^2
\frac{\partial^2 V}{\partial S^2}
\right)dt
+
\sigma S
\frac{\partial V}{\partial S}dW_t
$$

A hedged portfolio can then be constructed to eliminate the stochastic term.

Using the **no-arbitrage principle**, the resulting option-pricing equation is the Black-Scholes PDE:

$$
\frac{\partial V}{\partial t}
+
\frac{1}{2}\sigma^2S^2
\frac{\partial^2 V}{\partial S^2}
+
rS\frac{\partial V}{\partial S}
-rV
=0
$$

For a European call option, the terminal condition is:

$$
V(S,T)=\max(S-K,0)
$$

where:

* $K$ = strike price
* $T$ = maturity
* $r$ = risk-free interest rate

---

# 🔥 3. Transformation to the Heat Equation

The Black-Scholes PDE contains coefficients involving $S$ and $S^2$, making it difficult to solve directly.

A suitable change of variables transforms the equation into a form related to the **heat equation**.

The transformation used in the project is:

$$
S = Ke^x
$$

and

$$
t = T-\frac{2\tau}{\sigma^2}
$$

with the option value written in transformed form.

After an exponential transformation using the method of undetermined coefficients, the equation reduces to the standard heat equation:

$$
\frac{\partial u}{\partial \tau}
================================

\frac{\partial^2u}{\partial x^2}
$$

This connects the option-pricing problem to classical techniques from differential equations.

---

# 🧮 4. Laplace Transform Solution

Applying the Laplace transform with respect to $\tau$ converts the heat equation into a second-order ordinary differential equation:

$$
\frac{d^2\hat{u}}{dx^2}
-----------------------

# s\hat{u}

-u(x,0)
$$

The resulting ODE can be solved using standard techniques.

After applying the appropriate boundary conditions and taking the inverse Laplace transform, the classical **Black-Scholes formula** is obtained.

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
\left(r+\frac{\sigma^2}{2}\right)(T-t)
}{
\sigma\sqrt{T-t}
}
$$

and

$$
d_2
===

d_1-\sigma\sqrt{T-t}
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

### Step 1: Calculate $d_1$

$$
d_1
===

\frac{
\ln(100/100)
+
\left(0.05+\frac{0.20^2}{2}\right)(1)
}{
0.20\sqrt{1}
}
$$

Therefore:

$$
d_1=0.35
$$

### Step 2: Calculate $d_2$

$$
d_2
===

0.35-0.20
$$

Therefore:

$$
d_2=0.15
$$

### Step 3: Calculate the normal CDF values

$$
N(d_1)\approx0.6368
$$

$$
N(d_2)\approx0.5596
$$

### Step 4: Calculate the option price

$$
C
=

## 100(0.6368)

100e^{-0.05}(0.5596)
$$

This gives:

$$
\boxed{C\approx10.45}
$$

Therefore, the theoretical Black-Scholes price of the European call option is approximately:

> **10.45**

---

# 🎲 7. Monte Carlo Simulation

Monte Carlo simulation provides a numerical approach to option pricing by generating many possible future stock-price paths.

Under the risk-neutral dynamics, a stock-price simulation step can be written as:

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
* $\Delta t$ = simulation time step
* $Z$ = standard normal random variable

with:

$$
Z\sim N(0,1)
$$

---

## 🔄 Monte Carlo Procedure

The option price is estimated through the following steps:

### Step 1 — Initialize parameters

Set:

* Initial stock price $S_0$
* Strike price $K$
* Maturity $T$
* Risk-free rate $r$
* Volatility $\sigma$
* Number of simulations $N$

### Step 2 — Simulate stock-price paths

Generate random values:

$$
Z\sim N(0,1)
$$

and use the stock-price equation to generate future prices.

### Step 3 — Calculate the payoff

For a European call option:

$$
\text{Payoff}
=============

\max(S_T-K,0)
$$

### Step 4 — Repeat

Repeat the simulation for a large number of independent paths.

For example:

$$
N=100,000
$$

### Step 5 — Average the payoffs

Calculate the average simulated payoff:

$$
\frac{1}{N}
\sum_{i=1}^{N}
\max(S_T^{(i)}-K,0)
$$

### Step 6 — Discount to the present

The Monte Carlo estimate of the option price is:

$$
\hat{C}
=======

e^{-rT}
\frac{1}{N}
\sum_{i=1}^{N}
\max(S_T^{(i)}-K,0)
$$

As the number of simulations increases, the Monte Carlo estimate should converge toward the theoretical option price under the same model assumptions.

---

# 📈 8. Volatility Smile

One of the important limitations of the standard Black-Scholes model is its assumption of **constant volatility**.

If the Black-Scholes model perfectly described market prices, the implied volatility obtained from different options would be approximately constant across strike prices.

In real markets, however, implied volatility typically varies with strike price.

This produces a pattern known as the:

> **Volatility Smile**

The volatility smile indicates that market participants price options in a way that is inconsistent with the constant-volatility assumption of the basic Black-Scholes model.

---

## Why is this important?

If volatility varies with the underlying price or time, the standard Black-Scholes analytical framework becomes more difficult to apply.

This motivates the use of more flexible models, such as:

* Local volatility models
* Stochastic volatility models
* Jump-diffusion models
* Numerical simulation methods

Monte Carlo simulation is particularly useful because it can be adapted to more complex stochastic models.

---

# ⚖️ 9. Black-Scholes vs Monte Carlo

| Feature             | Black-Scholes                           | Monte Carlo                     |
| ------------------- | --------------------------------------- | ------------------------------- |
| Approach            | Analytical                              | Numerical                       |
| Main tool           | PDE solution                            | Random simulation               |
| Output              | Closed-form price                       | Estimated price                 |
| Speed               | Very fast for standard European options | Computationally more expensive  |
| Standard model      | Constant volatility                     | Can accommodate richer dynamics |
| Complex payoffs     | Can become difficult                    | Generally flexible              |
| Simulation error    | None for the closed-form formula        | Sampling error                  |
| Confidence interval | Not required                            | Can be estimated                |

---

# 📊 10. Key Results

For:

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

the analytical Black-Scholes price is:

$$
\boxed{C\approx10.45}
$$

A sufficiently large Monte Carlo simulation under the same assumptions should produce an estimate close to this value.

The comparison demonstrates how an analytical solution and a numerical simulation can be used to solve the same option-pricing problem.

---

# ⚠️ 11. Model Assumptions and Limitations

The standard Black-Scholes model relies on several simplifying assumptions:

* Volatility is constant.
* The risk-free interest rate is constant.
* Stock prices follow a geometric Brownian motion.
* Markets are frictionless.
* There are no transaction costs.
* Trading is continuous.
* The underlying asset can be traded continuously.
* The option is European and can only be exercised at maturity.
* The model does not directly account for jumps in asset prices.

These assumptions make the model mathematically tractable but limit its ability to perfectly describe real financial markets.

The **volatility smile** is one of the most visible pieces of market evidence against the constant-volatility assumption.

---

# 🔬 12. Mathematical Finance Perspective

This project demonstrates an important idea in quantitative finance:

> A mathematical model is useful not only because it produces a solution, but also because it helps us understand the assumptions behind that solution.

The Black-Scholes framework provides an elegant analytical solution under restrictive assumptions.

Monte Carlo simulation provides a more general numerical framework that can be extended to more complicated models.

This distinction between **analytical tractability and model flexibility** is central to quantitative finance.

---

# 📁 13. Project Structure

```text
Option-Pricing-Black-Scholes-Monte-Carlo/
│
├── README.md
│
└── Mathematical_Modeling_of_Option_Pricing.pdf
```

Additional Python implementations and notebooks can be added to the repository in future versions.

---

# 📄 14. Project Report

The complete mathematical derivation and discussion are available in the project report:

**[Mathematical Modeling of Option Pricing](./Mathematical_Modeling_of_Option_Pricing.pdf)**

The report includes:

* Introduction to options
* Geometric Brownian Motion
* Itô's Lemma
* Black-Scholes PDE derivation
* Risk-free hedging
* Heat-equation transformation
* Method of undetermined coefficients
* Laplace transform solution
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

## ⭐ Future Work

Potential extensions of this project include:

* Implementing Monte Carlo simulation in Python.
* Comparing Monte Carlo estimates with the analytical Black-Scholes price.
* Studying Monte Carlo convergence and standard error.
* Plotting simulated stock-price paths.
* Estimating implied volatility from market option prices.
* Studying stochastic volatility models such as the Heston model.
* Extending the framework to exotic options.
* Comparing different numerical option-pricing techniques.

---

**If you find this project useful, consider giving the repository a ⭐.**
