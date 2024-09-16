# 0. Introduction to combustion

## ⚡️ Basic notions

### Main Mechanism in Cantera tabulation

- Reduction/Oxidation chemical reaction
- Chain reaction and exothermic

<aside>
💡
CH4+2O2 → CO2+2H2O

</aside>

### Basic combustion terminology

- Stoichiometry(화학양론): the determination of the proportions in which elements or compounds react with one another.
- Equivalence ratio(등가비): Two ratios are said to be equivalent If they represent the same value when reduced to the simplest form.
- Laminar/Turbulent flames(층류/난류 유동): Laminar flames are smooth in appearance; they have what might be referred to as a smooth flow. Turbulent flames can be considered as an aggregation of small laminar flames embedded in a turbulent flow field, distributed randomly, and have a one-dimensional structure, and the concept of small laminar flames can be used to set up a model of turbulent flame.
- Premixed/Diffusion flames: A premixed flame refers to a chemical reaction in which the fuel and the air are mixed before combustion, whereas, in a diffusion flame the fuel and air are separated and must come together before combustion. In order to burn, in both cases the fuel and air must come together.

[https://www.youtube.com/watch?v=_gqO3ncLfRg](https://www.youtube.com/watch?v=_gqO3ncLfRg)

![Premixed flames](./img/premixedFlame.png)

Premixed flames


- Global/Detailed mechanism: Global mechanism is established to facilitate the mobilization of financial resources to implement the Convention and address desertification, land degradation and drought. Detailed reaction mechanisms refer to a series of reactions that explain the experimental determination of the order of a reaction for each species involved, while also reproducing the stoichiometry of the reaction.
- Flame speed: the measured rate of expansion of the flame front in a combustion reaction. It is important to model combustion in CFD.
- Flame thickness: the width over which the entirety of the chemical to thermal energy conversion occurs.

### Consumption speed tabulation - 3 different flame speeds

1. Laminar unstretched flames(SL)
2. Consumption speed(SC)
3. Turbulent speed(ST)

![image.png](./img/flameTypes.png)

<aside>
💡
The goal of the project is to compute the consumption speed depending on the stretch and heat loss.

</aside>