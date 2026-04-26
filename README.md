# Quantum “Optical Tornadoes”: Liquid-Crystal Torons, Ground-State OAM Lasing, and a DIY Fork-Grating Demonstration

 
**Core claim:** the 2026 breakthrough is not merely “making twisted light.” Optical vortices have been known for decades. The new result is **ground-state orbital-angular-momentum (OAM) lasing from liquid-crystal torons embedded in an optical microcavity**.

---

## 1. Executive Summary

Scientists from the University of Warsaw, the Military University of Technology, and collaborators created tiny laser-like “optical tornadoes”: structured light fields whose phase twists around the beam axis. These are formally known as **optical vortices** or **OAM beams**.

The key achievement was that the vortex appeared in the **ground state** of a microcavity system. In many earlier systems, vortex/OAM modes occur only in higher-energy excited modes. Here, the liquid-crystal toron structure produced a synthetic gauge-field effect that changed the ordering of the photonic modes, allowing the lowest-energy lasing state to carry non-zero OAM.

That matters because the lowest-energy state is usually the easiest state for a laser to occupy. So the result points toward smaller, simpler, and more scalable structured-light sources for optical communication, quantum technologies, optical tweezers, and photonic devices. It does **not** mean that smartphone quantum communication hardware already exists; that is a future possibility, not a finished engineering product.

---

## 2. One-Paragraph Explanation

An **optical tornado** is a beam of light whose wavefront twists around the propagation axis. Mathematically, the key vortex factor is $e^{i\ell\phi}$, where $\ell$ is the topological charge and $\phi$ is the angle around the beam centre. This spiral phase makes the centre of the beam a **phase singularity**, so the intensity must fall to zero there, producing a dark “eye.” In the 2026 liquid-crystal work, tiny topological defects called **torons** acted as microscopic light traps inside an optical microcavity. Their spatially varying birefringence created a **synthetic magnetic/gauge-field effect** for photons. This made the microcavity’s ground state carry OAM, enabling coherent, directional vortex lasing from a self-organised soft-material structure.

---

## 3. Important Corrections to the Original Draft

| Original wording / risk | Corrected version |
|---|---|
| “Voltage pulses created the synthetic magnetic field.” | More accurate: **spatially variable birefringence** in the liquid-crystal toron acts like a synthetic magnetic/gauge field for photons. External voltage can tune the trap size and optical properties. |
| “This could revolutionize quantum communication.” | Better: it **could help enable** simpler/scalable photonic devices for optical communication and quantum technologies. The practical engineering path is still open. |
| “Sub-micron toron experiment.” | Safer: **microscale liquid-crystal microcavity experiment** unless exact dimensions are being quoted from the paper/figures. |
| “Fork grating replicates the 2026 breakthrough.” | No. A fork grating demonstrates the **same OAM/vortex physics**, but it does **not** reproduce ground-state lasing, toron trapping, microcavity physics, or the non-Abelian gauge-field mechanism. |
| “Plane wave becomes an optical vortex.” | More precise: the fork grating creates vortex beams mainly in selected **diffracted orders**. The zero order remains mostly non-vortex light. |
| $\arctan(y/x)$ for the vortex phase. | Use $\operatorname{atan2}(y,x)$ to preserve the correct quadrant and avoid a discontinuity error. |
| Interference equation called “the equation of a spiral.” | More precise: the interference condition gives **forked or spiral-like fringes** depending on geometry. The full equation contains $x=r\cos\phi$, so it is not simply $\phi=(kx+2\pi m)/\ell$. |

---

## 4. Key Terms

