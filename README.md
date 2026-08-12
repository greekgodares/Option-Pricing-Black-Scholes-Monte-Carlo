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

The payoff at maturity is:

$$C_T = \max(S_T - K, 0)$$

where:
- $S_T$ is the stock price at maturity.
- $K$ is the strike price.
- $C_T$ is the option payoff.

If $S_T > K$, the option finishes in the money.  
If $S_T \le K$, the payoff is zero.

The central problem is to determine the fair value of the option before maturity.

---

# 3. Modeling the Stock Price

The stock price is modeled using **Geometric Brownian Motion**:

$$dS_t = \mu S_t \, dt + \sigma S_t \, dW_t$$

where:
- $S_t$ = stock price at time $t$
- $\mu$ = expected return
- $\sigma$ = volatility
- $W_t$ = standard Wiener process

The first term represents the deterministic component of the price movement, while the second term represents the random component.

---

# 4. Derivation of the Black-Scholes PDE

Let the option value be $V = V(S,t)$. Applying Itô's Lemma gives:

$$dV = \left( \frac{\partial V}{\partial t} + \mu S \frac{\partial V}{\partial S} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 V}{\partial S^2} \right) dt + \sigma S \frac{\partial V}{\partial S} \, dW_t$$

Construct the hedged portfolio:

$$\Pi = V - \frac{\partial V}{\partial S} S$$

The stochastic component can be eliminated through the appropriate hedge. The resulting portfolio is locally risk-free.

By the no-arbitrage principle, a risk-free portfolio must earn the risk-free rate $r$:

$$d\Pi = r \Pi \, dt$$

Substituting the portfolio value and simplifying gives the **Black-Scholes PDE**:

$$\frac{\partial V}{\partial t} + \frac{1}{2} \sigma^2 S^2 \frac{\partial^2 V}{\partial S^2} + r S \frac{\partial V}{\partial S} - r V = 0$$

For a European call option, the terminal condition is:

$$V(S, T) = \max(S - K, 0)$$

---

# 5. Transformation to the Heat Equation

The Black-Scholes PDE contains coefficients involving $S$ and $S^2$. A suitable change of variables transforms the equation into a simpler constant-coefficient PDE.

## Step 1 — Change of Variables

Define:

$$x = \ln\left(\frac{S}{K}\right)$$

and

$$\tau = \frac{\sigma^2}{2}(T - t)$$

Therefore,

$$t = T - \frac{2\tau}{\sigma^2}$$

Now write the option value as:

$$V(S,t) = K \, v(x,\tau)$$

Define:

$$k = \frac{2r}{\sigma^2}$$

After substituting these transformations into the Black-Scholes PDE, we obtain:

$$\frac{\partial v}{\partial \tau} = \frac{\partial^2 v}{\partial x^2} + (k - 1) \frac{\partial v}{\partial x} - k v$$

The terminal condition $V(S,T) = \max(S - K, 0)$ becomes:

$$v(x, 0) = \max(e^x - 1, 0)$$

---

# 6. Method of Undetermined Coefficients

To eliminate the first-order derivative and the term involving $v$, assume a solution of the form:

$$v(x,\tau) = e^{\alpha x + \beta \tau} u(x,\tau)$$

Substituting this expression into the transformed PDE and choosing $\alpha$ and $\beta$ appropriately gives:

$$\alpha = -\frac{k - 1}{2}$$

and

$$\beta = -\frac{(k + 1)^2}{4}$$

With these values, the equation reduces to the standard heat equation:

$$\frac{\partial u}{\partial \tau} = \frac{\partial^2 u}{\partial x^2}$$

The corresponding initial condition is:

$$u(x,0) = \max\left( e^{\frac{k+1}{2}x} - e^{\frac{k-1}{2}x}, 0 \right)$$

Thus, the original Black-Scholes PDE has been transformed into a classical heat-equation problem.

---

# 7. Laplace Transform Approach

The transformed equation is:

$$\frac{\partial u}{\partial \tau} = \frac{\partial^2 u}{\partial x^2}$$

Take the Laplace transform with respect to $\tau$:

$$\widehat{u}(x,s) = \int_0^\infty e^{-s\tau} u(x,\tau) \, d\tau$$

Using $\mathcal{L}\left[ \frac{\partial u}{\partial \tau} \right] = s \widehat{u}(x,s) - u(x,0)$, we obtain:

$$s \widehat{u}(x,s) - u(x,0) = \frac{d^2 \widehat{u}}{dx^2}$$

Therefore,

$$\frac{d^2 \widehat{u}}{dx^2} - s \widehat{u}(x,s) = -u(x,0)$$

The corresponding homogeneous equation is:

$$\frac{d^2 \widehat{u}}{dx^2} - s \widehat{u} = 0$$

Its general homogeneous solution is:

$$\widehat{u}_h(x,s) = A(s) e^{\sqrt{s}x} + B(s) e^{-\sqrt{s}x}$$

Applying the appropriate boundary conditions and performing the inverse Laplace transform leads to the classical Black-Scholes pricing formula.

---

# 8. Black-Scholes Formula

For a European call option, the Black-Scholes price is:

$$C = S N(d_1) - K e^{-r(T-t)} N(d_2)$$

where

$$d_1 = \frac{\ln(S/K) + \left(r + \frac{\sigma^2}{2}\right)(T-t)}{\sigma \sqrt{T-t}}$$

and

$$d_2 = d_1 - \sigma \sqrt{T-t}$$

Here, $N(\cdot)$ is the cumulative distribution function of the standard normal distribution:

$$N(x) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{x} e^{-z^2/2} \, dz$$

---

# 9. Numerical Example

Consider a European call option with the following parameters:

| Parameter | Value |
| :--- | :---: |
| Stock price $S$ | $100$ |
| Strike price $K$ | $100$ |
| Time to maturity $T-t$ | $1$ year |
| Risk-free rate $r$ | $0.05$ |
| Volatility $\sigma$ | $0.20$ |

## Step 1 — Calculate $d_1$

$$d_1 = \frac{\ln(100/100) + \left(0.05 + \frac{0.20^2}{2}\right)(1)}{0.20 \sqrt{1}}$$

Since $\ln(1) = 0$, we obtain:

$$d_1 = \frac{0.05 + 0.02}{0.20} = 0.35$$

---

## Step 2 — Calculate $d_2$

$$d_2 = d_1 - \sigma \sqrt{T-t}$$

Therefore,

$$d_2 = 0.35 - 0.20 = 0.15$$

---

## Step 3 — Standard Normal Probabilities

Using the standard normal CDF:

$$N(d_1) = N(0.35) \approx 0.6368$$

and

$$N(d_2) = N(0.15) \approx 0.5596$$

---

## Step 4 — Calculate the Option Price

Using the Black-Scholes formula:

$$C = S N(d_1) - K e^{-r(T-t)} N(d_2)$$

Substituting the values:

$$C = 100(0.6368) - 100 e^{-0.05}(0.5596)$$

Using $e^{-0.05} \approx 0.9512$, we obtain approximately:

$$C \approx 63.68 - 53.23$$

Therefore,

$$C \approx 10.45$$

The theoretical Black-Scholes price of the European call option is approximately **10.45**.

---

# 10. Implied Volatility

The Black-Scholes model takes volatility $\sigma$ as an input. In practice, the observed market option price can instead be used to determine the volatility implied by the model.

The implied volatility $\sigma_{\mathrm{imp}}$ satisfies:

$$C_{\mathrm{BS}}\left(S, K, T, r, \sigma_{\mathrm{imp}}\right) = C_{\mathrm{market}}$$

Thus, implied volatility is the value of $\sigma$ that makes the Black-Scholes price equal to the observed market price.

---

# 11. Volatility Smile

If the Black-Scholes assumptions perfectly described market prices, implied volatility would be approximately constant across strike prices.

In real markets, implied volatility varies with the strike price. Plotting implied volatility against strike price produces patterns commonly referred to as the **volatility smile** or **volatility skew**.

Conceptually:

```text
Implied
Volatility
    ^
    |
    |        \        /
    |         \______/
    |
    +----------------------> Strike Price
                ATM
