# SolarHNL Project Instructions

## Project Overview
This is a computational physics research project studying Heavy Neutral Leptons (HNLs) production from solar atmospheric neutrinos through transition magnetic moments. The analysis uses solar model data to calculate interaction and decay probabilities within the Sun.

## Core Physics Context
- **Main Research Topic**: HNL production via transition magnetic moments from solar atmospheric neutrinos
- **Key References**:
  - Solar atmospheric neutrinos: arXiv:2107.13696 (JV, JL, et al ICRC)
  - HAWC observations: arXiv:2212.00815
- **Energy Range**: ~10 GeV to 100 TeV neutrino energies
- **Physical Scales**: Solar radius (Rsun = 6.96e10 cm), solar luminosity

## Data Sources
- `SSM.dat`: Standard Solar Model (BP2004, astro-ph/0402114) containing radial profiles of:
  - Mass, radius, temperature, density, pressure, luminosity fractions
  - Elemental abundances (H, He3, He4, C12, N14, O16)
  - Always load with: `pd.read_csv('SSM.dat', sep='\s+', comment='#')`

## Physics Conventions & Units
- **Unit System**: Natural units with ℏc = 1.973e-14 GeV·cm
- **Standard masses**: electron mass = 0.511 MeV, Bohr magneton = 1/(2m_e) GeV^-1
- **Key quantities**:
  - Solar atmospheric flux at Earth: E³φ ≈ 4e-6 GeV² cm⁻² s⁻¹
  - Cross sections: σ ∝ d² ℏc² (where d = μ/2, μ is magnetic moment)
  - Decay width: Γ = d² m³/(4π)
  - Decay length: L_dec = (ℏc · E/m) / Γ
  - Interaction length: L_int = 1/(n · σ)

## Code Organization
- **Primary Notebook**: `Sandbox.ipynb` - all analysis is notebook-based
- **Plotting Style**: Always use `plt.style.use("figures.mplstyle")` for consistent figures
  - Configured with: 8x6 figure size, 18pt axis labels, 16pt tick labels, 16pt legend, no legend frame

## Common Analysis Patterns
1. **Parameter Space Scans**: Use `np.logspace()` for mass (1 MeV to 1 GeV) and magnetic moment ranges
2. **Solar Calculations**: Reference solar density ~100 g/cm³ at surface, number density = ρ × 6.02e23 cm⁻³
3. **Probability Calculations**: Interaction probability = 1 - exp(-R_sun/L_int)
4. **Visualization**: Use `LogNorm` for colormaps, contour plots with levels=[1e-5, 1e-3, 1e-1] for probabilities

## Physics Function Naming
- `xs(d, m)`: Cross section in cm² (d=dipole/2, m=mass)
- `gamma(d, m)`: Decay width in GeV
- `decay_length(d, m, E)`: Decay length in cm at energy E
- `E3phi`: Shorthand for E³ × flux (standard in high-energy neutrino physics)

## Solar Model Variables
- Load sun data into `the_sun` DataFrame
- Standard solar parameters: `Lsun = 3.8418E+33` erg/s, `Rsun = 6.9598E+10` cm
- Access radial profiles via: `Rsun * the_sun['R/Rsun']` for radius in cm
- Key columns: `Rho` (density), `M/Msun` (mass), `X` (hydrogen), `Y` (helium-4)

## Plotting Conventions
- Always use `plt.loglog()` for parameter space plots
- Label masses as `$m_N$ (GeV)`, magnetic moments as `$\mu/\mu_B$`
- Use orange for decay length contours, dodgerblue for interaction probability
- Contour label pattern: Define R_sun scale as level=1, probabilities as scientific notation

## Dependencies
- Core: `numpy`, `matplotlib`, `pandas`
- Physics specific: Use `matplotlib.colors.LogNorm` for normalized color scales
