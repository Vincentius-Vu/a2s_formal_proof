# Lean 4 Arithmetic Checks for $AS^2$-Curve Foundation

This repository contains **Lean 4 (v4.36.0)** integer and natural-number arithmetic checks supporting the **$AS^2$-Curve** manuscript.

**Scope Note:** These Lean 4 modules verify boundary evaluations of the septic polynomial and its prescribed derivative expressions over `Int`, as well as natural-number monotonicity and division-bound admissibility of the scaled contour-error product over `Nat`. Full real-analysis (`ℝ` / `HasDerivAt`) and Euclidean vector-space proofs are outside the scope of this Lean package.

## Modules and Theorems

### 1. `AS2Verification.Smoothness` (Integer Boundary Checks)
- `AS2.S_boundary_zero`, `AS2.S_boundary_one`: $S(0) = 0$, $S(1) = 1$ (`rfl`, no axioms)
- `AS2.S_vel_boundary_zero`, `AS2.S_vel_boundary_one`: $S_{\mathrm{vel}}(0) = 0$, $S_{\mathrm{vel}}(1) = 0$ (`rfl`, no axioms)
- `AS2.S_acc_boundary_zero`, `AS2.S_acc_boundary_one`: $S_{\mathrm{acc}}(0) = 0$, $S_{\mathrm{acc}}(1) = 0$ (`rfl`, no axioms)
- `AS2.S_jerk_boundary_zero`, `AS2.S_jerk_boundary_one`: $S_{\mathrm{jerk}}(0) = 0$, $S_{\mathrm{jerk}}(1) = 0$ (`rfl`, no axioms)
- `AS2.S_snap_at_zero`, `AS2.S_snap_at_one`: $S_{\mathrm{snap}}(0) = 840$, $S_{\mathrm{snap}}(1) = -840$ (`rfl`, no axioms)
- `AS2.S_midpoint_is_half`: $S_{\mathrm{scaled}}(1) = 64$ (`rfl`, no axioms)

### 2. `AS2Verification.ContourBound` (Scaled Natural-Number Arithmetic Checks)
- `AS2.straight_line_zero_contour_error`: `contourErrorScaled v T 0 = 0` (`[propext]`)
- `AS2.zero_blend_time_zero_error`: `contourErrorScaled v 0 sin_th = 0` (`[propext]`)
- `AS2.contour_error_monotonic_time`: $T_1 \le T_2 \implies \text{contourErrorScaled}(v, T_1, s) \le \text{contourErrorScaled}(v, T_2, s)$ (no axioms)
- `AS2.blend_time_guarantees_admissibility`: $\text{contourErrorScaled}(v, T, s) \le 4 \varepsilon \implies \text{contourErrorScaled}(v, T, s) / 4 \le \varepsilon$ (`[propext]`)

## How to Verify

From the repository root (with Lean `v4.36.0` via [Elan](https://github.com/leanprover/elan)):

```bash
lake build
lake env lean CheckAxioms.lean
```
