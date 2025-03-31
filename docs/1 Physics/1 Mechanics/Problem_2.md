# Investigating the Dynamics of a Forced Damped Pendulum

## 🎯 Motivation

The forced damped pendulum is a fascinating example of nonlinear dynamics. It behaves in simple and predictable ways under small forces, but when driven periodically and influenced by damping, it can transition into complex and chaotic motion. This system helps us understand a wide range of natural and engineered systems — from mechanical oscillators to electrical circuits.

---

## 📚 1. Theoretical Foundation

The general equation for a forced damped pendulum is:

$$
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \sin\theta = A \cos(\omega t)
$$

Where:
- $\theta$: angle of the pendulum (radians)
- $\gamma$: damping coefficient
- $\omega_0$: natural angular frequency $= \sqrt{g / L}$
- $A$: amplitude of the external driving force
- $\omega$: frequency of the external driving force

### 🧠 Small-Angle Approximation
For small $\theta$, $\sin\theta \approx \theta$, which simplifies the equation to:

$$
\frac{d^2\theta}{dt^2} + \gamma \frac{d\theta}{dt} + \omega_0^2 \theta = A \cos(\omega t)
$$

This linear version is easier to analyze and helps understand phenomena like resonance.

---

## ⚙️ 2. Python Simulation

Let's simulate the pendulum using Python and visualize its motion.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import solve_ivp

# Differential equation of motion
def pendulum(t, y, gamma, omega0, A, omega):
    theta, omega_theta = y
    dydt = [omega_theta, -gamma * omega_theta - omega0**2 * np.sin(theta) + A * np.cos(omega * t)]
    return dydt

# Parameters
gamma = 0.2         # damping
omega0 = 1.5        # natural frequency
A = 1.2             # driving amplitude
omega_drive = 2.0   # driving frequency

y0 = [0.1, 0.0]     # initial angle and angular velocity
t_span = (0, 50)
t_eval = np.linspace(*t_span, 5000)

# Solve the system
sol = solve_ivp(pendulum, t_span, y0, t_eval=t_eval, args=(gamma, omega0, A, omega_drive))

# Plot angle vs time
plt.figure(figsize=(10, 4))
plt.plot(sol.t, sol.y[0], label='Angle (θ)')
plt.title('Forced Damped Pendulum: Angle vs Time')
plt.xlabel('Time (s)')
plt.ylabel('Angle (rad)')
plt.grid(True)
plt.legend()
plt.show()
```

---

## 🔁 3. Phase Space

```python
# Plot phase diagram
plt.figure(figsize=(6, 6))
plt.plot(sol.y[0], sol.y[1], lw=0.7)
plt.title('Phase Space: Angular Velocity vs Angle')
plt.xlabel('Angle θ (rad)')
plt.ylabel('Angular Velocity ω (rad/s)')
plt.grid(True)
plt.show()
```

---

## 🌌 4. Poincaré Section

```python
# Time intervals at which to sample (stroboscopic view)
T = 2 * np.pi / omega_drive
poincare_times = np.arange(0, t_span[1], T)
poincare_points = []

for t_p in poincare_times:
    idx = np.argmin(np.abs(sol.t - t_p))
    poincare_points.append([sol.y[0][idx] % (2*np.pi), sol.y[1][idx]])

poincare_points = np.array(poincare_points)

# Plot
plt.figure(figsize=(6, 6))
plt.scatter(poincare_points[:, 0], poincare_points[:, 1], s=10, color='crimson')
plt.title('Poincaré Section')
plt.xlabel('θ mod $2\pi$ (rad)')
plt.ylabel('Angular Velocity (rad/s)')
plt.grid(True)
plt.show()
```

---

## 📊 5. Exploring Parameters

Try changing these values to see how the system behaves:
- Increase `A` to observe chaos.
- Decrease `γ` to reduce damping.
- Set `ω ≈ ω₀` to observe resonance.

This reveals how delicate and rich the system's response is.

---

## 🌍 6. Real-World Applications

- **Energy Harvesters**: Devices that extract power from vibration.
- **Suspension Bridges**: Preventing resonance avoids structural failure.
- **Washing Machines**: Reduce unbalanced vibrations via damping.
- **RLC Circuits**: Analogous systems in electronics.

---

## 🧪 7. Model Limitations and Extensions

- ✅ Uses idealized sine driving force.
- ❌ Doesn't include nonlinear damping (e.g., air resistance at high speeds).
- ❌ Doesn't account for 3D movement.

### 🔄 Possible Extensions
- Non-periodic or random driving forces
- Double pendulum (coupled chaos)
- Bifurcation diagrams to map parameter space

---

## ✅ Summary

This project showed how a simple mechanical system can exhibit complex dynamics. Using Python, we:
- Simulated motion using numerical integration
- Visualized time evolution, phase space, and Poincaré sections
- Observed transitions from regular to chaotic behavior

📌 _Learning how systems like this respond to forces is key to physics, engineering, and understanding nature._

---

Feel free to change parameters and explore! 🎉
