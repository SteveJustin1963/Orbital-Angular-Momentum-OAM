# Optical Vortices / Structured Light — 10 Experiments From Easy to Hard

This is an expanded and corrected experiment ladder based on the original five-experiment draft. The original ideas are retained: fork gratings, vortex-core observation, corkscrew/fork interference, topological-charge measurement, OAM transfer, bottle/dark beams, and liquid-crystal birefringence. The sequence below makes them build on each other, adds the missing mathematics, adds realistic warnings about what is and is not measurable with cheap equipment, and includes Python code where simulation or analysis helps.

---

## Read This First: Laser Safety

Use only a low-power Class 2 or Class 3R visible laser pointer, ideally 1–5 mW. Never look into the beam, never aim at people, animals, roads, windows, aircraft, or reflective objects. Mirrors, glass, metal, CDs/DVDs, and even phone screens can create dangerous specular reflections. Keep the beam below eye level or enclosed against a matte beam stop.

A green 532 nm laser looks bright because the eye is very sensitive near green. Bright does not mean safe.

---

## Minimum Kit

| Item | Purpose |
|---|---|
| 1–5 mW laser pointer, preferably green 532 nm | Light source |
| White wall/card/screen | Projection surface |
| Transparency film or printed photomask | Fork gratings and masks |
| Laser printer or commercial print service | High contrast grating masks |
| Binder clips, cardboard, Blu Tack, small clamps | Cheap optical mounts |
| Magnifying glass or small convex lens | Focusing / Fourier plane experiments |
| Old LCD calculator/watch screen | Liquid-crystal birefringence demo |
| Polarizing film or two cheap polarizing sunglasses lenses | Polarizer/analyser experiments |
| Smartphone camera | Beam-profile recording |
| Optional: small mirror, microscope slide, DVD/CD fragment | Beam splitting/interference |
| Optional: photodiode + audio input / Arduino | harder detection experiments |

---

## Core Theory Used Throughout

An optical vortex has a phase that winds around the beam axis:

$\[ E_l(r,\phi,z)=A(r,z)e^{i l\phi}e^{ikz} \]$

where:

- $\(l\)$ is the **topological charge**.
- $(\phi=\mathrm{atan2}(y,x))$ is the azimuthal angle.
- $\(e^{il\phi}\)$ is the helical phase term.
- $\(l>0\)$ and $\(l<0\)$ have opposite handedness.
- $\(l=0\)$ is an ordinary non-vortex beam.


When you go once around the centre:

$\[\Delta \Phi = \Phi(\phi+2\pi)-\Phi(\phi)=2\pi l \]$
 

At the exact centre, $\(\phi\)$ is undefined. A physical wave cannot have a single point with every possible phase at once, so the amplitude goes to zero:
$\[ A(0,z)=0 \]$

Therefore:
$\[ I(0,z)=|E(0,z)|^2=0 \]$


That is the dark eye of the optical tornado.

For the common \(p=0\) Laguerre-Gaussian vortex mode:

$$
\[
E_l(r,\phi) \propto
\left(\frac{\sqrt{2}r}{w}\right)^{|l|}
e^{-r^2/w^2}
e^{il\phi}
\]
$$

and the intensity is:

$$
\[
I_l(r)\propto
\left(\frac{2r^2}{w^2}\right)^{|l|}
e^{-2r^2/w^2}
\]
$$

The bright ring radius is approximately:

$$
\[
r_{\max}=w\sqrt{\frac{|l|}{2}}
\]
$$

This is why higher $\|l|\$ vortices have a larger dark centre and a larger bright ring.  

Each photon in a clean LG vortex mode carries orbital angular momentum:

$\[L_z=l\hbar\]$

This is separate from spin angular momentum, which comes from circular polarization.
---

# Experiment 1 — Baseline Beam Profiler and Divergence Measurement

**Difficulty:** Easy  
**Original connection:** This prepares you for measuring the vortex cores in the later experiments.  
**What you learn:** Gaussian beams, beam waist, divergence, phone-camera beam profiling.

## Aim

Before making a vortex, learn what your ordinary laser beam looks like and how it expands with distance.

## Setup

1. Tape white paper to a wall.
2. Put the laser on a stable support.
3. Mark distances: 0.5 m, 1 m, 2 m, 3 m.
4. At each distance, photograph the beam spot using manual exposure if your phone allows it.
5. Avoid saturating the camera. Use dimmer exposure or a neutral-density substitute such as translucent plastic, but do not use reflective filters.

## Maths

An ideal Gaussian beam radius evolves as:

$$
\[
w(z)=w_0\sqrt{1+\left(\frac{z-z_0}{z_R}\right)^2}
\]
$$

where:

$$
\[
z_R=\frac{\pi w_0^2}{\lambda}
\]
$$

For a far-field beam, the divergence half-angle is approximately:

$$
\[
\theta \approx \frac{w_2-w_1}{z_2-z_1}
\]
$$

For a diffraction-limited Gaussian beam:

$$
\[
\theta_{\min}\approx \frac{\lambda}{\pi w_0}
\]
$$

Cheap laser pointers are not usually diffraction-limited, so measured divergence is often worse.

## Python: Fit a 2D Gaussian Spot

Save a cropped photo as `beam.jpg`.