| Term | Meaning |
|---|---|
| **Optical vortex** | A light field with a phase singularity and a helical phase front. |
| **OAM** | Orbital angular momentum of light. For an ideal paraxial vortex mode, each photon carries $L_z=\ell\hbar$. |
| **Topological charge $\ell$** | Integer winding number of the optical phase around the beam centre. |
| **Phase singularity** | The centre of the vortex where the phase is undefined and the optical intensity goes to zero. |
| **Toron** | A stable, localised topological defect in a liquid-crystal texture; in this experiment it acts as a microscopic optical trap. |
| **Birefringence** | Direction-dependent refractive index. Liquid crystals commonly show birefringence because their molecules have preferred orientations. |
| **Synthetic magnetic/gauge field** | An effective field experienced by photons because of spatially varying optical properties. It is not a literal magnetic field acting on light in the ordinary Lorentz-force sense. |
| **Optical microcavity** | A mirror-based structure that confines light by repeated reflection, allowing strong interaction with the material inside. |
| **Ground state** | The lowest-energy optical mode of the system. Achieving OAM lasing here is the major breakthrough. |

---

## 5. What the 2026 Experiment Actually Did

### 5.1 The problem

Optical vortices are useful, but generating them compactly and efficiently is difficult. Common methods include:

- external spatial light modulators (SLMs),
- spiral phase plates,
- metasurfaces,
- etched nanostructures,
- special laser cavities,
- mode converters,
- fork gratings and holograms.

These can work very well in a laboratory, but many are bulky, lossy, difficult to fabricate, or hard to integrate into small devices.

### 5.2 The liquid-crystal solution

The team used a **liquid crystal**, a material that flows like a liquid but has internally ordered molecular alignment. In such a medium, special topological defects called **torons** can form.

A toron can be pictured as a tightly twisted liquid-crystal structure. The popular analogy is a twisted DNA-like spiral closed into a doughnut-like loop. This is only an analogy, but it captures the idea that the molecular orientation winds in space.

In the microcavity, the toron behaves as a **microscopic trap for light**. The light is confined vertically by the mirrors of the microcavity and laterally by the toron-induced optical potential.

### 5.3 The synthetic magnetic/gauge field

Light does not normally curve in a magnetic field the way an electron does, because photons are electrically neutral. But a structured optical medium can make photons behave **as if** they see a magnetic or gauge field.

In this case, the key ingredient is **spatially variable birefringence**. Because the refractive index depends on position and polarisation, the photon’s polarisation and motion become coupled. Mathematically, this can be described using an effective gauge field.

At a high level, one can write a photon-like effective Hamiltonian in the form

$$
\hat{H}_{\text{eff}} \sim \frac{1}{2m_{\text{ph}}}\left(-i\hbar\nabla - \mathbf{A}(\mathbf{r})\right)^2 + V(\mathbf{r}),
$$

where:

- $m_{\text{ph}}$ is an effective photon mass inside the microcavity description,
- $V(\mathbf{r})$ is the trapping potential,
- $\mathbf{A}(\mathbf{r})$ is an effective vector potential or gauge field,
- in the real liquid-crystal system this field is connected to the spatially varying optical anisotropy and polarisation structure.

The paper describes the effect more specifically as a **real-space non-Abelian gauge field**. “Non-Abelian” means the effective gauge-field components act on internal degrees of freedom such as polarisation and do not generally commute like ordinary scalar phases.

### 5.4 Why the ground state matters

In many older vortex systems, the lowest-energy mode has no OAM, while OAM modes appear as higher-energy excited states. That is awkward for lasers because a laser naturally tends to lase in the mode with the best gain/loss balance, often the lowest-loss and lowest-energy accessible mode.

The 2026 result shows a **topological inversion of ground and excited states**: the toron-induced gauge field changes the mode ordering so that the ground state itself carries OAM.

That means the system can lase directly into a vortex state rather than needing to force light into a higher-energy vortex mode.

### 5.5 How lasing was confirmed

The researchers added a laser dye to the liquid-crystal/microcavity system. When pumped, the system emitted light that was:

- coherent,
- narrow in energy compared with ordinary fluorescence,
- directionally emitted,
- structured as a vortex,
- carrying non-zero OAM in the circular-polarisation components.

That is why it is fair to call it a **laser tornado** or **ground-state OAM laser**, not just passive beam shaping.

