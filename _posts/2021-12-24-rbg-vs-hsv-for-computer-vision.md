---
layout: post
title: "RGB v. HSV for Computer Vision"
excerpt: "Computer vision is an interdisciplinary scientific field that deals with how computers can be made to gain high-level understanding from digital images or videos. If we consider Digital images then it can be represented in different color space and models. The most common model us RBG but is many cases it fails to perform well over other models."
categories: [Computer Vision, Color Space]
tags: [CV, RGB]
share: true
comments: true
mathjax: false
---

Computer vision is an interdisciplinary scientific field that deals with how computers can be made to gain high-level understanding from digital images or videos. If we consider Digital images then it can be represented in different color space and models. The most common model us RBG but is many cases it fails to perform well over other models.

So, let us explore why I think HSV and HVL performs better over RGB color space for Computer Vision applications.

## What is RGB?

RGB is an [additive](https://en.wikipedia.org/wiki/Additive_color) [color model](https://en.wikipedia.org/wiki/Color_model) in which **R**ed, **G**reen and, **B**lue are added to create whole range of colors.

Range for RGB is:-

Red: [0, 255]

Green: [0, 255]

Blue: [0, 255]

![](rgb_1.png)
<center>RGB Color Model (Source: <a href="https://en.wikipedia.org/wiki/RGB_color_model#/media/File:AdditiveColor.svg">Wikipedia</a>)</center>

For simplicity, we can consider the RGB color space as a cube as it can be represented 3D Coordinate system.

![](rgb_2.png)
<center>RGB Color Cube (Source: <a href="https://en.wikipedia.org/wiki/Color_model#/media/File:RGBCube_a.svg">Wikipedia</a>)</center>

There are other popular color models under **additive and subtractive models** such as [CYMK color model](https://en.wikipedia.org/wiki/CMYK_color_model) which is a subtractive model. Another kind of color model is **Cylindrical-coordinate color models**

## What is HSV?

HSV stands for **H**ue, **S**aturation and **V**alue, and it is designed in a way such that it is more closely align with the way human vision perceives color-making attributes.

![](rgb_3.png)
<center>Cylindrical Model for HSV (Source: <a href="https://en.wikipedia.org/wiki/HSL_and_HSV#/media/File:HSV_color_solid_cylinder_saturation_gray.png">Wikipedia</a>)</center>

OpenCV uses the following ranges to represent each of the parameters in the HSV spectrum:-

Hue: [0, 179]

Saturation: [0, 255]

Value: [0, 255]

Similar to HSV we have some HSL i.e. **H**ue, **S**aturation and **L**ightness

![](rgb_4.png)
<center>Cylindrical Model for HSL (Source: <a href="https://en.wikipedia.org/wiki/HSL_and_HSV#/media/File:HSL_color_solid_cylinder_saturation_gray.png">Wikipedia</a>)</center>

A basic representation how HSL and HSV is derived from RGB model

![](rgb_5.png)
<center>The geometric derivation of the cylindrical HSL and HSV representations of an RGB "colorcube" (Source: <a href="https://en.wikipedia.org/wiki/HSL_and_HSV#/media/File:Hsl-and-hsv.svg">Wikipedia</a>)</center>

## Why HSV & HSL performs better than RGB for Computer Vision?

Color is a perception based on electromagnetic waves. Natural properties of these waves are, for example intensity, frequency and wavelength. If we sweep the frequency of a light spectrum from infrared to ultraviolet, we would visually perceive a color variation along the rainbow colors those are the colors that human see and differentiate. Those colors could be considered as "pure colors" because they are represented by single-frequency waves.

Now, the human eye can only respond, or "resonate" to three main light frequencies(Red, Green, Blue). The fact is that this response is non-linear, so the retina can distinguish a given pure color/frequency by the combined response of the three color components using [Young–Helmholtz theory](https://en.wikipedia.org/wiki/Young%E2%80%93Helmholtz_theory).

The RGB color space replicates the inner workings of human [retina](http://www.color-theory-phenomena.nl/05.00.html), so that a vast range of colors can be represented on electronic displays by means of a convenient (from a computer point of view) [24 bits-per-pixel color coding](https://www.cambridgeincolour.com/tutorials/bit-depth.htm). The RGB color space has neither any fundamental relation to the natural color properties, nor to human interpretation of color.

Since these coordinates map to implementation rather to the physical, "real nature" properties of color, they are not suited to perform some mathematical processing, e.g. perceptually linear gradient interpolation, color correction, brightness and saturation ops, etc.

I feel any arithmetical operation performed channel-wise in RGB space gives very crude or even plainly misleading results. That's why I feel it is best to create colormaps by [converting the color stops from RGB to other color spaces](https://www.ryanjuckett.com/rgb-color-space-conversion/) (HLS, [Lab](https://en.wikipedia.org/wiki/CIELAB_color_space), etc.), performing the interpolations, then converting the interpolated values back to RGB.

Unlike RGB, HSV and HSL separates luma, or the image intensity, from chroma or the color information. This is very useful in many places like eg., if we want to perform histogram equalization of a color image, we probably want to do that only on the intensity component, and leave the color components untouched. Otherwise, we will get unexpected and strange colors.

> I feel it is beneficial to separate/differentiate the luma from the chroma for any color space. The luma varies greatly in the scene based on the amount of light falling on the object as it gives the luminosity. Chroma, on the other hand, correlates better with the object's intrinsic properties, and for properly white-balanced images is more-or-less invariant.

## Reference

1)  [https://www.vocal.com/video/rgb-and-hsvhsihsl-color-space-conversion/](https://www.vocal.com/video/rgb-and-hsvhsihsl-color-space-conversion/)

2) [https://www.red.com/red-101/cinema-color-management](https://www.red.com/red-101/cinema-color-management)

3) [http://coecsl.ece.illinois.edu/ge423/spring05/group8/FinalProject/HSV_writeup.pdf](http://coecsl.ece.illinois.edu/ge423/spring05/group8/FinalProject/HSV_writeup.pdf)

---

<center>SAME POST AT :: <a href="https://labs.imaginea.com/novel-corona-virus-sequence-alignment/">Imaginea Labs</a></center>
