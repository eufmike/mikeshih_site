---
title: "Point Pattern Analysis (Ripley's K)"
date: 2020-04-14T14:44:08-05:00
draft: true
---

As the usage of Airyscan increases, a type of super-resolution microscopy, more and more researchers are trying to take advantage of its resolution, combined with new organelle markers (MitoTracker or LysoTracker), to extract some information from their geographical distribution. While lacking the tool for spatial analysis, Ripley's K function can come in handy in this type of study. It is a standard geostatistical tool that has been widely used in ecology and geography. Despite being a stranger to most biologists, Ripley's K function and its derivatives are quite popular for analyzing data collected from Single-Molecule localization Microscopies (SMLM), such as stochastic optical reconstruction microscopy (STORM) or photoactivated localization microscopy (PALM). 

Interestingly, Ripley's K function was originally developed for Dr. Francis Crick's challenge of measuring cell clustering. It will be nice to see it finds its way home. 

# Point Patterns: testing note

## Getis & Franklin’s point pattern analysis
Second-Order Neighborhood Analysis

### Background
* This note documents materials required for Getis & Franklin’s point pattern analysis. This method has been used in several papers to describe and create density map for STORM dataset. 
* The analytic method was originally published in 1987 on *Ecology*, and later reprinted in the book titled ”*Perspectives on Spatial Data Analysis*”.  
* The incentive of building this method, was to provide a tool for ecologists and geographers, to quantify targets with flexibility in scale. 
* It was designed for a remote sensing study of canopy reflectance for a ponderosa pine (*Pinus ponderosa*) forest.
* People used to call the method Getis & Franklin’s method, but its actual name is “Second-Order Neighborhood Analysis”. 


### Note
* “Perhaps blocking, or contiguous quadrat analysis, is the most common method used for examining grain of pattern.”

