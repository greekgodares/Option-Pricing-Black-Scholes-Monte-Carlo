# Mathematical Modeling of Option Pricing

## Black-Scholes PDE and Monte Carlo Simulation

This project studies the mathematical modeling of European option pricing using the **Black-Scholes model** and **Monte Carlo simulation**.

The project covers:

- Geometric Brownian Motion
- Itô's Lemma
- Black-Scholes PDE
- Heat-equation transformation
- Risk-neutral pricing
- Black-Scholes closed-form solution
- Monte Carlo simulation
- Implied volatility
- Volatility smile
- Model limitations

---

## 1. Stock Price Model

The stock price is modeled using Geometric Brownian Motion:

$$
dS_t = \mu S_t\,dt + \sigma S_t\,dW_t
$$

where

$$
S_t = \text{stock price},
\qquad
\mu = \text{expected return},
\qquad
\sigma = \text{volatility}.
$$

Here, $W_t$ is a standard Wiener process.

---

## 2. Option Value

Let the option value be

$$
V = V(S,t).
$$

Applying Itô's Lemma gives

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
\frac{\partial V}{\partial S}
\,dW_t.
$$

---

## 3. Black-Scholes PDE

Using a risk-free hedging argument and the no-arbitrage condition, the Black-Scholes PDE is obtained:

$$
\boxed{
\frac{\partial V}{\partial t}
+
\frac{1}{2}\sigma^2S^2
\frac{\partial^2 V}{\partial S^2}
+
rS\frac{\partial V}{\partial S}
-rV
=0
}
$$

For a European call option, the terminal condition is

$$
\boxed{
V(S,T)=\max(S-K,0)
}
$$

where $K$ is the strike price and $T$ is the maturity time.

---

## 4. Transformation to the Heat Equation

Define

$$
x=\ln\left(\frac{S}{K}\right)
$$

and

$$
\tau=\frac{\sigma^2}{2}(T-t).
$$

Also define

$$
V(S,t)=K\,v(x,\tau).
$$

Let

$$
k=\frac{2r}{\sigma^2}.
$$

The Black-Scholes PDE becomes

$$
\frac{\partial v}{\partial\tau}
=
\frac{\partial^2v}{\partial x^2}
+
(k-1)\frac{\partial v}{\partial x}
-kv.
$$

---

## 5. Removing the First-Order Terms

Assume

$$
v(x,\tau)
=
e^{\alpha x+\beta\tau}u(x,\tau).
$$

Choose

$$
\alpha=-\frac{k-1}{2}
$$

and

$$
\beta=-\frac{(k+1)^2}{4}.
$$

The transformed equation becomes the standard heat equation:

$$
\boxed{
\frac{\partial u}{\partial\tau}
=
\frac{\partial^2u}{\partial x^2}
}
$$

---

## 6. Black-Scholes Closed-Form Solution

For a European call option,

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
\left(r+\frac{\sigma^2}{2}\right)(T-t)
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

Here, $N(\cdot)$ denotes the standard normal cumulative distribution function.

---

## 7. Risk-Neutral Pricing

Under the risk-neutral measure $\mathbb{Q}$,

$$
dS_t
=
rS_t\,dt
+
\sigma S_t\,dW_t^{\mathbb{Q}}.
$$

The European call price can therefore be written as

$$
\boxed{
C(S,t)
=
e^{-r(T-t)}
\mathbb{E}^{\mathbb{Q}}
\left[
\max(S_T-K,0)
\mid S_t=S
\right]
}
$$

This representation provides the foundation for Monte Carlo pricing.

---

## 8. Monte Carlo Simulation

The exact discrete-time evolution of the stock price is

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

For simulation path $i$, the European call payoff is

$$
P_i
=
\max(S_T^{(i)}-K,0).
$$

For $N$ independent simulations, the average payoff is

$$
\overline{P}
=
\frac{1}{N}
\sum_{i=1}^{N}
\max(S_T^{(i)}-K,0).
$$

The Monte Carlo estimate of the option price is therefore

$$
\boxed{
\widehat{C}
=
e^{-rT}
\frac{1}{N}
\sum_{i=1}^{N}
\max(S_T^{(i)}-K,0)
}
$$

---

## 9. Monte Carlo Procedure

1. Choose $S_0$, $K$, $r$, $\sigma$, and $T$.
2. Divide the maturity interval into time steps.
3. Generate independent random variables

$$
Z_1,Z_2,\ldots,Z_N\sim N(0,1).
$$

4. Simulate the stock-price paths.
5. Calculate the payoff for every path.
6. Average the simulated payoffs.
7. Discount the average payoff to the present.

---

## 10. Implied Volatility

Given an observed market price $C_{\text{market}}$, the implied volatility $\sigma_{\text{imp}}$ solves

$$
C_{\text{BS}}
\left(
S,K,T,r,\sigma_{\text{imp}}
\right)
=
C_{\text{market}}.
$$

Thus, implied volatility is the volatility parameter that makes the Black-Scholes model reproduce the observed market price.

---

## 11. Volatility Smile

In the standard Black-Scholes model, volatility is assumed to be constant.

In real markets, however, the implied volatility obtained from option prices varies with the strike price.

This produces the **volatility smile** or **volatility skew**.

The phenomenon demonstrates one of the limitations of the constant-volatility Black-Scholes framework.

---

## 12. Model Limitations

The Black-Scholes model assumes:

- Constant volatility
- Constant risk-free interest rate
- Lognormally distributed stock prices
- Continuous trading
- No transaction costs
- No arbitrage
- Continuous price paths
- European-style exercise

These assumptions are useful for analytical tractability but do not perfectly describe real financial markets.

---

## 13. Black-Scholes vs Monte Carlo

| Feature | Black-Scholes | Monte Carlo |
|---|---|---|
| Method | Analytical | Numerical |
| Main tool | PDE solution | Simulation |
| Standard European call | Closed-form solution | Numerical estimate |
| Computational cost | Low | Higher |
| Flexibility | Limited | High |
| Path-dependent products | Difficult | Well suited |
| Complex models | More difficult | More flexible |

---

## 14. Key Result

For the parameter set

$$
S_0=100,\qquad
K=100,\qquad
T=1,\qquad
r=0.05,\qquad
\sigma=0.20,
$$

the Black-Scholes price of the European call is approximately

$$
\boxed{
C\approx10.45
}
$$

A Monte Carlo simulation using the same parameters should converge toward this value as the number of simulations increases.

---

## 15. Conclusion

The project develops the complete mathematical connection between stochastic stock-price modeling, the Black-Scholes PDE, analytical option pricing, and Monte Carlo simulation.

The central pricing equation is

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

The Black-Scholes formula provides an analytical solution, while Monte Carlo simulation provides a flexible numerical method for estimating the same risk-neutral expectation.

The study of implied volatility and the volatility smile further highlights the limitations of the standard Black-Scholes assumptions.

---

## Project Report

The complete mathematical derivation is available in:

**[Mathematical Modeling of Option Pricing](./Mathematical_Modeling_of_Option_Pricing.pdf)**

---

## Repository Structure

```text
Option-Pricing-Black-Scholes-Monte-Carlo/
│
├── README.md
│
└── Mathematical_Modeling_of_Option_Pricing.pdf
