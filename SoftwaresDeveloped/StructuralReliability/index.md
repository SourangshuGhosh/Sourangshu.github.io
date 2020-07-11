## Welcome to My Page

## List of Softwares Developed by Me
Below is a list of softwares that I have developed by me in **Structural Reliability**. They are either used in my project works under various professors or was solely done by me due to my own interest on that topic. Please feel free to contact me if you found any bug or problem existing in the repositories listed below. Each of the repositories are explained in more **details** in a seperate page whose Link are given below each of them respectively.

1. **FORM( First Order Reliability Methods)**

![](https://raw.githubusercontent.com/SourangshuGhosh/SourangshuGhosh.github.io/master/Pictures/FORM.jpg)
<br />The first-order reliability method (FORM) has been widely used in structural reliability estimation applications. The method involves Taylor expansion of the failure function, i.e. the linearization of the limit state equation, not performed around the mean value of the function, but at a point that is called the &#39;most probable failure point&#39;. The selection of an appropriate linearization point is an important consideration (Ang and Tang, 1984), and actually leads to an iterative solving procedure.

Based on the underlying theory and adopting the method proposed by Hasofer and Lind, the following is a summary of the selection procedure. The process starts with the transformation of the non-normal variables to standard normal variables with zero mean and unit variance (Madsen _et al.,_ 1986), using the Rosenblatt transformation (see also Ang and Tang, 1984). The target is to find the most probable failure point, i.e. the point on the failure locus that defines the minimum distance of the limit state surface from the origin in the space of the reduced variables (Shinozuka, 1983). The shortest distance between the failure surface and the origin in the space of the reduced variables is called the reliability index _β_.

The point on the failure surface that has the minimum distance from the origin can be found by using, for example, the method of Lagrange multipliers (Ang and Tang, 1984), following an iterative procedure. Given that _β_ is now available, the failure probability of the system can be approximated by:

Pf=Φ−β

where Φ(–_β_) is the cumulative distribution of the standard normal variate (Madsen _et al.,_1986).

For linear failure functions this solution is exact. For non-linear failure functions, as in the case of the failure function of a composite material layer, the exact calculation of the failure probability or the reliability generally involves mathematical and computational difficulties. Following the reviews by, for example, Eamon _et al._ (2005) and Schueller _et al._ (2004), of various structural reliability methods and their accuracy and effectiveness in solving problems based on the number of random variables and the linearity (or not) of the failure function, FORM can be seen to have limitations for non-linear failure functions having a large number of random variables.

Several algorithms have been proposed for the approximation of the most probable failure point and the _β_ index (see e.g. Ang and Tang, 1984; Madsen _et al.,_ 1986). In a comparison between five algorithms that can be used for the approximation of the most probable failure point (Liu and Der Kiureghian, 1991), the general conclusion is that the decision as to which is the most effective algorithm depends on the failure function of interest. Similarly, in Wang and Grandhi (1994) a new search algorithm is proposed for the estimation of the _β_ index, and its application is compared with other widely used algorithms. An iterative algorithm already applied for composite laminates is described in Madsen _et al._ (1986). However, when a limit state function is not unimodal, that is, if there is more than one local minimum, it is not certain that the global minimum will be obtained. In fact the failure function as described in the previous section is multi-modal (Miki _et al.,_ 1990), and therefore the search algorithm might need modifications. Still, there is no guarantee that the algorithm will converge in all cases, and it is likely that when it is being applied it will produce, for the basic variables, values that are outside of their natural limits (Madsen _et al.,_ 1986).

The links to the Github Repository is[https://github.com/SourangshuGhosh/FORM](https://github.com/SourangshuGhosh/FORM)

