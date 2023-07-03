---
layout: post
title:  "Yonex Precision Scan Overanalyzed: Performance Swingweight Debunked"
categories: Analysis
---

# Yonex Precision Scan Overanalyzed: Performance Swingweight Debunked

Hello~

This is my first analysis-style blog that just overanalyzes something, usually about badminton! Today, I'll be looking at the __Yonex Precision Scan Machine__, how it measures racket balance, left vs right weight, and what performance swing weight really is!

![img](\assets\yonex-scan-machine.jpg){:style="display:block; margin-left:auto; margin-right:auto" width="50%"}

Highlights of the Yonex Precision Scan Machine:
- Measures balance point automatically.
- Calculates left & right side of racket weight. 
- Calculates swing weight and "performance" swing weight.

I'll just spill it right here: Yonex Performance Swingweight is simply 

$$ SW_{perf} = \left(0.655 \cdot \text{SW} + 0.335 \cdot \text{Mass} + .01 \cdot \text{Balance} \right)$$

truncated to the 1st decimal digit. The SW above is in kgcm^2, mass in grams, and balance in mm. What does this mean? Well, I will explain.


## Introduction

The Yonex Precision Scan is marketed as a racket fitting tool that helps match a player to the most suitable racket, mainly by measuring its weight, balance, and swing weight. These 3 measurements are widely used by the badminton community, and many tools such as the popular Victor WBS-10 already support these measurements. Two things set the Yonex Precision Scan apart:
- Balance is measured statically. No need to manually balance the racket on a stick.
- A new metric called Performance Swing Weight, which Yonex claims to be more tuned to the natural swing of a racket. 

Let's look deeper into how these 2 things work.

## Measuring Balance Without Using a Stick

Yonex Precision Scan has 3 pressure sensors used to measure weight and balance together. There is one sensor at the racket's butt end and two sensors at the frame. Of course, if the racket only lays on those 3 sensors, and each sensor measures weight, the sum of each sensor's measured weight will give the racket's total weight.

![img](\assets\yonex-scan-sensors.PNG){:style="display:block; margin-left:auto; margin-right:auto" width="50%"}

As you can imagine, each of these sensors' measurements may not be equal to each other. If a racket's balance is low, the sensor at the racket's butt end should measure the highest weight. If a racket's balance is high, the sensors at the racket's frame should measure the highest. Comparing each sensor's weight would allow the machine to deduce the racket's balance point.

