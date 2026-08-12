# Mathematical Modeling of Option Pricing

### Using the Black-Scholes PDE and Monte Carlo Simulation

This project studies **European option pricing** using two complementary approaches:

1. **Black-Scholes PDE** — an analytical approach based on stochastic calculus, partial differential equations, and the no-arbitrage principle.
2. **Monte Carlo Simulation** — a numerical approach based on simulating a large number of possible future stock-price paths.

The project also studies the **volatility smile**, which highlights an important limitation of the constant-volatility assumption in the standard Black-Scholes model.

The mathematical development connects concepts from **differential equations, stochastic processes, probability, and mathematical finance**.

---

## 1. Introduction

### 1.1 What is an Option?

An option is a financial contract that gives the buyer the **right, but not the obligation**, to buy or sell an underlying asset at a predetermined price, called the **strike price** $K$, on or before a specified date.

For a European call option, the payoff at maturity is:

$$
\operatorname{Payoff}
=
\max(S_T-K,0)
$$

where:

- $S_T$ = stock price at maturity
- $K$ = strike price

For example, if $K=100$ and the stock price at expiry is $120, the payoff is:

$$
\max(120-100,0)=20
$$

If the stock price is $80, the payoff is:

$$
\max(80-100,0)=0
$$

The central question is:

> **What is the fair price of this option today?**

This is the problem addressed by the Black-Scholes framework.

---

## 2. The Black-Scholes PDE

### 2.1 Modeling the Stock Price

The stock price $S_t$ is modeled as a **Geometric Brownian Motion**:

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

This stochastic differential equation describes the continuous evolution of the stock price with both a deterministic and a random component.

---

### 2.2 From SDE to PDE

Let $V(S,t)$ denote the value of the option.

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
\frac{\partial^2V}{\partial S^2}
\right)dt
+
\sigma S
\frac{\partial V}{\partial S}
dW_t
$$

To eliminate the random component, construct the hedged portfolio:

$$
\Pi
=
-V
+
\frac{\partial V}{\partial S}S
$$

The stochastic term cancels, giving:

$$
d\Pi
=
\left(
-\frac{\partial V}{\partial t}
-
\frac{1}{2}\sigma^2S^2
\frac{\partial^2V}{\partial S^2}
\right)dt
$$

Since the portfolio is risk-free, the **no-arbitrage principle** requires:

$$
d\Pi=r\Pi\,dt
$$

Substituting the portfolio value gives the **Black-Scholes PDE**:

$$
\frac{\partial V}{\partial t}
+
\frac{1}{2}\sigma^2S^2
\frac{\partial^2V}{\partial S^2}
+
rS\frac{\partial V}{\partial S}
-rV
=
0
$$

For a European call option, the terminal condition is:

$$
V(S,T)
=
\max(S-K,0)
$$

---

# 3. Reduction to the Heat Equation

The Black-Scholes PDE contains non-constant coefficients involving $S$ and $S^2$.

A change of variables transforms the equation into a constant-coefficient equation.

### Step 1: Change of Variables

Define:

$$
S=Ke^x
$$

and

$$
t
=
T-\frac{2\tau}{\sigma^2}
$$

and write:

$$
V(S,t)
=
Kv(x,\tau)
$$

Define:

$$
k=\frac{2r}{\sigma^2}
$$

After substitution, the Black-Scholes PDE becomes:

$$
\frac{\partial v}{\partial \tau}
=
\frac{\partial^2v}{\partial x^2}
+
(k-1)\frac{\partial v}{\partial x}
-kv
$$

---

### Step 2: Method of Undetermined Coefficients

Assume a solution of the form:

$$
v(x,\tau)
=
e^{\alpha x+\beta\tau}
u(x,\tau)
$$

Substituting this into the transformed PDE and choosing $\alpha$ and $\beta$ appropriately eliminates the first-order derivative and zeroth-order terms.

The required values are:

$$
\alpha
=
-\frac{k-1}{2}
$$

and

$$
\beta
=
-\frac{(k+1)^2}{4}
$$

The equation then reduces to the standard **heat equation**:

