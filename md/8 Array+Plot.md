# 8. Array+Plot

# ⚡️code corrections

### 1. Remove `fl1` object, use only `fl2` object

- You set your own temperature (Tp), so there's no need for the automatically determined temperature from fl1.
- Both fl1 and fl2 are the same type of flame object (CounterflowPremixedFlame), meaning you can perform the same calculations and analysis with just fl2.

### 2. Change `mdot_reactants` to an array

- Velocity and strain vary with mdot_reactants and width, so mdot_reactants is set as an array, and results are appended to ScF.>

### 3. Plot `ScF` Graph

- Plot a graph observing changes in ScF values by adjusting mdot_reactants while keeping width constant.

### 4. Redraw `grid-vel` Graph

- Adjust grid to the current width and redraw the graph.

---

### Questions

> Is the shape of the current(grid-vel) graph correct?
> 

⇒ Right. The flow is one direction, from left to right, with varying signs of velocity

⇒ Paper has a width of 1–2 cm and speed values range from 0.5 to 0.6, compare with these value

> instead of adjusting the `mdot_reactants` value, would it be better to vary the `width` and observe `ScF`?
> 

⇒ Changing the width increases velocity, which we want to avoid

⇒ We aim to stay within a reasonable velocity range

** High velocities are needed only for achieving stretch, so minimizing the domain width helps maintain reasonable velocities

> Are there any additional plots I should consider?
> 

⇒ plot from the Garcia paper, Figure 1

⇒ Otherwise, 3D plot → with the value of the ScF, Ka, heat loss (XYZ axis)

⇒ Or we can change the pressure value and check ScF values

> Currently, the `Ka`, `thermal diffusivity`, `max gradient` functions are used only to assess flame properties and overall conditions, not in the consumption speed calculation. In which other functions can these values be applied? +How can I improve the calculation speed?
> 

⇒ Add code within the loop that calculates ScF values based on mdot values, adjusting for the maximum gradient and the corresponding Ka to find the ScF while considering stretch

⇒ Additionally, append code to calculate heat loss to determine the temperature of the project