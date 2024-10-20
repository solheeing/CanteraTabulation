# 4. Garcia2022b

### ⚡️ Strain rate

- stagnation point: two flows meet
    - A premixed flame is a flame that mixes after when two flames enter, so it has a stagnation point.

$$
K_a = \frac{δ^0_L}{S^0_L}*κ
$$

- δ^0_L is the diffusive laminar flame thickness, defined as the ratio of the thermal diffusivity of the reactants
- S^0_L is the unstretched laminar flame speed
- as the mass flow rate of the reactants increases, the flame is more strained by the whole velocity field.
- while κ increases, the flame(reaction zone) moves toward a position closer to the stagnation point where the local flame speed balances the local axial velocity.

### ⚡️ Heat loss

$$
β = \frac{T_p-T_r}{T_{ad}-T_r}
$$

- T_r is the temperature of the reactants
- T_p is the temperature of the product stream
- T_{ad} is the temperature of the products under adiabatic conditions
- T_p is progressively decreased from Tad, so β<1

### ⚡️ Consumption speed

$$
S_{cF}=\frac{-1}{ρ_uY_{f,u}}\int_{-\infty}^{\infty} ω_f \, dx
$$

- Y_f is the mass fraction rate of the fuel
- ω_f is the volume fraction rate of the fuel
- For an unstretched laminar flame(K_a=0), the consumption speed corresponds to the value of S^o_L

$$
S_{cF}=\frac{\sum_{k=1}^{N_f}η_k\int_{-\infty}^{\infty} ω_k \, dx}{ρ_u\sum_{k=1}^{N_f}η_k(Y_{k,b}-{Y_{k,u}})}
$$

- suitable definition for multi-component fuel mixtures such as CH4-H2
- the subscripts u and b denote the unburned and burned sides of the flame
- η_k is a weighting factor

$$
S_{cQ}=\frac{\int_{-\infty}^{\infty} Q \, dx}{ρ_uc_p(T_b-T_u)}
$$

- alternative way to define the consumption speed based on the heat release rate by integrate the energy conservation equation
- Q is the total volumetric heat release
- c_p is the mass-specific heat
- it can be used for arbitrary fuel mixture without any change

$$
S_{cQ}=\frac{\int_{-\infty}^{\infty} Q \, dx}{ρ_u\sum_{k=1}^{N}Δh^0_{f,k}(Y_{k,b}-{Y_{k,u}})}
$$

- this is the modified version based on the idea that all the sensible enthalpy comes from the enthalpy of formation of all the species involved in the oxidation reaction
- influence on the reponse of the flames to strain and heat loss is discussed