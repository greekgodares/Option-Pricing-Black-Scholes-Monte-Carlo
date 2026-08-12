# Mathematical Modeling of Option Pricing

## Black-Scholes PDE and Monte Carlo Simulation

This project develops a mathematical framework for pricing **European call options** using the **Black-Scholes model** and **Monte Carlo simulation**.

The project connects concepts from:

- Stochastic calculus
- Geometric Brownian Motion
- Itô's Lemma
- No-arbitrage pricing
- Partial differential equations
- Heat equations
- Laplace transforms
- Risk-neutral valuation
- Monte Carlo simulation
- Implied volatility
- Volatility smile

The complete mathematical development is provided in the accompanying PDF report.

---

# 1. Project Overview

The objective of this project is to understand European option pricing from both an **analytical** and a **numerical** perspective.

### Analytical Approach

The Black-Scholes approach starts with a stochastic model for the stock price and derives a partial differential equation using Itô's Lemma and a no-arbitrage hedging argument.

The resulting PDE is transformed into the classical heat equation, which leads to the Black-Scholes closed-form solution.

### Numerical Approach

The Monte Carlo approach uses the risk-neutral representation of the option price as a discounted expected payoff.

The expectation is approximated by generating a large number of possible future stock-price paths.

---

# 2. European Call Option

A European call option gives its holder the right, but not the obligation, to buy an underlying asset at the strike price $K$ at maturity $T$.

The payoff at maturity is

$$
C_T = \max(S_T-K,0).
$$

where:

- $S_T$ is the stock price at maturity.
- $K$ is the strike price.
- $C_T$ is the option payoff.

If $S_T>K$, the option finishes in the money.

If $S_T\leq K$, the payoff is zero.

The central problem is to determine the fair value of the option before maturity.

---

# 3. Modeling the Stock Price

The stock price is modeled using **Geometric Brownian Motion**:

$$
dS_t
=
\mu S_t\,dt
+
\sigma S_t\,dW_t.
$$

where:

- $S_t$ = stock price at time $t$
- $\mu$ = expected return
- $\sigma$ = volatility
- $W_t$ = standard Wiener process

The first term represents the deterministic component of the price movement, while the second term represents the random component.

---

# 4. Derivation of the Black-Scholes PDE

Let the option value be

$$
V = V(S,t).
$$

Applying Itô's Lemma gives

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
\,dW_t.
$$

Construct the hedged portfolio

$$
\Pi
=
V
-
\frac{\partial V}{\partial S}S.
$$

The stochastic component can be eliminated through the appropriate hedge.

The resulting portfolio is locally risk-free.

By the no-arbitrage principle, a risk-free portfolio must earn the risk-free rate $r$:

$$
d\Pi = r\Pi\,dt.
$$

Substituting the portfolio value and simplifying gives the **Black-Scholes PDE**:

$$
\boxed{
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
}
$$

For a European call option, the terminal condition is

$$
\boxed{
V(S,T)=\max(S-K,0)
}
$$

---

# 5. Transformation to the Heat Equation

The Black-Scholes PDE contains coefficients involving $S$ and $S^2$.

A suitable change of variables transforms the equation into a simpler constant-coefficient PDE.

## Step 1 — Change of Variables

Define

$$
x=\ln\left(\frac{S}{K}\right)
$$

and

$$
\tau=\frac{\sigma^2}{2}(T-t).
$$

Therefore,

$$
t=T-\frac{2\tau}{\sigma^2}.
$$

Now write the option value as

$$
V(S,t)=K\,v(x,\tau).
$$

Define

$$
k=\frac{2r}{\sigma^2}.
$$

After substituting these transformations into the Black-Scholes PDE, we obtain

$$
\boxed{
\frac{\partial v}{\partial \tau}
=
\frac{\partial^2v}{\partial x^2}
+
(k-1)\frac{\partial v}{\partial x}
-
kv
}
$$

The terminal condition

$$
V(S,T)=\max(S-K,0)
$$

becomes

$$
v(x,0)=\max(e^x-1,0).
$$

---

# 6. Method of Undetermined Coefficients

To eliminate the first-order derivative and the term involving $v$, assume a solution of the form

$$
v(x,\tau)
=
e^{\alpha x+\beta\tau}
u(x,\tau).
$$

Substituting this expression into the transformed PDE and choosing $\alpha$ and $\beta$ appropriately gives

$$
\alpha
=
-\frac{k-1}{2}
$$

and

$$
\beta
=
-\frac{(k+1)^2}{4}.
$$

