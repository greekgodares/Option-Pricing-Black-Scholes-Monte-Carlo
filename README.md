# Option Pricing: Black-Scholes PDE and Monte Carlo

## Overview

This project studies the mathematical modeling of **European option pricing** using two complementary approaches:

1. **Black-Scholes PDE** — an analytical approach based on stochastic calculus, partial differential equations, and the no-arbitrage principle.
2. **Monte Carlo Simulation** — a numerical approach that estimates option prices by simulating a large number of possible future stock-price paths.

The project also examines the **volatility smile** and discusses limitations of the standard Black-Scholes framework.

The work connects concepts from **stochastic processes, differential equations, probability, and mathematical finance**.

---

## Objectives

The main objectives of this project are:

- Model stock prices using Geometric Brownian Motion.
- Derive the Black-Scholes PDE using Itô's Lemma.
- Construct a risk-free hedged portfolio using the no-arbitrage principle.
- Transform the Black-Scholes PDE into the heat equation.
- Study the method of undetermined coefficients.
- Apply the Laplace transform to the transformed equation.
- Derive the classical Black-Scholes formula.
- Calculate the theoretical price of a European call option.
- Understand the volatility smile and limitations of constant volatility.
- Introduce Monte Carlo simulation as a numerical pricing method.
- Compare analytical and numerical approaches to option pricing.

---

# 1. Mathematical Framework

## 1.1 Stock Price Model

The underlying stock price is modeled using **Geometric Brownian Motion**:

$$
dS_t
=
\mu S_t\,dt
+
\sigma S_t\,dW_t
$$

where:

- $S_t$ = stock price at time $t$
- $\mu$ = expected return or drift
- $\sigma$ = volatility
- $W_t$ = Wiener process

The first term represents the deterministic component of the stock return, while the second term represents the random component.

---

## 1.2 Derivation of the Black-Scholes PDE

Let $V(S,t)$ denote the value of an option.

Applying **Itô's Lemma** gives:

$$
dV
=
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
\frac{\partial V}{\partial S}
dW_t
$$

A hedged portfolio can be constructed to eliminate the stochastic term.

Using the **no-arbitrage principle**, the resulting Black-Scholes PDE is:

$$
\frac{\partial V}{\partial t}
+
\frac{1}{2}\sigma^2S^2
\frac{\partial^2 V}{\partial S^2}
+
rS\frac{\partial V}{\partial S}
-
rV
=
0
$$

For a European call option, the terminal condition is:

$$
V(S,T)
=
\max(S-K,0)
$$

where:

- $K$ = strike price
- $T$ = maturity
- $r$ = risk-free interest rate

---

# 2. Transformation to the Heat Equation

The Black-Scholes PDE contains variable coefficients involving $S$ and $S^2$.

A suitable change of variables transforms the equation into a form related to the classical heat equation.

One of the transformations used is:

$$
S=Ke^x
$$

and

$$
t=T-\frac{2\tau}{\sigma^2}
$$

After applying the appropriate transformation to the option value, the equation can be reduced to the standard heat equation:

$$
\frac{\partial u}{\partial \tau}
=
\frac{\partial^2u}{\partial x^2}
$$

This transformation connects the option-pricing problem with classical methods for solving partial differential equations.

---

# 3. Laplace Transform Approach

Applying the Laplace transform with respect to $\tau$ gives:

$$
\hat{u}(x,s)
=
\int_0^\infty
e^{-s\tau}
u(x,\tau)\,d\tau
$$

The transformed heat equation takes the form:

$$
\frac{d^2\hat{u}}{dx^2}
-
s\hat{u}
=
-u(x,0)
$$

The resulting ordinary differential equation can be solved subject to the appropriate boundary and initial conditions.

After applying the inverse Laplace transform, the classical Black-Scholes pricing formula is obtained.

---

# 4. Black-Scholes Formula

For a European call option, the Black-Scholes price is:

$$
C
=
SN(d_1)
-
Ke^{-r(T-t)}N(d_2)
$$

where:

$$
d_1
=
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
=
d_1
-
\sigma\sqrt{T-t}
$$

Here, $N(x)$ denotes the cumulative distribution function of the standard normal distribution.

---

# 5. Numerical Example

Consider a European call option with:

| Parameter | Value |
|---|---:|
| Current stock price ($S$) | 100 |
| Strike price ($K$) | 100 |
| Time to maturity ($T-t$) | 1 year |
| Risk-free rate ($r$) | 5% |
| Volatility ($\sigma$) | 20% |

### Step 1: Calculate $d_1$

$$
d_1
=
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
d_1=0.35
$$

### Step 2: Calculate $d_2$

$$
d_2
=
d_1-0.20
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
100(0.6368)
-
100e^{-0.05}(0.5596)
$$

Therefore:

$$
\boxed{C\approx10.45}
$$

Thus, the theoretical Black-Scholes price of the European call option is approximately **10.45**.

---

# 6. Monte Carlo Simulation

Monte Carlo simulation provides a numerical approach to option pricing by generating a large number of possible future stock-price paths.