$$
\frac{\partial u}{\partial \tau}
=
\frac{\partial^2u}{\partial x^2}
$$

The corresponding initial condition is:

$$
u(x,0)
=
\max
\left(
e^{\frac{k+1}{2}x}
-
e^{\frac{k-1}{2}x},
0
\right)
$$

This transformation is the key step that connects the Black-Scholes PDE with classical differential-equation techniques.

---

# 4. Solution Using the Laplace Transform

Apply the Laplace transform with respect to $\tau$:

$$
\hat{u}(x,s)
=
\int_0^\infty
e^{-s\tau}
u(x,\tau)
\,d\tau
$$

Since:

$$
\frac{\partial u}{\partial\tau}
=
\frac{\partial^2u}{\partial x^2}
$$

the transformed equation becomes:

$$
\frac{d^2\hat{u}}{dx^2}
-
s\hat{u}(x,s)
=
-u(x,0)
$$

This is a second-order linear ordinary differential equation with constant coefficients.

The homogeneous solution is:

$$
\hat{u}_h(x,s)
=
A(s)e^{-\sqrt{s}\,x}
+
B(s)e^{\sqrt{s}\,x}
$$

Applying the appropriate boundary conditions and taking the inverse Laplace transform leads to the classical **Black-Scholes formula**.

---

# 5. Black-Scholes Formula

For a European call option, the Black-Scholes price is:

$$
V(S,t)
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

Here, $N(x)$ is the cumulative distribution function of the standard normal distribution:

$$
N(x)
=
\frac{1}{\sqrt{2\pi}}
\int_{-\infty}^{x}
e^{-z^2/2}\,dz
$$

---

# 6. Worked Example

Consider a European call option with:

| Parameter | Value |
|---|---:|
| Current stock price $S$ | 100 |
| Strike price $K$ | 100 |
| Time to expiry $T-t$ | 1 year |
| Risk-free rate $r$ | 0.05 |
| Volatility $\sigma$ | 0.20 |

---

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

Since:

$$
\ln(1)=0
$$

we obtain:

$$
d_1
=
\frac{0.05+0.02}{0.20}
$$

Therefore:

$$
d_1=0.35
$$

---

### Step 2: Calculate $d_2$

$$
d_2
=
d_1-\sigma\sqrt{T-t}
$$

Therefore:

$$
d_2
=
0.35-0.20
=
0.15
$$

---

### Step 3: Calculate the Normal CDF Values

Using the standard normal distribution:

$$
N(d_1)
=
N(0.35)
\approx
0.6368
$$

and:

$$
N(d_2)
=
N(0.15)
\approx
0.5596
$$

---

### Step 4: Calculate the Option Price

Using the Black-Scholes formula:

$$
V
=
SN(d_1)
-
Ke^{-r(T-t)}N(d_2)
$$

Substituting the values:

$$
V
=
100(0.6368)
-
100e^{-0.05}(0.5596)
$$

Using:

$$
e^{-0.05}\approx0.9512
$$

we obtain approximately:

$$
V
=
63.68
-
53.23
$$

Therefore:

$$
\boxed{V\approx10.45}
$$

Thus, the theoretical Black-Scholes price of the European call option is approximately **10.45**.

---

# 7. The Volatility Smile

## 7.1 Implied Volatility

The Black-Scholes formula takes volatility $\sigma$ as an input.

We can also work in the opposite direction.

Given an observed market option price $V_{\text{market}}$, we can solve for the volatility that makes the Black-Scholes formula equal to the market price.

This volatility is called the **implied volatility**:

$$
V_{\text{BS}}
\left(
S,K,T,r,\sigma_{\text{imp}}
\right)
=
V_{\text{market}}
$$

If the Black-Scholes model were perfectly consistent with market prices, the implied volatility would be approximately constant across different strike prices.

---

## 7.2 What the Market Shows

In real markets, implied volatility varies with the strike price.

Plotting implied volatility against strike price often produces a pattern known as the **volatility smile** or **volatility skew**.

Conceptually:

```text
Implied
Volatility
   ^
   |
   |       \        /
   |        \______/
   |
   +----------------------> Strike Price
                ATM
