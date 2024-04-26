---
layout: default
title: Lab3
---

## Lab3 - Exploring the Stability of Mass Transfer

In Lab1 we assumed fully conservative mass transfer, i.e. ($\beta$ == 1). In this circumstance all of the mass lost by the Primary star is assumed to be accreted on to the doner. 

Need additional motivational text here for why mass transfer is not conservative in reality and all the methods by which mass can be lost to a binary system, Ryo, Sohan?


In the lab, we would like to explore how the primary - more massive - star evolves in a nonconservative binary where we allow for mass to be lost from the system during mass transfer.

We will continue to using the "star + point_mass" framework where we approximate the secondary as a point masss to save some computation time. Later on in Lab3, we will explore differences resulting from self-consistently evolving both stars.

### Toggling on nonconservative Mass transfer in MESA

For this lab we will continue using the `Lab1_binary` directory, from Lab1, with a few modifications. First, let's make a copy of `Lab1_binary` and name it `Lab2_binary`.

Now let's open `inlist_project` and make sure again that `evolve_both_stars = .false.`. Next let's turn on nonconservative mass transfer by setting the following parameters in `&binary_controls`:

```
! These controls were all set to 0 previously in Lab1
   mass_transfer_alpha = 0d0      ! fraction of mass lost from the vicinity of donor as fast wind
   mass_transfer_beta = 0.6d0     ! fraction of mass lost from the vicinity of accretor as fast wind
   mass_transfer_delta = 0.1d0    ! fraction of mass lost from circumbinary coplanar toroid
   mass_transfer_gamma = 1.2d0    ! radius of the circumbinary coplanar toroid is ``gamma**2 * orbital_separation``
```
Now we have turned on the non-conservative mass transfer controls.

Remember, for this lab we will keep the companion/accretor mass fixed at **`m2 = 12d0`**, do not adjust this mass. We will explore the binary evolution of our system with varying periods and mass ratios *m1/m2* by modifying `initial_period_in_days` and `m1`. We will explore the following mass range $M_{1} = 12.5 - 30 M_{\odot}$ and periods $Period = 2 - 200$ days. We've descritized this parameter space in the following two tables:

| Primary (Donor) Mass ( $M_{\odot}$ ) |   
|:------------------------|
| 12.5      |
| 15        |
| 20        |
| 25        |
| 30        |

| Period (days) |     
|:--------------|
| 2        | 
| 4        | 
| 6        | 
| 8        |
| 15       |
| 20       |
| 25       |
| 30       |
| 50       |
| 100       |
| 200        | 

Now again, choose a value for the initial mass and period of the binary system from this table (same or different, your choice) by entering your name in the row next to the corresponding mass and period in the [Day 4 Massive Binaries Lab2 tab in Google sheets](https://docs.google.com/spreadsheets/d/1__UPg_5JfiBkJpZTleyaSwW_faxHzmo_X7Us2RTfLOM/edit?usp=sharing). With `inlist_project` open, fill in your chosen values of Primary Mass and Period from the spread sheet.


Now, let's run our new non-conservative binary models by executing the commands below in our the terminal

```
./mk
./rn
```


The model should take roughly 7 minutes to run on a 4 core machine, you can use this time to inspect and discuss differences between your models and those of the others at your table. 

When your model is finished running, try to make a movie of your `&pgbinary` diagram so you can watch the movie instead of re-running your MESA model. In your `Lab1_binary` directory you can execute the `images_to_movie` command to convert your saved `&pgbinary` pngs into a movie. Here is an example that produces a .mp4 movie named `movie.mp4`.

```
images_to_movie "png/*.png" movie.mp4
```

Now that you have created a wonderful `&pgbinary` movie, let's use this movie in conjuction with our terminal output from our run to answer the following questions!

**CATCH UP:If you are having issues generating a pgstar movie, we have provided precomputed `&pgbinary` movies for all the runs [available for download here](https://drive.google.com/file/d/1iJG_rwzYHM-GbEj-1A5OgoO57eEwA3A5/view?usp=share_link).**

**Below are some questions to discuss at your table and answer while your model evolves**

1. What is the mass ratio of your system
2. What type of mass transfer does your system undergo? Case A, B, C?
3. Is the mass transfer in your system stable or unstable?
4. What is the approximate mass of your primary when the mass transfer phase ends?


In the [Day 4 Massive Binaries Lab2 tab in Google sheets](https://docs.google.com/spreadsheets/d/1__UPg_5JfiBkJpZTleyaSwW_faxHzmo_X7Us2RTfLOM/edit?usp=sharing), fill in each column for your chosen values so we can discuss the global results as a class.

| M<sub>primary</sub> / M<sub>accretor</sub> | M<sub>primary</sub> Final | M<sub>accretor</sub> Final | Type of Mass Transfer (A, B, C?) | Stable or Unstable? | Final Period (days) |
|:-----------------------------------------|:-------------------------|:-------------------------|:----------------------------------|:--------------------|:---------------------|



## What kind of outcomes to expect


Mass transfer in binary systems are often classified based on which burning stage the donor star is in. This is because stars have very different structures depending on the burning stage and therefore respond to mass loss in completely different ways.

<dl>
  <dt> Case A mass transfer </dt>
       <dd> Mass transfer from a core hydrogen burning star (main sequence star). It often starts off with a rapid phase (thermal timescale) and followed by a slower phase (nuclear timescale).</dd>
  <dt> Case B mass transfer </dt>
       <dd> Mass transfer from a core hydrogen depleted star (post-main sequence star).  </dd>
  <dt> Case C mass transfer </dt>
       <dd> Mass transfer from a core helium depleted star. </dd>
</dl>

How do we know which type of mass transfer occurs? This can be done by simply comparing the size of the star during various burning stages to the size of its  Roche lobe.