Under the risk-neutral dynamics, the stock price can be simulated using:

$$
S_{t+\Delta t}
=
S_t
\exp
\left[
\left(
r-\frac{\sigma^2}{2}
\right)\Delta t
+
\sigma\sqrt{\Delta t}\,Z
\right]
$$

where:

- $S_t$ = stock price at time $t$
- $r$ = risk-free interest rate
- $\sigma$ = volatility
- $\Delta t$ = time step
- $Z$ = standard normal random variable

with:

$$
Z\sim N(0,1)
$$

---

## 6.1 Simulation Procedure

### Step 1: Initialize Parameters

Set:

- Initial stock price: $S_0$
- Strike price: $K$
- Time to maturity: $T$
- Risk-free interest rate: $r$
- Volatility: $\sigma$
- Number of simulations: $N$

### Step 2: Simulate Stock Prices

Generate independent random variables:

$$
Z_i\sim N(0,1)
$$

and use the stock-price equation to simulate future stock prices.

For multiple time steps, the process is repeated until maturity $T$.

### Step 3: Calculate the Payoff

For a European call option, the payoff from simulation $i$ is:

$$
P_i
=
\max\left(S_T^{(i)}-K,0\right)
$$

where $S_T^{(i)}$ is the terminal stock price from simulation $i$.

### Step 4: Repeat the Simulation

The simulation is repeated for a large number of independent paths.

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

and a corresponding payoff for each path.

### Step 5: Average the Payoffs

The average simulated payoff is:

$$
\overline{P}
=
\frac{1}{N}
\sum_{i=1}^{N}
\max\left(S_T^{(i)}-K,0\right)
$$

### Step 6: Discount to the Present

The Monte Carlo estimate of the option price is:

$$
\hat{C}
=
e^{-rT}
\frac{1}{N}
\sum_{i=1}^{N}
\max\left(S_T^{(i)}-K,0\right)
$$

As the number of simulations increases, the Monte Carlo estimate converges toward the theoretical option price under the same model assumptions.

---

# 7. Volatility Smile

The standard Black-Scholes model assumes that volatility is constant.

If this assumption were fully consistent with observed market prices, implied volatility would be approximately constant across different strike prices.

In real financial markets, implied volatility varies with strike price and maturity. This produces patterns commonly referred to as the **volatility smile** or **volatility skew**.

The volatility smile demonstrates one of the important limitations of the standard Black-Scholes model.

---

## Why Does the Volatility Smile Matter?

The observed variation in implied volatility suggests that the assumptions of constant volatility and geometric Brownian motion do not fully capture real market dynamics.

This motivates the study of more flexible models, including:

- Local volatility models
- Stochastic volatility models
- Jump-diffusion models
- Numerical simulation methods

Monte Carlo simulation can be particularly useful when pricing under more complex stochastic models.

---

# 8. Black-Scholes vs Monte Carlo

| Feature | Black-Scholes | Monte Carlo |
|---|---|---|
| Approach | Analytical | Numerical |
| Main technique | PDE solution | Random simulation |
| Output | Closed-form price | Estimated price |
| Computational cost | Low for standard European options | Higher |
| Model flexibility | Limited by assumptions | Highly flexible |
| Complex dynamics | More difficult | Can be incorporated |
| Sampling error | None for closed-form solution | Present |
| Confidence interval | Not required | Can be estimated |

---

# 9. Key Results

For:

$$
S=100,\qquad
K=100,\qquad
T=1,\qquad
r=0.05,\qquad
\sigma=0.20
$$

the Black-Scholes analytical price is approximately:

$$
\boxed{C\approx10.45}
$$

A sufficiently large Monte Carlo simulation under the same assumptions should produce an estimate close to this value.

The comparison illustrates how an analytical solution and a numerical simulation can be used to solve the same option-pricing problem.

---

# 10. Model Assumptions and Limitations

The standard Black-Scholes model relies on several simplifying assumptions:

- Volatility is constant.
- The risk-free interest rate is constant.
- Stock prices follow geometric Brownian motion.
- Markets are frictionless.
- There are no transaction costs.
- Trading is continuous.
- The underlying asset can be traded continuously.
- The option is European.
- The model does not directly account for jumps in asset prices.

These assumptions make the model mathematically tractable but limit its ability to perfectly represent real financial markets.

The volatility smile is an important empirical observation that challenges the constant-volatility assumption.

---

# 11. Mathematical Finance Perspective

This project demonstrates an important principle in quantitative finance:

> A mathematical model is useful not only because it produces a solution, but also because it helps us understand the assumptions behind that solution.

The Black-Scholes framework provides an elegant analytical solution under a set of simplifying assumptions.

Monte Carlo simulation provides a flexible numerical framework that can be extended to more complicated models and payoff structures.

The distinction between **analytical tractability** and **model flexibility** is an important concept in quantitative finance.

---

# 12. Project Structure

```text
Option-Pricing-Black-Scholes-Monte-Carlo/
│
├── README.md
│
└── Mathematical_Modeling_of_Option_Pricing.pdf
