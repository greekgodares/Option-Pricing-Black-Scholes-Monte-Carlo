<div align="center">

# 📈 Mathematical Modeling of Option Pricing
**Using the Black–Scholes PDE and Monte Carlo Simulation**[cite: 2]

From stochastic differential equations to closed-form solutions—validated against a 100,000-path numerical simulation.

**Author:** Rahul Kumar (Roll Number: BSD-DH-2419)[cite: 2]
**Date:** May 4, 2026[cite: 2]

📄 **[Read Full Project Report (PDF)](./Mathematical_Modeling_of_Option_Pricing_(1)_2.pdf)**

</div>

---

## 📑 Table of Contents
* [Overview](#-overview)
* [The Analytical Approach: Black-Scholes PDE](#-the-analytical-approach-black-scholes-pde)
* [The Problem: Volatility Smile](#-the-problem-volatility-smile)
* [The Numerical Approach: Monte Carlo Simulation](#-the-numerical-approach-monte-carlo-simulation)
* [Benchmark Worked Example](#-benchmark-worked-example)
* [References](#-references)

---

## 🔭 Overview
This project explores option pricing through two distinct approaches: the analytical Black-Scholes PDE method and Monte Carlo simulation[cite: 2]. The core question addressed is determining the fair price (premium) of an option today, a problem originally solved by Fischer Black and Myron Scholes in 1973[cite: 2]. 

An option is a financial contract giving the buyer the right, but not the obligation, to buy or sell an asset at a fixed strike price ($K$) on or before a specific expiry date ($T$)[cite: 2].

---

## 🧮 The Analytical Approach: Black-Scholes PDE

### 1. Modeling the Stock Price
The stock price $S_{t}$ is modeled as Geometric Brownian Motion:
$$dS_{t}=\mu S_{t}dt+\sigma S_{t}dW_{t}$$[cite: 2]

Picard's theorem guarantees that this stochastic differential equation (SDE) has a unique solution for any given initial stock price $S_{0}$, as the Lipschitz condition is satisfied ($|\mu S|+|\sigma S|\le C(1+|S|)$)[cite: 2]. 

### 2. From SDE to PDE
Using Ito's Lemma (the stochastic chain rule) and a hedging trick, we construct a portfolio ($\Pi=-V+\frac{\partial V}{\partial S}S$) that eliminates random noise ($dW_{t}$)[cite: 2]. Since this portfolio is risk-free, it must earn the risk-free rate ($r$), yielding the Black-Scholes PDE:
$$\frac{\partial V}{\partial t}+\frac{1}{2}\sigma^{2}S^{2}\frac{\partial^{2}V}{\partial S^{2}}+rS\frac{\partial V}{\partial S}-rV=0$$[cite: 2]

### 3. Reduction to the Heat Equation
The PDE has non-constant coefficients ($S$ and $S^{2}$)[cite: 2]. We transform it into a constant-coefficient form using a change of variables ($S=Ke^{x}$, $t=T-\frac{2\tau}{\sigma^{2}}$, $V(S,t)=Kv(x,\tau)$)[cite: 2]. By applying the method of undetermined coefficients, we reduce this to the canonical 1-D Heat Equation:
$$\frac{\partial u}{\partial\tau}=\frac{\partial^{2}u}{\partial x^{2}}$$[cite: 2]

### 4. Solution via Laplace Transform
Applying the Laplace transform in $\tau$ converts the heat equation into a second-order linear ordinary differential equation (ODE) with constant coefficients:
$$\frac{d^{2}\hat{u}}{dx^{2}}-s\hat{u}(x,s)=-u(x,0)$$[cite: 2]

Solving this ODE and applying the inverse Laplace transform yields the closed-form Black-Scholes Formula:
$$V(S,t)=SN(d_{1})-Ke^{-r(T-t)}N(d_{2})$$[cite: 2]

---

## ⚠️ The Problem: Volatility Smile
A key limitation of the analytical Black-Scholes model is its assumption that volatility ($\sigma$) is constant[cite: 2]. When plotting implied volatility ($\sigma_{imp}$) against the strike price $K$ for real market data, the result is a U-shaped "Market Smile," not a flat line[cite: 2]. 

This shape indicates that the market expects more extreme price movements than the lognormal distribution predicts[cite: 2]. If volatility is not constant, the reduction to the heat equation no longer works (coefficients become state-dependent), and the Laplace transform method fails[cite: 2].

---

## 🎲 The Numerical Approach: Monte Carlo Simulation
Because the analytical PDE approach fails when volatility is not constant (such as in the Heston model where $\sigma$ is random), Monte Carlo simulation offers a highly flexible and robust alternative[cite: 2].

### The Feynman-Kac Theorem
This theorem provides a powerful connection between PDEs and expectations[cite: 2]. It states that the option price is simply the average discounted payoff over all possible future stock prices:
$$V(S,t)=e^{-r(T-t)}\times\mathbb{E}[max(S_{T}-K,0)]$$[cite: 2]

### Simulation Engine
1. Start with today's stock price ($S_{0}=100$)[cite: 2].
2. Simulate a single path by dividing 1 year into small steps (e.g., 252 trading days)[cite: 2]. At each step, update the price randomly using $Z \sim N(0,1)$: 
   $$S_{new}=S_{old}\times e^{(r-\sigma^{2}/2)\Delta t+\sigma\sqrt{\Delta t}\times Z}$$[cite: 2]
3. At expiry, calculate the payoff: $max(S_{T}-100,0)$[cite: 2].
4. Repeat this process for 100,000 paths[cite: 2].
5. Average all payoffs and discount back to today to find the price[cite: 2].

---

## ✅ Benchmark Worked Example
Both the analytical and Monte Carlo approaches were tested against a fixed set of parameters to verify their consistency[cite: 2].

**Parameters:**
* **Current stock price ($S$):** 100[cite: 2]
* **Strike price ($K$):** 100[cite: 2]
* **Time to expiry ($T-t$):** 1 year[cite: 2]
* **Risk-free rate ($r$):** 5% (0.05)[cite: 2]
* **Volatility ($\sigma$):** 20% (0.20)[cite: 2]

**Results:**
| Method | Final Call Option Price |
| :--- | :--- |
| **Analytical (Black-Scholes Formula)** | **Rs. 10.45**[cite: 2] |
| **Monte Carlo Simulation (100,000 paths)** | **~Rs. 10.45**[cite: 2] |

*Interpretation:* If you buy this option for Rs. 10.45, you make a profit if the stock ends above Rs. 110.45 (strike + premium)[cite: 2]. You recover part of your premium if it lands between Rs. 100 and Rs. 110.45, and you lose the entire Rs. 10.45 premium if it lands below Rs. 100[cite: 2].

---

## 📚 References
1. Black, F., & Scholes, M. (1973). The Pricing of Options and Corporate Liabilities. *Journal of Political Economy*, 81(3), 637-654[cite: 2].
2. Heston, S. L. (1993). A Closed-Form Solution for Options with Stochastic Volatility. *The Review of Financial Studies*, 6(2), 327-343[cite: 2].
3. Shreve, S. E. (2004). Stochastic Calculus for Finance II: Continuous-Time Models. *Springer*[cite: 2].