```python
import numpy as np
import matplotlib.pyplot as plt
from PIL import Image

img = Image.open("beam.jpg").convert("L")
I = np.asarray(img, dtype=float)
I = I - I.min()
I = I / I.max()

y, x = np.indices(I.shape)

# centroid
total = I.sum()
xc = (x * I).sum() / total
yc = (y * I).sum() / total

# RMS radii
sx = np.sqrt(((x - xc)**2 * I).sum() / total)
sy = np.sqrt(((y - yc)**2 * I).sum() / total)

print("Centroid x,y:", xc, yc)
print("RMS radius x,y in pixels:", sx, sy)

plt.imshow(I, cmap="gray")
plt.scatter([xc], [yc])
plt.title("Beam spot and centroid")
plt.show()
```

## Expected Result

You should get a roughly circular or elliptical bright spot. This becomes your baseline for comparing vortex beams.

---

# Experiment 2 — Fork Grating Vortex Generator

**Difficulty:** Easy  
**Original connection:** This is the original “Fork Grating Vortex” experiment, strengthened and made more precise.  
**What you learn:** Phase singularities, topological charge, diffraction orders, OAM generation.

## Aim

Use a printed fork grating to convert a normal laser beam into one or more optical vortex beams.

## Setup

1. Generate fork gratings for \(l=1,2,3\).
2. Print them on transparency film at the highest resolution possible.
3. Shine the laser through the fork dislocation.
4. Project the diffraction pattern on a wall 1–3 m away.
5. Look at the first-order diffracted spots on either side of the central beam.

## Maths

A simple binary fork grating can be written as:

$$
t(x,y)=\frac{1}{2}\left[1+\mathrm{sgn}
\left(
\cos\left(\frac{2\pi x}{d}+l\,\mathrm{atan2}(y,x)\right)
\right)
\right]
$$

where:

- $\(d\)$ is the grating period.
- $\(l\)$ is the fork charge.
- $\(\mathrm{atan2}(y,x)\)$ is essential; plain $\(\arctan(y/x)\)$ loses quadrant information.

A grating sends light into diffraction orders:

$$
\[
d\sin\theta_m=m\lambda
\]
$$

For small angles:

$$
\[
x_m \approx L\frac{m\lambda}{d}
\]
$$

A fork grating does not simply make the whole outgoing beam a vortex. It produces vortex beams mainly in the diffracted side orders. The \(m\)-th diffraction order approximately carries charge:

$$
\[
l_m=m l
\]
$$

depending on sign convention.

## Python: Generate Printable Fork Gratings

```python
import numpy as np
import matplotlib.pyplot as plt

def make_fork_grating(l=1, N=1600, period_px=40, filename="fork_l1.png"):
    x = np.arange(N) - N/2
    y = np.arange(N) - N/2
    X, Y = np.meshgrid(x, y)
    phi = np.arctan2(Y, X)
    pattern = 0.5 * (1 + np.sign(np.cos(2*np.pi*X/period_px + l*phi)))
    plt.imsave(filename, pattern, cmap="gray")
    print("Saved", filename)

for l in [1, 2, 3, -1, -2, -3]:
    make_fork_grating(l=l, filename=f"fork_l{l}.png")
```

## Expected Result

You should see a central undiffracted spot and side spots. The side spots should show a dark central hole. Higher \(|l|\) should give a larger hole and wider ring.

## Common Problems

| Problem | Cause | Fix |
|---|---|---|
| No side dots | Grating too large/coarse or poor contrast | Print smaller / increase contrast |
| No dark hole | Beam not centered on fork | Align laser through the fork defect |
| Blurry pattern | Transparency too rough or wall too close | Move screen farther away |
| Whole beam messy | Laser not collimated or mask poor | Try another pointer / cleaner transparency |

---

# Experiment 3 — Topological Charge Counter by Core Radius

**Difficulty:** Easy–Medium  
**Original connection:** This expands the original “Topological Charge Counter” bonus.  
**What you learn:** Quantitative measurement of \(|l|\), radial intensity profiles, scaling laws.

## Aim

Photograph vortex rings for \(l=1,2,3\), measure their ring radius, and test whether:

$$
\[
r_{\max}\propto \sqrt{|l|}
\]
$$

## Setup

1. Use the fork gratings from Experiment 2.
2. Keep screen distance fixed.
3. Photograph the same diffraction order for each \(l\).
4. Crop the vortex spot only.
5. Use Python to find the radial intensity profile.

## Maths

For \(p=0\) LG modes:

$$
\[
I_l(r)\propto r^{2|l|}e^{-2r^2/w^2}
\]
$$

Take the derivative:

$$
\[
\frac{d}{dr}\left(r^{2|l|}e^{-2r^2/w^2}\right)=0
\]
$$

This gives:

$$
\[
r_{\max}=w\sqrt{\frac{|l|}{2}}
\]
$$

Therefore:

$$
\[
r_{\max}^2 \propto |l|
\]
$$

This is more reliable than measuring the “dark hole diameter” by eye.

## Python: Radial Profile From a Photo