#### Contiguous quadrat analysis
Quadrat (樣方，方區): A quadrat is a frame, traditionally square, used in ecology and geography to isolate a standard unit of area for study of the distribution of an item over a large area. 
[Example for contiguous quadrat analysis](https://www.omicsonline.org/cmeias-quadrat-maker-a-digital-software-tool-to-optimize-grid-2157-7625.1000136.php?aid=18461)
![](https://i.imgur.com/sHvcY6N.png)


#### Spectral analysis
[Spectral density estimation - Wikipedia](https://en.wikipedia.org/wiki/Spectral_density_estimation)
[Kernel density estimation - Wikipedia](https://en.wikipedia.org/wiki/Kernel_density_estimation)

#### The model
$$
\hat{L}_i(d)= \Biggl[A\sum_{j=1}^n\frac{K_{ij}}{\pi(n-1)}\Biggr]^\frac{1}{2}
$$

This function is an modified function from Ripley's K, and returns  $\hat{L}_i(d)$ for individual points. 

![](https://i.imgur.com/e3HzTA0.png)

By plotting each point with its value in isoline, these are the plot:
![](https://i.imgur.com/uwiD1uP.png)

### Compare Getis and Franklin's Function with Ripley's K Function

#### Getis and Franklin's Function
$$
\hat{L}_i(d)= \Biggl[A\sum_{j=1}^n\frac{K_{ij}}{\pi(n-1)}\Biggr]^\frac{1}{2}
$$

$K_{ij}$: If for a given neighborhood point j the specified distance d is more than the distance between i and j, then the pair (kij ) counts as 1 (unless the boundary correction is required); otherwise kij counts 0.

Edge correction: 
* if the distance of between $i$ and $j$ is greater than the distance between $i$ and the nearest boundary:

$$K_{ij} = \biggl[1-\frac{\cos^{-1}(\frac{e_1}{d})}{\pi}\biggr]^{-1}$$

* if the distance of between $i$ and $j$ is greater than the distance to both of two boundaries $(e_1, e_2)$, use: 

$$K_{ij} = \biggl\{1-\frac{\cos^{-1}(\frac{e_1}{d}+\cos^{-1}(\frac{e_2}{d})+\frac{\pi}{2} )}{2\pi}\biggr\}^{-1}$$

#### Ripley's K Function
$$
\hat{K}(d)= \hat{\lambda}^{-1}\sum_{i}\sum_{j\neq1}\frac{\omega(l_i, l_j)I(d_{ij<t})}{N}
$$

Edge correction is controlled by $\omega$

Note: These two functions are similar because $K_{ij}$ and $I(d_{ij<t})$ are  the same. 

* In Ripley's K funtion, if the first sigma is ignored, it can also return $\hat{K}(d)$ for each spot with doing averaging. $\hat{\lambda}^{-1}$ is the estimated density, so it equals to ${A}/{N}$. When it describes a single spot, $N$ = 1. 

* In G&F's funtion, $\pi$ can be moved outside the sigma because it is a constant.

Which means, when we describe a single spot without edge correction, Getis and Franklin's Function looks like this:
$$
\hat{L}_i(d)= \Biggl[\frac{A}{\pi}\sum_{j=1}^n\frac{K_{ij}}{(n-1)}\Biggr]^\frac{1}{2}
$$

Ripley's K Function looks like this:
$$
\hat{K}_i(d)= A\sum_{j\neq1}\frac{I(d_{ij<t})}{N}
$$

Since $$\sum_{j=1}^n\frac{1}{(n-1)}$$

and $$\sum_{j\neq1}\frac{1}{N}$$

are the same, it is not hard to find that G&F's function is just a type of Ripley's K Function but divided by $\pi$ and sqare rooted, in order to keep the data linear. Getis's method is 



### Code in R
In R, we can use the `localL` funtion in `spatstat` to achive Getis's method. The problem is `localL` forces to run through the whole dataset. It is less flexible, and took significantly amount of time to run through hundred thousand of points. 


### Code in Python 
Rethink the code I have. 



```

file	time	version
0	P_ThomasPP_20	0.393422	ripleyk_v2
1	P_ThomasPP_20	1.751421	ripleyk_v3
2	P_ThomasPP_20	0.397242	ripleyk_v4
3	P_ThomasPP_256	891.318586	ripleyk_v4
4	P_ThomasPP_256	883.690282	ripleyk_v2
```





### Reference
* Williamson, D. J., Owen, D. M., Rossy, J., Magenau, A., Wehrmann, M., Gooding, J. J., & Gaus, K. (2011). Pre-existing clusters of the adaptor Lat do not participate in early T cell signaling events. *Nature Immunology*, *12*(7), 655–662. http://doi.org/10.1038/ni.2049
[Link to my paper3 database](papers3://publication/doi/10.1038/ni.2049)

* Bálint, Š., Lopes, F. B., & Davis, D. M. (2018). A nanoscale reorganization of the IL-15 receptor is triggered by NKG2D in a ligand-dependent manner. *Science Signaling*, *11*(525), eaal3606. http://doi.org/10.1126/scisignal.aal3606
[Link to my paper3 database](papers3://publication/doi/10.1126/scisignal.aal3606)

* Ripley, B. D. (1977). Modelling spatial patterns (with discussion). JR Statist. Soc. B, 39, 172-212.(1981) Spatial Statistics.
[Link to my paper3 database](papers3://publication/uuid/45A4FFCA-990E-4FEE-B12E-4456C3C3653C)

* Getis, A. (1984). Interaction Modeling Using Second-Order Analysis. Environment and Planning A, 16(2), 173–183. http://doi.org/10.1068/a160173
[Link to my paper3 database](papers3://publication/doi/10.1068/a160173)

* Getis, A., Franklin, J. (1987) Second-Order Neighborhood Analysis of Mapped Point Patterns. Ecology 68:473-477. Reprinted with permission of The Ecological Society of America, Washington DC
[Link to my paper3 database](papers3://publication/doi/10.1007/978-3-642-01976-0_7)

* Getis, A., & Franklin, J. (2008). Second-Order Neighborhood Analysis of Mapped Point Patterns. In *Perspectives on Spatial Data Analysis* (pp. 93–100). Berlin, Heidelberg: Springer Berlin Heidelberg. http://doi.org/10.1007/978-3-642-01976-0_7
[Link to my paper3 database](papers3://publication/uuid/D2CC985A-F970-4E38-A220-C5EE00E1B5FA)

## Book & Other Resource

Books for Spatial statistics
* [references - Learning Spatial Statistics? - Geographic Information Systems Stack Exchange](https://gis.stackexchange.com/questions/48754/learning-spatial-statistics)
* R code: [Point Patterns: Hypothesis Testing](http://rstudio-pubs-static.s3.amazonaws.com/5292_2b2fae3795a144b2a4b486fd2fc6fc57.html) 
* MATLAB tool:  [GitHub - quokka79/ClusterFields: Getis & Franklin Local Point Pattern Analysis for Localisation Microscopy Images](https://github.com/quokka79/ClusterFields)




## Statistical Concepts
### The order statistic
不是很容易找到有關定義Order Statistics的資料，無法確定是個慣用法還是有明確的出處。基本上1st跟2nd order statistics指的是first and second moments，包含arithmetic mean（算術平均數）跟variance（變異數）。
[Introducing Higher Order Statistics (HOS)](http://www1.maths.leeds.ac.uk/applied/news.dir/issue2/hos_intro.html)

moment [矩](https://zh.wikipedia.org/wiki/%E7%9F%A9_(%E6%95%B8%E5%AD%B8))
[Moment (mathematics) - Wikipedia](https://en.wikipedia.org/wiki/Moment_(mathematics))



Statistical dispersion（離散程度）

## Edge Correction
orrection=c("border", "isotropic", "Ripley", "translate")

Ripley: 

border:

### Interpolation
matlab: v4
biharmonic spline interpolation
https://www.mathworks.com/help/curvefit/interpolation-methods.html
http://www.fon.hum.uva.nl/praat/manual/biharmonic_spline_interpolation.html
Someone suggest this method for python:
https://mail.python.org/pipermail/scipy-dev/2014-July/019952.html
https://scipy.github.io/old-wiki/pages/Cookbook/RadialBasisFunctions.html

## Ripley's K Function and derivative

1. Ripley's K-function
$$
\hat{K}(r)= \hat{\lambda}^{-1}\sum_{i}\sum_{j\neq1}\frac{\omega(l_i, l_j)I(d_{ij<r})}{N}
$$
2. L-function: a normalization proposed by Besag
$$
\hat{L}(r)=\sqrt{\frac{\hat{K}(r)}{\pi}}
$$
3. H-function: also called $L(r)-r$
$$
\hat{H}(r)=
$$