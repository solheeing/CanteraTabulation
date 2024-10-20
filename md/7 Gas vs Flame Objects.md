# 7. Gas vs Flame Objects

## ⚡️ Difference between gas and flame objects

### 1. **Gas Object**

- **Purpose**: Represents the thermodynamic state of a gas mixture.
- **Usage**: It encapsulates all key properties of the gas, such as temperature, pressure, species concentrations, density, and reaction rates. The gas object is essential for setting up simulations involving chemical reactions or combustion.
- **Key Features**:
    - **Defining Gas Composition**: Defines the species in the mixture, like hydrogen and methane, and sets the initial concentrations.
    - **Thermodynamic Properties**: Allows the specification and retrieval of properties such as temperature, pressure, internal energy, and enthalpy.
    - **Reaction Mechanisms**: Handles calculations related to reaction rates, equilibrium constants, and other chemical kinetics aspects.

### 2. **Flame Object**

- **Purpose**: Represents the configuration of a flame. It models the behavior of the gas mixture undergoing combustion, such as freely propagating flames, counterflow flames, or burner-stabilized flames.
- **Usage**: Used to calculate flame dynamics, including temperature profiles, flame speed, and the distribution of species within the flame.
- **Key Features**:
    - **FreeFlame Object**: This object simulates freely propagating laminar flames. For example, it calculates the adiabatic flame temperature, flame speed, and spatial profiles of temperature and species concentrations.
    - **Counterflow Premixed Flame Object**: Simulates flames formed between two opposing streams of fuel and oxidizer. This is particularly useful for studying conditions like heat loss and flame extinction.

### Differences Between the Two (Context-Specific):

- **Gas Object**: Used to define the properties of the hydrogen-methane mixture. This includes setting parameters like temperature, pressure, and composition. The gas object represents the properties of the mixture before combustion occurs.
- **FreeFlame Object**: Builds on the gas object to calculate specific flame behaviors, such as flame speed and structure. In your laminar flame speed analysis, this object helps solve the 1D flame propagation problem and study how the flame changes with varying heat loss and strain rate.

In essence, the `gas` object defines the properties of the unburned mixture, while the `flame` object focuses on the behavior of that mixture as it undergoes combustion.

---

⇒ Use the `gas` object only for setting the initial conditions of the mixture, and use the `flame` object to study the reaction changes based on heat loss, strain rate, and consumption speed.