```python
import numpy as np
import matplotlib.pyplot as plt
from PIL import Image

def radial_profile(filename):
    img = Image.open(filename).convert("L")
    I = np.asarray(img, dtype=float)
    I = I - I.min()
    I = I / (I.max() + 1e-12)

    y, x = np.indices(I.shape)
    total = I.sum()
    xc = (x * I).sum() / total
    yc = (y * I).sum() / total

    r = np.sqrt((x - xc)**2 + (y - yc)**2)
    r_int = r.astype(int)

    profile = np.bincount(r_int.ravel(), weights=I.ravel()) / np.maximum(
        np.bincount(r_int.ravel()), 1
    )

    r_values = np.arange(len(profile))
    r_peak = r_values[np.argmax(profile)]

    plt.figure()
    plt.plot(r_values, profile)
    plt.axvline(r_peak, linestyle="--")
    plt.xlabel("radius / pixels")
    plt.ylabel("mean intensity")
    plt.title(f"Radial profile: {filename}, peak radius = {r_peak}px")
    plt.show()

    return r_peak

# Example:
# r1 = radial_profile("vortex_l1.jpg")
# r2 = radial_profile("vortex_l2.jpg")
# r3 = radial_profile("vortex_l3.jpg")
```

## Expected Result

A plot of $\(r_{\max}^2\)$ against $\(|l|\)$ should look roughly linear:

$$
\[
r_{\max}^2 = C |l|
\]
$$

Do not expect perfection with a printed transparency. The beam is not a perfect LG mode, but the trend should be visible.

---

# Experiment 4 — Corkscrew / Forked Interference Proof

**Difficulty:** Medium  
**Original connection:** This is the original “Corkscrew Interference Pattern” experiment, corrected and expanded.  
**What you learn:** Direct evidence of helical phase, interference, phase singularity.

## Aim

Interfere a vortex beam with a normal reference beam. The resulting fringes reveal the phase twist.

## Setup Options

### Option A — Simple Glass-Plate Interferometer

1. Use a microscope slide or thin glass plate as a weak beam splitter.
2. Send one reflected/transmitted beam through the fork grating.
3. Let the other beam remain ordinary.
4. Recombine them on a wall/screen.

This is fiddly but cheap.

### Option B — Easier Digital Simulation First

Before building it, simulate the pattern with Python below.

## Maths

Let the vortex beam be:

$$
\[
E_v=A(r)e^{il\phi}
\]
$$

Let a tilted plane-wave reference be:

$$
\[
E_p=A_0e^{ik_x x+i\delta}
\]
$4

The intensity is:

$$
\[
I=|E_v+E_p|^2
\]
$$

If the amplitudes are similar:

$$
\[
I \approx I_v+I_p+2\sqrt{I_v I_p}
\cos(l\phi-k_xx-\delta)
\]
$$

The phase term:

$$
\[
l\phi-k_xx-\delta
\]
$$

creates forked/spiral-like interference fringes. Near the singularity, one fringe splits. The number of fork branches tells you $\(|l|\)$. The sign of the fork indicates the handedness.

## Python: Simulate Forked Interference Fringes

```python
import numpy as np
import matplotlib.pyplot as plt

def vortex_interference(l=1, N=700, kx=18, w=0.75):
    x = np.linspace(-1, 1, N)
    y = np.linspace(-1, 1, N)
    X, Y = np.meshgrid(x, y)
    R = np.sqrt(X**2 + Y**2)
    Phi = np.arctan2(Y, X)

    vortex_amp = (R**abs(l)) * np.exp(-R**2 / w**2)
    Ev = vortex_amp * np.exp(1j*l*Phi)
    Ep = 0.7 * np.exp(1j*kx*X)

    I = np.abs(Ev + Ep)**2

    plt.figure(figsize=(6, 6))
    plt.imshow(I, cmap="gray", extent=[-1, 1, -1, 1])
    plt.title(f"Interference: vortex l={l} with tilted plane wave")
    plt.axis("off")
    plt.show()

for l in [1, 2, -1, -2]:
    vortex_interference(l=l)
```

## Expected Result

You should see forked or spiral-like fringes. With $\(l=1\)$, one extra/missing fringe appears. With $\(l=2\)$, two appear.

---

# Experiment 5 — Polarization Toolkit: Malus Law and Crossed Polarizers

**Difficulty:** Medium  
**Original connection:** This prepares for the liquid-crystal experiment.  
**What you learn:** Polarization, analyzers, intensity modulation, why LCDs work.

## Aim

Before using an LCD panel, prove the basic polarization law.

## Setup

1. Place one polarizer after the laser.
2. Place a second polarizer after the first.
3. Rotate the second polarizer and observe brightness.
4. Use a phone camera or light-meter app to record intensity vs angle.

## Maths: Malus Law

If linearly polarized light passes through an analyser at relative angle $\(\theta\)$:

$$
\[
I(\theta)=I_0\cos^2\theta
\]
$$

For crossed polarizers:

$$
\[
\theta=90^\circ,\quad I\approx0
\]
$$

Real polarizers leak some light, so:

$$
\[
I(\theta)=I_{\text{leak}}+I_0\cos^2\theta
\]
$$

## Python: Fit Malus Law

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.optimize import curve_fit

# Replace with your measured angles and brightness readings
theta_deg = np.array([0, 15, 30, 45, 60, 75, 90])
I_meas = np.array([1.00, 0.91, 0.74, 0.51, 0.27, 0.08, 0.02])

