---
title: Color
keywords: color, physics, matching, constancy
order: 8 # Lecture number for 2020
---

Lecture 8: Color
keywords: color, physics, matching, constancy
order: 8
---

- [Color Physics](#1-color-physics)
	- [Motivation](#1-1-motivation)
	- [Physics of Light](#1-2-physics-of-light)
	- [Photons](#1-3-photons)
	- [Radiometry](#1-4-radiometry)
- [Color Matching](#2-color-matching)
    - [Motivation](#2-1-motivation)
	- [Color Perception in Humans](#2-2-color-perception-in-humans)
	- [Linearity of Color Representation](#2-3-linearity-of-color-representation)
	- [Color-Matching Experiments](#2-4-color-matching-experiments)
- [Color Constancy](#3-color-constancy)
    - [Color Perception Inconsistencies](#3-1-color-perception-inconsistencies)
	- [Luminance Perception at Edges](#3-2-luminance-perception-at-edges)
	- [Retinex Theory](#3-3-retinex-theory)
	- [Color Perception in Three Dimensions](#3-4-color-perception-in-three-dimensions)

[//]: # (This is how you can make a comment that won't appear in the web page! It might be visible on some machines/browsers so use this only for development.)

[//]: # (Notice in the table of contents that [First Big Topic] matches #first-big-topic, except for all lowercase and spaces are replaced with dashes. This is important so that the table of contents links properly to the sections)

[//]: # (Leave this line here, but you can replace the name field with anything! It's used in the HTML structure of the page but isn't visible to users)

<a name='1-color-physics'></a>
## 1 Color Physics

<a name='Subtopic 1-1'></a>
### 1-1 Motivation
A visual system needs color for a variety of reasons: such as telling what food is edible, distinguishing material changes from shading changes, and grouping parts of one object within a scene. There's quite a lot of nuance and complexity associated with colors, as well as color standards. In fact, some companies even have color trademarks!

### 1-2 Physics of Light
#### Spectral Colors
A spectral color comprises a single wavelength that is correlated to a wavelength in the below diagram. 
![](https://i.imgur.com/4LEfqBr.png)
*Source: http://hyperphysics.phy-astr.gsu.edu/hbase/vision/specol.html#c2*

Any color can be described completely by its color spectrum: the number of photons (per time unit) at each wavelength 400-700nm. There are familiar names associated for different cartoon spectra, for example, wavelengths between 600-700nm are red and wavelengths between 400-500nm are blue. By mixing and finding complements of common colors, even more colors can be produced, for example cyan (wavelengths between 400-600nm).

#### Color Mixing

Because colors are photons at different wavelengths, they can be added together. In additive color mixing, the color spectra of two colors add together (for example, red and green combine to make yellow). Real world examples of additive color systems include Cathode Ray Tubes and Multiple Projectors.

In subtractive color mixing, color spectra are multiplied: each of the pigments are removed from white. A world example is printing on paper.

<a name='Subtopic 1-3'></a>
### 1-3 Photons
Photons from a light source can behave in many ways: 




| Concept             | Definitions                                                                  | Diagram |
| ------------------- | ---------------------------------------------------------------------------- | ------- |
| Absorption          | Photon is absorbed by the surface.                                           | ![](https://i.imgur.com/69pPnR0.png)
| Diffuse Reflection  | Photon is uniformly distributed/reflected in other directions.               | ![](https://i.imgur.com/ExUIvCp.png)
| Specular Reflection | Photon is reflected normally with respect to the incoming direction.         | ![](https://i.imgur.com/2qP7yOm.png)
| Transparency        | Photon goes through a transparent surface.                                   | ![](https://i.imgur.com/NWJROuH.png)
| Refraction          | Photon goes through surface but exits at a different angle due to reflecition within.   | ![](https://i.imgur.com/ZaaavqD.png)
| Fluorescence        | Photon leaves surface with a different wavelength than the wavelength it first contacted the surface with (experiencing change in color). |  ![](https://i.imgur.com/JFFhEYe.png) |
| Subsurface Scattering | Photon leaves surface at a different position than position it first contacted the surface with. |![](https://i.imgur.com/LYHstXB.png) |
| Phosphorescence       | Delay when the photon meets the surface.                                    | ![](https://i.imgur.com/iB8GVhu.png) |
| Interreflection       | If there are multiple surfaces, photon may be reflected multiple times     | ![](https://i.imgur.com/fQ6CK1i.png) |

<a name='Subtopic 1-4'></a>
### 1-4 Radiometry

#### Radiance & Irradiance
Radiance is defined as the power emitted per unit area in a direction. As illustrated in the diagram below, radiance is represented as the outgoing power in a certain direction, where the direction is specified by (polar angle, azimuth). On the other hand, irradiance is the total incident power falling on a surface, depicted by the incoming arrows in the diagram below.
![](https://i.imgur.com/fvgqJa2.png)
*Source: Horn, 1986.*

#### Bidirectional reflectance distribution function (BRDF)
The BRDF is a model of local reflection that tells how bright a surface appears when viewed from one direction when light falls from it from another. It takes four parameters: $\theta_i$, $\phi_i$, $\theta_e$, and $\phi_e$, which represent the incoming/exiting polar angle and azimuth: 

$BRDF = f(\theta_i, \phi_i, \theta_e, \phi_e)$ = $L(\theta_e, \phi_e)/E(\theta_i, \phi_i)$ 
= $radiance$ / $irradiance$
![](https://i.imgur.com/qHtXLMJ.png)

This model fails to take into account the fact that different surfaces may have different rates of reflectance and refractance for different wavelengths. Adding an additional parameter, $\lambda$ (the wavelength) alters the equation to be:

$BRDF = f(\theta_i, \phi_i, \theta_e, \phi_e, \lambda)$ = $L(\theta_e, \phi_e, \lambda)/E(\theta_i, \phi_i, \lambda)$ 
= $spectral$ $radiance$ / $spectral$ $irradiance$

The BRDF has many limitations: it is difficult to measure how much light is reflecting at all possible directions, and it is very unstable (minor bumps/surface damage can alter the whole BRDF). 

For many surfaces, light leaving the surface is independent of the exit angle: given a certain incoming light direction, regardless of the viewing angle, the light leaving the viewing surface is the same fraction of the incoming light direction.

#### Lambertian Reflection
Lambertian (diffuse) surfaces appear equally bright from all viewing directions. For this reason, we no longer need the viewing directions $\phi_e$ and $\theta_e$ to be parameters to the BRDF, as seen in the equation below:

![](https://i.imgur.com/wzHStsS.png)


#### Simplified Rendering Models for BRDF

1. Reflectance: for diffuse reflections, we replace the BRDF calculation with a wavelength-by-wavelength scalar multiplication. Assuming there's incoming light (and the illumination has its own color spectrum), the color of the reflectance surface can be parametrized by a single parameter that is the wavelength. For example, the diagram below depicts how much light is reflecting for incoming light at different wavelengths on a particular surface. After doing wavelength-by-wavelength multiplication between the illumination and reflectance, the absolute color is generated, represented by the color signal.
![](https://i.imgur.com/pCCDhCX.png)

1. Transmittance: Similarly, if we're seeing transparent objects or seeing through surfaces, then there's a transmittance function. Doing element-wise multiplication with illumination will produce the color signal. 
![](https://i.imgur.com/HPTvatM.png)


<a name='Topic 2'></a>
## 2 Color Matching
This lecture addresses how colors are perceived by humans, how they can be accurately represented, and how the color of a light source can be reproduced by the right combination of primary color intensities.

### 2-1 Motivation

The ability to represent and reproduce colors accurately has great commercial and aesthetic value. Colors are a key aspect of corporate branding and can instantly link a logo, website, or product to the company in a viewer’s mind. In fact, they are so important that corporations often trademark their signature colors; to do so they need a way to accurately represent the color. 

Being able to measure and match colors is also critical for textile manufacturers to consistently colored fabric. In the world of art, creating reproductions of artworks hinges on the ability to match the colors in the reproduction to those in the original. As our consumption of media becomes increasingly digital, the ability to capture and display colors with high fidelity becomes paramount.

### 2-2 Color Perception in Humans
There are two types of photoreceptors in the human eye – rods and cones. We will focus on **cones**, as they are capable of color vision. The human retina contains three different types of cones. Each type of cone is sensitive to a different range of the color spectrum. The **L-cones** are sensitive to longer wavelengths, and the **M-cones** and **S-cones** are sensitive to medium and shorter wavelengths respectively. The spectral sensitivities of the three cone types are shown in Figure 2.1. 

Let us represent the sensitivity curves mathematically as functions \\(S_L(\lambda)\\), \\(S_M(\lambda)\\), and \\(S_S(\lambda)\\), where \\(\lambda\\) is the wavelength of the incoming light.
<center>
<div>
  <img src="https://i.imgur.com/YqUhK8Y.png">
  <div class="figcaption"><b>Figure 2.1.</b> Spectral sensitivities of L-, M-, and S-cones in the human eye, adapted from Foundations of Vision, Brian Wandell, Sinauer Assoc., 1995   <br></br>    
  </div>
</div>
</center>

In reality, the perception of color is influenced by a number of factors other than the response of the cones to the incoming light. These factors include the type of the illumination, the adaptation level of the eye, and the colors and scene surrounding the observed color. 

However, for the purpose of this discussion **we assume that the perceived color is completely determined by the spectrum of the light entering the eye**. This assumption is valid under certain controlled conditions.

If we build on this assumption, we can understand how we sense light spectra. An intuitive understanding can be derived from the diagram below, where the **incoming light spectrum gets projected onto a 3-D space, one each for the L, M, and S receptors respectively**. From a biophysics point of view, we are essentially integrating the response over all wavelengths, weighted by the receptor's sensitivity at each wavelength. A more rigorous mathematical explanation is given below. 
<center>
<div>
  <img src="https://i.imgur.com/KGUFdC9.png">   
  </div>
</div>
</center>

Given an incoming light spectrum \\(I(\lambda)\\), the response of a photodetector of type \\(i\\) is given by $$ r_i = \int_\lambda I(\lambda)S_i(\lambda) d\lambda$$.
This can be interpreted as the dot product of the incoming light spectrum with the basis vectors \\(S_i(\lambda)\\), thus projecting the higher-dimensional input spectrum on to a vector \\((r_L, r_M, r_S)\\) in a 3-dimensional subspace. The perceived color is fully determined by this 3-D vector. In fact, **if two distinct incoming light spectra project on to the same vector in the 3-D subspace, they will be perceived to be the same color.**

### 2-3 Linearity of Color Representation

Human color perception has properties that can be modeled by the principle of superposition. Grassman’s Law tells us that if color \\(A_1\\) matches color \\(B_1\\) (in the sense that they produce the same \\((r_L, r_M, r_S)\\) response vector), and color \\(A_2\\) matches color \\(B_2\\), then color \\(A_1 + A_2\\) matches \\(B_1 + B_2\\). Here the summation means that light from both color spectra are combined before entering the eye. 

Satisfying the property of superposition means that any given color, or point in our 3D subspace, can be uniquely represented as a linear combination of three linearly independent vectors in the subspace. The linearly independent vectors correspond to primary colors – they are the projections of the primary colors on to the 3D subspace. This explains why any color we can perceive can be constructed by adding together different intensities of red, green, and blue light.

### 2-4 Color-Matching Experiments

Matching a color to a combination of its primary constituents has practical value because it enables accurate representation and reproduction of the color. It is possible to do color-matching empirically without knowing the projections of the primary colors on to the 3D subspace. To see how this is done, consider the experimental setup in Figure 2.2.

<center>
<div>
  <img src="https://i.imgur.com/76XltFR.png">
  <div class="figcaption"><b>Figure 2.2.</b> Color-matching experimental setup, adapted from Color in Business, Science, and Industry, Judd and Wyszecki, Wiley, 1975   <br></br>    
  </div>
</div>
</center>

In the experiment, the subject views a bipartite field. The left half of the field is illuminated by the test light T, which is the target color we are trying to match. The right half is illuminated by a combination of primary color sources R, G, and B, with adjustable intensities. The surround field is a neutral gray background of controlled brightness so that color perception is not affected by visual adaptation or surrounding colors. By adjusting the intensities of the primary sources, the subject matches the combination of the primary colors to the test color, obtaining a representation of the test color in terms of its primary constituents.

For certain test colors, however, it is not possible to match the color by adjusting the primary intensities as positive values. To see why this is the case, consider a hypothetical 2-dimensional color subspace. In this subspace, every color, or point in the subspace, can be represented as a linear combination of the projections \\(P_1\\) and \\(P_2\\) of two primary colors.

<center>
<div>
  <img src="https://i.imgur.com/ZUCjBN1.png">
  <div class="figcaption"><b>Figure 2.3.</b>  2-D color subspace with primary colors P<sub>1</sub> and P<sub>2</sub> and test colors T<sub>1</sub> and T<sub>2</sub><br></br>    
  </div>
</div>
</center>

In Figure 2.3(a), we have a test color \\(T_1\\) that can be expressed as a linear combination of \\(P_1\\) and \\(P_2\\). Since we can only add positive intensities of primary light, we are limited to representing the points in the shaded part of the graph. In particular, a test color \\(T_2\\) as shown in Figure 2.3(b) cannot be represented in this way because it requires a negative component of \\(P_2\\).

To get around this limitation, we again fall back on the principle of linearity and observe that **subtracting a color** from one side of the vector equation is equivalent to adding it to the other side. In Figure 2.3(b), we could add a \\(P_2\\) component to \\(T_2\\) to bring it back into the shaded area.  Figure 2.4 shows a modified experimental setup where the red primary light is added to the test side, giving a subtractive effect.

<center>
<div>
  <img src="https://i.imgur.com/w6900y1.png">
  <div class="figcaption"><b>Figure 2.4.</b>  Color-matching experiment with negative primary color<br></br>    
  </div>
</div>
</center>

In this setup, the subject adjusts the green and blue intensities on the primaries side and the red intensity on the “negative” test side to achieve color matching.

In summary, to measure a color we need to **choose a set of three primary colors** and **determine how much of each primary** needs to be added to our signal to match the test light. The key goal is to have the **same L/M/S responses**. Even if the color spectrums are different, the human eye will perceive the colors to be the same as long as the L/M/S responses are the same. 

<a name='color_constancy'></a>
## 3 Color Constancy

Color constancy refers to the percieved color of a surface remaining constant despite changes in illumination. Failure in color constancy can result in identical RGB values yielding different color percepts and different RGB values yielding identical color percepts.

### 3-1 Color Perception Inconsistencies

These inconsistencies in color perception arise from the inability to directly infer surface reflectance from image luminance. As we can see from the equation for calculating luminance,
$\text{Luminance(L)} = \text{Reflectanc(R)} \cdot \text{Illumination(I)}$
given a luminance, the reflectance solution is underconstrained due to the illumination variable. Thus, assumptions are required in order to have a unique solution for reflectance. However, as shown in Figure 3.1, different assumptions yield different reflectences.
<center>
<div>
  <img src="https://i.imgur.com/UnTY1pH.png">
  <div class="figcaption">
      <b>Figure 3.1.</b> 
          Reflectance can yield multiple solutions for a constant Luminance           depending on the perceived illumination.<br></br>  
  </div>
</div>
</center>

This is why we perceive the right square to be lighter than the left square in despite being the same gray level in Figure 3.2.

<center>
<div>
  <img src="https://i.imgur.com/o2K7Jh7.png"
>
  <div class="figcaption">
      <b>Figure 3.2.</b> Squares with same gray level are perceived to be different due to surrounding information.<br></br>  
  </div>
</div>
</center>

### 3-2 Luminance Perception at Edges

Assumptions that affect our perception of reflectence seem to be strongly dependent on edges or sharp changes in gradients. This can be seen in the Craik-O'Brien-Cornsweet Illusion shown in Figure 3.3. The existence of the edge and the added contrast cause us to make an assumption about the illuminace of the bottom object being lower, thus making the reflectence appear brighter.

<center>
<div>
  <img src="https://i.imgur.com/uVHeC6b.png"
>
  <div class="figcaption">
      <b>Figure 3.3.</b> In the left image, the top object appears to be darker than the bottom; however, in the right image, once we ignore the edge  contrast, it becomes clear that the top and bottom objects are the same color.<br></br>  
  </div>
</div>
</center>


### 3-3 Retinex Theory

How can we infer reflectance from luminance? To explain this, E.H. Land and J.J. McCann proposed the Retinex Theory.

---
#### Retinex Assumptions:
1. All surfaces exist in a flat world.
2. Surface reflectance always changes abruptly.
3. No sharp changes in illumination.

---
Taking these assumptions to be true, all sharp luminance variations must be caused by changes in the reflectance of the surface. Conversely, all gradual luminance variations must be caused by changes in illumination.

**Abrupt Changes in Luminance -> Changes in Reflectance**
**Gradual Changes in Luminance -> Changes in Illumination**

Therefore, a Retinex color perception system needs to discard small changes in luminance. We can determine the abruptness of a change in luminance by differentiating the luminance input. We can then threshold to exclude small values and integrate the result to get back the reflectance.

<center>
<div>
  <img src="https://i.imgur.com/xexr9I4.png">
  <div class="figcaption"><b>Figure 3.4.</b>  Computing Surface Reflectance Using Retinex<br></br>    
  </div>
</div>
</center>

### 3-4 Color Perception in Three Dimensions

Retinex relies on the assumption of a flat world. Therefore, there are many visual phenomena that cannot be explained by Retinex, such as Knill and Kersten's illusion, illustrated below. This illusion consists of two halves, where the left is darker than the right. The difference in shading is immediately perceptible when the two halves are shown as the front faces of adjacent cubes. However, when applied to adjacent cylinders, the difference in color is imperceptible. Here, the difference in color perception is being caused by the brain's interpretation of 3D shapes. The surface normal where the two cylinders meet can partially explain the difference in luminance between them. Since the two cubes are flush, the brain has no prior expectation of a difference in luminance.

<center>
<div>
  <img src="https://i.imgur.com/w5dw5yW.png">
  <div class="figcaption"><b>Figure 3.5.</b>  In this illusion, the left half is always darker than the right half <br></br>    
  </div>
</div>
</center>

In a 3D environment, it is difficult to determine whether a change in luminance for a given surface is caused by a change in orientation or a change in reflectance. This can be approached by segmenting the 3D object into flat faces, as seen below, and applying Retinex to each face. However, this approach requires a good understanding of the geometry of the object.

<center>
<div>
  <img src="https://i.imgur.com/RV4CgGh.png">
  <div class="figcaption"><b>Figure 3.6.</b>  Approach for 3D color perception <br></br>    
  </div>
</div>
</center>

