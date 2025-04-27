# Orbital Period and Orbital Radius

## Motivation

The relationship between the square of the orbital period and the cube of the orbital radius, known as **Kepler's Third Law**, is a cornerstone of celestial mechanics. It connects gravitational physics with real-world phenomena such as satellite trajectories, planetary orbits, and exoplanetary systems.

Understanding this relationship enables us to calculate masses of celestial objects, distances between them, and predict their motions across time.

---

## Derivation of Kepler's Third Law

Consider a small body of mass $m$ orbiting a much larger body of mass $M$ (e.g., a planet around a star) in a **circular orbit**.

From Newton's Law of Universal Gravitation:

\[ F_{gravity} = \frac{G M m}{r^2} \]

And from centripetal force requirement for circular motion:

\[ F_{centripetal} = m \frac{v^2}{r} \]

Setting these equal (since gravity provides the centripetal force):

\[ \frac{G M m}{r^2} = m \frac{v^2}{r} \]

Simplifying:

\[ v^2 = \frac{G M}{r} \]

The orbital period $T$ (time to complete one full circle) is:

\[ T = \frac{2 \pi r}{v} \]

Substituting $v$ from the previous expression:

\[ T = 2 \pi r \sqrt{\frac{r}{G M}} \]

Squaring both sides:

\[ T^2 = 4 \pi^2 \frac{r^3}{G M} \]

Thus, we have derived:

\[ T^2 \propto r^3 \]

where the proportionality constant is \( \frac{4\pi^2}{GM} \).

---

## Implications for Astronomy

- **Mass Determination**: If we can measure $T$ and $r$ for an orbit, we can find the mass $M$ of the central object.
- **Distance Measurements**: Knowing $T$, we can infer the orbital radius $r$.
- **Exoplanet Discovery**: Kepler's law helps detect planets around other stars by analyzing their orbital properties.
- **Satellite Deployment**: Engineers use these principles when placing satellites into orbit around Earth.

---

## Real-World Examples

### Moon around Earth
- Orbital radius: $r \approx 3.84 \times 10^8$ m
- Orbital period: $T \approx 27.3$ days

Using Kepler's law, we can predict the mass of Earth by measuring $T$ and $r$.

### Planets in the Solar System
- All planets obey the $T^2 \propto r^3$ relationship relative to the Sun.
- Deviations can indicate additional forces or masses (like Jupiter's effect on asteroids).

---

## Simulation: Verifying Kepler's Third Law

We will simulate multiple circular orbits with varying radii and verify that $T^2$ versus $r^3$ is a linear relationship.

```python
import numpy as np
import matplotlib.pyplot as plt

# Constants
G = 6.67430e-11  # gravitational constant, m^3 kg^-1 s^-2
M = 5.972e24     # mass of Earth, kg

# Define radii (from 1e7 m to 5e8 m)
radii = np.linspace(1e7, 5e8, 100)

# Calculate periods
periods = 2 * np.pi * np.sqrt(radii**3 / (G * M))

# Plot T^2 vs r^3
plt.figure(figsize=(8,6))
plt.plot(radii**3, periods**2, 'o', markersize=4)
plt.title("Verification of Kepler's Third Law")
plt.xlabel("$r^3$ (m$^3$)")
plt.ylabel("$T^2$ (s$^2$)")
plt.grid(True)
plt.show()
```

This plot should yield a straight line, confirming that $T^2 \propto r^3$.

### Bonus: Plotting Circular Orbits

Let's plot sample circular orbits for different radii.

```python
# Define function to plot orbits
def plot_orbits(radii):
    fig, ax = plt.subplots(figsize=(8,8))
    theta = np.linspace(0, 2*np.pi, 300)
    for r in radii:
        x = r * np.cos(theta)
        y = r * np.sin(theta)
        ax.plot(x, y, label=f"r = {r/1e6:.1f} Mm")

    ax.plot(0, 0, 'yo', markersize=12)  # central mass
    ax.set_aspect('equal')
    ax.set_title("Circular Orbits Around a Central Body")
    ax.set_xlabel("x (m)")
    ax.set_ylabel("y (m)")
    ax.legend()
    plt.grid(True)
    plt.show()

# Plot sample orbits
sample_radii = [1e7, 2e7, 3e7, 4e7]
plot_orbits(sample_radii)
```

---

## Extensions to Elliptical Orbits

Kepler's Third Law also applies to **elliptical orbits** if we replace $r$ with the **semi-major axis** $a$ of the ellipse:

\[ T^2 = \frac{4 \pi^2}{G M} a^3 \]

Thus, for any orbit (circle is a special case of an ellipse), the same $T^2 \propto a^3$ relationship holds.

This is crucial for studying:
- Planetary orbits
- Comets (which have highly elliptical orbits)
- Binary star systems

---

# Conclusion

Kepler's Third Law elegantly connects time and space in celestial mechanics. It reflects the deep relationship between mass, distance, and motion, providing a powerful tool across astrophysics, orbital mechanics, and cosmology.