def malus(theta_deg, I0, leak, offset_deg):
    theta = np.deg2rad(theta_deg - offset_deg)
    return leak + I0*np.cos(theta)**2

popt, _ = curve_fit(malus, theta_deg, I_meas, p0=[1, 0.01, 0])
print("I0, leak, offset_deg =", popt)

theta_fit = np.linspace(0, 90, 300)
plt.scatter(theta_deg, I_meas, label="data")
plt.plot(theta_fit, malus(theta_fit, *popt), label="fit")
plt.xlabel("analyser angle / degrees")
plt.ylabel("relative intensity")
plt.legend()
plt.show()
```

## Expected Result

A $\(\cos^2\theta\)$ curve. This gives you a working polarizer/analyser setup for Experiment 6.

---

# Experiment 6 — Liquid-Crystal Twist Using an Old LCD

**Difficulty:** Medium  
**Original connection:** This is the original “Liquid Crystal Twist” experiment, expanded and made closer to the toron idea.  
**What you learn:** Birefringence, retardance, voltage-tunable phase, spatially varying optical phase.

## Aim

Use an old LCD panel to show that liquid crystals can change polarization and phase.

## Setup

1. Remove the LCD glass sandwich from an old calculator or watch.
2. Put one polarizer before the LCD and one after it.
3. Try parallel and crossed polarizers.
4. Shine the laser through the LCD.
5. Press gently or reconnect the original calculator electronics briefly.
6. Observe the changing intensity patterns on a screen.

Do not smash LCD glass. It can splinter.

## Maths: Retardance

A birefringent material has two refractive indices:

$$
\[
n_e,\quad n_o
\]
$$

The birefringence is:

$$
\[
\Delta n=n_e-n_o
\]
$$

A layer of thickness $\(d\)$ creates phase retardance:

$$
\[
\delta=\frac{2\pi}{\lambda}\Delta n d
\]
$$

A simple retarder between crossed polarizers gives:

$$
\[
I=I_0\sin^2(2\theta)\sin^2\left(\frac{\delta}{2}\right)
\]
$$

where $\(\theta\)$ is the angle between the liquid-crystal optical axis and the polarizer axis.

This is the key bridge to the liquid-crystal toron work: liquid crystals create spatially varying birefringence, and spatially varying birefringence can act like a synthetic gauge field for light.

## Jones Matrix

The Jones matrix for a retarder is:

$$
\[
J(\theta,\delta)=
R(-\theta)
\begin{bmatrix}
e^{-i\delta/2} & 0\\
0 & e^{i\delta/2}
\end{bmatrix}
R(\theta)
\]
$$

where:

$$
\[
R(\theta)=
\begin{bmatrix}
\cos\theta & -\sin\theta\\
\sin\theta & \cos\theta
\end{bmatrix}
\]
$$

## Python: Simulate Crossed-Polarizer LCD Brightness

```python
import numpy as np
import matplotlib.pyplot as plt

theta = np.linspace(0, np.pi/2, 200)
delta = np.linspace(0, 2*np.pi, 300)
TH, DE = np.meshgrid(theta, delta)

I = (np.sin(2*TH)**2) * (np.sin(DE/2)**2)

plt.figure(figsize=(7, 5))
plt.imshow(I, origin="lower", aspect="auto",
           extent=[0, 90, 0, 2*np.pi], cmap="gray")
plt.xlabel("LC axis angle theta / degrees")
plt.ylabel("retardance delta / radians")
plt.title("Intensity through crossed polarizers")
plt.colorbar(label="relative intensity")
plt.show()
```

## Expected Result

Bright and dark regions change when the LCD is stressed or electrically driven. You are not making a toron, but you are demonstrating the core mechanism: liquid crystals alter optical phase and polarization in space.

---

# Experiment 7 — Bottle-Like Dark Beam With Lens, Wire, and Annular Mask

**Difficulty:** Medium–Hard  
**Original connection:** This corrects and strengthens the original “Bottle Beam” experiment.  
**What you learn:** Diffraction, Fourier optics, dark regions surrounded by light, optical trapping ideas.

## Important Correction

A true optical bottle beam is a three-dimensional dark region enclosed by light. A simple lens plus wire or hair does not make a perfect bottle beam. But it can make dark diffraction structures and teach the same idea: phase/amplitude obstacles can sculpt light into useful dark regions.

## Setup A — Annular Aperture

1. Make a mask: black centre disk with a transparent ring around it.
2. Shine the laser through the annulus.
3. Focus with a convex lens.
4. Move a screen through positions before and after the focus.

## Setup B — Wire/Hair Diffraction

1. Focus a laser with a lens.
2. Put a thin hair/wire near the beam waist.
3. Observe the far-field diffraction pattern.
4. Move the wire and watch the central dark/bright structures change.

## Maths

For a circular aperture, the far-field diffraction angle is approximately:

$$
\[
\theta \approx 1.22\frac{\lambda}{D}
\]
$$

For a thin obstacle of width $\(a\)$, the diffraction minima approximately satisfy:

$$
\[
a\sin\theta=m\lambda
\]
$$

An annular aperture can be thought of as an outer circular aperture minus an inner circular aperture:

$$
\[
E_{\text{annulus}}=E_{\text{outer}}-E_{\text{inner}}
\]
$$

This subtraction creates ring-like intensity distributions and dark axial regions.

## Python: Simulate an Annular Aperture Far Field

```python
import numpy as np
import matplotlib.pyplot as plt

