---
layout: default
title: Lab2
---

<script type="text/x-mathjax-config">MathJax.Hub.Config({tex2jax:{inlineMath:[['\$','\$'],['\\(','\\)']],processEscapes:true},CommonHTML: {matchFontHeight:false}});</script>
<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_CHTML"></script>

# Lab2 - Exploring the Stability of Mass Transfer

## Science goal

The goal of this lab is to explore how binaries evolve depending on the companion mass and mass ratios $q\equiv M_2/M_1$. The aim is to see the diversity of stellar evolution when the star is in a binary. This lab will focus on identifying when mass transfer is stable or unstable in low and high mass ratio binary systems. In this lab, we will push the numerical limits of what MESA Binary can handle. 

### Bonus goal

Our bonus goal is to explore the impact of adopting nonconservative mass transfer on mass transfer stability.




## Exploring a grid of mass transfer models with varying mass ratios
This lab will continue using the downloaded `Lab1_binary` directory, modeling this system as a star + point mass. To do this, open `inlist_project` and make sure to set `evolve_both_stars = .false.`.


To explore the stability of mass transfer across various mass ratios and orbital periods.


Let's start by assuming fully conservative mass transfer, i.e. ($\beta=0$).

For this lab we will keep the Primary/donor mass fixed at **`m1 = 15d0`**, do not adjust this mass. We will explore the binary evolution of our system with varying periods and mass ratios `m2/m1` by modifying `initial_period_in_days` and `m2`. We will explore the following mass range $M_{2} = 1.5 - 12 M_{\odot}$ and periods $P_\mathrm{orb} = 2 - 512$ days. We've descritized this parameter space in the following two tables:

| Companion (accretor) Mass ( $M_{\odot}$ ) |   
|:------------------------|
| 1.5      |
| 3        |
| 6        |
| 9        |
| 12        |

| Period (days) |     
|:--------------|
| 2        | 
| 4        | 
| 8        | 
| 16        |
| 32       |
| 64       |
| 128       |
| 256       |
| 512       |