In fact, this method is already known in the badminton community. In a [BadmintonCentral post](https://www.badmintoncentral.com/forums/index.php?threads/head-weight-an-easier-simpler-appoximation-of-swing-weight.123622/) by user visor, they detailed a method to measure "head weight". This simply involves putting the very top of the racket frame on a scale and taking the measurement. The bigger the measured weight, the heavier the racket head/frame. 

![img](\assets\yonex-scan-hw.jpg){:style="display:block; margin-left:auto; margin-right:auto" width="50%"}

After a few posts, visor soon realizes that this head weight does not need to be measured, and can be deduced directly by the racket weight and balance. That is, head weight is simply a measurement that summarizes racket weight and balance. The formula is given by 
$$ \text{Headweight} = \text{Weight}\frac{\text{Balance}}{\text{Racket Length}}.$$
Now, the formula is meant to derive head weight from balance, weight, and length. But with some rearranging, this can also be used to derive balance, i.e. knowing head weight, weight, and length will give you the racket's balance point. 

The Yonex Precision Scan uses exactly this mechanism to measure a racket's balance without a ruler. 
- It knows beforehand the length between the head sensors and the butt sensor. 
- It knows the distance from the butt sensor to the racket's bottom end (there is an additional moving sensor for this). 
- It can calculate the racket's total weight.
- It knows the racket's "head weight" from the sensors at the frame end. 

So, using all this information, the machine can calculate racket balance using a modification of the above formula.

### Left and Right Weight?

When posed with the measurements from Yonex Precision Scan, some online users are concerned that the measured LEFT and RIGHT weights of the rackets are uneven. Does this mean that one side of the racket is heavier than the other? Would this mess up the swing?

![img](\assets\yonex-scan-uneven.jpg){:style="display:block; margin-left:auto; margin-right:auto" width="50%"}

While that is possible, I suspect there is a bigger cause for the disparity between LEFT vs RIGHT weight. The machine is built such that the user can place their racket on the sensors without much alignment, so the racket may not be placed exactly in the center of the LEFT and RIGHT sensors. Sometimes the racket will tilt more to the left, or right. So naturally, one of the sensors would display a higher reading. The more important thing should be the sum of the left and right measurements.

## Performance Swing Weight
I found the [patent](https://worldwide.espacenet.com/patent/search?q=pn%3DJP2021052816A) that describes the Yonex Precision machine in more detail, including information about this new "Performance Swing Weight". In essence, Yonex gave a group of tennis players various rackets with various parameters. The players score the rackets by how heavy each one feels during testing. Then, Yonex tries to fit these players' scoring to the measured parameters of the rackets, namely weight, balance, and swing weight. Yonex claims that Performance Swing Weight is better than swing weight alone because swing weight is measured by swinging a racket from a fixed fulcrum, which does not accurately represent a tennis swing.

Intuitively, while you swing a racket, the force to rotate the racket from your grip can be described by swing weight. However, your grip is not stationary because you also drive your elbow forward during the swing; the force for moving the entire racket forward can be described by the racket mass. Next, if the racket center of mass is at the head (all other variables equal), it will feel heavier. Hence, the balance point also has an influence.

So, in the patent, Yonex gives the formula for performance swing weight (called A1) as 

$$ A1 = C1 \cdot SW + C2 \cdot MA + C3\cdot BP $$

with SW being the swing weight in kgcm^2, MA being the mass in grams, and BP balance point in mm (measured from the racket's butt). The coefficients C1, C2, and C3 are not disclosed but Yonex says they add up to 1.

![img](\assets\yonex-scan-A1.PNG){:style="display:block; margin-left:auto; margin-right:auto" width="50%"}

So, performance swing weight is just a linear combination of 3 other measurements. The equation has 3 unknown coefficients, and we already have 1 other equation that says they add to 1. So, we need 2 more data points to derive the coefficients. In practice, I found this a bit more tricky because of some implicit rounding, but I solved the formula to be:

$$ SW_{perf} = \left(0.655 \cdot \text{SW} + 0.335 \cdot \text{Mass} + .01 \cdot \text{Balance} \right)$$

truncated to the 1st decimal digit. I tested this on >10 data points (mostly videos from YouTube), and found it to be exactly accurate.

### So What Does It Mean?
Before anything, keep in mind that this performance swing weight is derived originally for tennis. I suspect it is not as useful for badminton, but we can still discuss what this formula means.

First, the coefficient on SW is the greatest, meaning swing weight is the most influential factor in how heavy a racket feels. This is kinda already well-known, but the more surprising part is the coefficients on mass and balance. 

In the performance swing weight formula, 1 g of mass is equal to 33.5 mm of balance. 33.5 mm of balance is HUGE in badminton; good luck changing a racket balance by 33.5 mm. If you want to make the racket feel lighter, you are better off lowering the swing weight or mass. 

Now, some people believe that adding grip to the racket, which adds mass but lowers balance points, makes a racket faster. According to the formula, if you want to make the racket feel faster/lighter, you should instead focus on decreasing the mass, considering that decreasing the swing weight of a racket is almost impossible. One method of lowering mass is taking off the base grip. This will increase the balance point, but the decrease in mass will have a much bigger effect on performance swing weight. I have never seen an example where taking off 1 g of grip equates to a 33.5 mm increase in balance point.


### The Elusive A2 Index
In the patent, Yonex also mentions a different index, called A2, which they derived from a __badminton__ experiment comparing grip weights vs how heavy a __badminton__ racket feels. They claim that they will use A2 for badminton rackets and A1 for tennis rackets.

![img](\assets\yonex-scan-gripdata.PNG){:style="display:block; margin-left:auto; margin-right:auto" width="50%"}

From the experiments, Yonex observed that adding grip weight may make a badminton racket feel faster to the participants. But after a certain threshold, adding more grip weight will make the racket feel heavier. This is then translated into another formula:

![img](\assets\yonex-scan-A2.PNG){:style="display:block; margin-left:auto; margin-right:auto" width="50%"}

In practice, or at least in all of the content involving the Yonex Precision Scan, I see no appearance of this A2 index. I have tried solving for unknowns, but none of the data can be fitted to this A2 formula. I suspect Yonex had this index in their design, but ultimately scrapped it. Or perhaps there is a hidden setting (that no one has discovered) that activates this A2 index? 

### Summary

1. You can measure the balance point of a racket using 2 or more pressure/weight sensors.
2. When it comes to how heavy a racket feels, the swing weight contributes most, followed by weight, followed by the balance point, though balance point has barely any influence.
3. Yonex has an undisclosed index A2 for badminton rackets that describes the optimum grip weight of a racket for a lighter feel. 

One advantage of the performance swing weight is that it allows you to compare rackets with widely different specs and ask which one will feel heavier or lighter. For example, say racket A has a swing weight of 87, mass of 80, and balance of 325. Racket B has a swing weight of 84, mass of 84, and balance of 305. Which one swings heavier? Well, racket A has a performance swing weight of 87.0 and B has a performance swing weight of 86.2, so racket A will feel heavier, despite the lower weight. 

Another interesting finding is Yonex's experiment on index A2. It would be nice to replicate their experiment and try different grip weights on the same racket to find which weight optimizes the racket's "lightness". I am skeptical that adding grip weight to a racket can make it faster, but it would be fun to see what others think. I personality just put enough grip for my desired thickness, regardless of weight.