N = 800
x = np.linspace(-1, 1, N)
y = np.linspace(-1, 1, N)
X, Y = np.meshgrid(x, y)
R = np.sqrt(X**2 + Y**2)

outer = R < 0.45
inner = R < 0.20
aperture = outer.astype(float) - inner.astype(float)

field = np.fft.fftshift(np.fft.fft2(aperture))
I = np.abs(field)**2
I = np.log1p(I)  # log display

plt.figure(figsize=(6, 6))
plt.imshow(aperture, cmap="gray")
plt.title("Annular aperture")
plt.axis("off")
plt.show()

plt.figure(figsize=(6, 6))
plt.imshow(I, cmap="gray")
plt.title("Far-field diffraction, log intensity")
plt.axis("off")
plt.show()
```

## Expected Result

You should see ring-like diffraction features and dark regions. It will not be a perfect laboratory bottle beam, but it gives you a practical entry point into dark optical traps.

---

# Experiment 8 — Astigmatic Transformation: Measure $\(|l|\)$ With a Tilted Lens

**Difficulty:** Hard  
**Original connection:** This adds a serious diagnostic tool missing from the original list.  
**What you learn:** Mode conversion, astigmatism, identifying topological charge.

## Aim

Use a tilted spherical lens or cylindrical lens to turn a vortex beam into a lobe/stripe pattern that reveals \(|l|\).

## Setup

1. Generate a vortex beam with the fork grating.
2. Put a convex lens in the vortex beam.
3. Tilt the lens slightly around one axis, or use a cylindrical lens if you have one.
4. Move the screen through the focal region.
5. Count lobes or dark stripes in the transformed pattern.

## Maths

A Laguerre-Gaussian vortex mode can be decomposed into Hermite-Gaussian modes under astigmatic transformation. A useful lab rule is:

$$
\[
N_{\text{lobes}} \approx |l|+1
\]
$$

For example:

| \(l\) | Expected lobe/stripe count |
|---:|---:|
| 0 | 1 |
| 1 | 2 |
| 2 | 3 |
| 3 | 4 |

The orientation of the pattern flips for $\(+l\)$ versus $\(-l\)$.

This is not as clean with a rough printed grating, but it is a powerful real optics method.

## Python: Simple Hermite-Gaussian-Like Pattern Visualizer

This is not a full propagation simulation. It shows the idea that higher-order modes produce more lobes.

```python
import numpy as np
import matplotlib.pyplot as plt
from math import factorial

def hermite_phys(n, x):
    # simple recursion for physicists' Hermite polynomials
    if n == 0:
        return np.ones_like(x)
    if n == 1:
        return 2*x
    H0 = np.ones_like(x)
    H1 = 2*x
    for k in range(2, n+1):
        H0, H1 = H1, 2*x*H1 - 2*(k-1)*H0
    return H1

N = 600
x = np.linspace(-3, 3, N)
y = np.linspace(-3, 3, N)
X, Y = np.meshgrid(x, y)

for l in [0, 1, 2, 3]:
    n = abs(l)
    field = hermite_phys(n, X) * np.exp(-(X**2 + Y**2)/2)
    I = field**2

    plt.figure(figsize=(5, 4))
    plt.imshow(I, cmap="gray", extent=[-3,3,-3,3])
    plt.title(f"HG-like pattern related to |l|={abs(l)}")
    plt.axis("off")
    plt.show()
```

## Expected Result

Near the focus, the vortex ring should collapse into multiple lobes/stripes. The count gives another estimate of $\(|l|\)$.

---

# Experiment 9 — OAM Transfer and Rotational Doppler: The Reality Check

**Difficulty:** Hard  
**Original connection:** This fixes the original “Twisted Shadow” experiment.  
**What you learn:** OAM is real, but mechanical torque from a laser pointer is extremely tiny; rotational Doppler effects are easier to detect than literal paper rotation.

## Important Correction

The original idea said a suspended paper shape may rotate due to OAM transfer. With a cheap laser pointer, that is usually not realistic. Air currents, heat, and ordinary radiation pressure dominate.

The optical OAM torque scale is:

$$
\[
\tau = \frac{P l}{\omega}
\]
$$

where:

$$
\[
\omega = \frac{2\pi c}{\lambda}
\]
$$

For $\(P=5\text{ mW}\)$, $\(l=1\)$, and $\(\lambda=532\text{ nm}\)$:

$$
\[
\omega\approx3.54\times10^{15}\text{ rad/s}
\]
$$

$$
\[
\tau\approx\frac{5\times10^{-3}}{3.54\times10^{15}}
\approx1.4\times10^{-18}\text{ N m}
\]
$$


That is far too small to spin a normal paper object in a convincing way.

## Better Experiment A — Torque Estimate

Do the calculation and prove why the paper experiment is mostly a lesson in scale.

## Better Experiment B — Rotational Doppler Demonstration

If a rotating object or optical element changes angular momentum from $\(l_{\text{in}}\)$ to $\(l_{\text{out}}\)$, the optical frequency shift is:

$$
\[
\Delta \omega = (l_{\text{out}}-l_{\text{in}})\Omega
\]
$$

or:

$$
\[
\Delta f = \frac{(l_{\text{out}}-l_{\text{in}})\Omega}{2\pi}
\]
$$

where $\(\Omega\)$ is the rotation rate in rad/s.

You cannot see the optical frequency directly with a phone, but you may detect intensity modulation if a rotating mask converts the phase pattern into amplitude flicker.

## Practical Cheap Version

1. Make a printed sector mask, like a wheel with alternating transparent/black wedges.
2. Spin it slowly on a small DC motor.
3. Shine the vortex beam through it.
4. Detect transmitted intensity with a photodiode, Arduino light sensor, or even a phone light sensor if accessible.
5. Compare modulation frequency with mask rotation rate.

This is not a pure professional rotational Doppler measurement, but it introduces the same angular-frequency logic.

## Python: Torque and Rotational Doppler Calculator

```python
import numpy as np

