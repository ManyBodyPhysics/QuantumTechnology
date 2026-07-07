# DVR grids and matrix elements

Reference for building single-particle bases and one-/two-body matrix elements. Two DVR flavours are
used across the papers: **sine-DVR** (particle-in-a-box endpoints, used in the sensing paper's 2D
solve) and **sinc-DVR** (uniform infinite grid, used in the gate/entanglement papers with a
barrier cut). Both are pseudospectral: operators that are local in position are diagonal on the grid.

## Sine-DVR kinetic matrix (finite box `[x₀, x_L]`, N interior points)

Points `x_j = x₀ + jL/(N+1)`, weights `w_j = L/(N+1)`. Exact 1D kinetic matrix (`ℏ²/2m = 1`):

```
T^{(1D)}_{jk} = ½(−1)^{j−k} ·
  ⎧ (π²/3)((N+1)/L)² − 1 / (L² sin²[πj/(N+1)]),                                   j = k
  ⎨
  ⎩ (1/L²)[ 1/sin²(π(j−k)/(2(N+1))) − 1/sin²(π(j+k)/(2(N+1))) ],                  j ≠ k
```

Same formula per axis. **2D kinetic** is the Kronecker sum `T_2D = T_x ⊗ I_y + I_x ⊗ T_y`. The
single-particle Hamiltonian is `H_sp = T_2D + V_2D`, with `V_2D` the diagonal potential `v(r)` on the
grid. Reference grid: `N_x = N_y = 20` (400 points). Diagonalize `H_sp` for `{ε_k, ψ_k}`.

## sinc-DVR (uniform grid, per well)

Basis functions on spacing `Δx`:

```
χ_α(x) = Δx^{-1/2} sinc((x − x_α)/Δx),   sinc(x) = sin(πx)/(πx),  sinc(0)=1
```

so `χ_α(x_β) = Δx^{-1/2} δ_{αβ}`. Cut the grid at the barrier `x_b` (right well starts at `x_b`) to
impose an effective infinite wall between wells — this forces each electron into its own well and lets
you use two small independent bases. Kinetic matrix:

```
t_{αβ} = ⟨χ_α| −½ d²/dx² |χ_β⟩ =
  ⎧ π² / (6 Δx²),                       α = β
  ⎨
  ⎩ (−1)^{α−β} / (Δx² (α−β)²),          α ≠ β
```

## Potential (diagonal on the quadrature)

```
v_{αβ} ≈ Δx Σ_γ χ_α(x_γ) v(x_γ) χ_β(x_γ) = δ_{αβ} v(x_β)
```

so `v` is diagonal with entries `v(x_β)`. The electrode potential is `v(x) = −Σ_k α_k(x) V_k`; the
form factors `α_k(x)` come from a finite-element solve of Laplace's equation for the device.

## Soft-Coulomb two-body matrix elements (diagonal per axis)

With the regularized interaction `u(x₁,x₂) = κ / sqrt((x₁−x₂)² + ε²)` (`κ=2326`, `ε=1e-2`):

```
u_{αβ,γδ} = ⟨χ^L_α χ^R_β | û | χ^L_γ χ^R_δ⟩ ≈ δ_{αγ} δ_{βδ} u(x^L_γ, x^R_δ)
```

i.e. diagonal in each particle's grid index. Label `u^{LR}_{γδ} ≡ u(x^L_γ, x^R_δ)`.

## Practical notes

- Restricting each electron to its own well makes results essentially unchanged versus a shared grid
  but is far cheaper — prefer it for deep double wells.
- Convergence knobs: number of grid points `N` (or `Δx`), box length `L`, and — after Hartree — the
  retained single-particle count `N_A` and CI truncation `N_CI`.
- For 2D, assemble via Kronecker products and keep everything sparse where possible; the potential and
  Coulomb pieces are diagonal, so only the kinetic Kronecker sum is dense per axis.