---

## 6. Why This Matters for Quantum and Optical Communication

### 6.1 Information density

Ordinary polarisation encoding often uses two basis states, for example horizontal/vertical or left/right circular polarisation. That gives a natural two-state qubit basis.

OAM can provide many possible integer states:

$$
\ell = 0, \pm 1, \pm 2, \pm 3, \ldots
$$

That means OAM can support **high-dimensional encoding**. In quantum information language, this can create **qudits** rather than only qubits. A qudit with dimension $d$ can carry

$$
\log_2(d)
$$

bits of classical information per ideal symbol, or a $d$-dimensional quantum state per photon.

### 6.2 Multiplexing

In classical optical communication, different OAM modes can in principle be used as different spatial channels, a method called **mode-division multiplexing**. Multiple data streams can be sent using different spatial modes of the same wavelength, though practical mode purity and mode mixing are major engineering challenges.

### 6.3 Quantum communication

For quantum communication, OAM states can be used for:

- high-dimensional quantum key distribution,
- entanglement in spatial modes,
- quantum state encoding beyond two-level polarisation states,
- tests of high-dimensional quantum mechanics.

### 6.4 Realistic caveats

This technology is promising, but it does not magically solve every communication problem. Important challenges remain:

- OAM modes can mix in ordinary fibres unless special fibres or careful mode control are used.
- Free-space OAM links are sensitive to turbulence, misalignment, scattering, and aperture size.
- Quantum OAM systems require excellent state preparation, transmission, and measurement fidelity.
- A working chip-scale OAM laser is only one component in a full quantum communication system.
- Smartphone integration is speculative and long-term, not something implied by the 2026 experiment alone.

---

## 7. The Quark / Vectorial-Charge Connection

The public explanation mentions that the theory is inspired by **vectorial charge** ideas, making photons behave “not even like electrons, but like quarks” in the mathematical analogy.

This should not be misunderstood. It does **not** mean the photons literally become quarks. It means the effective equations governing the polarised light in the structured microcavity resemble equations from gauge-field physics where internal degrees of freedom are coupled in a more complex, vector-like way.

The safe explanation is:

> The toron microcavity creates an effective gauge-field environment for photons. Because the field acts on polarisation/internal structure rather than merely adding a simple scalar phase, the mathematics has a non-Abelian flavour, which is why the researchers used analogies to advanced particle-physics concepts.

---

## 8. The DIY Demonstration: Fork-Grating Optical Vortex Generator

The DIY experiment is valuable, but it demonstrates **passive OAM beam shaping**, not the full toron microcavity breakthrough.

### 8.1 Goal

Generate an optical vortex using a printed or digitally displayed **fork grating**. The side diffraction orders should show a doughnut-like beam with a dark centre.

### 8.2 What it proves

It can show:

- helical phase,
- topological charge,
- a phase singularity,
- a dark vortex core,
- OAM-like beam structure,
- forked or spiral interference fringes if a reference beam is added.

### 8.3 What it does not prove

It does not show:

- liquid-crystal torons,
- synthetic gauge fields from birefringence,
- non-Abelian gauge physics,
- microcavity confinement,
- ground-state OAM lasing,
- electrically tunable toron trap size,
- quantum communication by itself.

---

## 9. Laser Safety

Use low-power visible lasers only, ideally Class 2 or low-power Class 3R depending on local rules. Never look into the beam. Never point it at people, animals, vehicles, aircraft, windows, mirrors, jewellery, tools, chrome parts, or glossy surfaces.

For an interference version using mirrors or beam splitters, the hazard increases because stray reflections can travel sideways at eye height. Keep the beam below seated eye level, terminate every beam with a matte beam stop, and wear appropriate laser safety glasses if power levels justify it.

---

## 10. Materials for the Fork-Grating Demonstration

Basic version:

