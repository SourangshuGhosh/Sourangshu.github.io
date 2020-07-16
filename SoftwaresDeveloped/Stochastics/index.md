## Welcome to My Page

## List of Softwares Developed by Me
Below is a list of softwares that I have developed in **Stochastic Processes and its application**. They are either used in my project works under various professors or was solely done by me due to my own interest on that topic. Please feel free to contact me if you found any bug or problem existing in the repositories listed below. Each of the repositories are explained in more **details** in a seperate page whose Link are given below each of them respectively.

1. **Stochastic Reactive Brownian Dynamics**

![](https://raw.githubusercontent.com/SourangshuGhosh/SourangshuGhosh.github.io/master/Pictures/SRBD.jpg)
<br />We develop a Split Reactive Brownian Dynamics (SRBD) algorithm for particle simulations of reaction-diffusion systems based on the Doi or volume reactivity model, in which pairs of particles react with a specified Poisson rate if they are closer than a chosen reactive distance. In our Doi model, we ensure that the microscopic reaction rules for various association and dissociation reactions are consistent with detailed balance (time reversibility) at thermodynamic equilibrium. The SRBD algorithm uses Strang splitting in time to separate reaction and diffusion, and solves both the diffusion-only and reaction-only subproblems exactly, even at high packing densities. To efficiently process reactions without uncontrolled approximations, SRBD employs an event-driven algorithm that processes reactions in a time-ordered sequence over the duration of the time step. A grid of cells with size larger than all of the reactive distances is used to schedule and process the reactions, but unlike traditional grid-based methods such as Reaction-Diffusion Master Equation (RDME) algorithms, the results of SRBD are statistically independent of the size of the grid used to accelerate the processing of reactions. We use the SRBD algorithm to compute the effective macroscopic reaction rate for both reaction- and diffusion-limited irreversible association in three dimensions, and compare to existing theoretical predictions at low and moderate densities. We also study long-time tails in the time correlation functions for reversible association at thermodynamic equilibrium, and compare to recent theoretical predictions. Finally, we compare different particle and continuum methods on a model exhibiting a Turing-like instability and pattern formation. Our studies reinforce the common finding that microscopic mechanisms and correlations matter for diffusion-limited systems, making continuum and even mesoscopic modeling of such systems difficult or impossible. We also find that for models in which particles diffuse off lattice, such as the Doi model, reactions lead to a spurious enhancement of the effective diffusion coefficients.

The links to the Github Repository is [https://github.com/SourangshuGhosh/Stochastic\_Reactive\_Brownian\_Dynamics](https://github.com/SourangshuGhosh/Stochastic_Reactive_Brownian_Dynamics)

2.  **Bayesian Belief Networks**

Belief networks are popular tools for encoding uncertainty in expert systems. These networks rely on inference algorithms to compute beliefs in the context of
observed evidence. One established method for exact inference on belief networks is the **Probability Propagation in Trees of Clusters (PPTC) algorithm**, as developed by Lauritzen and Spiegelhalter and refined by Jensen et al. PPTC converts the belief network into a secondary structure, then computes probabilities by manipulating the secondary structure.  PyBBN is Python library for Bayesian Belief Networks (BBNs) exact inference using the junction tree algorithm or **Probability Propagation in Trees of Clusters**. The implementation is taken directly from C. Huang and A. Darwiche, "Inference in Belief Networks: A Procedural Guide," in International Journal of Approximate Reasoning, vol. 15, pp. 225--263, 1999. Additionally, there is the ability to generate singly- and multi-connected graphs, which is taken from JS Ide and FG Cozman, "Random Generation of Bayesian Network," in Advances in Artificial Intelligence, Lecture Notes in Computer Science, vol 2507. There is also the option to generate sample data from your BBN. This synthetic data may be summarized to generate your posterior marginal probabilities and work as a form of approximate inference. Lastly, we have added Pearl's do-operator for causal inference.

The links to the Github Repository is [https://github.com/SourangshuGhosh/py-bbn](https://github.com/SourangshuGhosh/py-bbn)

3.  **Bayesian Optimization**

Bayesian optimization is a method of finding the maximum of expensive cost functions. Bayesian optimization employs the Bayesian technique of setting a prior over the objective function and combining it with evidence to get a posterior function. This permits a utility-based selection of the next observation to make on the objective function, which must take into account both exploration (sampling from areas of high uncertainty) and exploitation (sampling areas likely to offer improvement over the current best observation). Bayesian optimization techniques are some of the most efficient approaches in terms of the number of function evaluations required (see, e.g. [Moˇckus, 1994,Jones et al., 1998, Streltsov and Vakili, 1999, Jones, 2001, Sasena, 2002]). Much of the efficiency stems from the ability of Bayesian optimization to incorporate prior belief about the problem to help direct the sampling, and to trade off exploration and exploitation of the search space. It is called Bayesian because
it uses the famous “Bayes’ theorem”, which states (simplifying somewhat) that the posterior probability of a model (or theory, or hypothesis) M given evidence (or data, or observations) E is proportional to the likelihood of E given M multiplied by the prior probability of M. BayesianOptimization.jl is a code written in Julia to implement the Bayesian OPtimization technique. 

The links to the Github Repository is [https://github.com/SourangshuGhosh/BayesianOptimization.jl](https://github.com/SourangshuGhosh/BayesianOptimization.jl)

4. **AbstractGPs**

AbstractGPs.jl is a package that defines a low-level API for working with Gaussian processes (GPs), and basic functionality for working with them in the simplest cases. As such it is aimed more at developers and researchers who are interested in using it as a building block than end-users of GPs. This pakage is written entirely in Julia. 

![GP](https://raw.githubusercontent.com/SourangshuGhosh/AbstractGPs.jl/master/gp.gif)

The links to the Github Repository is [https://github.com/SourangshuGhosh/AbstractGPs.jl](https://github.com/SourangshuGhosh/AbstractGPs.jl)

5.  **Variational Inference for Stochastic Differential Equations**

Parameter inference for stochastic differential equations is challenging due to the presence of a latent diffusion process. Working with an Euler-Maruyama discretisation for the diffusion, we use variational inference to jointly learn the parameters and the diffusion paths. We use a standard mean-field variational approximation of the parameter posterior, and introduce a recurrent neural network to approximate the posterior for the diffusion paths conditional on the parameters. This neural network learns how to provide Gaussian state transitions which bridge between observations in a very similar way to the conditioned diffusion process. The resulting black-box inference method can be applied to any SDE system with light tuning requirements. This code is a Tensorflow implementation of the Lotka-Volterra example detailed in Black-box Variational Inference for Stochastic Differential Equations (ICML, 2018), by Tom Ryder, Andy Golightly, Stephen McGough and Dennis Prangle.

#### Visualisation
By saving the paths produced in training (not something the model will presently do by default), we can watch the model learn the latent diffusion process:
![](https://raw.githubusercontent.com/SourangshuGhosh/VIforSDEs/master/figs/LV_paths.gif)