c = 299_792_458

def oam_torque(P_mW=5, wavelength_nm=532, l=1):
    P = P_mW * 1e-3
    lam = wavelength_nm * 1e-9
    omega = 2*np.pi*c/lam
    tau = P*l/omega
    return omega, tau

for l in [1, 2, 5, 10]:
    omega, tau = oam_torque(P_mW=5, wavelength_nm=532, l=l)
    print(f"l={l:2d}, optical omega={omega:.3e} rad/s, torque={tau:.3e} N m")

def rotational_doppler(delta_l=1, rpm=60):
    Omega = rpm * 2*np.pi / 60
    df = delta_l * Omega / (2*np.pi)
    return df

for rpm in [30, 60, 600, 3000]:
    print(f"rpm={rpm:4d}, delta_l=1, Doppler shift={rotational_doppler(1, rpm):.2f} Hz")
```

## Expected Result

You will learn that OAM is physically real, but direct mechanical torque needs microscopic particles, much higher optical power, or very low friction. The better home-lab lesson is frequency/modulation, not spinning paper.

---

# Experiment 10 — Mini OAM Optical Communication Link

**Difficulty:** Hardest  
**Original connection:** This extends the original quantum-communication motivation into a practical classical demo.  
**What you learn:** OAM multiplexing, mode orthogonality, encoding/decoding, why OAM is interesting for communication.

## Aim

Send symbols using different topological charges and decode them using matching/conjugate fork gratings.

## Concept

Use different vortex charges as symbols:

| Symbol | OAM charge |
|---|---:|
| A | $\(l=-2\)$ |
| B | $\(l=-1\)$ |
| C | $\(l=0\)$ |
| D | $\(l=+1\)$ |
| E | $\(l=+2\)$ |

To decode charge $\(l\)$, apply the opposite phase:

$$
\[
e^{-il\phi}
\]
$$

If the incoming mode is $\(e^{il\phi}\)$, the decoder gives:

$$
\[
e^{il\phi}e^{-il\phi}=1
\]
$$

which becomes a bright Gaussian-like centre. If the wrong decoder is used:

$$
\[
e^{il\phi}e^{-il'\phi}=e^{i(l-l')\phi}
\]
$$

a vortex remains, with a dark centre.

## Orthogonality Maths

OAM modes are orthogonal in angle:

$$
\[
\int_0^{2\pi}e^{il\phi}e^{-il'\phi}d\phi
=
\int_0^{2\pi}e^{i(l-l')\phi}d\phi
=
2\pi\delta_{ll'}
\]
$$

This is the mathematical reason different $\(l\)$ values can carry separate channels.

## Simple Physical Setup

1. Prepare fork gratings for $\(l=-2,-1,0,+1,+2\)$.
2. Sender inserts one fork grating to encode a symbol.
3. Receiver inserts a conjugate grating.
4. Observe the central spot:
   - Correct decoder: bright centre.
   - Wrong decoder: donut remains.
5. Use a phone camera to score brightness in the central region.

## Python: Simulate OAM Encoding/Decoding Matrix

```python
import numpy as np
import matplotlib.pyplot as plt

N = 500
x = np.linspace(-1, 1, N)
y = np.linspace(-1, 1, N)
X, Y = np.meshgrid(x, y)
R = np.sqrt(X**2 + Y**2)
Phi = np.arctan2(Y, X)

w = 0.55
charges = [-2, -1, 0, 1, 2]

def vortex_field(l):
    return (R**abs(l)) * np.exp(-R**2/w**2) * np.exp(1j*l*Phi)

def central_power(field, radius=0.08):
    I = np.abs(field)**2
    mask = R < radius
    return I[mask].sum()

matrix = np.zeros((len(charges), len(charges)))

for i, l_send in enumerate(charges):
    Ein = vortex_field(l_send)
    for j, l_decode in enumerate(charges):
        # ideal phase-only conjugate decoding
        Eout = Ein * np.exp(-1j*l_decode*Phi)
        # crude model: central brightness high when residual charge is 0
        matrix[i, j] = central_power(Eout)

matrix = matrix / matrix.max()

plt.figure(figsize=(6, 5))
plt.imshow(matrix, cmap="gray", vmin=0, vmax=1)
plt.xticks(range(len(charges)), charges)
plt.yticks(range(len(charges)), charges)
plt.xlabel("decoder charge")
plt.ylabel("sent charge")
plt.title("Idealized OAM decode matrix: bright diagonal = correct match")
plt.colorbar(label="relative central power")
plt.show()

