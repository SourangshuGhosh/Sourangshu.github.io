\\chapter{Perfectly Matched Layer \\label{chap:pml}}

%\\setcounter{page}{1}

\\renewcommand{\\thefootnote}{\\fnsymbol{footnote}}

\\footnotetext[2]{Lecture notes by John Schneider.  {\\tt

fdtd-pml.tex}}

\\section{Introduction}

The perfectly matched layer (PML) is generally considered the

state-of-the-art for the termination of FDTD grids.  There are some

situations where specially designed ABC's can outperform a PML, but

this is very much the exception rather than the rule.  The theory

behind a PML is typically pertinent to the continuous world.  In the

continuous world the PML should indeed work \`\`perfectly'' (as its

name implies) for all incident angles and for all frequencies.

However, when a PML is implemented in the discretized world of FDTD,

there are always some imperfections (i.e., reflections) present.

There are several different PML formulations.  However, all PML's

essentially act as a lossy material.  The lossy material, or lossy

layer, is used to absorb the fields traveling away from the interior

of the grid.  The PML is anisotropic and constructed in such a way

that there is no loss in the direction tangential to the interface

between the lossless region and the PML (actually there can be loss in

the non-PML region too, but we will ignore that fact for the moment).

However, in the PML there is always loss in the direction normal to

the interface.

The PML was originally proposed by J.-P. B\\'{e}renger in 1994.  In

that original work he split each field component into two separate

parts.  The actual field components were the sum of these two parts

but by splitting the field B\\'{e}renger could create an (non-physical)

anisotropic medium with the necessary phase velocity and conductivity

to eliminate reflections at an interface between a PML and non-PML

region.  Since B\\'{e}renger first paper, others have described PML's

using different approaches such as the complex coordinate-stretching

technique put forward by Chew and Weedon, also in 1994.

Arguably the best PML formulation today is the Convolutional-PML

(CPML).  CPML constructs the PML from an anisotropic, dispersive

material.  CPML does not require the fields to be split and can be

implemented in a relatively straightforward manner. 

Before considering CPML, it is instructive to first consider a simple

lossy layer.  Recall that a lossy layer provided an excellent

ABC for 1D grids.  However, a traditional lossy layer does not work in

higher dimensions where oblique incidence is possible.  We will

discuss this and show how the split-field PML fixes this problem.

\\section{Lossy Layer, 1D}

A lossy layer was previously introduced in Sec.\\ \\ref{sec:loss}.  Here

we will revisit lossy material but initially focus of the continuous

world and time-harmonic fields.  For continuous, time-harmonic fields,

the governing curl equations can be written

\\begin{eqnarray}

  \\nabla\\times\\Hvec &=&

    j\\omega\\epsilon\\Evec + \\sigma\\Evec \\,=\\,

    j\\omega\\left(\\epsilon - j\\frac{\\sigma}{\\omega}\\right)\\Evec
\\,=\\,

    j\\omega\\teps\\,\\Evec, \\\\

  \\nabla\\times\\Evec &=&

    -j\\omega\\mu\\Hvec - \\sigma\_m\\Hvec \\,=\\,

    -j\\omega\\left(\\mu - j\\frac{\\sigma\_m}{\\omega}\\right)\\Hvec
\\,=\\,

    -j\\omega\\tmu\\Hvec,

\\end{eqnarray}

where the complex permittivity and permeability are given by

\\begin{eqnarray}

  \\teps &=& \\epsilon - j\\frac{\\sigma}{\\omega}, \\\\

  \\tmu &=& \\mu - j\\frac{\\sigma\_m}{\\omega}.

\\end{eqnarray}

For now, let us restrict consideration to a 1D field that is

\$z\$-polarized so that the electric field is given by

\\begin{equation}

  \\Evec = \\unitvec{z} e\^{-\\gamma x} = \\unitvec{z} E\_z(x)

\\end{equation}

where the propagation constant \$\\gamma\$ is yet to be determined.

Given the electric field, the magnetic field is given by

\\begin{equation}

  \\Hvec = -\\frac{1}{j\\omega\\tmu} \\nabla\\times\\Evec

        = -\\unitvec{y}\\frac{\\gamma}{j\\omega\\tmu} E\_z(x).

\\end{equation}

Thus the magnetic field only has a \$y\$ component, i.e.,

\$\\Hvec=\\unitvec{y}H\_y(x)\$.

The characteristic impedance of the medium \$\\eta\$ is the ratio of the

electric field to the magnetic field (actually, in this case, the

negative of that ratio).  Thus,

\\begin{equation}

  \\eta = -\\frac{E\_z(x)}{H\_y(x)} = \\frac{j\\omega\\tmu}{\\gamma}.

  \\label{eq:almostEta}

\\end{equation}

Since \$\\gamma\$ has not yet been determined, we have not actually

specified the characteristic impedance yet.  To determine \$\\gamma\$ we

use the other curl equation where we solve for the electric field in

terms of the magnetic field we just obtained:

\\begin{equation}

  \\Evec = \\frac{1}{j\\omega\\teps}\\nabla\\times\\Hvec

        = \\frac{1}{j\\omega\\teps}

          \\frac{\\gamma\^2}{j\\omega\\tmu}e\^{-\\gamma x} \\unitvec{z}.

  \\label{eq:eEqualsE}

\\end{equation}

However, we already know the electric field since we started with that

as a given, i.e., \$\\Evec = \\exp(-\\gamma x)\\unitvec{z}\$.  Thus, in

order for \\refeq{eq:eEqualsE} to be true, we must have

\\begin{equation}

  \\frac{\\gamma\^2}{(j\\omega)\^2\\tmu\\teps} = 1,

\\end{equation}

or, solving for \$\\gamma\$ (and only keeping the positive root)

\\begin{equation}

  \\gamma = j\\omega\\sqrt{\\tmu\\teps}.

\\end{equation}

Because \$\\tmu\$ and \$\\teps\$ are complex, \$\\gamma\$ will be
complex and

we write \$\\gamma=\\alpha + j\\beta\$ where \$\\alpha\$ is the
attenuation

constant and \$\\beta\$ is the phase constant (or wave number).

Returning to the characteristic impedance as given in

\\refeq{eq:almostEta}, we can now write

\\begin{equation}

  \\eta = \\frac{j\\omega\\tmu}{j\\omega\\sqrt{\\tmu\\teps}}

       = \\sqrt{\\frac{\\tmu}{\\teps}}.

\\end{equation}

Alternatively, we can write

\\begin{equation}

  \\eta =
\\sqrt{\\frac{\\mu\\left(1-j\\frac{\\sigma\_m}{\\omega\\mu}\\right)}

             
{\\epsilon\\left(1-j\\frac{\\sigma}{\\omega\\epsilon}\\right)}}.

\\end{equation}

Let us now consider a \$z\$-polarized plane wave normally incident from

a lossless material to a lossy material.  There is a planar interface

between the two media at \$x=0\$.  The (known) incident field

is given by

\\begin{equation}

  E\_z\^i = e\^{-j\\beta\_1x} \\qquad H\_y\^i = -\\frac{1}{\\eta\_1}
e\^{-j\\beta\_1x}

\\end{equation}

where \$\\beta\_1=\\omega\\sqrt{\\mu\_1\\epsilon\_1}\$.  The reflected
field is

given by

\\begin{equation}

  E\_z\^r = \\Gamma e\^{j\\beta\_1x} \\qquad H\_y\^r =
\\frac{\\Gamma}{\\eta\_1} e\^{j\\beta\_1x}

\\end{equation}

where the only unknown is the reflection coefficient \$\\Gamma\$.  The

transmitted field is given by

\\begin{equation}

  E\_z\^t = T e\^{-\\gamma\_2x} \\qquad H\_y\^t = -\\frac{T}{\\eta\_2}

                                           e\^{-\\gamma\_2 x}

\\end{equation}

where the only unknown is the transmission coefficient \$T\$.

Both the electric field and the magnetic field are tangential to the

interface at \$x=0\$.  Thus, the boundary conditions dictate that the

sum of the incident and reflected field must equal the transmitted

field at \$x=0\$.  Matching the electric fields at the interface yields

\\begin{equation}

  1+\\Gamma = T.  \\label{eq:matchingE1D}

\\end{equation}

Matching the magnetic fields yields

\\begin{equation}

  -\\frac{1}{\\eta\_1} + \\frac{\\Gamma}{\\eta\_1} =
-\\frac{T}{\\eta\_2}

\\end{equation}

or, rearranging slightly,

\\begin{equation}

  1 - \\Gamma = \\frac{\\eta\_1}{\\eta\_2}T. \\label{eq:matchingH1D}

\\end{equation}

Adding \\refeq{eq:matchingE1D} and \\refeq{eq:matchingH1D} and

rearranging yields

\\begin{equation}

  T = \\frac{2\\eta\_2}{\\eta\_2+\\eta\_1}.

\\end{equation}

Plugging this back into \\refeq{eq:matchingE1D} yields

\\begin{equation}

  \\Gamma = \\frac{\\eta\_2-\\eta\_1}{\\eta\_2+\\eta\_1}.

  \\label{eq:pmlGamma1D}

\\end{equation}

Consider the case where the media are related by

\\begin{equation}

  \\frac{\\mu\_2}{\\epsilon\_2} = \\frac{\\mu\_1}{\\epsilon\_1}

  \\qquad \\mbox{and} \\qquad

  \\frac{\\sigma\_m}{\\mu\_2} = \\frac{\\sigma}{\\epsilon\_2}.

\\end{equation}

We will call these conditions the \`\`matching conditions.''  Under

these conditions the impedances equal:

\\begin{equation}

 
\\eta\_2=\\sqrt{\\frac{\\mu\_2\\left(1-j\\frac{\\sigma\_m}{\\omega\\mu\_2}\\right)}

            
{\\epsilon\_2\\left(1-j\\frac{\\sigma}{\\omega\\epsilon\_2}\\right)}}

  =
\\sqrt{\\frac{\\mu\_1\\left(1-j\\frac{\\sigma}{\\omega\\epsilon\_2}\\right)}

            
{\\epsilon\_1\\left(1-j\\frac{\\sigma}{\\omega\\epsilon\_2}\\right)}}

  = \\sqrt{\\frac{\\mu\_1}{\\epsilon\_1}} = \\eta\_1.

\\end{equation}

When the impedances are equal, from \\refeq{eq:pmlGamma1D} we see that

the reflection coefficient must be zero (and the transmission

coefficient is unity).  We further note that this is true independent

of the frequency.

As we have seen previously, this type of lossy layer can be

implemented in an FDTD grid.  To minimize numeric artifacts it is best

to gradually increase the conductivity within the lossy region.  Any

field that makes it to the end of the grid will be reflected, but,

because of the loss, this reflected field can be greatly attenuated.

Furthermore, as the field propagates back through the lossy region

toward the lossless region, it is further attenuated.  Thus the

reflected field from this lossy region (and the termination of the

grid) can be made relatively inconsequential.

\\section{Lossy Layer, 2D}

Since a lossy layer works so well in 1D and is so easy to implement,

it is natural to ask if it can be used in 2D.  The answer, we shall

see, is that a simple lossy layer cannot be matched to the lossless

region for obliquely traveling waves.

Consider a TM\$\^z\$ field where the incident electric field is given by

\\begin{eqnarray}

  \\Evec\^i &=& \\unitvec{z} e\^{-j\\kvec\_1\\cdot\\rvec}, \\\\

      &=& \\unitvec{z} e\^{-j\\beta\_1\\cos(\\theta\_i)x
-j\\beta\_1\\sin(\\theta\_i)y}, \\\\

      &=& \\unitvec{z} e\^{-j\\beta\_{1x}x -j\\beta\_{1y}y}.

\\end{eqnarray}

Knowing that the angle of incidence equals the angle of reflection

(owing to the required phase matching along the interface), the

reflected field is given by

\\begin{equation}

  \\Evec\^r  = \\unitvec{z} \\Gamma e\^{j\\beta\_{1x}x -j\\beta\_{1y}y}.

\\end{equation}

Combining the incident and reflected field yields

\\begin{equation}

  \\Evec\_1  = \\unitvec{z}

             \\left( e\^{-j\\beta\_{1x}x} + \\Gamma
e\^{j\\beta\_{1x}x}\\right)

            e\^{-j\\beta\_{1y}y}

           = \\unitvec{z} E\_{1z}.

\\end{equation}

The magnetic field in the first medium is given by

\\begin{eqnarray}

  \\Hvec\_1 &=& -\\frac{1}{j\\omega\\mu\_1}\\nabla\\times\\Evec\_1, \\\\

    &=& \\unitvec{x}\\frac{\\beta\_{1y}}{\\omega\\mu\_1}

      \\left(e\^{-j\\beta\_{1x}x} + \\Gamma e\^{\\beta\_{1x}x}\\right)

      e\^{-j\\beta\_{1y}y}

    + \\unitvec{y}\\frac{\\beta\_{1x}}{\\omega\\mu\_1}

      \\left(-e\^{-j\\beta\_{1x}x} + \\Gamma e\^{\\beta\_{1x}x}\\right)

      e\^{-j\\beta\_{1y}y}.

\\end{eqnarray}

The transmitted electric field is

\\begin{eqnarray}

  \\Evec\^t &=& \\unitvec{z} T e\^{-\\gammavec\_2\\cdot\\rvec} \\\\

          &=& \\unitvec{z} T e\^{-\\gamma\_{2x}x - \\gamma\_{2y}y}, \\\\

         &=& \\unitvec{z} E\^t\_z.

\\end{eqnarray}

Plugging this expression into Maxwell's equations (or, equivalently,

the wave equation) ultimately yields the constraint equation

\\begin{equation}

  \\gamma\_{2x}\^2 + \\gamma\_{2y}\^2 = -\\omega\^2\\tmu\_2\\teps\_2.

  \\label{eq:gammaConstraint}

\\end{equation}

Owing to the boundary condition that the fields must match at the

interface, the propagation in the \$y\$ direction (i.e., tangential to

the boundary) must be the same in both media.  Thus,

\$\\gamma\_{2y} = j\\beta\_{1y}\$.  Plugging this into
\\refeq{eq:gammaConstraint}

and solving for \$\\gamma\_{2x}\$ yields

\\begin{equation}

  \\gamma\_{2x} = \\sqrt{\\beta\_{1y}\^2 -\\omega\^2\\tmu\_2\\teps\_2}

    = \\alpha\_{2x} + j\\beta\_{2x}.

\\end{equation}

Note that when \$\\beta\_{1y}=0\$, i.e., there is no propagation in the
\$y\$

direction and the field is normally incident on the interface, this

reduces to \$\\gamma\_{2x} = j\\omega\\sqrt{\\tmu\_2\\teps\_2}\$ which
is what

we had for the 1D case.  On the other hand, when
\$\\sigma=\\sigma\_m=0\$

we obtain \$\\gamma\_{2x} = j\\left(\\omega\^2\\mu\_2\\epsilon\_2 -

\\beta\_{1y}\^2\\right)\^{1/2}\$ where the term in parentheses is purely
real

(so that \$\\gamma\_{2x}\$ will either be purely real or purely

imaginary).  The transmitted magnetic field is given by

\\begin{eqnarray}

  \\Hvec\^t &=& -\\frac{1}{j\\omega\\tmu\_2}\\nabla\\times\\Evec\^t,
\\\\

    &=& \\unitvec{x} \\frac{\\beta\_{1y}}{\\omega\\tmu\_2} E\_z\^t -

        \\unitvec{y} \\frac{\\gamma\_{2x}}{j\\omega\\tmu\_2} E\_z\^t.

\\end{eqnarray}

Enforcing the boundary condition on the electric field and the

\$y\$-component of the magnetic field at \$x=0\$ yields

\\begin{eqnarray}

  1 + \\Gamma &=& T, \\label{eq:eMatchingOblique} \\\\

  \\frac{\\beta\_{1x}}{\\omega\\mu\_1}\\left(-1+\\Gamma\\right) &=&

  -\\frac{\\gamma\_{2x}}{j\\omega\\tmu\_2} T,

\\end{eqnarray}

or, rearranging the second equation,

\\begin{equation}

  1-\\Gamma = \\frac{\\mu\_1\\gamma\_{2x}}{j\\tmu\_2 \\beta\_{1x}} T.

 \\label{eq:hMatchingOblique}

\\end{equation}

Adding \\refeq{eq:eMatchingOblique}  and \\refeq{eq:hMatchingOblique}

and rearranging  yields

\\begin{equation}

  T = \\frac{j\\frac{2\\tmu\_2}{\\gamma\_{2x}}}

           {j\\frac{\\tmu\_2}{\\gamma\_{2x}} +
\\frac{\\mu\_1}{\\beta\_{1x}}}.

\\end{equation}

Using this in \\refeq{eq:eMatchingOblique} yields the reflection

coefficient

\\begin{equation}

  \\Gamma = \\frac{j\\frac{\\tmu\_2}{\\gamma\_{2x}} -
\\frac{\\mu\_1}{\\beta\_{1x}}}

                {j\\frac{\\tmu\_2}{\\gamma\_{2x}} +
\\frac{\\mu\_1}{\\beta\_{1x}}}.

\\end{equation}

The reflection coefficient will be zero only if the terms in the

numerator cancel.  Let us consider these terms individually.

Additionally, let us enforce a more restrictive form of the matching

conditions where now \$\\mu\_2=\\mu\_1\$, \$\\epsilon\_2=\\epsilon\_1\$
and, as

before, \$\\sigma/\\epsilon\_2=\\sigma\_m/\\mu\_2\$.  The first term in
the

numerator can be written

\\begin{eqnarray}

  j\\frac{\\tmu\_2}{\\gamma\_{2x}} &=&

   
\\frac{\\tmu\_2}{\\sqrt{\\omega\^2\\tmu\_2\\teps\_2-\\beta\_{1y}\^2}},
\\\\

  &=&

   \\frac{\\mu\_1\\left(1-j\\frac{\\sigma}{\\omega\\epsilon\_1}\\right)}

  
{\\sqrt{\\omega\^2\\mu\_1\\epsilon\_1\\left(1-j\\frac{\\sigma}{\\omega\\epsilon\_1}\\right)\^2-\\beta\_{1y}\^2}},
\\\\

  &=&

  \\frac{\\mu\_1}

  {\\sqrt{\\omega\^2\\mu\_1\\epsilon\_1-\\frac{\\beta\_{1y}\^2}

                                     
{\\left(1-j\\frac{\\sigma}{\\omega\\epsilon\_1}\\right)\^2}}}.

  \\label{eq:lossGammaNum1}

\\end{eqnarray}

The second term in the numerator of the reflection coefficient is

\\begin{equation}

  \\frac{\\mu\_1}{\\beta\_{1x}} =  

 
\\frac{\\mu\_1}{\\sqrt{\\omega\^2\\mu\_1\\epsilon\_1-\\beta\_{1y}\^2}}.

  \\label{eq:lossGammaNum2}

\\end{equation}

Clearly \\refeq{eq:lossGammaNum1} and \\refeq{eq:lossGammaNum2} are not

equal (unless we further require that \$\\sigma=0\$, but then the lossy

layer is not lossy).  Thus, for oblique incidence, the numerator of

the reflection coefficient cannot be zero and there will always be

some reflection from this lossy medium.

\\section{Split-Field Perfectly Matched Layer}

To obtain a perfect match between the lossless and lossy regions,

B\\'{e}renger proposed a non-physical anisotropic material known as a

perfectly matched layer (PML).  In a PML there is no loss in the

direction tangential to the interface but there is loss normal to the

interface.

First, consider the governing equations for the components of the

magnetic fields for TM\$\^z\$ polarization.  We have

\\begin{eqnarray}

  j\\omega\\mu\_2 H\_y + \\sigma\_{mx} H\_y &=& \\frac{\\partial
E\_z}{\\partial x} \\\\

  j\\omega\\mu\_2 H\_x + \\sigma\_{my} H\_x &=& -\\frac{\\partial
E\_z}{\\partial y}

\\end{eqnarray}

where \$\\sigma\_{mx}\$ and \$\\sigma\_{my}\$ are the magnetic
conductivities

associated {\\em not} with the \$x\$ and \$y\$ components of the
magnetic

field, but rather with propagation in the \$x\$ or \$y\$ direction. 
(Note

that for 1D propagation in the \$x\$ direction the non-zero fields are

\$H\_y\$ and \$E\_z\$ while for 1D propagation in the \$y\$ direction
they are

\$H\_x\$ and \$E\_z\$.)

For the electric field the governing equation is

\\begin{equation}

  j\\omega\\epsilon\_2 E\_z + \\sigma E\_z =

  \\frac{\\partial H\_y}{\\partial x} - \\frac{\\partial H\_x}{\\partial
y}

  \\label{eq:pmlEBeforeSplit}

\\end{equation}

Here there is a single conductivity and no possibility to have
explicitly

anisotropic behavior of the electrical conductivity.  Thus, it would

still be impossible to match the lossy region to the lossless one.

B\\'{e}renger's fix was to split the electric field into two

(non-physical) components.  To get the \`\`actual'' field, we merely sum

these components.  Thus we write

\\begin{equation}

  E\_z = E\_{zx} + E\_{zy}

\\end{equation}

These components are governed by

\\begin{eqnarray}

  j\\omega\\epsilon\_2 E\_{zx} + \\sigma\_x E\_{zx} &=& \\frac{\\partial
H\_y}{\\partial x},  \\\\

  j\\omega\\epsilon\_2 E\_{zy} + \\sigma\_y E\_{zy} &=&
-\\frac{\\partial H\_x}{\\partial y}.

\\end{eqnarray}

Note that there are now two electrical conductivities: \$\\sigma\_x\$
and

\$\\sigma\_y\$.  If we set \$\\sigma\_x = \\sigma\_y = \\sigma\$ and add
these

two equations together, we recover the original equation

\\refeq{eq:pmlEBeforeSplit}.  Further note that if

\$\\sigma\_y=\\sigma\_{my}=0\$ but \$\\sigma\_x\\neq 0\$ and
\$\\sigma\_{mx}\\neq 0\$,

then a wave with components \$H\_x\$ and \$E\_{zy}\$ would not attenuate

while a wave with components \$H\_y\$ and \$E\_{zx}\$ would attenuate.

Let us define the terms \$S\_w\$ and \$S\_{mw}\$ as

\\begin{eqnarray}

   S\_w &=& 1 + \\frac{\\sigma\_w}{j\\omega\\epsilon\_2} \\\\

   S\_{mw} &=& 1 + \\frac{\\sigma\_{mw}}{j\\omega\\mu\_2}

\\end{eqnarray}

where \$w\$ is either \$x\$ or \$y\$.  We can then write the governing

equations as

\\begin{eqnarray}

  j\\omega\\epsilon\_2 S\_x E\_{zx} &=& \\frac{\\partial H\_y}{\\partial
x},

    \\label{eq:ezxSplit} \\\\

  j\\omega\\epsilon\_2 S\_y E\_{zy} &=& -\\frac{\\partial
H\_x}{\\partial y},

    \\label{eq:ezySplit} \\\\

  j\\omega\\mu\_2 S\_{mx} H\_y &=&

    \\frac{\\partial}{\\partial x} \\left(E\_{zx}+E\_{zy}\\right),

    \\label{eq:hySplit} \\\\

  j\\omega\\mu\_2 S\_{my} H\_x &=&

    -\\frac{\\partial}{\\partial y} \\left(E\_{zx}+E\_{zy}\\right).

    \\label{eq:hxSplit}

\\end{eqnarray}

Taking the partial of \\refeq{eq:hySplit} with respect to \$x\$ and then

substituting in the left-hand side of \\refeq{eq:ezxSplit} yields

\\begin{equation}

  -\\omega\^2\\mu\_2\\epsilon\_2 S\_x S\_{mx} E\_{zx} =

    \\frac{\\partial\^2}{\\partial x\^2} \\left(E\_{zx}+E\_{zy}\\right).

\\end{equation}

Taking the partial of \\refeq{eq:hxSplit} with respect to \$y\$ and then

substituting in the left-hand side of \\refeq{eq:ezySplit} yields

\\begin{equation}

  -\\omega\^2\\mu\_2\\epsilon\_2 S\_y S\_{my} E\_{zy} =

    \\frac{\\partial\^2}{\\partial y\^2} \\left(E\_{zx}+E\_{zy}\\right).

\\end{equation}

Adding these two expressions together after dividing by the \$S\$ terms

yields

\\begin{equation}

  -\\omega\^2\\mu\_2\\epsilon\_2 \\left(E\_{zx} + E\_{zy}\\right) =

  \\left(\\frac{1}{S\_{mx}S\_x} \\frac{\\partial\^2}{\\partial x\^2} +

        \\frac{1}{S\_{my}S\_y}  \\frac{\\partial\^2}{\\partial
y\^2}\\right)

  \\left(E\_{zx} + E\_{zy}\\right)

\\end{equation}

or, after rearranging and recalling that \$E\_{zx} + E\_{zy} = E\_z\$,

\\begin{equation}

  \\left(\\frac{1}{S\_{mx}S\_x} \\frac{\\partial\^2}{\\partial x\^2} +

        \\frac{1}{S\_{my}S\_y}  \\frac{\\partial\^2}{\\partial y\^2} +

        \\omega\^2\\mu\_2\\epsilon\_2

  \\right) E\_z = 0.

\\end{equation}

To satisfy this equation the transmitted field in the PML region would

be given by

\\begin{equation}

  E\_z\^t = T e\^{-j\\sqrt{S\_{mx}S\_x}\\beta\_{2x} x
-j\\sqrt{S\_{my}S\_y}\\beta\_{2y} y}

\\end{equation}

where we must also have

\\begin{equation}

  \\beta\_{2x}\^2 + \\beta\_{2y}\^2 = \\omega\^2 \\mu\_2\\epsilon\_2.

\\end{equation}

Using \\refeq{eq:hySplit}, the \$y\$ component of the magnetic field in

the PML is given by

\\begin{eqnarray}

  H\_y\^t &=& \\frac{1}{j\\omega\\mu\_2 S\_{mx}}

          \\frac{\\partial E\_z\^t}{\\partial x} \\\\

        &=& -\\frac{\\sqrt{S\_{mx}S\_x}\\beta\_{2x}}{\\omega\\mu\_2
S\_{mx}} E\_z\^t, \\\\

        &=& -\\frac{\\beta\_{2x}}{\\omega\\mu\_2}

             \\sqrt{\\frac{S\_x}{S\_{mx}}} E\_z\^t.

\\end{eqnarray}

As always, the tangential fields must match at the interface.

Matching the electric fields again yields

\\refeq{eq:eMatchingOblique}.  Matching the \$y\$ component of the

magnetic fields yields

\\begin{equation}

  1 - \\Gamma = \\frac{\\mu\_1 \\beta\_{2x}}{\\mu\_2 \\beta\_{1x}}

               \\sqrt{\\frac{S\_x}{S\_{mx}}} T.

\\end{equation}

Using this and \\refeq{eq:eMatchingOblique} to solve for the

transmission and reflection coefficients yields

\\begin{eqnarray}

  T &=& \\frac{2\\frac{\\beta\_{1x}}{\\mu\_1}}

           {\\frac{\\beta\_{1x}}{\\mu\_1} +
\\frac{\\beta\_{2x}}{\\mu\_2}

               \\sqrt{\\frac{S\_x}{S\_{mx}}}}, \\\\

  \\Gamma &=&  \\frac{\\frac{\\beta\_{1x}}{\\mu\_1} -
\\frac{\\beta\_{2x}}{\\mu\_2}

               \\sqrt{\\frac{S\_x}{S\_{mx}}}}

           {\\frac{\\beta\_{1x}}{\\mu\_1} +
\\frac{\\beta\_{2x}}{\\mu\_2}

               \\sqrt{\\frac{S\_x}{S\_{mx}}}}.

  \\label{eq:gPml2D}

\\end{eqnarray}

It is now possible to match the PML to the non-PML region so that

\$\\Gamma\$ is zero.  We begin by setting \$\\mu\_2=\\mu\_1\$ and

\$\\epsilon\_2=\\epsilon\_1\$.  Thus we have

\$\\omega\^2\\mu\_2\\epsilon\_2=\\omega\^2\\mu\_1\\epsilon\_1\$ and

\\begin{eqnarray}

  \\beta\_{2x} &=& \\left(\\omega\^2\\mu\_2\\epsilon\_2 -
\\beta\_{2y}\^2\\right)\^{1/2}, \\\\

         &=& \\left(\\omega\^2\\mu\_1\\epsilon\_1 -
\\beta\_{2y}\^2\\right)\^{1/2}.

  \\label{eq:k2xPml}

\\end{eqnarray}

Recall that within the PML the propagation in the \$y\$ direction is not

given by \$\\beta\_{2y}\$ but rather by \$\\sqrt{S\_y
S\_{my}}\\beta\_{2y}\$.

Phase matching along the interface requires that

\\begin{equation}

  \\sqrt{S\_y S\_{my}}\\beta\_{2y} = \\beta\_{1y}.

\\end{equation}

If we let \$S\_y = S\_{my} = 1\$, which can be realized by setting

\$\\sigma\_y=\\sigma\_{my}=0\$, then the phase matching condition
reduces to

\\begin{equation}

  \\beta\_{2y} = \\beta\_{1y}.

\\end{equation}

Then, from \\refeq{eq:k2xPml}, we have

\\begin{eqnarray}

  \\beta\_{2x} &=& \\left(\\omega\^2\\mu\_1\\epsilon\_1 -
\\beta\_{1y}\^2\\right)\^{1/2},\\\\

         &=&  \\beta\_{1x}.

\\end{eqnarray}

Returning to \\refeq{eq:gPml2D}, we now have

\\begin{eqnarray}

  \\Gamma &=&  \\frac{\\frac{\\beta\_{1x}}{\\mu\_1} -
\\frac{\\beta\_{1x}}{\\mu\_1}

               \\sqrt{\\frac{S\_x}{S\_{mx}}}}

           {\\frac{\\beta\_{1x}}{\\mu\_1} +
\\frac{\\beta\_{1x}}{\\mu\_1}

               \\sqrt{\\frac{S\_x}{S\_{mx}}}}, \\\\

   &=& \\frac{1 - \\sqrt{\\frac{S\_x}{S\_{mx}}}}

            {1 + \\sqrt{\\frac{S\_x}{S\_{mx}}}}.

\\end{eqnarray}

The last remaining requirement to achieve a perfect match is to have

\$S\_x=S\_{mx}\$.  This can be realized by having
\$\\sigma\_x/\\epsilon\_2 =

\\sigma\_{mx}/\\mu\_2\$. 

To summarize, the complete set of matching

conditions for a constant-\$x\$ interface are

\\begin{eqnarray}

  \\epsilon\_2 &=& \\epsilon\_1 \\\\

  \\mu\_2 &=& \\mu\_1 \\\\

  \\sigma\_y &=& \\sigma\_{my} \\,=\\, 0 \\\\

  \\frac{\\sigma\_x}{\\epsilon\_2} &=& \\frac{\\sigma\_{mx}}{\\mu\_2}.

\\end{eqnarray}

Under these conditions propagation in the PML is governed by

\\begin{eqnarray}

  e\^{-j S\_x \\beta\_{1x} x - j \\beta\_{1y} y} &=&

  \\exp\\!\\left(-j \\left(1 +
\\frac{\\sigma}{j\\omega\\epsilon\_1}\\right) \\beta\_{1x} x

   - j \\beta\_{1y} y\\right), \\\\

 &=& 
\\exp\\!\\left(-\\frac{\\beta\_{1x}\\sigma}{\\omega\\epsilon\_1}x\\right)

  e\^{-j\\beta\_{1x} x - j \\beta\_{1y} y}.

\\end{eqnarray}

This shows that there is exponential decay in the \$x\$ direction but

otherwise the phase propagates in exactly the same way as it does in

the non-PML region.

\\section{Un-Split PML}

In the previous section we had \$S\_w\$ and \$S\_{mw}\$ where
\$w\\in\\{x,y\\}\$.

However, once the matching condition has been applied, i.e.,

\$\\sigma\_w/\\epsilon\_2 = \\sigma\_{mw}/\\mu\_2\$, then we have
\$S\_w=S\_{mw}\$.

Hence we will drop the \$m\$ from the subscript.  Additionally, with the

understanding that we are talking about the PML region, we will drop

the subscript \$2\$ from the material constants.  We thus write

\\begin{equation}

  S\_w = 1 + \\frac{\\sigma\_w}{j\\omega\\epsilon}.

\\end{equation}

The conductivity in the PML is not dictated by underlying parameters

in the physical space being modeled.  Rather, this conductivity is set

so as to minimize the reflections from the termination of the grid.

In that sense \$\\sigma\_w\$ is somewhat arbitrary.  Therefore let us

normalize the conductivity by the relative permittivity that pertains

at that particular location, i.e.,

\\begin{equation}

  S\_w = 1 + \\frac{\\sigma'\_w}{j\\omega\\epsilon\_0}

\\end{equation}

where \$\\sigma'\_w = \\sigma\_w/\\epsilon\_r\$.  However, since the

conductivity has not yet been specified, we drop the prime and merely

write

\\begin{equation}

  S\_w = 1 + \\frac{\\sigma\_w}{j\\omega\\epsilon\_0}

\\end{equation}

Note that there could potentially be a problem with \$S\_w\$ when the

frequency goes to zero.  In practice, in the curl equations this term

is also multiplied by \$\\omega\$ and in that sense this is not a major

problem.  However, if we want to move these \$S\_w\$ terms around, low

frequencies may cause problems.  To fix this, we add an additional

factor to ensure that \$S\_w\$ remains finite as the frequency goes to

zero.

We can further generalize \$S\_w\$ by allowing the leading term to take

on values other than unity.  This is effectively equivalent to

allowing the relative permittivity in the PML to change.  The general

expression for \$S\_w\$ we will use is

\\begin{equation}

  S\_w = \\kappa\_w + \\frac{\\sigma\_w}{a\_w + j\\omega\\epsilon\_0}.

\\end{equation}

For the sake of considering 3D problems we also assume
\$w\\in\\{x,y,z\\}\$.

Dividing by the \$S\$ terms, the governing equations for TM\$\^z\$

polarization are

\\begin{eqnarray}

  j\\omega\\epsilon E\_{zx} &=&

    \\frac{1}{S\_x}\\frac{\\partial H\_y}{\\partial x}, \\\\

  j\\omega\\epsilon E\_{zy} &=&

    -\\frac{1}{S\_y}\\frac{\\partial H\_x}{\\partial y}, \\\\

  j\\omega\\mu H\_y &=&

    \\frac{1}{S\_x}\\frac{\\partial E\_z}{\\partial x},\\\\

  j\\omega\\mu H\_x &=&

    -\\frac{1}{S\_y}\\frac{\\partial E\_z}{\\partial y}.

\\end{eqnarray}

Adding the first two equations together we obtain

\\begin{equation}

  j\\omega\\epsilon E\_z =

    \\frac{1}{S\_x}\\frac{\\partial H\_y}{\\partial x}

    -\\frac{1}{S\_y}\\frac{\\partial H\_x}{\\partial y}.

\\end{equation}

Note that in all these equations each \$S\_w\$ term is always paired

with the derivative in the \`\`\$w\$'' direction.

Let us define a new del operator \$\\nabpml\$ that incorporates this

pairing

\\begin{equation}

  \\nabpml \\equiv \\unitvec{x}
\\frac{1}{S\_x}\\frac{\\partial}{\\partial x}

   + \\unitvec{y} \\frac{1}{S\_y}\\frac{\\partial}{\\partial y}

   + \\unitvec{z} \\frac{1}{S\_z}\\frac{\\partial}{\\partial z}.

  \\label{eq:nabpml}

\\end{equation}

Using this operator Maxwell's curl equations become

\\begin{eqnarray}

 j\\omega\\epsilon\\Evec &=& \\nabpml\\times\\Hvec,

   \\label{eq:curlEStretched}

\\\\

 -j\\omega\\mu\\Hvec &=& \\nabpml\\times\\Evec.

   \\label{eq:curlHStretched}

\\end{eqnarray}

Note that these equations pertain to the general 3D case.  This is

known as the stretch-coordinate PML formulation since, as shown in

\\refeq{eq:nabpml}, the complex \$S\$ terms scale the various coordinate

directions.  Additionally, note there is no explicit mention of split

fields in these equations.  If we can find a way to implement these

equations directly in the FDTD algorithm, we can avoid splitting the

fields.

From these curl equations we obtain scalar equations such as (using

the \$x\$-component of \\refeq{eq:curlEStretched} and

\\refeq{eq:curlHStretched} as examples)

\\begin{eqnarray}

  j\\omega\\epsilon E\_x &=&

    \\frac{1}{S\_y}\\frac{\\partial H\_z}{\\partial y} -

    \\frac{1}{S\_z}\\frac{\\partial H\_y}{\\partial z}, \\\\

  j\\omega\\mu H\_x &=&

    -\\frac{1}{S\_y}\\frac{\\partial E\_z}{\\partial y} +

    \\frac{1}{S\_z}\\frac{\\partial E\_y}{\\partial z}.

\\end{eqnarray}

Converting these to the time-domain yields

\\begin{eqnarray}

  \\epsilon \\frac{\\partial E\_x}{\\partial t} &=&

    \\bar{S}\_y \\star \\frac{\\partial H\_z}{\\partial y} -

    \\bar{S}\_z \\star \\frac{\\partial H\_y}{\\partial z},

  \\label{eq:exConvolution}

  \\\\

  \\mu \\frac{\\partial H\_x}{\\partial t} &=&

    -\\bar{S}\_y \\star \\frac{\\partial E\_z}{\\partial y} +

    \\bar{S}\_z \\star \\frac{\\partial E\_y}{\\partial z},

\\end{eqnarray}

where \`\`\$\\star\$'' indicates convolution and \$\\bar{S}\_w\$ is the
inverse

Fourier transform of \$1/S\_w\$, i.e.,

\\begin{equation}

  \\bar{S}\_w = {\\cal F}\^{-1}\\left[\\frac{1}{S\_w}\\right].

\\end{equation}

The reciprocal of \$S\_w\$ is given by

\\begin{equation}

  \\frac{1}{S\_w} =

  \\frac{1}{\\kappa\_w + \\frac{\\sigma\_w}{a\_w +
j\\omega\\epsilon\_0}} =

  \\frac{a\_w + j\\omega\\epsilon\_0}

       {a\_w\\kappa\_w + \\sigma\_w + j\\omega\\kappa\_w\\epsilon\_0}.

\\end{equation}

This is of the form \$(a+j\\omega b)/(c+j\\omega d)\$ and we cannot do a

partial fraction expansion since the order of the numerator and

denominator are the same.  Instead, we can divide the denominator into

the numerator to obtain

\\begin{equation}

  \\frac{a+j\\omega b}{c+j\\omega d} =

   \\frac{b}{d} +

   \\frac{a-c\\frac{b}{d}}{c+j\\omega d}

   = 

   \\frac{b}{d} +

   \\frac{\\frac{a}{c}-\\frac{b}{d}}{1+j\\omega\\frac{d}{c}}.

\\end{equation}

Recall the following Fourier transform pairs:

\\begin{eqnarray}

  1 &\\Leftrightarrow& \\delta(t), \\\\

  \\frac{1}{1+j\\omega\\tau} &\\Leftrightarrow&

    \\frac{1}{\\tau} e\^{-t/\\tau} u(t),

\\end{eqnarray}

where \$\\delta(t)\$ is the Dirac delta function and \$u(t)\$ is the
unit

step function.  Thus, we have

\\begin{equation}

  {\\cal F}\^{-1}\\left[\\frac{b}{d} +

     \\frac{\\frac{a}{c}-\\frac{b}{d}}{1+j\\omega\\frac{d}{c}}\\right] =

  \\frac{b}{d}\\delta(t) + \\frac{ad-bc}{d\^2}e\^{-ct/d} u(t).

  \\label{eq:fourierDetail}

\\end{equation}

For the problem at hand, we have \$a=a\_w\$, \$b=\\epsilon\_0\$,

\$c=a\_w\\kappa\_w+\\sigma\_w\$, and \$d=\\kappa\_w\\epsilon\_0\$. 
Using these

values in \\refeq{eq:fourierDetail} yields

\\begin{equation}

  \\bar{S}\_w =

  \\frac{1}{\\kappa\_w}\\delta(t) -

  \\frac{\\sigma\_w}{\\kappa\_w\^2\\epsilon\_0}

   \\exp\\!\\left(-t\\left[\\frac{a\_w}{\\epsilon\_0}+

                      
\\frac{\\sigma\_w}{\\kappa\_w\\epsilon\_0}\\right]\\right) u(t).

  \\label{eq:sBarTime}

\\end{equation}

Let us define \$\\zeta\_w(t)\$ as

\\begin{equation}

  \\zeta\_w(t) = -\\frac{\\sigma\_w}{\\kappa\_w\^2\\epsilon\_0}

   \\exp\\!\\left(-t\\left[\\frac{a\_w}{\\epsilon\_0}+

                      
\\frac{\\sigma\_w}{\\kappa\_w\\epsilon\_0}\\right]\\right) u(t)

\\end{equation}

so that

\\begin{equation}

  \\bar{S}\_w =

  \\frac{1}{\\kappa\_w}\\delta(t) + \\zeta\_w(t).

\\end{equation}

Recall that the convolution of a Dirac delta function with another

function yields the original function, i.e.,

\\begin{equation}

  \\delta(t)\\star f(t) = f(t).

\\end{equation}

Incorporating this fact into \\refeq{eq:exConvolution} yields

\\begin{eqnarray}

  \\epsilon \\frac{\\partial E\_x}{\\partial t} &=&

    \\frac{1}{\\kappa\_y} \\frac{\\partial H\_z}{\\partial y} -

    \\frac{1}{\\kappa\_z} \\frac{\\partial H\_y}{\\partial z}
\\nonumber\\\\

  &&\\mbox{} + \\zeta\_y(t) \\star \\frac{\\partial H\_z}{\\partial y} -

    \\zeta\_z(t) \\star \\frac{\\partial H\_y}{\\partial z}.

    \\label{eq:exInPml}

\\end{eqnarray}

Note that the first line of this equation is almost the usual

governing equation.  The only differences are the \$\\kappa\$'s.

However, these are merely real constants.  In the FDTD algorithm it is

trivial to incorporate these terms in the update-equation

coefficients.  The second line again involves convolutions.

Fortunately, these convolution are rather \`\`benign'' and, as we shall

see, can be calculated efficiently using recursive convolution.

\\section{FDTD Implementation of Un-Split PML}

We now wish to develop an FDTD implementation of the PML as formulated

in the previous section.  We start by defining the function

\$\\Psi\_{E\_uw}\^q\$ as

\\begin{eqnarray}

  \\Psi\_{E\_uw}\^q &=&

    \\left.\\zeta\_w(t)\\star

          \\frac{\\partial H\_v}{\\partial w}\\right|\_{t=q\\Delt} \\\\

  &=&

  \\int\_{\\tau=0}\^{q\\Delt}

   \\zeta\_w(\\tau)

          \\frac{\\partial H\_v(q\\Delt-\\tau)}{\\partial w} d\\tau

  \\label{eq:psiFunction}

\\end{eqnarray}

where \$E\_uw\$ in the subscript indicates this function will appear

in the update of the \$E\_u\$ component of the electric field and it is

concerned with the spatial derivative in the \$w\$ direction.  In

\\refeq{eq:psiFunction} the derivative is of the \$H\_v\$ component of
the

magnetic field where \$w\$, \$u\$, and \$v\$ are such that

\$\\{w,u,v\\}\\in\\{x,y,z\\}\$ and \$w\\neq u\\neq v\$.

In \\refeq{eq:psiFunction} note that \$\\zeta\_w(\\tau)\$ is zero for

\$\\tau\<0\$ hence the integrand would be zero for \$\\tau\<0\$.  This
fixes

the lower limit of integration to zero.  On the other hand, we assume
the

fields are zero prior to \$t=0\$, i.e., \$H\_v(t)\$ is zero for
\$t\<0\$.  In

the convolution the argument of the magnetic field is \$q\\Delt-\\tau\$.

This argument will be negative when \$\\tau\>q\\Delt\$.  Thus the
integrand

will be zero for \$\\tau\>q\\Delt\$ and this fixes the upper limit of

integration to \$q\\Delt\$.

Let us assume the integration variable \$\\tau\$ in

\\refeq{eq:psiFunction} varies continuously but, since we are

considering fields in the FDTD method, \$H\_v\$ varies discretely.  We

can still express \$H\_v\$ in terms of a continuously varying argument

\$t\$, but it takes on discrete values.  Specifically \$\\partial

H\_v(t)/\\partial w\$ can be represented by

\\begin{equation}

  \\frac{\\partial H\_v(t)}{\\partial w} =

  \\sum\_{i=0}\^{I\_{\\mbox{\\scriptsize max}}}

   \\frac{\\partial H\_v(i\\Delt)}{\\partial w} p\_i(t)

\\end{equation}

where \$p\_i(t)\$ is the unit pulse function given by

\\begin{equation}

p\_i(t) =\\left\\{

\\begin{array}{l}

1 \\qquad \\mbox{if}\\quad i\\Delt\\leq t \< (i+1)\\Delt, \\\\

0 \\qquad \\mbox{otherwise}.

\\end{array}

\\right.

\\end{equation}

To illustrate this further, for notational convenience let us

write \$f(t) = \\partial H\_v(t)/\\partial w\$.  The stepwise

representation of this function is shown in Fig.\\

\\ref{fig:stepwise}(a).  Although not necessary, as is typical with

FDTD simulations, this function is assumed to be zero for the first

time-step.  At \$t=\\Delt\$ the function is \$f\_1\$ and it remains
constant

until \$t=2\\Delt\$ when it changes to \$f\_2\$.  At \$t=3\\Delt\$ the
function

is \$f\_3\$, and so on.

\\begin{figure}

  \\begin{center}

  \\epsfig{width=3.5in,file=Figures/Fdtd-pml/step-wise-function.eps}
\\\\

  (a)\\\\

  \\vspace{.15in}

  \\epsfig{width=3.5in,file=Figures/Fdtd-pml/step-wise-reverse.eps}\\\\

  (b) \\\\

  \\vspace{.15in}

 
\\epsfig{width=3.5in,file=Figures/Fdtd-pml/step-wise-reverse-shifted.eps}\\\\

  (c)

\\mbox{}

\\end{center}

\\caption{(a) Stepwise representation of a function

  \$f(t)\$.  The function is a constant \$f\_0\$ for \$0\\leq t\<
\\Delt\$,

  \$f\_1\$ for \$\\Delt \\leq t\< 2\\Delt\$, \$f\_2\$ for \$2 \\Delt
\\leq t \<

  3\\Delt\$, and so on. (b) Stepwise representation of a function

  \$f(-\\tau)\$.  Here the constants \$f\_n\$ are flipped about the
origin

  but the pulses still extend for one time-step to the right of the

  corresponding point.  Hence the function is a constant \$f\_1\$ for

  \$-\\Delt\\leq\\tau\<0\$, \$f\_2\$ for
\$-2\\Delt\\leq\\tau\<-\\Delt\$, etc. (c)

  Stepwise representation of the function \$f(q\\Delt-\\tau)\$ when

  \$q=4\$.}  \\label{fig:stepwise}

\\end{figure}

The convolution contains the function \$f(q\\Delt-\\tau)\$.  At
time-step

zero (i.e., \$q=0\$), this is merely \$f(-\\tau)\$ which is illustrated
in

Fig.\\ \\ref{fig:stepwise}(b).  Here all the sample points \$f\_n\$ are

flipped symmetrically about the origin.  We assume that the function

is constant to the right of these sample points so that the function

is \$f\_1\$ for \$-\\Delt\\leq\\tau\<0\$, it is \$f\_2\$ for

\$-2\\Delt\\leq\\tau\<-\\Delta\$, \$f\_3\$ for
\$-3\\Delt\\leq\\tau\<-2\\Delt\$, and so

on.

Fig.\\ \\ref{fig:stepwise}(c) shows an example of \$f(q\\Delt-\\tau)\$
when

\$q\\neq 0\$, specifically for \$q=4\$.  Recall that in

\\refeq{eq:psiFunction} the limits of integration are from zero to

\$q\\Delt\$---we do not need to concern ourselves with \$\\tau\$ less
than

zero nor greater than \$q\\Delt\$.  As shown in Fig.\\

\\ref{fig:stepwise}(c), the first \`\`pulse'' extending to the right of

\$\\tau=0\$ has a value of \$f\_q\$, the pulse extending to the right of

\$\\tau=\\Delt\$ has a value of \$f\_{q-1}\$, the one to the right of

\$\\tau=2\\Delt\$ has a value of \$f\_{q-2}\$, and so on.  Thus, this
shifted

function can be written as

\\begin{equation}

  f(q\\Delt-\\tau) = \\sum\_{i=0}\^{q-1}f\_{q-i}p\_i(\\tau).

\\end{equation}

Returning to the derivative of the magnetic field, we write

\\begin{equation}

  \\frac{\\partial H\_v(q\\Delt-\\tau)}{\\partial w} =

  \\sum\_{i=0}\^{q-1}\\frac{\\partial H\_v\^{q-i}}{\\partial
w}p\_i(\\tau)

\\end{equation}

where \$H\_v\^{q-i}\$ is the magnetic field at time-step \$q-i\$ and,
when

implemented in the FDTD algorithm, the spatial derivative will be

realized as a spatial finite difference.

At time-step \$q\$, \$\\Psi\_{E\_uw}\$ is given by

\\begin{equation}

  \\Psi\_{E\_uw}\^q =

  \\int\_{\\tau=0}\^{q\\Delt} \\zeta\_w(\\tau)

   \\sum\_{i=0}\^{q-1} \\frac{\\partial H\_v\^{q-i}}{\\partial
w}p\_i(\\tau) d\\tau

\\end{equation}

Interchanging the order of summation and integration yields

\\begin{eqnarray}

  \\Psi\_{E\_uw}\^q &=&

     \\sum\_{i=0}\^{q-1} \\frac{\\partial H\_v\^{q-i}}{\\partial w}

     \\int\_{\\tau=0}\^{q\\Delt} \\zeta\_w(\\tau)p\_i(\\tau) d\\tau,

     \\label{eq:psiIntOne}

  \\\\

   &=&

     \\sum\_{i=0}\^{q-1} \\frac{\\partial H\_v\^{q-i}}{\\partial w}

     \\int\_{\\tau=i\\Delt}\^{(i+1)\\Delt} \\zeta\_w(\\tau) d\\tau,

     \\label{eq:psiIntTwo}

\\end{eqnarray}

where, in going from \\refeq{eq:psiIntOne} to \\refeq{eq:psiIntTwo}, the

pulse function was used to establish the limits of integration.

Consider the following integral

\\begin{eqnarray}

  -\\int\_{i\\Delta}\^{(i+1)\\Delta} e\^{-a t}dt &=&

     \\left. \\frac{1}{a} e\^{-at}
\\right|\_{i\\Delta}\^{(i+1)\\Delta}\\\\

   &=& \\frac{1}{a} \\left(e\^{-a(i+1)\\Delta} - e\^{-ai\\Delta}\\right)
\\\\

   &=& \\frac{1}{a} \\left(e\^{-a\\Delta}-1\\right)e\^{-ai\\Delta} \\\\

   &=& \\frac{1}{a} \\left(e\^{-a\\Delta}-1\\right)

                   \\left(e\^{-a\\Delta}\\right)\^i

\\end{eqnarray}

Keeping this in mind, the integration in \\refeq{eq:psiIntTwo} can be

written as

\\begin{eqnarray}

  \\int\_{\\tau=i\\Delt}\^{(i+1)\\Delt} \\zeta\_w(\\tau) d\\tau &=&

  -\\frac{\\sigma\_w}{\\kappa\_w\^2\\epsilon\_0}

  \\int\_{\\tau=i\\Delt}\^{(i+1)\\Delt}

   \\exp\\!\\left(-\\tau\\left[\\frac{a\_w}{\\epsilon\_0}+

                      
\\frac{\\sigma\_w}{\\kappa\_w\\epsilon\_0}\\right]\\right)

    d\\tau \\\\

  &=& C\_w (b\_w)\^i

  \\label{eq:cbTerm}

\\end{eqnarray}

where

\\begin{eqnarray}

  b\_w &=& \\exp\\!\\left(-\\left[

    \\frac{a\_w}{\\epsilon\_0} +

    \\frac{\\sigma\_w}{\\kappa\_w\\epsilon\_0}\\right]\\Delt\\right),
\\\\

  C\_w &=& \\frac{\\sigma\_w}{\\sigma\_w\\kappa\_w + \\kappa\_w\^2 a\_w}

          \\left(b\_w - 1\\right).

\\end{eqnarray}

Note that in \\refeq{eq:cbTerm} \$b\_w\$ is raised to the power \$i\$
which

is an integer index.  It is now possible to express
\$\\Psi\_{E\_uw}\^q\$ as

\\begin{equation}

  \\Psi\_{E\_uw}\^q =

  \\sum\_{i=0}\^{q-1} \\frac{\\partial H\_v\^{q-i}}{\\partial w} C\_w
(b\_w)\^i.

  \\label{eq:psiSum}

\\end{equation}

Let us explicitly separate the \$i=0\$ term from the rest of the

summation:

\\begin{equation}

  \\Psi\_{E\_uw}\^q =

   C\_w \\frac{\\partial H\_v\^q}{\\partial w}+

  \\sum\_{i=1}\^{q-1} \\frac{\\partial H\_v\^{q-i}}{\\partial w} C\_w
(b\_w)\^i.

\\end{equation}

Replacing the index \$i\$ with \$i'=i-1\$ (so that \$i=i'+1\$), this
becomes

\\begin{equation}

  \\Psi\_{E\_uw}\^q =

   C\_w \\frac{\\partial H\_v\^q}{\\partial w}+

  \\sum\_{i'=0}\^{q-2}

    \\frac{\\partial H\_v\^{q-i'-1}}{\\partial w} C\_w (b\_w)\^{i'+1}.

\\end{equation}

Dropping the prime from the index and rearranging slightly yields

\\begin{equation}

  \\Psi\_{E\_uw}\^q =

  C\_w \\frac{\\partial H\_v\^q}{\\partial w}+

  b\_w \\sum\_{i=0}\^{[q-1]-1}

    \\frac{\\partial H\_v\^{[q-1]-i}}{\\partial w} C\_w (b\_w)\^i.

\\end{equation}

Comparing the summation in this expression to the one in

\\refeq{eq:psiSum} one sees that this expression can be written as

\\begin{equation}

  \\Psi\_{E\_uw}\^q =

  C\_w \\frac{\\partial H\_v\^q}{\\partial w} +

  b\_w \\Psi\_{E\_uw}\^{q-1}.

  \\label{eq:psiRecursive}

\\end{equation}

Note that \$\\Psi\_{E\_uw}\$ at time-step \$q\$ is a function of

\$\\Psi\_{E\_uw}\$ at time-step \$q-1\$.  Thus \$\\Psi\_{E\_uw}\$ can be

updated recursively---there is no need to store the entire history of

\$\\Psi\_{E\_uw}\$ to obtain the next value.  As is typical with FDTD,
one

merely needs to know \$\\Psi\_{E\_uw}\$ at the previous time step.

We now have all the pieces in place to implement a PML in the FDTD

method.  The algorithm to update the electric fields is

\\begin{enumerate}

\\item Update the \$\\Psi\_{E\_uw}\$ terms employing the recursive
update

equation given by \\refeq{eq:psiRecursive}.  Recall that these

\$\\Psi\_{E\_uw}\$ functions represent the convolutions given in the
second

line of \\refeq{eq:exInPml}.

\\item Update the electric fields in the standard way.  However,

incorporate the \$\\kappa\$'s where appropriate.  Essentially one

employs the update equation implied by the top line of

\\refeq{eq:exInPml} (where that equation applies to \$E\_x\$ and similar

equations apply to \$E\_y\$ and \$E\_z\$). 

\\item Apply, i.e., add or subtract, \$\\Psi\_{E\_uw}\$ to the electric

field as indicated by the second line of \\refeq{eq:exInPml}.

\\end{enumerate}

This completes the update of the electric field.

The magnetic fields are updated in a completely analogous manner.

First the \$\\Psi\$ functions that pertain to the magnetic fields are

updated (in this case there are \$\\Psi\_{H\_uw}\$ functions that
involve

the spatial derivatives of the electric fields), then the magnetic

fields are updated in the usual way (accounting for any \$\\kappa\$'s),

and finally the \$\\Psi\$ functions are applied to the magnetic fields

(i.e., added or subtracted).

 
