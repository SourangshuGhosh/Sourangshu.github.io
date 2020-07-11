## Welcome to My Page

1. **Solution of Three Dimensional Isotropic/Anisotropic Seismic Wave Equation**

![](https://raw.githubusercontent.com/SourangshuGhosh/SourangshuGhosh.github.io/master/Blogs/Schematic-of-perfectly-matched-layer.png)
<br />One of the most popular methods to simulate numerically the seismic wave propagation in an elastic medium is the finite difference method. In the context of numerically modelling in unbounded medium, the wave needs to be absorbed at the artificial boundaries of the computational domain and therefore it is necessary to define non-reflecting conditions at these boundaries to mimic an unbounded medium.

The Perfectly Matched Layer(PML) has the remarkable property of having a zero reflection coefficient for all angles of incidence and all frequencies before discretezition and has become widely used( eg Collino and Tsogka 2001). However the reflection coefficient is not zero anymore after the discretezition and becomes even very large at grazing incidence. Therefore an improved version of the PML condition has been developed: the convolution perfectly matched layer condition(CPML) (e.g. Komatitisch and martin 2007). The repository developed is a similar implementation of this in Fortran.

### For More Details. 
Please click [here](https://sourangshughosh.github.io/Blogs) <br>
The links to the Github Repository is[https://github.com/SourangshuGhosh/SeismicAnalyzer](https://github.com/SourangshuGhosh/SeismicAnalyzer)
