# 5. counterflow premixed flame

# ⚡️ Codes & Questions

```python
# parameter values
p0 = 101325  # pressure
T0 = 296  # inlet temperature
phi = 0.7 # equivalence ratio
alpha = 0.566 # volume fraction(<1)

#mdot(=mass flux, 단위 면적당 시간당 전달되는 질량)
mdot_reactants = 80  # kg/m^2/s # 반응물이 1초당 1m² 면적을 통해 80kg 만큼 들어온다
mdot_products = mdot_reactants  # kg/m^2/s #생성물이 반응 후에 같은 속도로 배출된다, mass conservation

# Mechanism and fuel composition
xh2 = alpha / (1 - alpha) * 1  # xh2 = alpha/(1-alpha)*xc
fuel = {'CH4': 1, 'H2': xh2}
oxidizer = {'O2': 1, 'N2': 3.76}

# Calculation params
width = 0.1  # m domain width
loglevel = 0  # amount of diagnostic output (0 to 5)
```

> the code is adjusting xh2 but I want to change CH4 so I tried to set ‘xh4’. But I don’t know how to set up. xh2 is derived by equivalence ratio and set as alpha/(1-alpha), and there’s no idea for xch4.
> 

⇒ alpha is the equation of the mass fraction, and I can change the phi and alpha values instead of changing or making xch4.

> I couldn’t understand the exact meaning of fl1.products.T and fl2.products.T. How can I use it?
> 

⇒ laminar flame. adiabatic temp(no heat loss)

⇒ *check the temperature after reactions

```python
# compare temperature
temperature_fl1 = fl1.products.T
temperature_fl2 = fl2.products.T

# plot
plt.figure()
#plt.plot(temperature_fl1, label='fl1 temperature')
#plt.plot(temperature_fl2, label='fl2 temperature')

plt.plot(fl1.grid,temperature_fl1)
plt.plot(fl2.grid,temperature_fl2)

plt.xlabel('position (m)')
plt.ylabel('temperature (K)')
plt.title('compare reactants temperature')
plt.legend()
plt.show()
```

> I tried to compare temperatures so wrote the code regards of fl1.products.T and fl2.products.T. I know that the temperature is fixed to a certain temp but I just wanted to compare so decided to make a plot of this but it isn’t working.
> 

> The only thing I can change in the code is the mdot_reactants value and the product temperature at fl2?
> 

⇒ yeah I can change the mdot_reactants and fl2.products.T

```python
# Heat loss coefficient and environment temperature
heat_loss_coefficient = 0.1  # W/m^2·K (example value)
T_env = 300  # K (example value)

# Calculate temperature drop due to heat loss
def calculate_temperature_drop(T_flame, T_env, heat_loss_coefficient):
    # Heat loss calculation
    Q_loss = heat_loss_coefficient * (T_flame - T_env)
    print(Q_loss)
    
    # Assuming specific heat and flame density for delta_T calculation
    specific_heat = 1000  # J/kg·K (simplified value)
    flame_density = fl1.density[0]  # kg/m^3
    delta_T = Q_loss / (specific_heat * flame_density)  # Temperature drop
    return delta_T

# Calculate temperature drop and apply it to fl2
delta_T = calculate_temperature_drop(fl1.products.T, T_env, heat_loss_coefficient)
fl2.products.T = fl1.products.T - delta_T  # Adjust fl2's product temperature
fl2.products.X = fl1.products.X  # Composition of the products

# Solve the flame simulation for fl2 with adjusted temperature
fl2.set_initial_guess(equilibrate=False)
fl2.solve(loglevel, auto=True)
print(f'Adjusted product temperature (fl2): {fl2.products.T:.2f} K')
```

> I set the environment temperature to 300K because I wanted to reflect the lab temperature. And should I have to change it to the exact temperature? or keep it
> 

⇒ Can keep it

---

### Important Things

- heat loss ← by changing Tp
- stretch rate(value) ← by changing mass flow