- low-power red or green laser pointer,
- printed fork grating on transparency film,
- white wall or screen,
- clamp, tripod, Blu Tack, or optical mount,
- ruler or tape measure,
- darkened room.

Better version:

- expanded/collimated laser beam,
- high-resolution printed transparency or photographic film mask,
- iris or aperture to select one diffraction order,
- lens for beam expansion or Fourier-plane observation,
- camera or phone camera with manual exposure,
- optional polariser.

Advanced version:

- spatial light modulator (SLM),
- beam splitter,
- mirrors,
- reference Gaussian beam,
- optical table or stable breadboard.

---

## 11. How to Make the Fork Grating

A fork grating is a diffraction grating with a phase dislocation. Visually, one grating line splits like a fork.

### 11.1 Printed version

1. Generate or download a fork-grating pattern.
2. Print it at the highest possible resolution on transparency film.
3. If the pattern is too coarse, shrink it by printing smaller or using a high-resolution photocopier.
4. A pattern around $2\,\text{cm}\times2\,\text{cm}$ can work for a simple demonstration, but the useful scale depends strongly on printer resolution and laser beam diameter.
5. Shine the laser through the central dislocation.
6. Project the diffraction pattern onto a screen 2–3 metres away.
7. Observe the first diffraction orders to the left and right of the central beam.

### 11.2 What you should see

You should see:

- a bright central zero-order spot,
- side diffraction orders,
- one or more side spots with a dark central hole,
- opposite handedness in opposite diffraction orders.

The dark hole is the vortex core. The phase is undefined at the centre, so the intensity must vanish there.

### 11.3 Why smaller grating spacing helps

The diffraction angle approximately follows

$$
\sin\theta_m \approx \frac{m\lambda}{d},
$$

where:

- $m$ is the diffraction order,
- $\lambda$ is the laser wavelength,
- $d$ is the grating period.

Smaller $d$ gives larger separation between diffraction orders. But if the grating is too fine for the printer, the pattern will blur and performance will get worse.

---

## 12. Mathematical Core of an Optical Vortex

### 12.1 Coordinates

Use cylindrical coordinates around the beam axis:

$$
(x,y,z) \rightarrow (r,\phi,z),
$$

where

$$
r=\sqrt{x^2+y^2},
$$

and

$$
\phi = \operatorname{atan2}(y,x).
$$

The use of $\operatorname{atan2}(y,x)$ matters because it gives the correct angle in all four quadrants. A plain $\arctan(y/x)$ loses quadrant information.

---

### 12.2 Fundamental vortex phase

The essential vortex factor is

$$
\boxed{e^{i\ell\phi}}
$$

where $\ell$ is the integer topological charge.

The phase contribution is

$$
\Phi_{\text{vortex}}(r,\phi,z)=\ell\phi.
$$

Going once around the beam centre gives

$$
\Delta\Phi = \Phi(\phi+2\pi)-\Phi(\phi)=2\pi\ell.
$$

For examples:

| $\ell$ | Meaning |
|---:|---|
| $0$ | no vortex phase |
| $+1$ | one positive phase winding |
| $-1$ | one negative phase winding, opposite handedness |
| $+2$ | two positive phase windings |
| $-2$ | two negative phase windings |

The integer condition exists because the optical field must be single-valued after one full turn:

$$
e^{i\ell(\phi+2\pi)}=e^{i\ell\phi}
$$

only when $\ell$ is an integer.

---

### 12.3 Why the centre is dark

At $r=0$, the angle $\phi$ is undefined. If the field contains $e^{i\ell\phi}$ and $\ell\neq0$, the phase depends on direction as you approach the centre.

For the optical field to remain physically consistent, the amplitude must vanish at the centre:

$$
A(0,z)=0.
$$

Therefore

$$
I(0,z)=|\psi(0,\phi,z)|^2=0.
$$

This is the dark “eye” of the optical tornado.

---

## 13. Laguerre-Gaussian Vortex Modes

A common mathematical model for vortex beams is the Laguerre-Gaussian mode $LG_p^{\ell}$.

