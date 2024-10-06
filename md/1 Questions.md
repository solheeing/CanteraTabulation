# 1. Questions

```python
loglevel=0
premixed_flame.solve(loglevel, auto=True)
```

> I tried to use refine_grid instead of auto, but it didn’t work.
How can I use refine_grid exactly?
What is the main reason that it didn’t work?
> 

```python
plt.figure()
plt.plot(premixed_flame.grid, premixed_flame.T)
plt.ylabel('Temperature (K)')
plt.xlabel('Grid (m)')
plt.title('1D flame temperature profile')
plt.show()
```

> In this code, the overall code didn’t have a parameter grid but this works.
So what are the criteria that the grid sets automatically? Does it depend on the temperature and pressure that I set already?
And shouldn’t I set the grid manually?
> 

```python
#Soret effect (only with multi component transport model)
flame.soret_enabled = False
```

> I understood all parameters in the Tutorial_LaminarFlame file except for this code.
I searched soret and got what is the soret effect, but I couldn’t understand the multi-component transport model in the premier.
> 

```python
plt.figure()
plt.plot(premixed_flame.grid, premixed_flame.P, color='r')
plt.ylabel('Pressure (Pa)')
plt.xlabel('Grid (m)')
plt.title('1D flame temperature profile')
plt.show()
```

> I tried to make a plot of Pressure, and it didn’t work.
The reason why premixed_flame.P doesn't work in the last plt code is because I didn't define premixed_flame.P, and this should be defined as originally premixed_flame.inlet.P, but is this not defined in the function, so should I say it's an error?
>
