# 1. Cantera Examples

## ⚡️ How to start with Cantera

### Definition

```python
#Importation of Cantera in a script
import cantera as ct

#Define the mixture
gas = ct.Solution('gri30.yaml')

# You can print the gas state with:
gas()

# To know how you can handle a solution, type:
help(gas)
```

- **The file 'gri30.yaml' contains (basically included in Cantera package)**
    - The properties of the different species
    - The kinetic reactions
    - The type of transport used (not necessarily)

```python
# Previously explained code lines
import cantera as ct
gas = ct.Solution('gri30.yaml')

# Impose directly the composition:
gas.TPX = 300, 1e5, {'H2':4, 'O2':1, 'N2':3.76}

# Or equivalently set the equivalence ratio:
gas.TP = 300, 1e5
gas.set_equivalence_ratio(1.0, 'H2:1', 'O2:1, N2:3.76')
```

```python
gas.TP = 300, 1e5
gas.X = {'H2':4, 'O2':1, 'N2':3.76}

# density and T are kept constant but P varies when X is set alone !!!
```

### Tutorial

```python
# Previously explained code lines
import cantera as ct
gas = ct.Solution('gri30.yaml')

# Defining a premixed flame object
premixed_flame = ct.FreeFlame(gas, width=0.02)

# Defining a counterflow diffusion flame object
counterflowdiffusion_flame = ct.CounterflowDiffusionFlame(gas, width=0.02)
```

```python
# Previously explained code lines
import cantera as ct
gas = ct.Solution('gri30.yaml')
premixed_flame = ct.FreeFlame(gas, width=0.02)

# Defining the inlet conditions
premixed_flame.inlet.X = gas.X
premixed_flame.inlet.T = gas.T
```

```python
# Previously explained code lines
import cantera as ct
gas = ct.Solution('gri30.yaml')
counterflowpremixed_flame = ct.CounterflowDiffusionFlame(gas, width=0.02)

# Defining the inlet conditions
counterflowdiffusion_flame.fuel_inlet.mdot = 0.10 # kg/m^2/s
counterflowdiffusion_flame.fuel_inlet.X = 'H2:1'
counterflowdiffusion_flame.fuel_inlet.T = 300 # K

counterflowdiffusion_flame.oxidizer.mdot = 0.12 # kg/m^2/s
counterflowdiffusion_flame.oxidizer_inlet.X = 'O2:0.21, N2:0.79'
counterflowdiffusion_flame.oxidizer_inlet.T = 300 # K
```

```python
# Previously explained code lines
import cantera as ct
gas = ct.Solution('gri30.yaml')
f = ct.FreeFlame(gas, width=0.02)
f.inlet.X = gas.X
f.inlet.T = gas.T

# Solve for chemistry and mesh refinement criteria
f.energy_enabled = True #에너지 방정식 활성화
#세분화 기준, 기울기, 곡률, 메시 제거 기준
f.set_refine_criteria(ratio=2.0, slope=0.05, curve=0.05, prune=0.01)

# Lines below used for premixed flames (see appendix for more info)
#야코비언 함수 갱신 주기 설정, 10번의 반복 동안 갱신 없이 사용, 최대 10번의 반복 허용
f.set_max_jac_age(10, 10) 
#초기 시간 스텝 설정, 시간 스텝 증가 조건
f.set_time_step(1e-8, [10, 20, 40, 80, 100, 100, 150])
f.max_time_step_count = 500 #최대 500번

# Launch flame resolution
f.solve(loglevel, refine_grid)
```