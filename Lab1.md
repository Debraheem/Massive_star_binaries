[Introduction](./index.html)

[Lab1](./Lab1.html)

[Lab2](./Lab2.html)

[Lab3](./Lab3.html)


Here is a downloadable copy of the desired [Lab1_binary](https://drive.google.com/file/d/1y0AEFWzGv4vHgohqnEJMNITR15oGPHRi/view?usp=share_link) MESA work directory.
This work directory is a slightly modified version of the `$MESA_DIR/binary/test_suite/evolve_both_stars` test_suite.

## MiniLab1 - Modeling a star through envelope stripping



Assume that we have a binary star system where the components are close enough to undergo Roche Lobe overflow (RLOF) from the inner L1 Lagrangian point. Additionally, assume that both components do not have the same mass so that the evolution of one star slightly lags the other star. In the lab, we would like to explore how the primary - more massive - star evolves in such a binary.

Since here we are primarily interested in the evolution of the primary, to save some computation time we are going to approximate the secondary as a point mass further. In other words, we are not going to model the evolution of the secondary. Then, later in Section~\ref{subsec: evolve both stars}, we will relax this assumption and evolve both stars in detail.

### The evolution of the primary star

To begin, we will use our `Lab1_binary` directory from the introduction. We will begin by modeling this system as a star + point mass, so open `inlist_project` and
make sure to set `evolve_both_stars = .false.`.

Open the `inlist_project` file and choose desired values for the initial mass and period of the binary from the [Day 4 Massive Binaries Lab1 tab in Google sheets](https://docs.google.com/spreadsheets/d/1__UPg_5JfiBkJpZTleyaSwW_faxHzmo_X7Us2RTfLOM/edit?usp=sharing) table below

Let's start by assuming fully conservative mass transfer, i.e. ($\beta$ == 1).

| Primary (Donor) Mass ( $M_{\odot}$ ) |   
|:------------------------|
| 12.5      |
| 15        |
| 20        |
| 25        |

| Period (days) |     
|:--------------|
| 2        | 
| 4        | 
| 8        | 
| 15       |
| 30       | 
| 2        | 
| 4        | 
| 8        | 
| 15       |
| 30       | 

For this lab we agree to work with a standard set of values for these parameters. Open the `inlist_project` fill in your chosen values of Primary Mass, Period, and $\beta$ from the spread sheet. This can be done by modifying the following lines

```
m1 = 15d0  ! donor mass in Msun
m2 = 9d0 ! companion mass in Msun
initial_period_in_days = 6d0
```


Before running our model, let's uncomment some values from the `history_columns.list` and `profile_columns.list` so we can plot in our `&pgbinary ` plots.

Now, we will run the model. As before, for this, we need to execute the below commands in the terminal

```
./mk
./rn
```


The model should take roughly 7 minutes to run on a 4 core machine, so let's use this time to modify our pgstar to output some quantities of interest.







once we have our nice pgstar, let's modify the stopping conditions! We want our binary evolution to terminate when the mass transfer phase is complete. To do this, we can set a stopping condition which terminates  


we want something like the following:



## Add a custom stopping condition, something like...

```fortran
if (b% point_mass_i == 0) then
            if (b% m(2) > 1.2d0 * b % m(1) ) then
               extras_binary_finish_step = terminate
               write(*,*) "Terminate due to m2 > 1.3 x m1"
               return
            end if
         end if
```



### Bonus exercise - Evolving both stars (Over lunch if necessary)




