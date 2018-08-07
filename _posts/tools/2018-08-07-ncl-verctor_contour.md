---
layout: blog
tools: true
title: "NCL"
background-image: https://www.ncl.ucar.edu/Images/NCLLogoWeb.jpg
date:  2018-06-22 10:13:56
category: tools
tags:
- tools
- NCL
- plot
---



----

<a href="http://www.ncl.ucar.edu/Applications/lcnative.shtml" title="NCL"> Lambert Conformal Native Grid Projections</a>

[script](http://www.ncl.ucar.edu/Applications/Scripts/lcnative_overlay_5.ncl) 
[/script1](http://www.ncl.ucar.edu/Applications/Scripts/lcnative_5.ncl)

Vectors on a scalar field. This example shows two ways of overlaying vectors on a color scalar field.
One way is to use the "all-in-one" function called gsn_csm_vector_scalar_map.

The second way is to create the vector and contour plots separately using gsn_csm_contour_map and gsn_csm_vector, and then overlay them with overlay. This second method is the recommended one, as it allows more control over individual plots.

![pic1](http://www.ncl.ucar.edu/Applications/Images/lcnative_5_sm.png)


