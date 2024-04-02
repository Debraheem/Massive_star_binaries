```markdown
## MiniLab1 - Modeling a star through envelope stripping

Assume that we have a binary star system where the components are close enough to undergo Roche Lobe overflow (RLOF) from the inner L1 Lagrangian point. Additionally, assume that both components do not have the same mass so that the evolution of one star slightly lags the other star. In the lab, we would like to explore how the primary - more massive - star evolves in such a binary.

Since here we are primarily interested in the evolution of the primary, to save some computation time we are going to approximate the secondary as a point mass further. In other words, we are not going to model the evolution of the secondary. Then, later in Section~\ref{subsec: evolve both stars}, we will relax this assumption and evolve both stars in detail.

### The evolution of the primary star

To begin, we will first make a copy of the `evolve_star_and_point_mass` directory located in the binary `test_suites` directory. To do this, type the following in your terminal.

```
cp - r $MESA_DIR/binary/test_suite/evolve_star_poin_mass my_thursday_lab1
cd my_thursday_lab1
```

Now that you have cloned the directory, you should choose desired values for the initial mass and period of the binary in the `inlist_project` file. For this lab we agree to work with a standard set of values for these parameters. Open the `inlist_project` file in your preferred text editor and modify the following lines

```
m1 = 15d0  ! donor mass in Msun
m2 = 9d0 ! companion mass in Msun
initial_period_in_days = 6d0
```

Now, we will run the model. As before, for this, we need to execute the below commands in the terminal

```
./mk
./rn
```

### Bonus exercise - Evolving both stars

## MiniLab2 - Modelling the mass gainer
```