With these values, the equation reduces to the standard heat equation

$$
\boxed{
\frac{\partial u}{\partial \tau}
=
\frac{\partial^2u}{\partial x^2}
}
$$

The corresponding initial condition is

$$
u(x,0)
=
\max
\left(
e^{\frac{k+1}{2}x}
-
e^{\frac{k-1}{2}x},
0
\right).
$$

Thus, the original Black-Scholes PDE has been transformed into a classical heat-equation problem.

---

# 7. Laplace Transform Approach

The transformed equation is

$$
\frac{\partial u}{\partial \tau}
=
\frac{\partial^2u}{\partial x^2}.
$$

Take the Laplace transform with respect to $\tau$:

$$
\widehat{u}(x,s)
=
\int_0^\infty
e^{-s\tau}
u(x,\tau)\,d\tau.
$$

Using

$$
\mathcal{L}
\left[
\frac{\partial u}{\partial\tau}
\right]
=
s\widehat{u}(x,s)-u(x,0),
$$

we obtain

$$
s\widehat{u}(x,s)-u(x,0)
=
\frac{d^2\widehat{u}}{dx^2}.
$$

Therefore,

$$
\boxed{
\frac{d^2\widehat{u}}{dx^2}
-
s\widehat{u}(x,s)
=
-u(x,0)
}
$$

The corresponding homogeneous equation is

$$
\frac{d^2\widehat{u}}{dx^2}
-
s\widehat{u}
=
0.
$$

Its general homogeneous solution is

$$
\widehat{u}_h(x,s)
=
A(s)e^{\sqrt{s}x}
+
B(s)e^{-\sqrt{s}x}.
$$

Applying the appropriate boundary conditions and performing the inverse Laplace transform leads to the classical Black-Scholes pricing formula.

---

# 8. Black-Scholes Formula

For a European call option, the Black-Scholes price is

$$
\boxed{
C
=
SN(d_1)
-
Ke^{-r(T-t)}N(d_2)
}
$$

where

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

and

$$
d_2
=
d_1-\sigma\sqrt{T-t}.
$$

Here, $N(\cdot)$ is the cumulative distribution function of the standard normal distribution:

$$
N(x)
=
\frac{1}{\sqrt{2\pi}}
\int_{-\infty}^{x}
e^{-z^2/2}\,dz.
$$

---

# 9. Numerical Example

Consider a European call option with the following parameters:

| Parameter | Value |
|---|---:|
| Stock price $S$ | $100$ |
| Strike price $K$ | $100$ |
| Time to maturity $T-t$ | $1$ year |
| Risk-free rate $r$ | $0.05$ |
| Volatility $\sigma$ | $0.20$ |

## Step 1 — Calculate $d_1$

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

Since

$$
\ln(1)=0,
$$

we obtain

$$
d_1
=
\frac{0.05+0.02}{0.20}
=
0.35.
$$

---

## Step 2 — Calculate $d_2$

$$
d_2
=
d_1-\sigma\sqrt{T-t}.
$$

Therefore,

$$
d_2
=
0.35-0.20
=
0.15.
$$

---

## Step 3 — Standard Normal Probabilities

Using the standard normal CDF,

$$
N(d_1)
=
N(0.35)
\approx
0.6368
$$

and

$$
N(d_2)
=
N(0.15)
\approx
0.5596.
$$

---

## Step 4 — Calculate the Option Price

Using the Black-Scholes formula,

$$
C
=
SN(d_1)
-
Ke^{-r(T-t)}N(d_2).
$$

Substituting the values,

$$
C
=
100(0.6368)
-
100e^{-0.05}(0.5596).
$$

Using

$$
e^{-0.05}\approx0.9512,
$$

we obtain approximately

$$
C
\approx
63.68-53.23.
$$

Therefore,

$$
\boxed{
C\approx10.45
}
$$

The theoretical Black-Scholes price of the European call option is approximately **10.45**.

---

# 10. Implied Volatility

The Black-Scholes model takes volatility $\sigma$ as an input.

In practice, the observed market option price can instead be used to determine the volatility implied by the model.

The implied volatility $\sigma_{\mathrm{imp}}$ satisfies

$$
C_{\mathrm{BS}}
\left(
S,K,T,r,\sigma_{\mathrm{imp}}
\right)
=
C_{\mathrm{market}}.
$$

Thus, implied volatility is the value of $\sigma$ that makes the Black-Scholes price equal to the observed market price.

---

# 11. Volatility Smile

