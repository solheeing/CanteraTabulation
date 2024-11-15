# 9. Fix graph

# ⚡️code corrections

### 1. Modify the `ScF` loop

- Move max.grad index, thermal diffusivity, and Ka into the for loop.

### 2. Initialize `Gas` object

- Moved the gas object inside the loop to reinitialize it on each iteration, ensuring that an outdated gas object is not used repeatedly.

### 3. Obtain positive `ScF` value

- To ensure the consumption speed value is **positive**, it's necessary to check the signs of  integral_numerator and mass_fraction_diff.
- Applied the **abs** function to obtain positive values.

---

### Status

1. using different gases, thermal diffusivity, Ka values
2. positive ScF values, but not continuous
3. using laminar flame speed
4. Dynamically update the values of density, cp, and thermal diffusivity according to each mdot.

---

### Questions

> I feel like I don't fully understand the role of each function in my code. I know that mdot and width affect the overall speed and strain of the project. However, in the current code, I'm defining speed in the laminar state first, and I feel this should be modified to use the counterflow premixed flame. However, I'm confused because you previously mentioned that I should use the laminar flame speed. What role does the initially defined laminar speed play?
> 

⇒ There are multiple velocities with different meaning, the flames speed which only concerns the flame irrespective of the the flow speed. The laminar unstretched flame speed (sl0) and the consumption speed (sc). The laminar unstretched flame speed is used to compute the diffusive flame thickness and other quantity related to the chemistry of the flame without flow interaction. You can see it as a "constant" as it describes the flame speed without stretch, turbulence or other phenomenon. It is not strictly necessary to use it but the reference we have (Garcia2022) uses it to normalize quantities.

> I've structured `ScF` based on the Garcia paper, and I resolved the issue of consumption speed appearing as negative by using the abs function. However, this function does not reflect the `Ka` value, so I’m wondering if I need to modify it.
> 

⇒ Using abs to solve for the the sign problem is not the right way as it doesn't actually solve the problem but hide it. The consumption speed should be positive without it

> Currently, I have heat loss included within a `for` loop to continuously calculate temperature, but I'm wondering if I should modify the consumption speed function to incorporate it into the `ScF` calculation. Also, I’m unsure whether I should use the product temperature or just set a fixed temperature.
> 

⇒ The heat loss is included within the flame solving when you set the temperature of the products. The consumption speed is computed using the chemical reaction rate it already includes all the effect of temperature stretch and so on. You should set the product temperature to match the desired heat loss you are targeting.

> Finally, I know that `Tp` starts from `Tad` and decreases, and I set the initial temperature to 300K to observe how `beta` changes with different `mdot` values. However, using the heat loss formula from Garcia, `beta` doesn’t directly reflect `mdot`, resulting in `beta` values continually coming out as NaN. How can I resolve this?
> 

⇒ beta doesn't change with mass flow, beta is the ratio of reactant and product temperature compared to the adiabatic temperature. The heat loss only concerns temperature.