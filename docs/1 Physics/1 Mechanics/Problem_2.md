# Investigating the Dynamics of a Forced Damped Pendulum

## Motivation

The forced damped pendulum is an excellent example of a nonlinear dynamical system that exhibits a wide range of behaviors—from periodic motion to chaos. Understanding such systems can help explain real-world phenomena, such as how structures respond to external forces or how energy can be harvested from vibrations.

---

## 1. Theoretical Foundation

The equation of motion for a forced damped pendulum is:

$$
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \sin\theta = A \cos(\omega t)
$$

Where:
- $\theta$ is the angle,
- $\gamma$ is the damping coefficient,
- $\omega_0$ is the natural frequency,
- $A$ is the driving force amplitude,
- $\omega$ is the driving frequency.

For small angles ($\theta \approx \sin\theta$):

$$
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \theta = A \cos(\omega t)
$$

This becomes a linear second-order differential equation.

---

## 2. Analysis of Dynamics

We will explore how varying $\gamma$, $A$, and $\omega$ affects the system.

---

## 3. Python Implementation

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Equation of motion
def pendulum(t, y, gamma, omega0, A, omega):
    theta, omega_theta = y
    dydt = [omega_theta, -gamma * omega_theta - omega0**2 * np.sin(theta) + A * np.cos(omega * t)]
    return dydt

# Simulation parameters
gamma = 0.2       # damping
omega0 = 1.5      # natural frequency
A = 1.2           # driving force amplitude
omega_drive = 2.0 # driving frequency
y0 = [0.1, 0.0]   # initial conditions
t_span = (0, 50)
t_eval = np.linspace(t_span[0], t_span[1], 5000)

# Solve the ODE
sol = solve_ivp(pendulum, t_span, y0, t_eval=t_eval, args=(gamma, omega0, A, omega_drive))

# Plot the results
plt.figure(figsize=(10, 4))
plt.plot(sol.t, sol.y[0])
plt.title('Forced Damped Pendulum Motion')
plt.xlabel('Time (s)')
plt.ylabel('Angle (rad)')
plt.grid(True)
plt.show()
```

---

## 4. Phase Space

```python
# Phase space plot
plt.figure(figsize=(6, 6))
plt.plot(sol.y[0], sol.y[1], lw=0.5)
plt.title('Phase Space')
plt.xlabel('Angle (rad)')
plt.ylabel('Angular Velocity (rad/s)')
plt.grid(True)
plt.show()
```

---

## 5. Poincaré Section

```python
# Take stroboscopic points at every period of the driving force
T = 2 * np.pi / omega_drive
poincare_times = np.arange(0, t_span[1], T)
poincare_points = []

for t_p in poincare_times:
    idx = np.argmin(np.abs(sol.t - t_p))
    poincare_points.append([sol.y[0][idx] % (2*np.pi), sol.y[1][idx]])

poincare_points = np.array(poincare_points)

plt.figure(figsize=(6, 6))
plt.scatter(poincare_points[:, 0], poincare_points[:, 1], s=10, color='red')
plt.title('Poincaré Section')
plt.xlabel('Angle mod $2\pi$')
plt.ylabel('Angular Velocity')
plt.grid(True)
plt.show()
```

---

## 6. Interpretation and Discussion

### Resonance
At certain driving frequencies, the system can resonate, leading to large amplitude oscillations. This is critical in engineering as it can cause systems to fail.

### Chaos
As the driving amplitude increases, or damping is reduced, the system can behave chaotically, showing extreme sensitivity to initial conditions.

---

## 7. Applications
- **Energy Harvesting**: Using pendulum-like systems to convert vibration into electrical energy.
- **Suspension Bridges**: Understanding resonance is essential to prevent collapse (e.g., Tacoma Narrows Bridge).
- **Oscillating Circuits**: Analogy with RLC circuits under AC driving forces.

---

## 8. Limitations and Extensions
- **Nonlinear damping**: Real-world damping may not be linear.
- **Non-periodic driving**: Real forces can be irregular.
- **3D pendulums**: More degrees of freedom introduce richer behavior.

---

This notebook offers a blend of theoretical, numerical, and graphical analysis, providing an accessible but thorough exploration of the forced damped pendulum system.