If the Black-Scholes assumptions perfectly described market prices, implied volatility would be approximately constant across strike prices.

In real markets, implied volatility varies with the strike price.

Plotting implied volatility against strike price produces patterns commonly referred to as the **volatility smile** or **volatility skew**.

Conceptually:

```text
Implied
Volatility
    ^
    |
    |        \      /
    |         \____/
    |
    +----------------------> Strike Price
                  ATM
```

The volatility smile demonstrates an important limitation of the constant-volatility assumption in the standard Black-Scholes model.

---

# 12. Limitations of the Black-Scholes Model

The standard Black-Scholes model assumes:

- Constant volatility.
- Constant risk-free interest rate.
- Geometric Brownian Motion for the underlying asset.
- Frictionless markets.
- No transaction costs.
- Continuous trading.
- Continuous asset-price paths.
- European-style exercise.

Real financial markets do not perfectly satisfy these assumptions.

In particular, the observed variation in implied volatility across strike prices suggests that a constant-volatility model does not fully capture market option prices.

This motivates more flexible models and numerical methods.

---

# 13. Feynman-Kac Representation

The Feynman-Kac theorem provides a connection between certain partial differential equations and expectations of stochastic processes.

Under the risk-neutral measure $\mathbb{Q}$, the stock price follows

$$
dS_t
=
rS_t\,dt
+
\sigma S_t\,dW_t^{\mathbb{Q}}.
$$

For a European call option, the price can be written as

$$
C(S,t)
=
e^{-r(T-t)}
\mathbb{E}^{\mathbb{Q}}
\left[
\max(S_T-K,0)
\mid S_t=S
\right].
$$

Therefore, the option price is the **discounted expected payoff under the risk-neutral measure**.

Monte Carlo simulation approximates this expectation numerically.

---

# 14. Monte Carlo Simulation

## 14.1 Risk-Neutral Stock Dynamics

Under the risk-neutral measure,

$$
dS_t
=
rS_t\,dt
+
\sigma S_t\,dW_t^{\mathbb{Q}}.
$$

For a time step $\Delta t$, the exact discretization of Geometric Brownian Motion is

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
\right],
$$

where

$$
Z\sim N(0,1).
$$

---

## 14.2 Simulation Procedure

### Step 1 — Initialize the Parameters

For the numerical example,

$$
S_0=100,
\qquad
K=100,
\qquad
T=1,
$$

$$
r=0.05,
\qquad
\sigma=0.20.
$$

---

### Step 2 — Divide the Time Interval

If one year is divided into $252$ trading days,

$$
\Delta t=\frac{1}{252}.
$$

---

### Step 3 — Generate Random Variables

At every time step, generate a standard normal random variable:

$$
Z\sim N(0,1).
$$

Then update the stock price using

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
\right].
$$

Continue until maturity.

---

### Step 4 — Calculate the Payoff

For simulation $i$, the European call payoff is

$$
P_i
=
\max
\left(
S_T^{(i)}-K,
0
\right).
$$

---

### Step 5 — Repeat the Simulation

Repeat the simulation for a large number of independent paths.

For example,

$$
N=100{,}000.
$$

This produces terminal stock prices

$$
S_T^{(1)},
S_T^{(2)},
\ldots,
S_T^{(N)}
$$

and corresponding payoffs

$$
P_1,
P_2,
\ldots,
P_N.
$$

---

### Step 6 — Average the Payoffs

The average simulated payoff is

$$
\overline{P}
=
\frac{1}{N}
\sum_{i=1}^{N}
P_i.
$$

Substituting the call payoff gives

$$
\overline{P}
=
\frac{1}{N}
\sum_{i=1}^{N}
\max
\left(
S_T^{(i)}-K,
0
\right).
$$

---

### Step 7 — Discount to the Present

The Monte Carlo estimate of the option price is

$$
\boxed{
\widehat{C}
=
e^{-rT}
\frac{1}{N}
\sum_{i=1}^{N}
\max
\left(
S_T^{(i)}-K,
0
\right)
}
$$

As $N$ increases, the Monte Carlo estimator converges to the corresponding risk-neutral expected value under the assumed model.

---

# 15. Monte Carlo Convergence

Monte Carlo simulation contains sampling error because the expectation is estimated using a finite number of paths.

The standard error decreases approximately as

$$
O\left(\frac{1}{\sqrt{N}}\right),
$$

where $N$ is the number of simulated paths.

Therefore, increasing the number of simulations generally improves the accuracy of the estimate, although it also increases computational cost.

---

# 16. Black-Scholes vs. Monte Carlo

