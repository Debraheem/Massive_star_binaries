---
layout: default
title: Introduction
---
![](Figures/contact_binary_image.jpg)

credit: ESO/L. Calçada

# Introduction

[Lab1](./Lab1.html)

[Lab2](./Lab2.html)

[Lab3](./Lab3.html)


[HELP LINK for website building](./help.html)

[Google drive link to download Thursday Lab Materials](https://drive.google.com/drive/folders/1yFy2I7kBh6UZPYmhFxkZswQVPI0Qavjc?usp=share_link)

[Link to Lab Solutions](https://drive.google.com/drive/folders/11WEpwn17_XuxKugH0B57OHMjby-jomUj?usp=share_link)



To begin, please download and unzip a copy of the [Lab1_binary](https://drive.google.com/file/d/1y0AEFWzGv4vHgohqnEJMNITR15oGPHRi/view?usp=share_link) MESA work directory.
This work directory is a slightly modified version of the `$MESA_DIR/binary/test_suite/evolve_both_stars` test_suite.



To get an idea of what is inside `Lab1_binary` we can use the `tree` command.

The `tree` command shows the files contained in the `Lab1_binary` directory and its subdirectories.

If your terminal does not have `tree` installed, you  can do it by executing

```
brew install tree (on mac)
or
sudo apt-get install tree (on linux)
```
It's alright if you don't have `tree` or cannot download it, `ls` should suffice.

`tree ./Lab1_binary` should return the following.

```shell
├── binary
├── ck
├── clean
├── history_columns.list
├── inlist
├── inlist1
├── inlist2
├── inlist_pgbinary
├── inlist_pgstar
├── inlist_project
├── make
│   ├── binary_run.o
│   ├── makefile
│   ├── run_binary.mod
│   ├── run_binary.o
│   ├── run_binary_extras.mod
│   ├── run_binary_extras.o
│   ├── run_binary_extras.smod
│   ├── run_star_extras.mod
│   ├── run_star_extras.o
│   └── run_star_extras.smod
├── mk
├── profile_columns.list
├── re
├── rn
├── rn1
└── src
    ├── binary_run.f90
    ├── run_binary_extras.f90
    └── run_star_extras.f90

3 directories, 28 files
```

You will not modify anything in `make/` directory so we will not discuss this files here. 

All other files are briefly described in the table below

### Setting the stellar parameters

| head1                   | head two          | three |
|:------------------------|:------------------|:------|
| `binary`                | good swedish fish | nice  |
| `ck`                    | good swedish fish | nice  |
| `clean`                 | good swedish fish | nice  |
| `history_columns.list`  | good swedish fish | nice  |
| `inlist`                | good swedish fish | nice  |
| `inlist1`               | good and plenty   | nice  |
| `inlist2`               | good `oreos`      | hmm   |
| `inlist_pgbinary`       | good `oreos`      | hmm   |
| `inlist_pgstar`         | good `oreos`      | hmm   |
| `inlist_project`        | good swedish fish | nice  |
| `make`                  | good and plenty   | nice  |
| `mk`                    | good `oreos`      | hmm   |
| `profile_columns`       | good `oreos`      | hmm   |
| `re`                    | good `oreos`      | hmm   |
| `rn`                    | good `oreos`      | hmm   |
| `rn1`                   | good `oreos`      | hmm   |
| `src`                   | good `oreos`      | hmm   |
| `binary_run.f90`        | good `oreos`      | hmm   |
| `run_binary_extras.f90` | good `oreos`      | hmm   |
| `run_star_extras.f90`   | good `oreos`      | hmm   |

`inlist_project`, `inlist1`, and `inlist2` are the three main files that contain the microphysics information of our binary stellar evolution simulation.

#### Binary parameters

The `inlist_project` - which is relevant for binary parameters -  will look something like this

```plaintext
&binary_job

   inlist_names(1) = 'inlist1'
   inlist_names(2) = 'inlist2'

   evolve_both_stars = .true.

/ ! end of binary_job namelist

&binary_controls

   m1 = 15d0  ! donor mass in Msun
   m2 = 11d0 ! companion mass in Msun
   initial_period_in_days = 2d0

/ ! end of binary_controls namelist
```

and will allow us to set the binary parameters, e.g., the initial mass of the stars and their orbital period. The full list of available parameter for `&binary_job` can be found in the directory

```
$MESA_DIR/binary/defaults/binary_job.defaults
```

and those of `&binary_controls` can be found in

```
$MESA_DIR/binary/defaults/binary_controls.defaults
```

If you would like to change any of these default values, just copy them to `inlist_project` and set the new values there.

#### Parameters of the component stars

Any (non-default) values for the parameters of the individual stars will be set in the `inlist1` (for primary star) and `inlist2` (for secondary star) files. The more massive star is considered as the primary star and dictates the initial evolution of the binary system. An example of the contents in `inlist1` is

```plaintext
&star_job

      show_log_description_at_start = .false.
      save_model_when_terminate = .true.
      save_model_filename = 'final1.mod'

/ ! end of star_job namelist

&eos

/ ! end of eos namelist

&kap

      Zbase = 0.02

/ ! end of kap namelist


&controls
      profile_interval = 50
      history_interval = 10
      terminal_interval = 1
      write_header_frequency = 10
      
      ! reduce resolution and solver tolerance to make runs faster
      mesh_delta_coeff = 3d0
      time_delta_coeff = 3d0
      varcontrol_target = 1d-2

/ ! end of controls namelist


&pgstar
   read_extra_pgstar_inlist(1) = .true.
   extra_pgstar_inlist_name(1)= 'inlist_pgstar'

/ ! end of pgstar namelist
```

Many other (default) parameters which are not modified in the above inlist can be found in the directory

```
$MESA_DIR/star/defaults/
```

As before copy the relevant parameter you wish to change to `inlist1` before making the change. Similarly, `inlist2` contains the parameters of star 2.

#### Setting values for an initial run

Here, we will run our first model. For this, we need to set the masses of the stars in the binary and the binary's orbit period. Choose a desired value and then execute the below commands in your terminal

```
./mk
./rn
```

#### Terminal Output

On executing the above commands, MESA will print the model output on the terminal. After each step the new updated values of the binaries parameters would be printed to the display. An example output is shown in Fig. 2.

![An example of the output printed on the terminal](Figures/image.png)

#### Pgstar Output

A picture is worth a thousand words

, so rather than reading the output from the terminal, at times, an intuitive understanding of stellar evolution can be grasped from a diagram. The `Pgstar` module does exactly that. It plots the model output in real-time - depending on the chosen step size.
```

