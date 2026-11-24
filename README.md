# Formal Verification of $AS^2$-Curve Foundation in Lean 4

This directory contains the machine-checked mathematical proofs for the proposed **$AS^2$-Curve (Asymmetric Sigmoid S-Curve)** trajectory planning framework.

All theorems and lemmas are formalized and formally verified using the **Lean 4 Interactive Theorem Prover** (Toolchain: `leanprover/lean4:v4.36.0`).

---

## Formalized Modules and Theorems

### 1. `AS2Verification.Smoothness` ($C^3$ Continuity & Bounded Snap)
* **Theorem 1 (Exact Boundary Vanishing Conditions):**
  - Position: $S(0) = 0$, $S(1) = 1$
  - Velocity: $S'(0) = 0$, $S'(1) = 0$
  - Acceleration: $S''(0) = 0$, $S''(1) = 0$
  - Jerk: $S'''(0) = 0$, $S'''(1) = 0$ (Guarantees $C^3$ boundary vanishing jerk, eliminating Dirac delta impulses in snap)
* **Theorem 2 (Finite and Strictly Bounded Snap at Boundaries):**
  - Finite snap: $S''''(0) = 840$, $S''''(1) = -840$ (No Dirac delta impulses in motor drive voltage / current derivatives)

### 2. `AS2Verification.ContourBound` (Corner Blending Contour Error Bound)
* **Theorem 1.1 (Straight-Line Zero Contour Error):**
  - When $\theta = 0$, geometric contour error $\delta \equiv 0$.
* **Theorem 1.2 (Zero-Duration Boundary):**
  - When $T_{\text{blend}} = 0$ (stop-and-go mode), $\delta \equiv 0$.
* **Theorem 1.3 (Monotonicity w.r.t Blend Time):**
  - $T_1 \le T_2 \implies \delta(T_1) \le \delta(T_2)$.
* **Theorem 1.4 (Tolerance Admissibility Guarantee):**
  - $V_{\text{corner}} T_{\text{blend}} \sin(\theta) \le 4 \cdot \varepsilon_{\text{allowable}} \implies \text{Contour Deviation} \le \varepsilon_{\text{allowable}}$.

### 3. `AS2Verification.TorqueScaling` (Inertial Torque Saturation Invariance)
* **Theorem 3.1 (Quadratic Dilation Monotonicity):**
  - $\forall s \ge 1 \implies s^2 \ge s \ge 1$.
* **Theorem 3.2 (Torque Invariance Property):**
  - Under quadratic time scaling $a' = a / s^2$, for $s^2 \cdot \tau_{\text{safe}} \ge \tau$, the effective torque is strictly bounded by the actuator threshold: $\tau' \le \tau_{\text{safe}}$.
* **Corollary 3.3 (Nominal Scaling Recovery):**
  - When $s = 1$, the bound collapses identically to the nominal torque condition $\tau \le \tau_{\text{safe}}$.

---

## How to Verify the Proofs

Ensure [Elan](https://github.com/leanprover/elan) and Lean 4 are installed, then execute:

```bash
cd formal_proofs/AS2Verification
lake build
```

Expected output:
```text
✔ [2/12] Built AS2Verification.Basic
✔ [4/12] Built AS2Verification.Smoothness
✔ [6/12] Built AS2Verification.TorqueScaling
✔ [8/12] Built AS2Verification.ContourBound
✔ [10/12] Built AS2Verification
Build completed successfully (12 jobs).
```
