# Virtual Lab: The Jump Phenomenon

_Version 1.0_

An interactive browser lab demonstrating the jump phenomenon in a hardening Duffing oscillator
(the midpoint of a clamped–clamped beam undergoing large deflections).


## Running it

Open `index.html` in any modern browser (Chrome, Edge, Firefox, Safari): double-click it, or host it on any
static web server / VLE. It is a single self-contained file with no dependencies and no network access.

## Model

$$
m\ddot{y} + c\dot{y} + ky + k_3 y^3 = x(t), \qquad x(t) = X \sin(2\pi f t)
$$

Notation follows the course: $x(t)$ is the input (excitation force, amplitude $X$ in N), $y(t)$ is the output
(midpoint displacement, amplitude $Y$), and the gain is $Y/X$ (plotted in mm/N).

| Parameter | Value |
|---|---|
| $m$ | 1 kg |
| $c$ | 20 N·s/m |
| $k$ | $1 \times 10^{4}$ N/m |
| $k_3$ | $5 \times 10^{9}$ N/m³ |

The underlying linear system has natural frequency and damping ratio

$$
f_n = \frac{1}{2\pi}\sqrt{\frac{k}{m}} \approx 15.9\ \text{Hz}, \qquad \zeta = \frac{c}{2\sqrt{km}} = 0.1 .
$$

The equation is integrated with fixed-step RK4 ($\Delta t = 2 \times 10^{-5}$ s). The state is never reset when
the frequency or amplitude changes, so the response depends on its history.


## Controls

- **Defaults on opening**: $f = 10$ Hz, $X = 1$ N, animation 20× slower than real time, sweep 1–60 Hz.
- **Excitation frequency / amplitude**: sliders or number boxes. ◀ ▶ (or the ← / → keys) step the frequency by
  $\Delta f$. Stepping slowly upward and then back down by hand reproduces the jumps.
- **Time-slowing factor**: slows the animation only (1×–200×, default 20×).
- **Stepped sine sweep**: at each frequency step the sweep waits for steady state, where the per-cycle peak
  amplitude is constant to within 0.5% over 5 cycles. If that takes more than 2 s of simulated time, it moves on
  anyway. It records the gain and then steps on. Sweep speed is independent of the animation slow-down
  (default 1× real time ≈ 65 s per sweep).
- **Slow-motion animation during sweep** (ticked by default): the sweep still runs at the chosen speed, but
  the beam animation and time history replay the most recently measured steady-state cycle at the
  slow-motion rate. Consecutive cycles are crossfaded over a quarter of a cycle. Steady state is periodic, so
  the replay is exactly what was measured, and the jumps still appear as a sudden change in amplitude. Untick
  it to see the live simulation at sweep speed instead.
- **Record gain**: while on, the steady-state gain $Y/X$ at the current $(f, X)$ is stored. Points are coloured
  by $X$ and shaped by how they were recorded (▲ sweep up, ▼ sweep down, ● manual). **Clear measurements**
  empties the plot. **Export CSV** downloads the points.
- **Linear FRF / Theory (HB)**: optional overlays. They show the linear system's response and the
  single-harmonic harmonic-balance solution at the current $X$, with the unstable branch dashed. Both are off by
  default.

## Suggested exercise

1. Run an increasing sine sweep from 1 Hz to 60 Hz with $X = 0.5$ N.
2. Run a decreasing sine sweep with the same parameters.
3. Compare results with the linear FRF. What do you notice? 
4. Repeat sine sweeps but set $X = 5$ N. Pay attention to any differences in the increasing and decreasing sweeps!
5. Investigate using the sliders: Can you find any evidence of additional harmonics? Do these appear in the harmonic balance approximation?

Think about:
- Why does the jump phenomenon occur?
- If the Duffing oscillator was asymmetric (i.e. includes a $k_2x^2$ stiffness term) which harmonics might we see?

## Spoilers: System behaviour (1–60 Hz sweeps, $\Delta f = 0.5$ Hz)

| $X$ (N) | Bistable region (HB theory) | Sweep up jumps down at | Sweep down jumps up at | Behaviour |
|---|---|---|---|---|
| 1 | none | — | — | essentially linear, single-valued |
| 3 | 19.6–19.9 Hz | ≈ 20 Hz | ≈ 20 Hz | onset of nonlinearity, narrow bistable region |
| 10 | 24.2–30.2 Hz | ≈ 31 Hz | ≈ 24 Hz | clear bistable region: up and down sweeps differ |
| 30 | 31.0–49.6 Hz | ≈ 50 Hz | ≈ 31 Hz | strong nonlinearity, wide bistable region |

## Contact

Dr Aidan Hughes\
Dynamics Research Group\
School of Mechanical, Aerospace, and Civil Engineering\
University of Sheffield

Email: [aidan.j.hughes@sheffield.ac.uk](mailto:aidan.j.hughes@sheffield.ac.uk)

## Licence

Copyright © 2026 Aidan Hughes. Released under the [MIT License](LICENSE): you are free to use, copy, modify and
share this tool, provided the copyright and licence notice is kept with it.