| Feature | Black-Scholes | Monte Carlo |
|---|---|---|
| Approach | Analytical | Numerical |
| Main method | PDE solution | Simulation |
| Output | Closed-form price | Numerical estimate |
| Computational cost | Low for standard European options | Higher |
| Flexibility | Limited by model assumptions | Highly flexible |
| Complex payoffs | More difficult | More adaptable |
| Random simulation | No | Yes |
| Risk-neutral valuation | Yes | Yes |

The two approaches are based on the same risk-neutral pricing framework but provide different computational methods.

---

# 17. Why Monte Carlo is Useful

Monte Carlo methods become particularly useful when a closed-form solution is difficult or unavailable.

Applications include:

- Path-dependent options
- Barrier options
- Asian options
- Stochastic-volatility models
- Jump-diffusion models
- High-dimensional derivatives

The main advantage is flexibility: complicated stochastic models and payoffs can often be handled by simulation.

---

# 18. Key Result

For the numerical example,

$$
S=100,
\qquad
K=100,
\qquad
T=1,
\qquad
r=0.05,
\qquad
\sigma=0.20,
$$

the Black-Scholes analytical solution gives

$$
\boxed{
C\approx10.45
}
$$

A Monte Carlo implementation using the same model should produce an estimate close to this analytical value when a sufficiently large number of simulations is used.

Any difference is primarily due to Monte Carlo sampling error.

---

# 19. Conclusion

This project demonstrates two complementary approaches to European option pricing.

The Black-Scholes approach begins with the stochastic stock-price model

$$
dS_t
=
\mu S_t\,dt
+
\sigma S_t\,dW_t
$$

and uses Itô's Lemma, hedging, and the no-arbitrage principle to obtain the Black-Scholes PDE

$$
\frac{\partial V}{\partial t}
+
\frac{1}{2}\sigma^2S^2
\frac{\partial^2V}{\partial S^2}
+
rS\frac{\partial V}{\partial S}
-
rV
=
0.
$$

Through an appropriate change of variables, this PDE is transformed into the heat equation

$$
\frac{\partial u}{\partial\tau}
=
\frac{\partial^2u}{\partial x^2}.
$$

The resulting solution leads to the classical Black-Scholes formula

$$
C
=
SN(d_1)
-
Ke^{-r(T-t)}N(d_2).
$$

The Monte Carlo approach instead uses the risk-neutral representation

$$
C(S,t)
=
e^{-r(T-t)}
\mathbb{E}^{\mathbb{Q}}
\left[
\max(S_T-K,0)
\mid S_t=S
\right].
$$

The expectation is estimated by simulating many possible stock-price paths.

The project therefore illustrates an important principle in quantitative finance:

> **Analytical models provide mathematical insight and computational efficiency, while numerical methods provide flexibility when analytical solutions become difficult or unavailable.**

The volatility smile further demonstrates that the assumptions of the standard Black-Scholes model do not completely capture real market behavior.

---

# 20. Project Report

The complete mathematical derivation is available in the accompanying PDF:

**[Mathematical Modeling of Option Pricing — Full Report](./Mathematical_Modeling_of_Option_Pricing.pdf)**

The report covers:

- European option pricing
- Geometric Brownian Motion
- Itô's Lemma
- Black-Scholes PDE
- Risk-free hedging
- Heat-equation transformation
- Method of undetermined coefficients
- Laplace transforms
- Black-Scholes formula
- Numerical example
- Implied volatility
- Volatility smile
- Feynman-Kac theorem
- Monte Carlo simulation
- Analytical vs. numerical pricing

---

# 21. Repository Structure

```text
Option-Pricing-Black-Scholes-Monte-Carlo/
│
├── README.md
│
└── Mathematical_Modeling_of_Option_Pricing.pdf
```

---

# 22. References

1. Black, F. and Scholes, M. (1973).  
   *The Pricing of Options and Corporate Liabilities*.  
   Journal of Political Economy, 81(3), 637–654.

2. Shreve, S. E. (2004).  
   *Stochastic Calculus for Finance II: Continuous-Time Models*.  
   Springer.

3. Heston, S. L. (1993).  
   *A Closed-Form Solution for Options with Stochastic Volatility with Applications to Bond and Currency Options*.  
   The Review of Financial Studies, 6(2), 327–343.

---

# Author

**Rahul Kumar**

Indian Statistical Institute, Kolkata

**Interests:** Quantitative Finance · Mathematical Finance · Algorithmic Trading · Financial Modeling
