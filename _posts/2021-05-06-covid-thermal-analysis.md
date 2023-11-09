---
title:  "Thermal Analysis of a COVID-19 Vaccine Storage Container"
mathjax: true
layout: post
categories: media
---

During the year of 2020 within the United States one of the most infamous pandemics in recent memory occurred. This was COVID-19, and after a long wait the first vaccines were made available and were mass produced to be distributed among the public. This distribution of these was critical because if the vaccines fell below a certain temperature, they would lose their effectiveness. This would be detrimental as since COVID was such an infectious disease and was impacting the lives of so many, every lost vaccine had a significant impact. This project aims to mitigate failure of vaccines by conducting a thermal analysis of the container transporting them and to obtain a timeline for effectiveness of the vaccine. Specifically, through deriving a mathematical model to predict how the temperature of the vaccine varies with time within the storage container.


## Procedure
![Container](/assets/thermal_analysis_images/actual_container.jpg)

Figure: Photograph of an actual insulated container for the COVID-19 vaccine

### Problem Definition
With knowing the material and shape of the container in question the first step was to develop and idealized cubical model to assist in streamlining the analysis. With this new model of the container a three-step strategy was then employed to solve the problem. First, was to utilize an electrical network analysis to determine an expression for the heat transfer from the vaccine. Second, was to use an energy balance to determine a differential equation to represent the time-varying vaccine temperature. The third, and final, was to use the previously derived equation to calculate the time (in days) for the vaccine (and other storage container contents) to increase from -25 to -15 degrees Celsius for a freezer air (storage) temperature of -10 degrees.

![Model](/assets/thermal_analysis_images/cube_model.jpg)

Figure: Idealized Cubical Model of Storage Container

### Results
With this strategy outlined, the first action was conducting the electrical analysis which began with identifying that the heat transfer mode between the inside and outside temperatures which was treated as a series circuit in which on both the inside and outside temperature of the box passed heat to the container walls through convection, and heat is transferred through the walls through conduction in the walls, edges, and corners of the container. It was determined that the thermal resistance of the system to be equivalent to:

$$ R_{tot} = 6 \frac{K}{W} $$

The second action was conducting an energy balance which once completed resulting in the following differential equations. The following equations are equivalent, the theta, also known as temperature excess, was just introduced to simplify the computation:

$$ m*C_p*\frac{\partial \theta}{\partial t} = \frac{T_{\infty} - T(t)}{R_tot} $$

The third, and final action involved solving the differential equation for time, t, to solve the number of days it would take for the storage container to go from -25 to -15 degrees with -10 degrees as the ambient storage temperature. The following results determined that roughly 1.7 days it would take to reach this temperature. Below are the following assumptions and resulting equation:

* No Steady-State:
  * The temperature of the vaccine is changing with time
* No Heat Generation:
  * The vaccine is not producing heat
* Constant Thermal Properties:
  * Properties don't change with the time-dependent temperature
* Constant Freezer Temperature:
  * The freezer is producing a constant ambient temperature
* No Heat Transfer Out:
  * The vaccine is colder than the surrounding temperature
 
$$ T(t) = T_{\infty} - (T_{\infty} - T_i) * e^{\frac{-t}{m*C_p*R_{tot}}} $$

$$ t = -m*C_p*R_{tot}*\naturallogarithm{\frac{T_{\infty} - T(t)}{T_{\infty} - T_i}} $$

As an extra step, an additional plot was made to show the variation of safe storage time in days with changing temperatures in Celsius.

![Plot](/assets/thermal_analysis_images/temp_vs_time.jpg)