With the time factor $e^{-i\omega t}$ omitted, one common convention is

$$
\boxed{
\begin{aligned}
u_p^{\ell}(r,\phi,z) &=
\sqrt{\frac{2p!}{\pi(p+|\ell|)!}}\,
\frac{1}{w(z)}
\left(\frac{\sqrt{2}r}{w(z)}\right)^{|\ell|}
L_p^{|\ell|}\!\left(\frac{2r^2}{w^2(z)}\right)
\exp\!\left(-\frac{r^2}{w^2(z)}\right) \\
&\quad \times
\exp(i\ell\phi)
\exp(ikz)
\exp\!\left(-i\frac{kr^2}{2R(z)}\right)
\exp\!\left[-i(2p+|\ell|+1)\zeta(z)\right].
\end{aligned}
}
$$

where

$$
k=\frac{2\pi}{\lambda},
$$

$$
z_R=\frac{\pi w_0^2}{\lambda},
$$

$$
w(z)=w_0\sqrt{1+\left(\frac{z}{z_R}\right)^2},
$$

$$
R(z)=z\left[1+\left(\frac{z_R}{z}\right)^2\right],
$$

and

$$
\zeta(z)=\arctan\left(\frac{z}{z_R}\right).
$$

Different optics books use different sign conventions for the phase factors depending on whether they choose $e^{i(kz-\omega t)}$ or $e^{-i(kz-\omega t)}$. The physical vortex content is unchanged.

### Symbol table

| Symbol | Meaning |
|---|---|
| $p$ | radial index, a non-negative integer |
| $\ell$ | topological charge / azimuthal index |
| $w_0$ | beam waist at focus |
| $w(z)$ | beam radius at axial position $z$ |
| $z_R$ | Rayleigh range |
| $R(z)$ | wavefront radius of curvature |
| $\zeta(z)$ | Gouy phase |
| $L_p^{|\ell|}(x)$ | associated Laguerre polynomial |
| $k$ | wave number |

---

## 14. Radial Intensity and Dark-Core Size

For the simplest vortex case $p=0$, the field magnitude near the centre behaves like

$$
|u_0^{\ell}| \propto r^{|\ell|}.
$$

So the intensity behaves as

$$
I(r)\propto r^{2|\ell|}\exp\left(-\frac{2r^2}{w^2}\right).
$$

That gives:

| $\ell$ | Near-centre intensity scaling | Visual effect |
|---:|---|---|
| $1$ | $I\propto r^2$ | small dark core |
| $2$ | $I\propto r^4$ | wider dark core |
| $3$ | $I\propto r^6$ | wider again |

For $p=0$, the radius of maximum intensity is approximately

$$
\boxed{r_{\max}=w\sqrt{\frac{|\ell|}{2}}.}
$$

This is why a higher-charge fork grating usually produces a larger doughnut hole.

---

## 15. OAM Per Photon

For an ideal paraxial Laguerre-Gaussian mode, each photon carries orbital angular momentum

$$
\boxed{L_z=\ell\hbar.}
$$

This is separate from spin angular momentum associated with polarisation. For circular polarisation, spin angular momentum is often written as

$$
S_z=\sigma\hbar,
$$

where

$$
\sigma=+1 \quad \text{or} \quad -1
$$

for right- or left-circular polarisation, depending on sign convention.

For a simple separable paraxial mode, the total angular momentum per photon along the propagation axis can be written schematically as

$$
J_z=(\ell+\sigma)\hbar.
$$

In complex structured media, especially with spin-orbit coupling or non-Abelian gauge effects, spin and orbital components can mix, so this simple split must be used carefully.

---

## 16. Fork Grating Mathematics

### 16.1 Continuous vortex phase mask

The ideal spiral phase mask is

$$
\Phi_{\text{vortex}}(x,y)=\ell\operatorname{atan2}(y,x).
$$

Its transmission is

