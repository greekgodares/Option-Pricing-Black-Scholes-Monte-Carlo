# Option Pricing: Black-Scholes PDE & Monte Carlo

Mathematical modeling of European option pricing using the **Black-Scholes partial differential equation (PDE)** and **Monte Carlo simulation**, with a study of the **volatility smile** and limitations of the Black-Scholes model.

## 📌 Project Overview

This project studies the mathematical foundations of European option pricing through two complementary approaches:

1. **Black-Scholes PDE** — an analytical approach that derives the option pricing formula using differential equation techniques.
2. **Monte Carlo Simulation** — a numerical approach that estimates option prices by simulating a large number of possible future stock-price paths.

The project connects concepts from differential equations, stochastic processes, probability, and mathematical finance.

## 🎯 Objectives

* Derive the **Black-Scholes PDE** from the stock-price model using Itô's Lemma and a risk-free hedging argument.
* Transform the Black-Scholes PDE into the **heat equation**.
* Solve the transformed equation using the **Laplace transform** and method of undetermined coefficients.
* Obtain the classical **Black-Scholes option pricing formula**.
* Calculate the price of a European call option using the analytical formula.
* Understand the **volatility smile** and why it challenges the constant-volatility assumption.
* Introduce **Monte Carlo simulation** as a flexible numerical alternative.
* Compare analytical and simulation-based option pricing.

## 📐 Mathematical Framework

### 1. Stock Price Model

The stock price is modeled using Geometric Brownian Motion:

$$
dS_t = \mu S_t,dt + \sigma S_t,dW_t
$$

where:

* $S_t$ = stock price at time $t$
* $\mu$ = expected return
* $\sigma$ = volatility
* $W_t$ = Wiener process

### 2. Black-Scholes PDE

Using Itô's Lemma and constructing a risk-free hedged portfolio leads to the Black-Scholes PDE:

$$
\frac{\partial V}{\partial t}
+
\frac{1}{2}\sigma^2S^2
\frac{\partial^2 V}{\partial S^2}
+
rS\frac{\partial V}{\partial S}
-rV=0
$$

For a European call option, the terminal condition is:

$$
V(S,T)=\max(S-K,0)
$$

### 3. Black-Scholes Formula

The resulting analytical solution for a European call option is:

$$
V = SN(d_1)-Ke^{-r(T-t)}N(d_2)
$$

where

$$
d_1 =
\frac{
\ln(S/K)+(r+\sigma^2/2)(T-t)
}{
\sigma\sqrt{T-t}
}
$$

and

$$
d_2=d_1-\sigma\sqrt{T-t}
$$

Here, $N(\cdot)$ is the cumulative distribution function of the standard normal distribution.

## 🎲 Monte Carlo Simulation

Monte Carlo pricing uses the Feynman-Kac representation of the option price:

$$
V(S,t)=e^{-r(T-t)}
E[\max(S_T-K,0)]
$$

The stock price is simulated using:

$$
S_{t+\Delta t}
==============

S_t
\exp
\left[
\left(r-\frac{\sigma^2}{2}\right)\Delta t
+
\sigma\sqrt{\Delta t}Z
\right]
$$

where:

$$
Z\sim N(0,1)
$$

The simulation procedure is:

1. Set the initial stock price and model parameters.
2. Simulate future stock-price paths.
3. Calculate the option payoff at maturity.
4. Repeat the simulation for many paths.
5. Average the simulated payoffs.
6. Discount the average payoff back to the present.

## 💻 Worked Example

Consider a European call option with:

| Parameter                 |  Value |
| ------------------------- | -----: |
| Current stock price ($S$) |    100 |
| Strike price ($K$)        |    100 |
| Time to expiry ($T$)      | 1 year |
| Risk-free rate ($r$)      |     5% |
| Volatility ($\sigma$)     |    20% |

Using the Black-Scholes formula:

$$
d_1=0.35
$$

$$
d_2=0.15
$$

with

$$
N(d_1)\approx0.6368
$$

and

$$
N(d_2)\approx0.5596
$$

The resulting European call option price is approximately:

$$
\boxed{V\approx10.45}
$$

Thus, the theoretical fair price of the call option is approximately **10.45**.

## 📈 Volatility Smile

A key limitation of the Black-Scholes model is its assumption of **constant volatility**.

In real financial markets, implied volatility varies across different strike prices. Plotting implied volatility against strike price produces the **volatility smile**.

This indicates that market prices do not fully agree with the constant-volatility assumption of the standard Black-Scholes model.

When volatility is stochastic or depends on the underlying asset price and time, the analytical Black-Scholes approach becomes considerably more difficult.

## 🔬 Black-Scholes vs Monte Carlo

| Feature               | Black-Scholes PDE                 | Monte Carlo         |
| --------------------- | --------------------------------- | ------------------- |
| Approach              | Analytical                        | Numerical           |
| Main technique        | PDE transformation and solution   | Random simulation   |
| Output                | Closed-form price                 | Estimated price     |
| Computational cost    | Low for standard European options | Higher              |
| Complex models        | Limited                           | Flexible            |
| Stochastic volatility | Difficult                         | Can be incorporated |
| Confidence interval   | Not required for exact formula    | Can be estimated    |

## 📊 Key Result

For the parameters:

$$
S=100,\quad K=100,\quad T=1,\quad r=0.05,\quad \sigma=0.20
$$

the Black-Scholes model gives:

$$
\boxed{C\approx10.45}
$$

A sufficiently large Monte Carlo simulation should converge toward the same theoretical value.

## ⚠️ Limitations

The standard Black-Scholes framework relies on several simplifying assumptions:

* Constant volatility
* Constant risk-free interest rate
* Lognormally distributed stock prices
* Continuous trading
* No transaction costs
* No arbitrage
* European-style exercise
* Continuous and frictionless markets

The volatility smile demonstrates that the constant-volatility assumption does not fully describe observed market prices.

## 📄 Project Report

The complete mathematical derivation and discussion are available in the project report:

**[Mathematical Modeling of Option Pricing](./Mathematical_Modeling_of_Option_Pricing.pdf)**

The report covers:

* Black-Scholes PDE derivation
* Itô's Lemma
* Risk-free hedging
* Transformation to the heat equation
* Method of undetermined coefficients
* Laplace transform
* Black-Scholes formula
* Worked option-pricing example
* Volatility smile
* Feynman-Kac theorem
* Monte Carlo simulation

## 📚 References

1. Black, F., & Scholes, M. (1973). *The Pricing of Options and Corporate Liabilities*. Journal of Political Economy, 81(3), 637–654.
2. Heston, S. L. (1993). *A Closed-Form Solution for Options with Stochastic Volatility*. The Review of Financial Studies, 6(2), 327–343.
3. Shreve, S. E. (2004). *Stochastic Calculus for Finance II: Continuous-Time Models*. Springer.

## 👤 Author

**Rahul Kumar**
Indian Statistical Institute, Kolkata

**Area of Interest:** Quantitative Finance, Mathematical Finance, Algorithmic Trading

---

⭐ If you find this project useful, feel free to star the repository.