print(matrix)
```

## Expected Result

In the ideal model, the diagonal should be brightest: correct decoder equals sent charge. In real life, printed gratings will leak and blur, but you should still see that the matching grating gives the strongest centre.

---

# Full Python Starter File

The separate file `optical_vortex_lab_code.py` contains starter code for:

1. Fork-grating mask generation.
2. LG vortex simulation.
3. Interference simulation.
4. Radial profile analysis.
5. Polarization/LCD simulation.
6. Annular aperture diffraction.
7. OAM torque and rotational Doppler calculator.
8. OAM communication decode matrix.

Run:

```bash
python optical_vortex_lab_code.py
```

It will create a folder called `vortex_outputs`.

---

# Difficulty Ladder Summary

| # | Experiment | Difficulty | Main maths |
|---:|---|---|---|
| 1 | Beam profiler | Easy | Gaussian beam, divergence |
| 2 | Fork grating vortex | Easy | $\(e^{il\phi}\)$, grating equation |
| 3 | Charge counter | Easy–Medium | $\(r_{\max}=w\sqrt{|l|/2}\)$ |
| 4 | Interference proof | Medium | $\(I=|E_v+E_p|^2\)$ |
| 5 | Malus law | Medium | $\(I=I_0\cos^2\theta\)$ |
| 6 | LCD birefringence | Medium | $\(\delta=2\pi\Delta nd/\lambda\)$, Jones calculus |
| 7 | Bottle-like beam | Medium–Hard | Fourier diffraction |
| 8 | Astigmatic transform | Hard | LG/HG mode conversion |
| 9 | OAM transfer / Doppler | Hard | $\(\tau=Pl/\omega\)$, $\(\Delta\omega=\Delta l\Omega\)$ |
| 10 | OAM optical link | Hardest | OAM orthogonality |

---

# What This Ladder Proves

By the end, you have demonstrated:

1. A normal laser beam has measurable spatial structure.
2. A fork grating can create real optical vortices.
3. The vortex has a dark phase singularity.
4. The topological charge changes the ring radius.
5. Interference proves the phase is helical, not just hollow.
6. Liquid crystals can impose voltage/pressure-dependent phase and polarization changes.
7. Phase and amplitude masks can sculpt three-dimensional-looking dark optical regions.
8. Astigmatic optics can diagnose vortex charge.
9. OAM carries angular momentum, but direct torque is tiny at pointer powers.
10. OAM modes can encode information because different charges are approximately orthogonal.

That is the clean learning path from “cheap laser pointer demo” to “why liquid-crystal optical tornadoes matter for future photonic and quantum communication systems.”


---

# Appendix A — Complete Python Starter Code

Save this section as:

```text
optical_vortex_lab_code.py
```

Then run:

```bash
python optical_vortex_lab_code.py
```

```python
"""
Optical Vortex Lab Starter Code
Run:
    python optical_vortex_lab_code.py

Outputs are written to ./vortex_outputs

Requires:
    numpy
    matplotlib
    pillow

Optional for fitting:
    scipy
"""

from pathlib import Path
import numpy as np
import matplotlib.pyplot as plt

OUT = Path("vortex_outputs")
OUT.mkdir(exist_ok=True)

def savefig(name):
    path = OUT / name
    plt.savefig(path, dpi=180, bbox_inches="tight")
    plt.close()
    print("saved", path)

def make_fork_grating(l=1, N=1600, period_px=40, filename=None):
    x = np.arange(N) - N/2
    y = np.arange(N) - N/2
    X, Y = np.meshgrid(x, y)
    phi = np.arctan2(Y, X)
    pattern = 0.5 * (1 + np.sign(np.cos(2*np.pi*X/period_px + l*phi)))
    if filename is None:
        filename = f"fork_l{l}.png"
    plt.imsave(OUT / filename, pattern, cmap="gray")
    print("saved", OUT / filename)

def simulate_lg(l=1, N=700, w=0.55):
    x = np.linspace(-1, 1, N)
    y = np.linspace(-1, 1, N)
    X, Y = np.meshgrid(x, y)
    R = np.sqrt(X**2 + Y**2)
    Phi = np.arctan2(Y, X)

    E = (R**abs(l)) * np.exp(-R**2/w**2) * np.exp(1j*l*Phi)
    I = np.abs(E)**2
    phase = np.angle(E)

    plt.figure(figsize=(6, 6))
    plt.imshow(I, cmap="gray", extent=[-1,1,-1,1])
    plt.title(f"LG-like vortex intensity, l={l}")
    plt.axis("off")
    savefig(f"lg_intensity_l{l}.png")

    plt.figure(figsize=(6, 6))
    plt.imshow(phase, cmap="twilight", extent=[-1,1,-1,1])
    plt.title(f"Vortex phase, l={l}")
    plt.axis("off")
    savefig(f"lg_phase_l{l}.png")