Now choose a value for the initial mass and period of the binary system from this table by entering your name in the row next to the corresponding mass and period in the [Day 4 Massive Binaries Lab1 tab in Google sheets](https://docs.google.com/spreadsheets/d/1__UPg_5JfiBkJpZTleyaSwW_faxHzmo_X7Us2RTfLOM/edit?usp=sharing). With `inlist_project` open, fill in your chosen values of Primary Mass and Period from the spread sheet.


In the `&binary_controls`, you should see the following lines:

```
   m1 = 15d0  ! donor mass in Msun
   m2 = 12d0 ! companion mass in Msun
   initial_period_in_days = 6d0
```

In `inlist1`, set a stopping condition such that the model terminates when the primary reaches helium depletion. Let's terminate the model when $X(^4\mathrm{He})\leq10^{-4}$:


```plaintext
   xa_central_lower_limit_species(1) = 'he4'
   xa_central_lower_limit(1) = 1d-4
```

|:clipboard: NOTE|
|:--|
|Not all models in this lab will reach this stopping condition, as they might terminate pre-maturely due to numerical difficulties associated with resolving unstable mass transfer.|


### Let's review the different types of mass transfer

Mass transfer in binary systems are often classified based on which burning stage the donor star is in. This is because stars have very different structures depending on the burning stage and therefore respond to mass loss in completely different ways.

<dl>
  <dt> Case A mass transfer </dt>
       <dd> Mass transfer from a core hydrogen burning star (main sequence star).</dd>
  <dt> Case B mass transfer </dt>
       <dd> Mass transfer from a core hydrogen depleted star (post-main sequence star).  </dd>
  <dt> Case C mass transfer </dt>
       <dd> Mass transfer from a core helium depleted star. </dd>
</dl>

### When is mass transfer stable versus unstable?

Mass transfer in binary systems is often classified as stable or unstable.

Stable Mass transfer: When mass transfer proceeds in a controlled manner, without leading to dramatic changes in the system. The donor star loses mass at a rate that allows the binary system to remain bound and evolve over time. Typically, this results in a smooth and gradual transfer of mass.

Unstable Mass Transfer: This occurs when the mass transfer process leads to rapid and uncontrollable changes in the system. The donor star loses mass at a rate that destabilizes the system, typically considered to a common envelope phase, where the envelope of the donor star engulfs both stars, or even to the merger of the two stars. This usually results in dramatic, often short-lived, evolutionary changes in the binary system. 




Now, we will run the model. As before, for this, we need to execute the below commands in the terminal

```shell-session
$ ./mk
$ ./rn
```


The model should take roughly 11 minutes to run on a 4 core machine, you can use this time to inspect and discuss differences between your models and those of the others at your table. 

When your model is finished running, try to make a movie of your `&pgbinary` diagram so you can watch the movie instead of re-running your MESA model. In your `Lab1_binary` directory you can execute the `images_to_movie` command to convert your saved `&pgbinary` pngs into a movie. Here is an example that produces a .mp4 movie named `movie.mp4`.

```shell-session
$ images_to_movie "png/*.png" movie.mp4
```

Now that you have created a wonderful `&pgbinary` movie, let's use this movie in conjuction with our terminal output from our run to answer the following questions!

|:information_source: CATCH UP|
|:--|
| If you are having issues generating a pgstar movie, we have provided precomputed `&pgbinary` movies for all the runs [available for download here](https://drive.google.com/drive/folders/1yubo5s121aMKaxUs690oLAcAwxqOcm52?usp=share_link).|


| :question: Below are some questions to discuss at your table and answer while your model evolves | 
| :--- |
| 1. What type of mass transfer does your system undergo? Case A, B, C? |
| 2. Is the mass transfer in your system stable or unstable?|
| 3. What is the approximate mass of the primary when the mass transfer phase ends?|
| 4. What is the approximate mass of the secondary (accretor) when the mass transfer phase ends?|


In the [Day 4 Massive Binaries Lab3 tab in Google sheets](https://docs.google.com/spreadsheets/d/1__UPg_5JfiBkJpZTleyaSwW_faxHzmo_X7Us2RTfLOM/edit?usp=sharing), fill in each column for your chosen values so we can discuss the global results as a class.

| M<sub>primary</sub> / M<sub>accretor</sub> | M<sub>primary</sub> Final | M<sub>accretor</sub> Final | Type of Mass Transfer (A, B, C?) | Stable or Unstable? | Final Period (days) |
|:-----------------------------------------|:-------------------------|:-------------------------|:----------------------------------|:--------------------|:---------------------|
|||||||


|:question: DISCUSSION|
|:--|
| 1. What are the qualitative differences between Case A vs B mass transfer? |
| 2. How does the mass ratio influence the stability of mass transfer and their outcome? |
| 3. We have ignored the effect of winds here. How do you think the evolution would change if we added winds on top of binary effects? |

## Bonus1 : Evolving to Core-Carbon Depletion

Let's try extending our stopping condition to when the primary reaches core-Carbon depletion, and look for a second mass transfer phase. Then fill in the last column in the [Day 4 Massive Binaries Lab3 tab in Google sheets](https://docs.google.com/spreadsheets/d/1__UPg_5JfiBkJpZTleyaSwW_faxHzmo_X7Us2RTfLOM/edit?usp=sharing) .

| :question: Below are some questions to discuss at your table and answer while your model evolves | 
| :--- |
| 1. Does your system undergo a second mass transfer phase?|
| 2. Is your primary a BSG, YSG, or RSG when it reaches core-Carbon depletion?|
| 3. What type of observation supernova will your primary result in?|
| 4. Is the mass transfer in your system stable or unstable?|


## Bonus 2: Nonconservative Mass Transfer

As in Lab1, try adopting the following nonconservative Mass transfer controls and re run your model.

| $\alpha$ | $\beta$ | $\delta$ | $\gamma$ |
|:-----|:--------------|:--------------|:----------------|
| 0 | 0.5 | 0 | 0 |


Do your answers to any of the aforementioned questions change? Discuss with your group.

