# Stochastic Differential Equations (SDEs)

## Introduction

Stochastic Differential Equations (SDEs) are differential equations in which one or more terms are stochastic processes. They are used to model systems that exhibit random behavior and are ubiquitous in fields like physics, finance, biology, and engineering.

## What is an SDE?

A general form of an SDE is given by:

$$ dX_t = \mu(X_t, t) dt + \sigma(X_t, t) dW_t $$

where:
- $X_t$ is the state variable at time $t$.
- $\mu(X_t, t)$ is the drift coefficient, representing the deterministic part of the equation.
- $\sigma(X_t, t)$ is the diffusion coefficient, representing the stochastic part of the equation.
- $W_t$ is a Wiener process or Brownian motion.

In this equation:
- The drift term $\mu(X_t, t) dt$ describes the average rate of change of $X_t$.
- The diffusion term $\sigma(X_t, t) dW_t$ introduces randomness into the system, with $dW_t$ representing an increment of a Wiener process.

## Numerical Solvers for SDEs

Analytical solutions to SDEs are rare, making numerical methods crucial for solving them. Here are some commonly used numerical solvers:

### Euler-Maruyama Method

The Euler-Maruyama method is a straightforward extension of the Euler method for ordinary differential equations (ODEs) to SDEs. It is simple to implement and computationally efficient, though not highly accurate for small time steps.

**Key Points:**
- Approximates the solution by incrementing the state variable using both the drift and diffusion terms.
- Suitable for problems where high precision is not critical.

**Formula:**

$$X_{t+\Delta t} = X_t + \mu(X_t, t) \Delta t + \sigma(X_t, t) \Delta W_t$$

where $\Delta W_t \sim \mathcal{N}(0, \Delta t)$.

### Milstein Method

The Milstein method improves upon the Euler-Maruyama method by adding a correction term that takes into account the derivative of the diffusion coefficient. This increases the accuracy, particularly for problems where the diffusion term is significant.

**Key Points:**
- Adds a second-order term to improve accuracy.
- More complex and computationally intensive than Euler-Maruyama.

**Formula:**

$$X_{t+\Delta t} = X_t + \mu(X_t, t) \Delta t + \sigma(X_t, t) \Delta W_t + \frac{1}{2} \sigma(X_t, t) \frac{\partial \sigma(X_t, t)}{\partial X} \left( (\Delta W_t)^2 - \Delta t \right)$$

### Runge-Kutta Methods for SDEs

Runge-Kutta methods adapted for SDEs provide higher-order accuracy and are suitable for more complex problems. These methods generalize the Runge-Kutta approach from ODEs to SDEs.

**Key Points:**
- Suitable for problems requiring high precision.
- Computationally more demanding than simpler methods.

### Stochastic Heun Method

The Stochastic Heun method is an extension of the Heun method for ODEs. It provides better accuracy than the Euler-Maruyama method by incorporating both predictor and corrector steps.

**Key Points:**
- Incorporates a predictor-corrector approach.
- Balances between computational complexity and accuracy.

**Formula:**

1. Predictor step: $$X_{t+\Delta t}^{*} = X_t + \mu(X_t, t) \Delta t + \sigma(X_t, t) \Delta W_t$$
   
2. Corrector step: $$X_{t+\Delta t} = X_t + \frac{1}{2}  \left(\mu(X_t, t) + \mu(X_{t+\Delta t}^{*}, t+\Delta t)\right)  \Delta t + \frac{1}{2} \left( \sigma(X_t, t) + \sigma(X_{t+\Delta t}^{\ast}, t+\Delta t) \right) \Delta W_t$$

### Adaptive Methods

Adaptive methods adjust the time step size based on an estimate of the local error. These methods can significantly enhance efficiency, particularly for problems where the solution exhibits rapid changes.

**Key Points:**
- Dynamically adjusts step size for efficiency.
- Suitable for systems with varying rates of change.

### Monte Carlo Methods

Monte Carlo methods are used to approximate the solutions of SDEs by performing repeated random sampling. These methods are particularly useful for high-dimensional problems and for estimating statistical properties of the solution.

**Key Points:**
- Useful for high-dimensional problems.
- Provides statistical estimates of the solution.

**Approach:**
- Generate a large number of sample paths of the SDE.
- Compute the desired statistics (e.g., mean, variance) from the sample paths.

### Feynman-Kac Formula

The Feynman-Kac formula connects solutions of SDEs with solutions of certain partial differential equations (PDEs). It provides a way to solve PDEs by simulating the corresponding SDE.

**Key Points:**
- Links SDEs to PDEs.
- Useful for solving certain types of PDEs using SDE simulations.

**Formula:**

If $u(x,t)$ is the solution to the PDE:

$$ \frac{\partial u}{\partial t} + \mu(x,t) \frac{\partial u}{\partial x} + \frac{1}{2} \sigma^2(x,t) \frac{\partial^2 u}{\partial x^2} - r u = 0$$

with terminal condition $u(x,T) = g(X_T)$, then $u(x,t)$ can be represented as:

$$u(x,t) = \mathbb{E} \left[ e^{-\int_t^T r(X_s, s) \, ds} g(X_T) \mid X_t = x \right]$$

where $X_t$ follows the SDE:

$$dX_t = \mu(X_t, t) dt + \sigma(X_t, t) dW_t$$

### Other Methods

- **Implicit Methods**: These methods involve solving equations at each time step, often leading to more stable solutions for stiff SDEs.
- **Split-Step Methods**: These methods separate the drift and diffusion steps, solving them alternately. They are useful for certain types of SDEs.
- **Higher-Order Methods**: These include methods like the stochastic Taylor expansion, which provide higher-order accuracy at the cost of increased computational complexity.

## Conclusion

Stochastic Differential Equations are powerful tools for modeling systems with inherent randomness. The choice of numerical solver depends on the specific requirements of the problem, including the desired accuracy and computational resources. The Euler-Maruyama method is a good starting point due to its simplicity, while methods like Milstein and Stochastic Heun offer better accuracy at the cost of increased computational complexity. Monte Carlo methods and the Feynman-Kac formula provide powerful techniques for high-dimensional problems and linking SDEs to PDEs, respectively. Adaptive methods provide efficiency gains for complex problems with variable dynamics.

For detailed implementation and code examples, refer to the `examples` directory in this repository.