$$
T_{\text{phase}}(x,y)=\exp\left[i\ell\operatorname{atan2}(y,x)\right].
$$

A plane wave passing through that ideal phase mask acquires the vortex phase.

### 16.2 Blazed fork hologram

A practical computer-generated hologram combines a linear grating with the vortex phase:

$$
\Phi_{\text{holo}}(x,y)=\frac{2\pi x}{d}+\ell\operatorname{atan2}(y,x).
$$

A phase-only version can be written as

$$
T_{\text{holo}}(x,y)=\exp\left[i\left(\frac{2\pi x}{d}+\ell\operatorname{atan2}(y,x)\right)\right].
$$

This sends the desired vortex mostly into one first diffraction order.

### 16.3 Binary printed fork grating

For a printed transparency, a binary amplitude grating is more realistic:

$$
T_{\text{binary}}(x,y)=\frac{1}{2}\left[1+\operatorname{sgn}\left(\cos\left(\frac{2\pi x}{d}+\ell\operatorname{atan2}(y,x)\right)\right)\right].
$$

Because this is a binary amplitude mask, the output is split into multiple diffraction orders. The useful vortex is normally observed in a side order, not in the central zero order.

General rule:

- zero order: mostly non-vortex light,
- $+1$ order: usually carries approximately $+\ell$,
- $-1$ order: usually carries approximately $-\ell$,
- higher orders can carry higher multiples depending on the grating/hologram structure.

---

## 17. Interference Proof of the Phase Twist

A dark doughnut beam strongly suggests a vortex, but the clean proof is interference with a reference beam.

Let the vortex field be

$$
E_v=A(r)e^{i\ell\phi},
$$

and let a tilted plane-wave reference be

$$
E_r=B e^{i(k_x x+\delta)}.
$$

The measured intensity is

$$
\begin{aligned}
I &= |E_v+E_r|^2 \\
&= A^2(r)+B^2+2A(r)B\cos\left(\ell\phi-k_xx-\delta\right).
\end{aligned}
$$

Since

$$
x=r\cos\phi,
$$

the bright-fringe condition is

$$
\ell\phi-k_xr\cos\phi-\delta=2\pi m,
$$

where $m$ is an integer.

This creates forked or spiral-like interference fringes. The number and orientation of the forks reveal the sign and magnitude of $\ell$.

---

## 18. Comparison: 2026 Toron Microcavity vs DIY Fork Grating

| Feature | 2026 liquid-crystal toron microcavity | DIY fork grating |
|---|---|---|
| Main purpose | Generate ground-state OAM lasing | Demonstrate OAM beam shaping |
| Method | Torons + microcavity + synthetic gauge field | Diffraction through a fork hologram |
| Material | Liquid crystal with topological defects | Printed transparency, film mask, or SLM |
| Active or passive? | Active laser emission with gain medium | Passive reshaping of an existing laser beam |
| Ground-state OAM? | Yes | No |
| Coherent lasing? | Yes, with dye and pumping | No, unless the input laser is already coherent; the grating itself does not lase |
| Tunability | Electrical tuning of trap/properties reported | Fixed if printed; tunable if using SLM |
| Scale | Microcavity / microscale photonic structure | Macroscopic classroom/bench setup |
| Quantum-tech relevance | Possible future integrated OAM source | Educational demonstration only |
| Difficulty | Specialist photonics lab | Home/university demonstration, with laser safety |

---

## 19. Suggested Experimental Procedure

### 19.1 Simple demonstration

1. Mount a low-power laser so it cannot roll or move.
2. Put the fork grating in the beam.
3. Align the beam through the dislocation point of the fork.
4. Place a screen 2–3 metres away.
5. Identify the zero order and side diffraction orders.
6. Look for a side order with a dark centre.
7. Photograph the pattern with fixed exposure.

### 19.2 Higher-charge comparison

Repeat with fork gratings designed for:

$$
\ell=1,2,3.
$$

Expected result:

