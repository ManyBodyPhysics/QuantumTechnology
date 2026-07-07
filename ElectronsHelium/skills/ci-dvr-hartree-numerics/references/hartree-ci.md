# Hartree method and full CI (distinguishable particles)

Reference for the mean-field basis and the two-body diagonalization. The electrons are treated as
**distinguishable** (deep wells suppress tunnelling), so the many-body ansatz uses **product states**,
not antisymmetrized determinants. This was validated against fermionic full CI in the entanglement
paper — the two agree for the systems of interest.

## Hartree for two distinguishable particles

Approximate the ground state as a product `|Φ⟩ = |φ^L_0 φ^R_0⟩` with orthonormal orbitals, and
minimize the Hartree energy

```
E_H = ⟨φ^L_0|ĥ_L|φ^L_0⟩ + ⟨φ^R_0|ĥ_R|φ^R_0⟩ + ⟨φ^L_0 φ^R_0|u|φ^L_0 φ^R_0⟩
```

Expanding each orbital in the sinc-DVR basis, `|φ^A_i⟩ = Σ_α B^A_{αi}|χ^A_α⟩`, stationarity gives two
**coupled** eigenvalue problems (mean field of one well depends on the density in the other):

```
Σ_β [ h^L_{αβ} + δ_{αβ} Σ_γ |B^R_{γ0}|² u^{LR}_{βγ} ] B^L_{β0} = λ_L B^L_{α0}
Σ_β [ h^R_{αβ} + δ_{αβ} Σ_γ |B^L_{γ0}|² u^{LR}_{γβ} ] B^R_{β0} = λ_R B^R_{α0}
```

Solve **self-consistently** (initialize `f^A = h^A`, iterate) until `|ε^{A,(k+1)}_i − ε^{A,(k)}_i| < δ`
with `δ = 1e-10`. Diagonalizing each converged Hartree matrix yields not just the lowest pair but a
full set; **keep the lowest `N_A + 1` eigenvectors** as the compact single-particle basis
`P_A = {|φ^A_i⟩ : i = 0..N_A}` (`N_A ≪ K_A`, the DVR size). These bases already contain most of the
Coulomb physics, so the CI converges with only a few states per well.

## Basis transformation DVR → Hartree

```
h^A_{ij} = Σ_{αβ} B^A*_{αi} B^A_{βj} h^A_{αβ}
u_{ij,kl} = Σ_{αβ} B^L*_{αi} B^R*_{βj} B^L_{αk} B^R_{βl} u^{LR}_{αβ}
```

## Full CI assembly and diagonalization

Two-body ansatz and Hamiltonian in the Hartree product basis:

```
|Ψ_n⟩ = Σ_{ij} C_{ij,n} |φ^L_i φ^R_j⟩
H_{ij,kl} = h^L_{ik} δ_{jl} + δ_{ik} h^R_{jl} + u_{ij,kl}
```

Diagonalize `H` for eigenpairs `{E_n, C_{ij,n}}` (each eigenvector is a coefficient *matrix*). For
dynamics, obtain only the lowest states with the **Davidson** iterative eigensolver. **Truncate** the
configuration space by ordering product configurations by one-body energy sum `ε_a + ε_b` and keeping
the lowest `N_CI` — this preserves low-energy mixed-orbital configurations near avoided crossings.

## Entanglement from the coefficient matrix (Schmidt / SVD)

For a two-body state `C_{kl}`, the SVD `C_{kl} = Σ_p U_{kp} σ_p V*_{lp}` gives Schmidt states and the
**von Neumann entropy** (base-2):

```
S = − Σ_p σ_p² log₂(σ_p²)
```

The Hartree basis is an approximate common Schmidt basis, so each eigenstate is dominated by one/two
product terms — a good diagnostic when reading configurations (I: S≈0; II: two states with S≈1; III:
triple crossing S≈{1.5,1,1.5}).

## Dominant natural orbitals (for the sensor's reference states)

From the spin-summed one-body density matrix `ρ^{(1)}_{µν}` restricted to L and R blocks, the
largest-eigenvalue eigenvectors give the best single left/right orbital of a correlated CI state.
Build the reference singlet/triplet from these dominant modes:

```
|S*⟩ = (1/√2)(d†_{L↑} d†_{R↓} − d†_{L↓} d†_{R↑})|0⟩
|T₀*⟩ = (1/√2)(d†_{L↑} d†_{R↓} + d†_{L↓} d†_{R↑})|0⟩,   d†_{Lσ}=Σ_{µ∈L} u^{(L)}_µ c†_{µσ}, etc.
```

Overlaps `⟨S*|g⟩`, `⟨T₀*|e⟩` measure how ideal the sensing two-level system is (see `quantum-sensing`).

## ZZ coupling (effective-Hamiltonian cross-check)

`ζ = E₄ − E₂ − E₁ + E₀`. In the Bogoliubov/effective-oscillator model,
`ζ ≈ 2g²/(Δ+β_L) − 2g²/(Δ−β_R)`, which vanishes for opposite-sign equal-magnitude anharmonicities in
the harmonic limit; the full CI shows deviations away from it, motivating direct numerical
minimization of `ζ` when optimizing configurations.
