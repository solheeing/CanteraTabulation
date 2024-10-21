# 7. Flame speed, maximum gradient, Ka, ScF

# ⚡️code corrections

### 1. flame speed, maximum gradient

```python
# calculate flame speed using laminar unstretched flame
flame = ct.FreeFlame(gas1, width=width)
flame.solve(loglevel, auto=True)
flame_speed = flame.velocity[0]  # flame velocity(first one)
print(f'Flame speed: {flame_speed:.5f} m/s')
```

```python
# calculate velocity gradient
grad_u = np.gradient(flame.velocity, flame.grid) 

# find index that has max|du/dx|
max_grad_idx = np.argmax(np.abs(grad_u))
print(f"Index of max |du/dx|: {max_grad_idx}")

# value of max|du/dx|
max_grad_value = grad_u[max_grad_idx]
print(f"Value of max |du/dx|: {max_grad_value}")
```

### 2. adiabatic temperature(from laminar flame)

```python
# get adiabatic temperature from the FreeFlame object
def get_adiabatic_temperature_from_flame(flame):
    Tad = flame.T[-1]  # final status of the flame
    return Tad

Tad = get_adiabatic_temperature_from_flame(fl1)
print(f'Adiabatic temperature (Tad) from FreeFlame: {Tad:.2f} K')
```

- **`flame.gas.density`**:  current density(current point during flame calculation)
- **`gas.density`**: initial condition density

### 3. thermal diffusivity

```python
# calculate thermal diffusivity
cp = flame.cp_mass[0]  # specific heat capacity at constant pressure(Cp), first grid point (J/kg/K)
density = flame.density_mass[0]  # density at the first grid point (kg/m^3)
lambda_ = flame.thermal_conductivity[0]  # thermal conductivity at the first grid point (W/m/K)

thermal_diffusivity = lambda_ / (density * cp)  # thermal diffusivity calculation
print(f"Thermal diffusivity of reactants (α): {thermal_diffusivity:.5e} m^2/s")
```

### 4. strain rate Ka

```python
# calculate strain rate
Ka = thermal_diffusivity / (flame_speed * max_grad_value)
print(f"Strain rate (Ka): {Ka:.5e} 1/s")
```

### 5. consumption speed S_cF (using flame density, net production rate code)

```python
def calculate_consumption_speed(flame, gas, fuel_species):
    # unburnt density (first point of the grid)
    rho_u = flame.density[0]  
    
    # calculate (Y_k,b - Y_k,u) for each fuel species
    mass_fraction_diff = 0
    integral_numerator = 0

    # (Y_f,u, first point)
    total_fuel_mass_fraction = 0
    for fuel in fuel_species:
        i_fuel = gas.species_index(fuel)
        total_fuel_mass_fraction += flame.Y[i_fuel, 0]

    for fuel in fuel_species:
        i_fuel = gas.species_index(fuel)  # fuel index

        # calculate Y_k,b (end value) and Y_k_u (first value)
        Y_k_b = flame.Y[i_fuel, -1]  # end point (product)
        Y_k_u = flame.Y[i_fuel, 0]   # first point (reactant)
        mass_fraction_diff += Y_k_b - Y_k_u  # sigma (Y_k,b - Y_k,u)

    # calculate nk (n_k = Y_k,u / Y_f,u)
    ih2 = gas.species_index('H2')
    Y_h2_u = flame.Y[ih2, 0]  # mass fraction
    nk_h2 = Y_h2_u / total_fuel_mass_fraction

    ich4 = gas.species_index('CH4')
    Y_ch4_u = flame.Y[ich4, 0]  # mass fraction
    nk_ch4 = Y_ch4_u / total_fuel_mass_fraction

    # integral about production rates
    integral_h2 = scipy.integrate.simpson(gas.molecular_weights[ih2] * flame.net_production_rates[ih2], x=flame.grid)
    integral_ch4 = scipy.integrate.simpson(gas.molecular_weights[ich4] * flame.net_production_rates[ich4], x=flame.grid)

    # integral_numerator update (nk*integral value)
    integral_numerator = (nk_h2 * integral_h2) + (nk_ch4 * integral_ch4)

    S_cF = integral_numerator / (rho_u * mass_fraction_diff)
    
    return S_cF

fuel_species = ['CH4', 'H2']
S_cF = calculate_consumption_speed(fl2, gas1, fuel_species)
print(f'Consumption speed S_cF: {S_cF:.5f} m/s')
```

- **`fl2`** represents the **state of the flame**, providing data after the flame has formed. It is used to retrieve values such as density, production rates, and mass fractions after the flame has been established.
- **`gas1`** defines the **initial state** of the mixture, and it is used to get information like species indices and molecular weights. This initial information is necessary for calculating the net production rates during the reaction.

### Questions

> How can I set up the x-axis? just set Ka values between 10^(-2) and 10^2? and append them into the array?
> 

⇒ Change the velocity and strain using `mdot_reactants` and `width`, then determine the Ka value based on those.