- higher $|\ell|$ gives a larger dark core,
- opposite signs give opposite handedness,
- the side diffraction orders should have opposite handedness.

### 19.3 Interference version

1. Split the laser into two paths.
2. Send one path through the fork grating.
3. Keep the other path as a clean reference beam.
4. Recombine them at a small angle.
5. Observe forked or spiral-like interference fringes.

This is stronger evidence of true phase winding than just seeing a doughnut-shaped intensity pattern.

---

## 20. SLM / Liquid-Crystal Upgrade

A spatial light modulator is effectively a programmable liquid-crystal phase screen. It can display the fork hologram digitally instead of using a printed transparency.

Benefits:

- change $\ell$ instantly,
- switch between $+\ell$ and $-\ell$,
- display blazed holograms for cleaner first-order output,
- animate phase patterns,
- test mode purity,
- perform more advanced OAM experiments.

This still does **not** reproduce the 2026 toron microcavity result, but it is a powerful bridge between the DIY demonstration and serious structured-light optics.

---

## 21. What Would Be Needed to Approach the Real 2026 Experiment?

A true reproduction would require specialist equipment, likely including:

- liquid-crystal cell fabrication,
- chiral nematic liquid-crystal materials,
- controlled toron formation,
- optical microcavity mirrors / distributed Bragg reflectors,
- laser dye or gain medium,
- optical pump laser,
- microscope objective and imaging optics,
- spectrometer,
- polarisation-resolved imaging,
- momentum-space imaging,
- voltage control electrodes,
- clean sample preparation.

So the realistic path is:

1. **Start with fork gratings** to understand OAM.
2. **Move to SLM holograms** to control phase digitally.
3. **Study liquid-crystal q-plates** for electrically tunable spin-to-OAM conversion.
4. **Study microcavities and dye lasers**.
5. **Only then attempt toron microcavity devices**.

---

## 22. Practical Takeaway

The 2026 breakthrough shows a new way to get structured vortex laser light from self-organised liquid-crystal defects inside a microcavity. The important part is the **ground-state OAM lasing**, not simply the existence of a vortex beam.

The fork-grating experiment remains excellent because it teaches the same visible signature of OAM:

- spiral phase,
- phase singularity,
- dark centre,
- topological charge,
- interference proof.

The two are related like this:

> The fork grating is the classroom doorway into OAM physics. The liquid-crystal toron microcavity is a research-level route toward compact, self-organised OAM lasers.

---

## 23. Quick Formula Summary

| Concept | Formula | Meaning |
|---|---|---|
| Vortex phase | $e^{i\ell\phi}$ | phase winds around beam axis |
| Phase winding | $\Delta\Phi=2\pi\ell$ | phase change after one full loop |
| Centre intensity | $I(0)=0$ for $\ell\neq0$ | dark vortex core |
| OAM per photon | $L_z=\ell\hbar$ | quantised orbital angular momentum |
| Beam radius | $w(z)=w_0\sqrt{1+(z/z_R)^2}$ | Gaussian beam spreading |
| Rayleigh range | $z_R=\pi w_0^2/\lambda$ | diffraction length scale |
| Simple vortex intensity | $I\propto r^{2|\ell|}e^{-2r^2/w^2}$ | doughnut profile |
| Peak radius for $p=0$ | $r_{\max}=w\sqrt{|\ell|/2}$ | dark core grows with $|\ell|$ |
| Ideal spiral phase mask | $T=e^{i\ell\operatorname{atan2}(y,x)}$ | directly imposes vortex phase |
| Fork hologram phase | $\Phi=2\pi x/d+\ell\operatorname{atan2}(y,x)$ | separates vortex into diffraction order |
| Interference intensity | $I=A^2+B^2+2AB\cos(\ell\phi-k_xx-\delta)$ | forked/spiral-like fringes |

---

## 24. Source Notes

The central source-checked facts are:

- The paper is **Marcin Muszyński et al., “Ground-state orbital angular momentum lasing from liquid crystal torons embedded in a microcavity,” Science Advances 12, eaeb6167 (2026), DOI: 10.1126/sciadv.aeb6167**.
- The public university/press summaries describe torons as liquid-crystal defects that act as microscopic light traps.
- The synthetic magnetic-field analogy is attributed to spatially variable birefringence, not ordinary magnetism.
- The toron was placed in an optical microcavity to strengthen confinement.
- The ground-state OAM result is the major breakthrough.
- Laser dye was used to confirm coherent lasing behaviour.
- Future applications are phrased as possible routes to optical communication and quantum technologies, not as finished commercial devices.

---

## 25. References and Further Reading

1. Marcin Muszyński et al., **“Ground-state orbital angular momentum lasing from liquid crystal torons embedded in a microcavity,”** *Science Advances* 12, eaeb6167 (2026). DOI: `10.1126/sciadv.aeb6167`  
   https://www.science.org/doi/10.1126/sciadv.aeb6167

2. University of Warsaw / Phys.org, **“Physicists create laser tornado in miniature structures using synthetic magnetic field,”** 27 March 2026.  
   https://phys.org/news/2026-03-physicists-laser-tornado-miniature-synthetic.html

3. ScienceDaily, **“New ‘optical tornado’ technology could transform quantum communication,”** 25 April 2026.  
   https://www.sciencedaily.com/releases/2026/04/260424233215.htm

4. University of Warsaw research dataset for the Science Advances paper, **“Ground-state orbital angular momentum lasing from liquid crystal torons embedded in a microcavity.”**  
   https://doi.org/10.58132/RN5SGP

5. L. Allen, M. W. Beijersbergen, R. J. C. Spreeuw, and J. P. Woerdman, **“Orbital angular momentum of light and the transformation of Laguerre-Gaussian laser modes,”** *Physical Review A* 45, 8185 (1992).  
   DOI: `10.1103/PhysRevA.45.8185`

6. M. W. Beijersbergen et al., **“Helical-wavefront laser beams produced with a spiral phaseplate,”** *Optics Communications* 112, 321–327 (1994).  
   DOI: `10.1016/0030-4018(94)90638-6`

7. E. Nagali et al., **“Quantum information transfer from spin to orbital angular momentum of photons,”** *Physical Review Letters* 103, 013601 (2009).  
   DOI: `10.1103/PhysRevLett.103.013601`

8. B. Piccirillo, V. D’Ambrosio, S. Slussarenko, L. Marrucci, and E. Santamato, **“Photon spin-to-orbital angular momentum conversion via an electrically tunable q-plate,”** arXiv:1010.4473.  
   https://arxiv.org/abs/1010.4473

---

## 26. Final Bottom Line

The corrected technical statement is:

> Liquid-crystal torons embedded in an optical microcavity can generate a synthetic non-Abelian gauge-field effect for photons. This changes the microcavity mode structure so that the ground state carries orbital angular momentum. With gain from laser dye, the system can lase coherently in a vortex state. A fork grating can demonstrate the same visible OAM phase-singularity physics, but it is only a passive educational analogue, not a reproduction of the ground-state toron-microcavity laser.

# errata
Done — I rebuilt the README into a clean, stronger technical document, keeping the original information but correcting the weak/incorrect parts. I checked it against the uploaded draft and current source material: the actual result is ground-state orbital-angular-momentum lasing from liquid-crystal torons in a microcavity, not just a generic “optical tornado” demo; the synthetic magnetic-field effect comes from spatially variable birefringence, with voltage used for tuning the trap/properties; and the paper is listed as Science Advances 12, eaeb6167, DOI 10.1126/sciadv.aeb6167.

I also added the missing/cleaned maths: full Laguerre-Gaussian mode form, Rayleigh range, Gouy phase, radius of maximum intensity, correct atan2(y,x) vortex phase, fork-grating diffraction-order caveats, and the proper interference-fringe equation.

///


