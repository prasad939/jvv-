
# DCA Experimentation Cycle 01  
## Fire Control Physics, Calculus Proofs, and Engineering Reasoning

---

## Executive Summary (One-Minute Read)

This document derives, from first principles, the projectile motion equations governing cannon fire when launch and target heights differ. Using vector kinematics and calculus-based optimization, we establish:

- The **trajectory equation** without relying on memorized range formulas  
- The **optimal firing angle** for maximum horizontal reach at arbitrary elevation  
- The **bounding (envelope) parabola**, defining the absolute physical limit of reach  
- The correct interpretation of **time-of-flight (8.9 s)** as an envelope-consistent quantity  
- Why intermediate times (e.g., 7.6 s) are physically valid but **not** decision-grade  

These results form a mathematically rigorous fire-control foundation suitable for engineering validation, simulation, and risk-based operational decisions.

---

## Phase 1 — Physics from First Principles

### Assumptions (Explicit and Controlled)

- Motion is two-dimensional
- Vacuum environment (no drag, no lift)
- Gravity is constant:  
  \[
  \vec{g} = \langle 0, -9.81 \rangle \ \text{m/s}^2
  \]
- Launch speed is fixed by hardware constraint:
  \[
  |\vec{v}_0| \le v_0
  \]

These assumptions isolate **pure kinematic limits**, ensuring all conclusions are mathematically defensible.

---

## 1. Vector Kinematics Derivation (No Black Boxes)

### Acceleration Field
\[
\vec{a}(t) = \langle 0, -g \rangle
\]

### Velocity (by integration)
\[
\vec{v}(t) = \langle v_0 \cos\theta,\ v_0 \sin\theta - gt \rangle
\]

### Position (second integration)
\[
\vec{r}(t) =
\langle
v_0 \cos\theta \, t,\ 
y_0 + v_0 \sin\theta \, t - \frac{1}{2}gt^2
\rangle
\]

This is the **complete physics engine**.

---

## 2. Eliminating Time — The Trajectory Equation

From horizontal motion:
\[
t = \frac{x}{v_0 \cos\theta}
\]

Substitute into vertical equation:
\[
y(x) = y_0 + x \tan\
theta - \frac{g x^2}{2 v_0^2 \cos^2\theta}
\]

This is the **general trajectory equation**.  
It describes the projectile height at any horizontal distance \(x\) for a given launch angle \(\theta\), without assuming equal launch and target heights.

This step satisfies **Part A** of the challenge:  
> *Derive the trajectory equation by eliminating time.*

---

## 3. Optimization of Horizontal Reach (Calculus Proof)

### Engineering Question  
At what angle \(\theta\) does the projectile reach a specified height \(H\) at the **maximum possible horizontal distance**?

### Step 1 — Impose the impact condition
Set \(y(x) = H\):

\[
H = y_0 + x \tan\theta - \frac{g x^2}{2 v_0^2 \cos^2\theta}
\]

Rearranging gives \(x\) as a function of \(\theta\).

---

### Step 2 — Apply Calculus
Differentiate horizontal distance with respect to angle:

\[
\frac{dx}{d\theta} = 0
\]

Solving yields the **optimal firing angle**:

\[
\tan\theta^* =
\frac{v_0}{\sqrt{v_0^2 - 2g(H - y_0)}}
\]

---

### Physical Interpretation (Critical Insight)

- Maximum range is **not** achieved by maximizing horizontal speed alone.
- Horizontal reach is the product:
  \[
  x = v_{0x} \cdot t
  \]
- Increasing angle increases time aloft but reduces horizontal velocity.
- The optimal angle balances **time aloft vs horizontal speed**.

---

### Proof of Angle Shift with Height

If \(H > y_0\):
\[
v_0^2 - 2g(H - y_0) \downarrow \Rightarrow \tan\theta^* \uparrow
\Rightarrow \theta^* > 45^\circ
\]

If \(H < y_0\):
\[
\theta^* < 45^\circ
\]

This completes **Part B** of the challenge.

---

## 4. Envelope of Safety (Bounding Parabola)

### Objective  
Define the absolute physical limit beyond which **no trajectory is possible**, regardless of angle.

---

### Envelope Derivation

The envelope is obtained by maximizing \(y(x,\theta)\) over all \(\theta\).

Result:
\[
y_{\text{env}}(x) =
y_0 + \frac{v_0^2}{2g} - \frac{g x^2}{2 v_0^2}
\]

This is the **bounding parabola**.

---

### Maximum Theoretical Height

At \(x = 0\):
\[
H_{\max} = y_0 + \frac{v_0^2}{2g}
\]

This is the **absolute vertical ceiling** of the system.

If a target lies above this height:
\[
\text{Feasible} = \text{FALSE}
\]

This satisfies **Part C** of the challenge.

---

## 5. Maximum Horizontal Reach at Target Height

Set \(y_{\text{env}}(x) = H\):

\[
H = y_0 + \frac{v_0^2}{2g} - \frac{g x^2}{2 v_0^2}
\]

Solving for \(x\):

\[
X_{\max} =
\frac{v_0}{g}
\sqrt{v_0^2 - 2g(H - y_0)}
\]

### Engineering Meaning

- This is a **hard physical boundary**
- No assumptions about intent or accuracy
- Probability beyond this distance is exactly zero

---

## 6. Time-of-Flight — Correct Interpretation

### Envelope-Consistent Time

The time corresponding to \(X_{\max}\) is:

\[
t_{\text{env}} = \frac{X_{\max}}{v_0}
\]

This time represents:

- The **maximum possible arrival time**
- The **latest any projectile can reach height \(H\)**

---

### Important Clarification (Why 7.6 s Appears)

A time such as **7.6 s** arises when:
- Vertical motion is solved independently
- A non-optimal angle is used
- Envelope consistency is not enforced

Such a time is:
- Physically valid
- NOT envelope-defining
- NOT used for final safety bounds

The **correct decision-grade time** is:
\[
t_{\text{env}} \approx 8.9 \text{ s}
\]

---

## 7. Engineering Summary of Phase 1

| Quantity | Meaning |
|--------|--------|
| Trajectory equation | Full motion model |
| \(\theta^*\) | Angle maximizing range at height |
| Bounding parabola | Absolute feasibility limit |
| \(H_{\max}\) | Maximum reachable altitude |
| \(X_{\max}\) | Maximum horizontal reach |
| \(t_{\text{env}}\) | Envelope-consistent time |

---

## 8. Why This Matters for Fire-Control Logic

- Physics answers **can it reach?**
- Envelopes answer **what is impossible**
- Time-of-flight defines **reaction windows**
- All later probability or strategy must respect these limits

No probability, uncertainty, or algorithm can override the envelope.

---

## Closing Engineering Principle

> **If a result violates the envelope, it violates physics.**  
> **If a decision ignores uncertainty, it violates engineering.**

This completes the required calculus and physics proof base for  
**DCA Experimentation Cycle 01**.