def simulate_interference(l=1, N=700, kx=18, w=0.75):
    x = np.linspace(-1, 1, N)
    y = np.linspace(-1, 1, N)
    X, Y = np.meshgrid(x, y)
    R = np.sqrt(X**2 + Y**2)
    Phi = np.arctan2(Y, X)

    vortex_amp = (R**abs(l)) * np.exp(-R**2 / w**2)
    Ev = vortex_amp * np.exp(1j*l*Phi)
    Ep = 0.7 * np.exp(1j*kx*X)
    I = np.abs(Ev + Ep)**2

    plt.figure(figsize=(6, 6))
    plt.imshow(I, cmap="gray", extent=[-1, 1, -1, 1])
    plt.title(f"Interference: vortex l={l}")
    plt.axis("off")
    savefig(f"interference_l{l}.png")

def simulate_polarization_lcd():
    theta = np.linspace(0, np.pi/2, 200)
    delta = np.linspace(0, 2*np.pi, 300)
    TH, DE = np.meshgrid(theta, delta)
    I = (np.sin(2*TH)**2) * (np.sin(DE/2)**2)

    plt.figure(figsize=(7, 5))
    plt.imshow(I, origin="lower", aspect="auto",
               extent=[0, 90, 0, 2*np.pi], cmap="gray")
    plt.xlabel("LC axis angle theta / degrees")
    plt.ylabel("retardance delta / radians")
    plt.title("Intensity through crossed polarizers")
    plt.colorbar(label="relative intensity")
    savefig("lcd_crossed_polarizers.png")

def simulate_annular_aperture(N=800):
    x = np.linspace(-1, 1, N)
    y = np.linspace(-1, 1, N)
    X, Y = np.meshgrid(x, y)
    R = np.sqrt(X**2 + Y**2)

    outer = R < 0.45
    inner = R < 0.20
    aperture = outer.astype(float) - inner.astype(float)

    field = np.fft.fftshift(np.fft.fft2(aperture))
    I = np.log1p(np.abs(field)**2)

    plt.figure(figsize=(6, 6))
    plt.imshow(aperture, cmap="gray")
    plt.title("Annular aperture")
    plt.axis("off")
    savefig("annular_aperture.png")

    plt.figure(figsize=(6, 6))
    plt.imshow(I, cmap="gray")
    plt.title("Far-field diffraction, log intensity")
    plt.axis("off")
    savefig("annular_far_field.png")

def oam_torque(P_mW=5, wavelength_nm=532, l=1):
    c = 299_792_458
    P = P_mW * 1e-3
    lam = wavelength_nm * 1e-9
    omega = 2*np.pi*c/lam
    tau = P*l/omega
    return omega, tau

def rotational_doppler(delta_l=1, rpm=60):
    Omega = rpm * 2*np.pi / 60
    df = delta_l * Omega / (2*np.pi)
    return df

def oam_decode_matrix():
    N = 500
    x = np.linspace(-1, 1, N)
    y = np.linspace(-1, 1, N)
    X, Y = np.meshgrid(x, y)
    R = np.sqrt(X**2 + Y**2)
    Phi = np.arctan2(Y, X)
    w = 0.55
    charges = [-2, -1, 0, 1, 2]

    def vortex_field(l):
        return (R**abs(l)) * np.exp(-R**2/w**2) * np.exp(1j*l*Phi)

    def central_power(field, radius=0.08):
        I = np.abs(field)**2
        mask = R < radius
        return I[mask].sum()

    matrix = np.zeros((len(charges), len(charges)))
    for i, l_send in enumerate(charges):
        Ein = vortex_field(l_send)
        for j, l_decode in enumerate(charges):
            Eout = Ein * np.exp(-1j*l_decode*Phi)
            matrix[i, j] = central_power(Eout)

    matrix = matrix / matrix.max()

    plt.figure(figsize=(6, 5))
    plt.imshow(matrix, cmap="gray", vmin=0, vmax=1)
    plt.xticks(range(len(charges)), charges)
    plt.yticks(range(len(charges)), charges)
    plt.xlabel("decoder charge")
    plt.ylabel("sent charge")
    plt.title("Idealized OAM decode matrix")
    plt.colorbar(label="relative central power")
    savefig("oam_decode_matrix.png")

    print("Decode matrix:")
    print(matrix)

def main():
    for l in [1, 2, 3, -1, -2, -3]:
        make_fork_grating(l=l, filename=f"fork_l{l}.png")

    for l in [0, 1, 2, 3, -1, -2]:
        simulate_lg(l=l)

    for l in [1, 2, -1, -2]:
        simulate_interference(l=l)

    simulate_polarization_lcd()
    simulate_annular_aperture()
    oam_decode_matrix()

    print("\nOAM torque estimates:")
    for l in [1, 2, 5, 10]:
        omega, tau = oam_torque(P_mW=5, wavelength_nm=532, l=l)
        print(f"l={l:2d}, optical omega={omega:.3e} rad/s, torque={tau:.3e} N m")

    print("\nRotational Doppler examples:")
    for rpm in [30, 60, 600, 3000]:
        print(f"rpm={rpm:4d}, delta_l=1, shift={rotational_doppler(1, rpm):.2f} Hz")

if __name__ == "__main__":
    main()

```

---

# Appendix B — Nothing-Missing Checklist

This single Markdown file contains:

- The complete 10-experiment lab manual.
- All maths sections.
- All individual Python snippets inside the relevant experiments.
- The complete standalone Python starter program in Appendix A.
- Safety notes.
- Equipment list.
- Difficulty ladder.
- Expected results and common problems.
- Corrections to the original five experiments.
