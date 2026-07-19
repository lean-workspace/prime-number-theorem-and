---
title: 'Second approach'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

**Residue calculus on rectangles**

This files gathers definitions and basic properties about rectangles.

The border of a rectangle is the union of its four sides.

## Definition: RectangleBorder {#RectangleBorder lean="RectangleBorder"}

A Rectangle's border, given corners $z$ and $w$ is the union of the four
    sides.

## Definition: RectangleIntegral {#RectangleIntegral lean="RectangleIntegral"}

A RectangleIntegral of a function $f$ is one over a rectangle
  determined by $z$ and $w$ in $\mathbb{C}$.
  We will sometimes denote it by $\int_{z}^{w} f$.
  (There is also a primed version, which is
  $1/(2\pi i)$ times the original.)

## Definition: UpperUIntegral {#UpperUIntegral lean="UpperUIntegral"}

An UpperUIntegral of a function $f$ comes from
  $\sigma+i\infty$ down to $\sigma+iT$, over to
  $\sigma'+iT$, and back up to $\sigma'+i\infty$.

## Definition: LowerUIntegral {#LowerUIntegral lean="LowerUIntegral"}

A LowerUIntegral of a function $f$ comes from
  $\sigma-i\infty$ up to $\sigma-iT$, over to
  $\sigma'-iT$, and back down to $\sigma'-i\infty$.

It is very convenient to define integrals along vertical lines
in the complex plane, as follows.

## Definition: VerticalIntegral {#VerticalIntegral lean="VerticalIntegral"}

Let $f$ be a function from $\mathbb{C}$ to $\mathbb{C}$,
  and let $\sigma$ be a real number. Then we define
  
$$
\int_{(\sigma)}f(s)ds =
    \int_{\sigma-i\infty}^{\sigma+i\infty}f(s)ds.
$$

We also have a version with a factor of $1/(2\pi i)$.

## Lemma: DiffVertRect-eq-UpperLowerUs {#DiffVertRect_eq_UpperLowerUs lean="DiffVertRect_eq_UpperLowerUs" uses="LowerUIntegral, UpperUIntegral, RectangleIntegral, VerticalIntegral"}

The difference of two vertical integrals and a rectangle is
  the difference of an upper and a lower U integrals.

### Proof {uses="LowerUIntegral, UpperUIntegral"}

Follows directly from the definitions.

## Theorem: existsDifferentiableOn-of-bddAbove {#existsDifferentiableOn_of_bddAbove lean="existsDifferentiableOn_of_bddAbove"}

If $f$ is differentiable on a set $s$ except at $c\in s$,
  and $f$ is bounded above on $s\setminus\{c\}$, then there
  exists a differentiable function $g$ on $s$ such that $f$
  and $g$ agree on $s\setminus\{c\}$.

### Proof

This is the Riemann Removable Singularity Theorem, slightly
  rephrased from what's in Mathlib. (We don't care what the
  function $g$ is, just that it's holomorphic.)

## Theorem: HolomorphicOn.vanishesOnRectangle {#HolomorphicOn.vanishesOnRectangle lean="HolomorphicOn.vanishesOnRectangle" uses="RectangleIntegral"}

If $f$ is holomorphic on a rectangle $z$ and $w$, then the
  integral of $f$ over the rectangle with corners $z$ and $w$
  is $0$.

### Proof

This is in a Mathlib PR.

The next lemma allows to zoom a big rectangle down to a small
square, centered at a pole.

## Lemma: RectanglePullToNhdOfPole {#RectanglePullToNhdOfPole lean="RectanglePullToNhdOfPole" uses="RectangleIntegral"}

If $f$ is holomorphic on a rectangle $z$ and $w$ except at
  a point $p$, then the integral of $f$ over the rectangle
  with corners $z$ and $w$ is the same as the integral of $f$
  over a small square centered at $p$.

### Proof {uses="HolomorphicOn.vanishesOnRectangle, RectangleBorder"}

Chop the big rectangle with two vertical cuts and two
  horizontal cuts into smaller rectangles, the middle one
  being the desired square. The integral over each of the
  outer rectangles vanishes, since $f$ is holomorphic there.
  (The constant $c$ being ``small enough'' here just means
  that the inner square is strictly contained in the big
  rectangle.)

## Lemma: ResidueTheoremAtOrigin {#ResidueTheoremAtOrigin lean="ResidueTheoremAtOrigin" uses="RectangleIntegral"}

The rectangle (square) integral of $f(s) = 1/s$ with
  corners $-1-i$ and $1+i$ is equal to $2\pi i$.

### Proof

This is a special case of the more general result above.

## Lemma: ResidueTheoremOnRectangleWithSimplePole {#ResidueTheoremOnRectangleWithSimplePole lean="ResidueTheoremOnRectangleWithSimplePole" uses="RectangleIntegral"}

Suppose that $f$ is a holomorphic function on a rectangle,
  except for a simple pole at $p$.
  By the latter, we mean that there is a function $g$
  holomorphic on the rectangle such that,
  $f = g + A/(s-p)$ for some $A\in\mathbb{C}$. Then the integral of
  $f$ over the rectangle is $A$.

### Proof {uses="HolomorphicOn.vanishesOnRectangle, RectangleBorder"}

Replace $f$ with $g + A/(s-p)$ in the integral.
  The integral of $g$ vanishes by
  Lemma [HolomorphicOn.vanishesOnRectangle](#HolomorphicOn.vanishesOnRectangle).
  To evaluate the integral of $1/(s-p)$, pull everything to a
  square about the origin using
  Lemma [RectanglePullToNhdOfPole](#RectanglePullToNhdOfPole), and rescale by $c$;
  what remains is handled by
  Lemma [ResidueTheoremAtOrigin](#ResidueTheoremAtOrigin).

**Perron Formula**

In this section, we prove the Perron formula, which plays a key role in our proof of Mellin
inversion.

The following is preparatory material used in the proof of the Perron formula, see Lemma
[formulaLtOne](#formulaLtOne).

## Lemma: zeroTendstoDiff {#zeroTendstoDiff lean="zeroTendstoDiff"}

If the limit of $0$ is $L_1 - L_2$, then $L_1 = L_2$.

### Proof

Obvious.

## Lemma: RectangleIntegral-tendsTo-VerticalIntegral {#RectangleIntegral_tendsTo_VerticalIntegral lean="RectangleIntegral_tendsTo_VerticalIntegral" uses="RectangleIntegral, VerticalIntegral"}

Let $\sigma,\sigma' \in \mathbb{R}$, and $f : \mathbb{C} \to \mathbb{C}$ such that
  the vertical integrals $\int_{(\sigma)}f(s)ds$ and $\int_{(\sigma')}f(s)ds$ exist and
  the horizontal integral $\int_{(\sigma)}^{\sigma'}f(x + yi)dx$ vanishes as $y \to \pm \infty$.
  Then the limit of rectangle integrals
  
$$
\lim_{T\to\infty}\int_{\sigma-iT}^{\sigma'+iT}f(s)ds =
  \int_{(\sigma')}f(s)ds - \int_{(\sigma)}f(s)ds.
$$

### Proof {uses="RectangleIntegral"}

Almost by definition.

## Lemma: RectangleIntegral-tendsTo-UpperU {#RectangleIntegral_tendsTo_UpperU lean="RectangleIntegral_tendsTo_UpperU" uses="UpperUIntegral, RectangleIntegral"}

Let $\sigma,\sigma' \in \mathbb{R}$, and $f : \mathbb{C} \to \mathbb{C}$ such that
  the vertical integrals $\int_{(\sigma)}f(s)ds$ and $\int_{(\sigma')}f(s)ds$ exist and
  the horizontal integral $\int_{(\sigma)}^{\sigma'}f(x + yi)dx$ vanishes as $y \to \pm \infty$.
  Then the limit of rectangle integrals
  
$$
\int_{\sigma+iT}^{\sigma'+iU}f(s)ds
$$

  as $U\to\infty$ is the ``UpperUIntegral'' of $f$.

### Proof {uses="UpperUIntegral, RectangleIntegral"}

Almost by definition.

## Lemma: RectangleIntegral-tendsTo-LowerU {#RectangleIntegral_tendsTo_LowerU lean="RectangleIntegral_tendsTo_LowerU" uses="LowerUIntegral, RectangleIntegral"}

Let $\sigma,\sigma' \in \mathbb{R}$, and $f : \mathbb{C} \to \mathbb{C}$ such that
  the vertical integrals $\int_{(\sigma)}f(s)ds$ and $\int_{(\sigma')}f(s)ds$ exist and
  the horizontal integral $\int_{(\sigma)}^{\sigma'}f(x + yi)dx$ vanishes as $y \to -\infty$.
  Then the limit of rectangle integrals
  
$$
\int_{\sigma-iU}^{\sigma'-iT}f(s)ds
$$

  as $U\to\infty$ is the ``LowerUIntegral'' of $f$.

### Proof {uses="LowerUIntegral, RectangleIntegral"}

Almost by definition.

TODO : Move to general section

## Lemma: limitOfConstant {#limitOfConstant lean="limitOfConstant"}

Let $a:\mathbb{R}\to\mathbb{C}$ be a function, and let $\sigma>0$ be a real number. Suppose that, for all
  $\sigma, \sigma'>0$, we have $a(\sigma')=a(\sigma)$, and that
  $\lim_{\sigma\to\infty}a(\sigma)=0$. Then $a(\sigma)=0$.

### Proof

$$
\begin{aligned}
  \lim_{\sigma'\to\infty}a(\sigma) &= \lim_{\sigma'\to\infty}a(\sigma') \\
  &= 0
  \end{aligned}
$$

## Lemma: limitOfConstantLeft {#limitOfConstantLeft lean="limitOfConstantLeft"}

Let $a:\mathbb{R}\to\mathbb{C}$ be a function, and let $\sigma<-3/2$ be a real number. Suppose that, for all
  $\sigma, \sigma'>0$, we have $a(\sigma')=a(\sigma)$, and that
  $\lim_{\sigma\to-\infty}a(\sigma)=0$. Then $a(\sigma)=0$.

### Proof

$$
\begin{aligned}
    \lim_{\sigma'\to-\infty}a(\sigma) &= \lim_{\sigma'\to-\infty}a(\sigma') \\
    &= 0
  \end{aligned}
$$

## Lemma: tendsto-rpow-atTop-nhds-zero-of-norm-lt-one {#tendsto_rpow_atTop_nhds_zero_of_norm_lt_one lean="tendsto_rpow_atTop_nhds_zero_of_norm_lt_one"}

Let $x>0$ and $x<1$. Then
  
$$
\lim_{\sigma\to\infty}x^\sigma=0.
$$

### Proof

Standard.

## Lemma: tendsto-rpow-atTop-nhds-zero-of-norm-gt-one {#tendsto_rpow_atTop_nhds_zero_of_norm_gt_one lean="tendsto_rpow_atTop_nhds_zero_of_norm_gt_one"}

Let $x>1$. Then 
$$
\lim_{\sigma\to-\infty}x^\sigma=0.
$$

### Proof {uses="tendsto_rpow_atTop_nhds_zero_of_norm_lt_one"}

Standard.

## Lemma: isHolomorphicOn {#isHolomorphicOn lean="Perron.isHolomorphicOn"}

Let $x>0$. Then the function $f(s) = x^s/(s(s+1))$ is holomorphic on the half-plane
  $\{s\in\mathbb{C}:\Re(s)>0\}$.

### Proof

Composition of differentiabilities.

## Lemma: integralPosAux {#integralPosAux lean="Perron.integralPosAux"}

The integral
  
$$
\int_\mathbb{R}\frac{1}{|(1+t^2)(2+t^2)|^{1/2}}dt
$$

  is positive (and hence convergent - since a divergent integral is zero in Lean, by
  definition).

### Proof

This integral is between $\frac{1}{2}$ and $1$ of the integral of $\frac{1}{1+t^2}$,
  which is $\pi$.

## Lemma: vertIntBound {#vertIntBound lean="Perron.vertIntBound" uses="VerticalIntegral"}

Let $x>0$ and $\sigma>1$. Then
  
$$
\left|
  \int_{(\sigma)}\frac{x^s}{s(s+1)}ds\right| \leq
    x^\sigma \int_\mathbb{R}\frac{1}{|(1+t ^ 2)(2+t ^ 2)|^{1/2}}dt.
$$

### Proof {uses="integralPosAux"}

Triangle inequality and pointwise estimate.

## Lemma: vertIntBoundLeft {#vertIntBoundLeft lean="Perron.vertIntBoundLeft" uses="VerticalIntegral"}

Let $x>1$ and $\sigma<-3/2$. Then
  
$$
\left|
  \int_{(\sigma)}\frac{x^s}{s(s+1)}ds\right| \leq
    x^\sigma \int_\mathbb{R}\frac{1}{|(1/4+t ^ 2)(2+t ^ 2)|^{1/2}}dt.
$$

### Proof

Triangle inequality and pointwise estimate.

## Lemma: isIntegrable {#isIntegrable lean="Perron.isIntegrable"}

Let $x>0$ and $\sigma\in\mathbb{R}$. Then
  
$$
\int_{\mathbb{R}}\frac{x^{\sigma+it}}{(\sigma+it)(1+\sigma + it)}dt
$$

  is integrable.

### Proof {uses="isHolomorphicOn"}

By [isHolomorphicOn](#isHolomorphicOn), $f$ is continuous, so it is integrable on any interval.

Also, $|f(x)| = \Theta(x^{-2})$ as $x\to\infty$,

and $|f(-x)| = \Theta(x^{-2})$ as $x\to\infty$.

Since $g(x) = x^{-2}$ is integrable on $[a,\infty)$ for any $a>0$, we conclude.

## Lemma: tendsto-zero-Lower {#tendsto_zero_Lower lean="Perron.tendsto_zero_Lower"}

Let $x>0$ and $\sigma',\sigma''\in\mathbb{R}$. Then
  
$$
\int_{\sigma'}^{\sigma''}\frac{x^{\sigma+it}}{(\sigma+it)(1+\sigma + it)}d\sigma
$$

  goes to $0$ as $t\to-\infty$.

### Proof

The numerator is bounded and the denominator tends to infinity.

## Lemma: tendsto-zero-Upper {#Perron.tendsto_zero_Upper lean="Perron.tendsto_zero_Upper"}

Let $x>0$ and $\sigma',\sigma''\in\mathbb{R}$. Then
  
$$
\int_{\sigma'}^{\sigma''}\frac{x^{\sigma+it}}{(\sigma+it)(1+\sigma + it)}d\sigma
$$

  goes to $0$ as $t\to\infty$.

### Proof

The numerator is bounded and the denominator tends to infinity.

We are ready for the first case of the Perron formula, namely when $x<1$:

## Lemma: formulaLtOne {#formulaLtOne lean="Perron.formulaLtOne" uses="VerticalIntegral"}

For $x>0$, $\sigma>0$, and $x<1$, we have
  
$$
\frac1{2\pi i}
  \int_{(\sigma)}\frac{x^s}{s(s+1)}ds =0.
$$

### Proof {uses="vertIntBound, limitOfConstant, zeroTendstoDiff, tendsto_zero_Lower, isIntegrable, Perron.tendsto_zero_Upper, RectangleIntegral_tendsTo_VerticalIntegral, tendsto_rpow_atTop_nhds_zero_of_norm_lt_one, integralPosAux, RectangleIntegral, isHolomorphicOn"}

Let $f(s) = x^s/(s(s+1))$. Then $f$ is holomorphic on the half-plane
  $\{s\in\mathbb{C}:\Re(s)>0\}$. The rectangle integral of $f$ with corners $\sigma-iT$ and
  $\sigma+iT$ is zero. The limit of this rectangle integral as $T\to\infty$ is
  $\int_{(\sigma')}-\int_{(\sigma)}$. Therefore, $\int_{(\sigma')}=\int_{(\sigma)}$.

But we also have the bound $\int_{(\sigma')} \leq x^{\sigma'} * C$, where
  $C=\int_\mathbb{R}\frac{1}{|(1+t)(1+t+1)|}dt$.

Therefore $\int_{(\sigma')}\to 0$ as $\sigma'\to\infty$.

So pulling contours gives $\int_{(\sigma)}=0$.

The second case is when $x>1$.
Here are some auxiliary lemmata for the second case.
TODO: Move to more general section

## Lemma: keyIdentity {#keyIdentity lean="Perron.keyIdentity"}

Let $x\in \mathbb{R}$ and $s \ne 0, -1$. Then
  
$$
\frac{x^\sigma}{s(1+s)} = \frac{x^\sigma}{s} - \frac{x^\sigma}{1+s}
$$

### Proof

By ring.

## Lemma: diffBddAtZero {#diffBddAtZero lean="Perron.diffBddAtZero"}

Let $x>0$. Then for $0 < c < 1 /2$, we have that the function
  
$$
s ↦ \frac{x^s}{s(s+1)} - \frac1s
$$

  is bounded above on the rectangle with corners at $-c-i*c$ and $c+i*c$ (except at $s=0$).

### Proof {uses="keyIdentity"}

Applying Lemma [keyIdentity](#keyIdentity), the
   function $s ↦ x^s/s(s+1) - 1/s = x^s/s - x^0/s - x^s/(1+s)$. The last term is bounded for $s$
   away from $-1$. The first two terms are the difference quotient of the function $s ↦ x^s$ at
   $0$; since it's differentiable, the difference remains bounded as $s\to 0$.

## Lemma: diffBddAtNegOne {#diffBddAtNegOne lean="Perron.diffBddAtNegOne"}

Let $x>0$. Then for $0 < c < 1 /2$, we have that the function
  
$$
s ↦ \frac{x^s}{s(s+1)} - \frac{-x^{-1}}{s+1}
$$

  is bounded above on the rectangle with corners at $-1-c-i*c$ and $-1+c+i*c$ (except at $s=-1$).

### Proof {uses="keyIdentity"}

Applying Lemma [keyIdentity](#keyIdentity), the
   function $s ↦ x^s/s(s+1) - x^{-1}/(s+1) = x^s/s - x^s/(s+1) - (-x^{-1})/(s+1)$. The first term
   is bounded for $s$
   away from $0$. The last two terms are the difference quotient of the function $s ↦ x^s$ at
   $-1$; since it's differentiable, the difference remains bounded as $s\to -1$.

## Lemma: residueAtZero {#residueAtZero lean="Perron.residueAtZero" uses="RectangleIntegral"}

Let $x>0$. Then for all sufficiently small $c>0$, we have that
  
$$
\frac1{2\pi i}
  \int_{-c-i*c}^{c+ i*c}\frac{x^s}{s(s+1)}ds = 1.
$$

### Proof {uses="diffBddAtZero, ResidueTheoremOnRectangleWithSimplePole, existsDifferentiableOn_of_bddAbove, isHolomorphicOn"}

For $c>0$ sufficiently small,

$x^s/(s(s+1))$ is equal to $1/s$ plus a function, $g$, say,
  holomorphic in the whole rectangle (by Lemma [diffBddAtZero](#diffBddAtZero)).

Now apply Lemma [ResidueTheoremOnRectangleWithSimplePole](#ResidueTheoremOnRectangleWithSimplePole).

## Lemma: residueAtNegOne {#residueAtNegOne lean="Perron.residueAtNegOne" uses="RectangleIntegral"}

Let $x>0$. Then for all sufficiently small $c>0$, we have that
  
$$
\frac1{2\pi i}
  \int_{-c-i*c-1}^{c+ i*c-1}\frac{x^s}{s(s+1)}ds = -\frac1x.
$$

### Proof {uses="ResidueTheoremOnRectangleWithSimplePole, diffBddAtNegOne, existsDifferentiableOn_of_bddAbove, isHolomorphicOn"}

Compute the integral.

## Lemma: residuePull1 {#residuePull1 lean="Perron.residuePull1" uses="VerticalIntegral"}

For $x>1$ (of course $x>0$ would suffice) and $\sigma>0$, we have
  
$$
\frac1{2\pi i}
  \int_{(\sigma)}\frac{x^s}{s(s+1)}ds =1
  +
  \frac 1{2\pi i}
  \int_{(-1/2)}\frac{x^s}{s(s+1)}ds.
$$

### Proof {uses="residueAtZero, HolomorphicOn.vanishesOnRectangle, tendsto_zero_Lower, isIntegrable, Perron.tendsto_zero_Upper, RectangleBorder, RectangleIntegral_tendsTo_VerticalIntegral, RectangleIntegral, isHolomorphicOn"}

We pull to a square with corners at $-c-i*c$ and $c+i*c$ for $c>0$
  sufficiently small.
  By Lemma [residueAtZero](#residueAtZero), the integral over this square is equal to $1$.

## Lemma: residuePull2 {#residuePull2 lean="Perron.residuePull2" uses="VerticalIntegral"}

For $x>1$, we have
  
$$
\frac1{2\pi i}
  \int_{(-1/2)}\frac{x^s}{s(s+1)}ds = -1/x +
  \frac 1{2\pi i}
  \int_{(-3/2)}\frac{x^s}{s(s+1)}ds.
$$

### Proof {uses="HolomorphicOn.vanishesOnRectangle, tendsto_zero_Lower, isIntegrable, Perron.tendsto_zero_Upper, RectangleBorder, residueAtNegOne, RectangleIntegral_tendsTo_VerticalIntegral, RectangleIntegral, isHolomorphicOn"}

Pull contour from $(-1/2)$ to $(-3/2)$.

## Lemma: contourPull3 {#contourPull3 lean="Perron.contourPull3" uses="VerticalIntegral"}

For $x>1$ and $\sigma<-3/2$, we have
  
$$
\frac1{2\pi i}
  \int_{(-3/2)}\frac{x^s}{s(s+1)}ds = \frac 1{2\pi i}
  \int_{(\sigma)}\frac{x^s}{s(s+1)}ds.
$$

### Proof {uses="zeroTendstoDiff, tendsto_zero_Lower, isIntegrable, Perron.tendsto_zero_Upper, RectangleIntegral_tendsTo_VerticalIntegral, RectangleIntegral, isHolomorphicOn"}

Pull contour from $(-3/2)$ to $(\sigma)$.

## Lemma: formulaGtOne {#formulaGtOne lean="Perron.formulaGtOne" uses="VerticalIntegral"}

For $x>1$ and $\sigma>0$, we have
  
$$
\frac1{2\pi i}
  \int_{(\sigma)}\frac{x^s}{s(s+1)}ds =1-1/x.
$$

### Proof {uses="vertIntBoundLeft, residuePull1, tendsto_rpow_atTop_nhds_zero_of_norm_gt_one, residuePull2, limitOfConstantLeft, contourPull3"}

Let $f(s) = x^s/(s(s+1))$. Then $f$ is holomorphic on $\mathbb{C} \setminus {0,-1}$.

First pull the contour from $(\sigma)$ to $(-1/2)$, picking up a residue $1$ at $s=0$.

Next pull the contour from $(-1/2)$ to $(-3/2)$, picking up a residue $-1/x$ at
  $s=-1$.

Then pull the contour all the way to $(\sigma')$ with $\sigma'<-3/2$.

For $\sigma' < -3/2$, the integral is bounded by
  $x^{\sigma'}\int_\mathbb{R}\frac{1}{|(1+t ^ 2)(2+t ^ 2)|^{1/2}}dt$.

Therefore $\int_{(\sigma')}\to 0$ as $\sigma'\to\infty$.

So pulling contours gives $\int_{(-3/2)}=0$.

The two together give the Perron formula. (Which doesn't need to be a separate lemma.)

For $x>0$ and $\sigma>0$, we have

$$
\frac1{2\pi i}
\int_{(\sigma)}\frac{x^s}{s(s+1)}ds = \begin{cases}
1-\frac1x & \text{ if }x>1\\
0 & \text{ if } x<1
\end{cases}.
$$

**Mellin transforms**

## Lemma: PartialIntegration {#PartialIntegration lean="PartialIntegration"}

Let $f, g$ be once differentiable functions from $\mathbb{R}_{>0}$ to $\mathbb{C}$ so that $fg'$
  and $f'g$ are both integrable, and $f\cdot g (x)\to 0$ as $x\to 0^+,\infty$.
  Then
  
$$
\int_0^\infty f(x)g'(x) dx = -\int_0^\infty f'(x)g(x)dx.
$$

### Proof

Partial integration.

In this section, we define the Mellin transform (already in Mathlib, thanks to David Loeffler),
prove its inversion formula, and
derive a number of important properties of some special functions and bumpfunctions.

Def: (Already in Mathlib)
Let $f$ be a function from $\mathbb{R}_{>0}$ to $\mathbb{C}$. We define the Mellin transform of
$f$ to be the function $\mathcal{M}(f)$ from $\mathbb{C}$ to $\mathbb{C}$ defined by

$$
\mathcal{M}(f)(s) = \int_0^\infty f(x)x^{s-1}dx.
$$

[Note: My preferred way to think about this is that we are integrating over the multiplicative
group $\mathbb{R}_{>0}$, multiplying by a (not necessarily unitary!) character $|\cdot|^s$, and
integrating with respect to the invariant Haar measure $dx/x$. This is very useful in the kinds
of calculations carried out below. But may be more difficult to formalize as things now stand. So
we might have clunkier calculations, which ``magically'' turn out just right - of course they're
explained by the aforementioned structure...]

Finally, we need Mellin Convolutions and properties thereof.

## Definition: MellinConvolution {#MellinConvolution lean="MellinConvolution"}

Let $f$ and $g$ be functions from $\mathbb{R}_{>0}$ to $\mathbb{C}$. Then we define the
  Mellin convolution of $f$ and $g$ to be the function $f\ast g$ from $\mathbb{R}_{>0}$
  to $\mathbb{C}$ defined by
  
$$
(f\ast g)(x) = \int_0^\infty f(y)g(x/y)\frac{dy}{y}.
$$

Let us start with a simple property of the Mellin convolution.

## Lemma: MellinConvolutionSymmetric {#MellinConvolutionSymmetric lean="MellinConvolutionSymmetric" uses="MellinConvolution"}

Let $f$ and $g$ be functions from $\mathbb{R}_{>0}$ to $\mathbb{R}$ or $\mathbb{C}$, for $x\neq0$,
  
$$
(f\ast g)(x)=(g\ast f)(x)
    .
$$

### Proof

By Definition [MellinConvolution](#MellinConvolution),
  
$$
(f\ast g)(x) = \int_0^\infty f(y)g(x/y)\frac{dy}{y}
$$

  in which we change variables to $z=x/y$:
  
$$
(f\ast g)(x) = \int_0^\infty f(x/z)g(z)\frac{dz}{z}
    =(g\ast f)(x)
    .
$$

The Mellin transform of a convolution is the product of the Mellin transforms.

## Theorem: MellinConvolutionTransform {#MellinConvolutionTransform lean="MellinConvolutionTransform" uses="MellinConvolution"}

Let $f$ and $g$ be functions from $\mathbb{R}_{>0}$ to $\mathbb{C}$ such that
  
$$
    (x,y)\mapsto f(y)\frac{g(x/y)}yx^{s-1}
$$

  is absolutely integrable on $[0,\infty)^2$.
  Then
  
$$
\mathcal{M}(f\ast g)(s) = \mathcal{M}(f)(s)\mathcal{M}(g)(s).
$$

### Proof

By Definitions (MellinTransform) and [MellinConvolution](#MellinConvolution)
  
$$
\mathcal M(f\ast g)(s)=
    \int_0^\infty \int_0^\infty f(y)g(x/y)x^{s-1}\frac{dy}ydx
$$

  By ((eq:assm_integrable_Mconv)) and Fubini's theorem,
  
$$
\mathcal M(f\ast g)(s)=
    \int_0^\infty \int_0^\infty f(y)g(x/y)x^{s-1}dx\frac{dy}y
$$

  in which we change variables from $x$ to $z=x/y$:
  
$$
\mathcal M(f\ast g)(s)=
    \int_0^\infty \int_0^\infty f(y)g(z)y^{s-1}z^{s-1}dzdy
$$

  which, by Definition (MellinTransform), is
  
$$
\mathcal M(f\ast g)(s)=
    \mathcal M(f)(s)\mathcal M(g)(s)
    .
$$

The $\nu$ function has Mellin transform $\mathcal{M}(\nu)(s)$ which is entire and decays (at
least) like $1/|s|$.

[Of course it decays faster than any power of $|s|$, but it turns out that we will just need one
power.]

## Theorem: MellinOfPsi {#MellinOfPsi lean="MellinOfPsi"}

The Mellin transform of $\nu$ is
  
$$
\mathcal{M}(\nu)(s) =  O\left(\frac{1}{|s|}\right),
$$

  as $|s|\to\infty$ with $\sigma_1 \le \Re(s) \le 2$.

### Proof {uses="PartialIntegration"}

Integrate by parts:
  
$$
\left|\int_0^\infty \nu(x)x^s\frac{dx}{x}\right| =
  \left|-\int_0^\infty \nu'(x)\frac{x^{s}}{s}dx\right|
$$

  
$$
\le \frac{1}{|s|} \int_{1/2}^2|\nu'(x)|x^{\Re(s)}dx.
$$

  Since $\Re(s)$ is bounded, the right-hand side is bounded by a
  constant times $1/|s|$.

We can make a delta spike out of this bumpfunction, as follows.

## Definition: DeltaSpike {#DeltaSpike lean="DeltaSpike"}

Let $\nu$ be a bumpfunction supported in $[1/2,2]$. Then for any $\epsilon>0$, we define the
  delta spike $\nu_\epsilon$ to be the function from $\mathbb{R}_{>0}$ to $\mathbb{C}$ defined by
  
$$
\nu_\epsilon(x) = \frac{1}{\epsilon}\nu\left(x^{\frac{1}{\epsilon}}\right).
$$

This spike still has mass one:

## Lemma: DeltaSpikeMass {#DeltaSpikeMass lean="DeltaSpikeMass" uses="DeltaSpike"}

For any $\epsilon>0$, we have
  
$$
\int_0^\infty \nu_\epsilon(x)\frac{dx}{x} = 1.
$$

### Proof

Substitute $y=x^{1/\epsilon}$, and use the fact that $\nu$ has mass one, and that $dx/x$ is Haar
  measure.

The Mellin transform of the delta spike is easy to compute.

## Theorem: MellinOfDeltaSpike {#MellinOfDeltaSpike lean="MellinOfDeltaSpike" uses="DeltaSpike"}

For any $\epsilon>0$, the Mellin transform of $\nu_\epsilon$ is
  
$$
\mathcal{M}(\nu_\epsilon)(s) = \mathcal{M}(\nu)\left(\epsilon s\right).
$$

### Proof

Substitute $y=x^{1/\epsilon}$, use Haar measure; direct calculation.

In particular, for $s=1$, we have that the Mellin transform of $\nu_\epsilon$ is $1+O(\epsilon)$.

## Corollary: MellinOfDeltaSpikeAt1 {#MellinOfDeltaSpikeAt1 lean="MellinOfDeltaSpikeAt1" uses="DeltaSpike"}

For any $\epsilon>0$, we have
  
$$
\mathcal{M}(\nu_\epsilon)(1) =
  \mathcal{M}(\nu)(\epsilon).
$$

### Proof {uses="MellinOfDeltaSpike"}

This is immediate from the above theorem.

## Lemma: MellinOfDeltaSpikeAt1-asymp {#MellinOfDeltaSpikeAt1_asymp lean="MellinOfDeltaSpikeAt1_asymp"}

As $\epsilon\to 0$, we have
  
$$
\mathcal{M}(\nu_\epsilon)(1) = 1+O(\epsilon).
$$

### Proof

By Lemma [MellinOfDeltaSpikeAt1](#MellinOfDeltaSpikeAt1),
  
$$
\mathcal M(\nu_\epsilon)(1)=\mathcal M(\nu)(\epsilon)
$$

  which by Definition (MellinTransform) is
  
$$
\mathcal M(\nu)(\epsilon)=\int_0^\infty\nu(x)x^{\epsilon-1}dx
    .
$$

  Since $\nu(x) x^{\epsilon-1}$ is integrable (because $\nu$ is continuous and compactly
  supported),
  
$$
\mathcal M(\nu)(\epsilon)-\int_0^\infty\nu(x)\frac{dx}x
    =\int_0^\infty\nu(x)(x^{\epsilon-1}-x^{-1})dx
    .
$$

  By Taylor's theorem,
  
$$
x^{\epsilon-1}-x^{-1}=O(\epsilon)
$$

  so, since $\nu$ is absolutely integrable,
  
$$
\mathcal M(\nu)(\epsilon)-\int_0^\infty\nu(x)\frac{dx}x=O(\epsilon)
    .
$$

  We conclude the proof using Theorem [SmoothExistence](#SmoothExistence).

Let $1_{(0,1]}$ be the function from $\mathbb{R}_{>0}$ to $\mathbb{C}$ defined by

$$
1_{(0,1]}(x) = \begin{cases}
1 & \text{ if }x\leq 1\\
0 & \text{ if }x>1
\end{cases}.
$$

This has Mellin transform:
[Note: this already exists in mathlib]

## Theorem: MellinOf1 {#MellinOf1 lean="MellinOf1"}

The Mellin transform of $1_{(0,1]}$ is
  
$$
\mathcal{M}(1_{(0,1]})(s) = \frac{1}{s}.
$$

### Proof

This is a straightforward calculation.

What will be essential for us is properties of the smooth version of $1_{(0,1]}$, obtained as the
 Mellin convolution of $1_{(0,1]}$ with $\nu_\epsilon$.

## Definition: Smooth1 {#Smooth1 lean="Smooth1"}

Let $\epsilon>0$. Then we define the smooth function $\widetilde{1_{\epsilon}}$ from
  $\mathbb{R}_{>0}$ to $\mathbb{C}$ by
  
$$
\widetilde{1_{\epsilon}} = 1_{(0,1]}\ast\nu_\epsilon.
$$

### Proof {uses="DeltaSpike, MellinConvolution"}

Let $c:=2^\epsilon > 1$, in terms of which we wish to prove
  
$$
-1 < c \log c - c .
$$

  Letting $f(x):=x\log x - x$, we can rewrite this as $f(1) < f(c)$.
  Since
  
$$
\frac {d}{dx}f(x) = \log x > 0 ,
$$

  $f$ is monotone increasing on [1, \infty), and we are done.

In particular, we have the following two properties.

## Lemma: Smooth1Properties-below {#Smooth1Properties_below lean="Smooth1Properties_below" uses="Smooth1"}

Fix $\epsilon>0$. There is an absolute constant $c>0$ so that:
  If $0 < x \leq (1-c\epsilon)$, then
  
$$
\widetilde{1_{\epsilon}}(x) = 1.
$$

### Proof {uses="DeltaSpikeMass, DeltaSpike, MellinConvolution"}

Opening the definition, we have that the Mellin convolution of $1_{(0,1]}$ with $\nu_\epsilon$ is
  
$$
\int_0^\infty 1_{(0,1]}(y)\nu_\epsilon(x/y)\frac{dy}{y}
  =
  \int_0^1 \nu_\epsilon(x/y)\frac{dy}{y}.
$$

  The support of $\nu_\epsilon$ is contained in $[1/2^\epsilon,2^\epsilon]$, so it suffices to
  consider $y \in [1/2^\epsilon x,2^\epsilon x]$ for nonzero contributions. If $x < 2^{-\epsilon}$,
  then the integral is the same as that over $(0,\infty)$:
  
$$
\int_0^1 \nu_\epsilon(x/y)\frac{dy}{y}
  =
  \int_0^\infty \nu_\epsilon(x/y)\frac{dy}{y},
$$

  in which we change variables to $z=x/y$ (using $x>0$):
  
$$
\int_0^\infty \nu_\epsilon(x/y)\frac{dy}{y}
  =
  \int_0^\infty \nu_\epsilon(z)\frac{dz}{z},
$$

  which is equal to one by Lemma [DeltaSpikeMass](#DeltaSpikeMass).
  We then choose
  
$$
c:=\log 2,
$$

  which satisfies
  
$$
c > \frac{1-2^{-\epsilon}}\epsilon
$$

  by Lemma (Smooth1Properties_estimate), so
  
$$
1-c\epsilon < 2^{-\epsilon}.
$$

## Lemma: Smooth1Properties-above {#Smooth1Properties_above lean="Smooth1Properties_above" uses="Smooth1"}

Fix $0<\epsilon<1$. There is an absolute constant $c>0$ so that:
  if $x\geq (1+c\epsilon)$, then
  
$$
\widetilde{1_{\epsilon}}(x) = 0.
$$

### Proof {uses="DeltaSpike, MellinConvolution"}

Again the Mellin convolution is
  
$$
\int_0^1 \nu_\epsilon(x/y)\frac{dy}{y},
$$

  but now if $x > 2^\epsilon$, then the support of $\nu_\epsilon$ is disjoint
  from the region of integration, and hence the integral is zero.
  We choose
  
$$
c:=2\log 2
    .
$$

  By Lemma (Smooth1Properties_estimate),
  
$$
c > 2\frac{1-2^{-\epsilon}}\epsilon > 2^\epsilon\frac{1-2^{-\epsilon}}\epsilon
    =
    \frac{2^\epsilon-1}\epsilon,
$$

  so
  
$$
1+c\epsilon > 2^\epsilon.
$$

## Lemma: Smooth1Nonneg {#Smooth1Nonneg lean="Smooth1Nonneg" uses="Smooth1"}

If $\nu$ is nonnegative, then $\widetilde{1_{\epsilon}}(x)$ is nonnegative.

### Proof {uses="DeltaSpike, MellinConvolution"}

By Definitions [Smooth1](#Smooth1), [MellinConvolution](#MellinConvolution) and [DeltaSpike](#DeltaSpike)
  
$$
\widetilde{1_\epsilon}(x)
    =\int_0^\infty 1_{(0,1]}(y)\frac1\epsilon\nu((x/y)^{\frac1\epsilon}) \frac{dy}y
$$

  and all the factors in the integrand are nonnegative.

## Lemma: Smooth1LeOne {#Smooth1LeOne lean="Smooth1LeOne" uses="Smooth1"}

If $\nu$ is nonnegative and has mass one, then $\widetilde{1_{\epsilon}}(x)\le 1$, $\forall x>0$.

### Proof {uses="DeltaSpike, MellinConvolution"}

By Definitions [Smooth1](#Smooth1), [MellinConvolution](#MellinConvolution) and [DeltaSpike](#DeltaSpike)
  
$$
\widetilde{1_\epsilon}(x)
    =\int_0^\infty 1_{(0,1]}(y)\frac1\epsilon\nu((x/y)^{\frac1\epsilon}) \frac{dy}y
$$

  and since $1_{(0,1]}(y)\le 1$, and all the factors in the integrand are nonnegative,
  
$$
\widetilde{1_\epsilon}(x)\le\int_0^\infty \frac1\epsilon\nu((x/y)^{\frac1\epsilon}) \frac{dy}y
$$

  (because in mathlib the integral of a non-integrable function is $0$, for the inequality above
  to be true, we must prove that $\nu((x/y)^{\frac1\epsilon})/y$ is integrable; this follows from
  the computation below).
  We then change variables to $z=(x/y)^{\frac1\epsilon}$:
  
$$
\widetilde{1_\epsilon}(x)\le\int_0^\infty \nu(z) \frac{dz}z
$$

  which by Theorem [SmoothExistence](#SmoothExistence) is 1.

Combining the above, we have the following three Main Lemmata of this section on the Mellin
transform of $\widetilde{1_{\epsilon}}$.

## Lemma: MellinOfSmooth1a {#MellinOfSmooth1a lean="MellinOfSmooth1a" uses="Smooth1"}

Fix  $\epsilon>0$. Then the Mellin transform of $\widetilde{1_{\epsilon}}$ is
  
$$
\mathcal{M}(\widetilde{1_{\epsilon}})(s) =
  \frac{1}{s}\left(\mathcal{M}(\nu)\left(\epsilon s\right)\right).
$$

### Proof {uses="MellinOf1, MellinOfDeltaSpike, DeltaSpike, MellinConvolution, MellinConvolutionTransform, MellinConvolutionSymmetric"}

By Definition [Smooth1](#Smooth1),
  
$$
\mathcal M(\widetilde{1_\epsilon})(s)
    =\mathcal M(1_{(0,1]}\ast\nu_\epsilon)(s)
    .
$$

  We wish to apply Theorem [MellinConvolutionTransform](#MellinConvolutionTransform).
  To do so, we must prove that
  
$$
(x,y)\mapsto 1_{(0,1]}(y)\nu_\epsilon(x/y)/y
$$

  is integrable on $[0,\infty)^2$.
  It is actually easier to do this for the convolution: $\nu_\epsilon\ast 1_{(0,1]}$, so we use
  Lemma [MellinConvolutionSymmetric](#MellinConvolutionSymmetric): for $x\neq0$,
  
$$
1_{(0,1]}\ast\nu_\epsilon(x)=\nu_\epsilon\ast 1_{(0,1]}(x)
    .
$$

  Now, for $x=0$, both sides of the equation are 0, so the equation also holds for $x=0$.
  Therefore,
  
$$
\mathcal M(\widetilde{1_\epsilon})(s)
    =\mathcal M(\nu_\epsilon\ast 1_{(0,1]})(s)
    .
$$

  Now,
  
$$
(x,y)\mapsto \nu_\epsilon(y)1_{(0,1]}(x/y)\frac{x^{s-1}}y
$$

  has compact support that is bounded away from $y=0$ (specifically
  $y\in[2^{-\epsilon},2^\epsilon]$ and $x\in(0,y]$), so it is integrable.
  We can thus apply Theorem [MellinConvolutionTransform](#MellinConvolutionTransform) and find
  
$$
\mathcal M(\widetilde{1_\epsilon})(s)
    =\mathcal M(\nu_\epsilon)(s)\mathcal M(1_{(0,1]})(s)
    .
$$

  By Lemmas [MellinOf1](#MellinOf1) and [MellinOfDeltaSpike](#MellinOfDeltaSpike),
  
$$
\mathcal M(\widetilde{1_\epsilon})(s)
    =\frac1s\mathcal M(\nu)(\epsilon s)
    .
$$

## Lemma: MellinOfSmooth1b {#MellinOfSmooth1b lean="MellinOfSmooth1b" uses="Smooth1"}

Given $0<\sigma_1\le\sigma_2$, for any $s$ such that $\sigma_1\le\mathcal Re(s)\le\sigma_2$,
  we have
  
$$
\mathcal{M}(\widetilde{1_{\epsilon}})(s) = O\left(\frac{1}{\epsilon|s|^2}\right).
$$

### Proof {uses="MellinOfSmooth1a, MellinOfPsi"}

Use Lemma [MellinOfSmooth1a](#MellinOfSmooth1a) and the bound in Lemma [MellinOfPsi](#MellinOfPsi).

## Lemma: MellinOfSmooth1c {#MellinOfSmooth1c lean="MellinOfSmooth1c" uses="Smooth1"}

At $s=1$, we have
  
$$
\mathcal{M}(\widetilde{1_{\epsilon}})(1) = 1+O(\epsilon)).
$$

### Proof {uses="MellinOfDeltaSpikeAt1_asymp, MellinOfSmooth1a"}

Follows from Lemmas [MellinOfSmooth1a](#MellinOfSmooth1a), [MellinOfDeltaSpikeAt1](#MellinOfDeltaSpikeAt1) and
  [MellinOfDeltaSpikeAt1-asymp](#MellinOfDeltaSpikeAt1_asymp).

## Lemma: Smooth1ContinuousAt {#Smooth1ContinuousAt lean="Smooth1ContinuousAt" uses="Smooth1"}

Fix a nonnegative, continuously differentiable function $F$ on $\mathbb{R}$ with support in
  $[1/2,2]$. Then for any $\epsilon>0$, the function
  $x \mapsto \int_{(0,\infty)} x^{1+it} \widetilde{1_{\epsilon}}(x) dx$ is continuous at any $y>0$.

### Proof {uses="DeltaSpike, MellinConvolution, MellinConvolutionSymmetric"}

Use Lemma (MellinconvolutionSymmetric) to write $\widetilde{1_{\epsilon}}(x)$ as an integral
  over an integral near $1$, in particular avoiding the singularity at $0$. The integrand may be
  bounded by $2^{\epsilon}\nu_\epsilon(t)$ which is independent of $x$ and we can use dominated
  convergence to prove continuity.

Let $\nu$ be a bumpfunction.

## Theorem: SmoothExistence {#SmoothExistence lean="SmoothExistence"}

There exists a smooth (once differentiable would be enough),
  nonnegative ``bumpfunction'' $\nu$,
  supported in $[1/2,2]$ with total mass one:
  
$$
\int_0^\infty \nu(x)\frac{dx}{x} = 1.
$$

### Proof

Same idea as Urysohn-type argument.

**Zeta Bounds**

Now in Mathlib:

## Theorem: deriv-conj-conj {#deriv_conj_conj' lean="deriv_conj_conj'"}

Let $f : \mathbb{C} \to \mathbb{C}$ be a function at $p \in \mathbb{C}$ with derivative $a$.
    Then the derivative of the function $g(z) = \overline{f(\overline{z})}$ at $\overline{p}$ is
    $\overline{a}$.

### Proof

We proceed by case analysis on whether $f$ is differentiable at $p$. If $f$ is differentiable
    at $p$, then we can apply the previous theorem. If $f$ is not differentiable at $p$, then
    neither is $g$, and both derivatives have the default value of zero.

## Theorem: conj-riemannZeta-conj-aux1 {#conj_riemannZeta_conj_aux1 lean="conj_riemannZeta_conj_aux1"}

Conjugation symmetry of the Riemann zeta function in the half-plane of convergence. Let
    $s \in \mathbb{C}$ with $\Re(s) > 1$. Then $\overline{\zeta(\overline{s})} = \zeta(s)$.

### Proof

We expand the definition of the Riemann zeta function as a series and find that the two sides
    are equal term by term.

## Theorem: conj-riemannZeta-conj {#conj_riemannZeta_conj lean="conj_riemannZeta_conj"}

Conjugation symmetry of the Riemann zeta function. Let $s \in \mathbb{C}$. Then
    
$$
\overline{\zeta(\overline{s})} = \zeta(s).
$$

### Proof {uses="conj_riemannZeta_conj_aux1"}

By the previous lemma, the two sides are equal on the half-plane
    $\{s \in \mathbb{C} : \Re(s) > 1\}$. Then, by analytic continuation, they are equal on the
    whole complex plane.

## Theorem: deriv-riemannZeta-conj {#deriv_riemannZeta_conj lean="deriv_riemannZeta_conj"}

Conjugation symmetry of the derivative of the Riemann zeta function. Let $s \in \mathbb{C}$.
    Then 
$$
\zeta'(\overline{s}) = \overline{\zeta'(s)}.
$$

### Proof {uses="deriv_conj_conj'"}

We apply the derivative conjugation symmetry to the Riemann zeta function and use the
    conjugation symmetry of the Riemann zeta function itself.

## Theorem: intervalIntegral-conj {#intervalIntegral_conj lean="intervalIntegral_conj"}

The conjugation symmetry of the interval integral. Let $f : \mathbb{R} \to \mathbb{C}$ be a
    measurable function, and let $a, b \in \mathbb{R}$. Then
    
$$
\int_{a}^{b} \overline{f(x)} \, dx = \overline{\int_{a}^{b} f(x) \, dx}.
$$

### Proof

We unfold the interval integral into an integral over a uIoc and use the conjugation property
    of integrals.

We record here some prelimiaries about the zeta function and general
holomorphic functions.

## Theorem: ResidueOfTendsTo {#ResidueOfTendsTo lean="ResidueOfTendsTo"}

If a function $f$ is holomorphic in a neighborhood of $p$ and
  $\lim_{s\to p} (s-p)f(s) = A$, then
  $f(s) = \frac{A}{s-p} + O(1)$ near $p$.

### Proof {uses="existsDifferentiableOn_of_bddAbove"}

The function $(s - p)\cdot f(s)$ bounded, so by Theorem
  [existsDifferentiableOn-of-bddAbove](#existsDifferentiableOn_of_bddAbove), there is a holomorphic function, $g$, say, so that
  $(s-p)f(s) = g(s)$ in a neighborhood of $s=p$, and $g(p)=A$. Now because $g$ is holomorphic,
  near $s=p$, we have $g(s)=A+O(s-p)$. Then when you divide by $(s-p)$, you get
  $f(s) = A/(s-p) + O(1)$.

## Theorem: riemannZetaResidue {#riemannZetaResidue lean="riemannZetaResidue"}

The Riemann zeta function $\zeta(s)$ has a simple pole at $s=1$ with residue $1$. In particular,
  the function $\zeta(s) - \frac{1}{s-1}$ is bounded in a neighborhood of $s=1$.

### Proof {uses="ResidueOfTendsTo"}

From `riemannZeta\_residue\_one` (in Mathlib), we know that
  $(s-1)\zeta(s)$ goes to $1$ as $s\to1$. Now apply Theorem [ResidueOfTendsTo](#ResidueOfTendsTo).
  (This can also be done using $\zeta_0$ below, which is expressed as
  $1/(s-1)$ plus things that are holomorphic for $\Re(s)>0$...)

## Theorem: nonZeroOfBddAbove {#nonZeroOfBddAbove lean="nonZeroOfBddAbove"}

If a function $f$ has a simple pole at a point $p$ with residue $A \neq 0$, then
  $f$ is nonzero in a punctured neighborhood of $p$.

### Proof

We know that $f(s) = \frac{A}{s-p} + O(1)$ near $p$, so we can write
  
$$
f(s) = \left(f(s) - \frac{A}{s-p}\right) + \frac{A}{s-p}.
$$

  The first term is bounded, say by $M$, and the second term goes to $\infty$ as $s \to p$.
  Therefore, there exists a neighborhood $V$ of $p$ such that for all $s \in V \setminus \{p\}$,
  we have $f(s) \neq 0$.

## Theorem: logDerivResidue {#logDerivResidue lean="logDerivResidue"}

If $f$ is holomorphic in a neighborhood of $p$, and there is a simple pole at $p$, then $f'/
  f$ has a simple pole at $p$ with residue $-1$:
  
$$
\frac{f'(s)}{f(s)} = \frac{-1}{s - p} + O(1).
$$

### Proof {uses="existsDifferentiableOn_of_bddAbove"}

Using Theorem [existsDifferentiableOn-of-bddAbove](#existsDifferentiableOn_of_bddAbove), there is a function $g$ holomorphic
  near $p$, for which $f(s) = A/(s-p) + g(s) = h(s)/ (s-p)$. Here $h(s):= A + g(s)(s-p)$ which
  is nonzero in a neighborhood of $p$ (since $h$ goes to $A$ which is nonzero).
  Then $f'(s) = (h'(s)(s-p) - h(s))/(s-p)^2$, and we can compute the quotient:
  
$$
\frac{f'(s)}{f(s)}+1/(s-p) = \frac{h'(s)(s-p) - h(s)}{h(s)} \cdot \frac{1}{(s-p)}+1/(s-p)
  =
  \frac{h'(s)}{h(s)}.
$$

  Since $h$ is nonvanishing near $p$, this remains bounded in a neighborhood of $p$.

## Theorem: BddAbove-to-IsBigO {#BddAbove_to_IsBigO lean="BddAbove_to_IsBigO"}

If $f$ is bounded above in a punctured neighborhood of $p$, then $f$ is $O(1)$ in that
  neighborhood.

### Proof

Elementary.

Let's also record that if a function $f$ has a simple pole at $p$ with residue $A$, and $g$ is
holomorphic near $p$, then the residue of $f \cdot g$ is $A \cdot g(p)$.

## Theorem: ResidueMult {#ResidueMult lean="ResidueMult"}

If $f$ has a simple pole at $p$ with residue $A$, and $g$ is holomorphic near $p$, then the
  residue of $f \cdot g$ at $p$ is $A \cdot g(p)$. That is, we assume that
  
$$
f(s) = \frac{A}{s - p} + O(1)
$$

  near $p$, and that $g$ is holomorphic near $p$. Then
  
$$
f(s) \cdot g(s) = \frac{A \cdot g(p)}{s - p} + O(1).
$$

### Proof

Elementary calculation.
  
$$
f(s) * g(s) - \frac{A * g(p)}{s - p} =
  \left(f(s) * g(s) - \frac{A * g(s)}{s - p}\right)
  + \left(\frac{A * g(s) - A * g(p)}{s - p}\right).
$$

  The first term is $g(s)(f(s) - \frac{A}{s - p})$, which is bounded near $p$ by the assumption
  on $f$
   and the fact that $g$ is holomorphic near $p$.
  The second term is $A$ times the log derivative of $g$ at $p$, which is bounded by the assumption
  that  $g$ is holomorphic.

As a corollary, the log derivative of the Riemann zeta function has a simple pole at $s=1$:

## Theorem: riemannZetaLogDerivResidue {#riemannZetaLogDerivResidue lean="riemannZetaLogDerivResidue"}

The log derivative of the Riemann zeta function $\zeta(s)$ has a simple pole at $s=1$ with
  residue $-1$: $-\frac{\zeta'(s)}{\zeta(s)} - \frac{1}{s-1} = O(1)$.

### Proof {uses="logDerivResidue, nonZeroOfBddAbove, riemannZetaResidue"}

This follows from Theorem [logDerivResidue](#logDerivResidue) and Theorem [riemannZetaResidue](#riemannZetaResidue).

## Definition: riemannZeta0 {#riemannZeta0 lean="riemannZeta0"}

For any natural $N\ge1$, we define
  
$$
\zeta_0(N,s) :=
  \sum_{1\le n \le N} \frac1{n^s}
  +
  \frac{- N^{1-s}}{1-s} + \frac{-N^{-s}}{2} + s \int_N^\infty \frac{\lfloor x\rfloor + 1/2 - x}{x^{s+1}} \, dx
$$

## Lemma: sum-eq-int-deriv {#sum_eq_int_deriv lean="sum_eq_int_deriv"}

Let $a < b$, and let $\phi$ be continuously differentiable on $[a, b]$.
  Then
  
$$
\sum_{a < n \le b} \phi(n) = \int_a^b \phi(x) \, dx
    + \left(\lfloor b \rfloor + \frac{1}{2} - b\right) \phi(b)
    - \left(\lfloor a \rfloor + \frac{1}{2} - a\right) \phi(a)
    - \int_a^b \left(\lfloor x \rfloor + \frac{1}{2} - x\right) \phi'(x) \, dx.
$$

### Proof

This is first order Euler-Maclaurin.

## Lemma: ZetaSum-aux1 {#ZetaSum_aux1 lean="ZetaSum_aux1"}

Let $0 < a < b$ be natural numbers and $s\in \mathbb{C}$ with $s \ne 1$ and $s \ne 0$.
  Then
  
$$
\sum_{a < n \le b} \frac{1}{n^s} =  \frac{b^{1-s} - a^{1-s}}{1-s} + \frac{b^{-s}-a^{-s}}{2}
    + s \int_a^b \frac{\lfloor x\rfloor + 1/2 - x}{x^{s+1}} \, dx.
$$

### Proof {uses="sum_eq_int_deriv"}

Apply Lemma [sum-eq-int-deriv](#sum_eq_int_deriv) to the function $x \mapsto x^{-s}$.

## Lemma: ZetaBnd-aux1a {#ZetaBnd_aux1a lean="ZetaBnd_aux1a"}

For any $0 < a < b$ and  $s \in \mathbb{C}$ with $\sigma=\Re(s)>0$,
  
$$
\int_a^b \left|\frac{\lfloor x\rfloor + 1/2 - x}{x^{s+1}} \, dx\right|
  \le \frac{a^{-\sigma}-b^{-\sigma}}{\sigma}.
$$

### Proof

Apply the triangle inequality
  
$$
\left|\int_a^b \frac{\lfloor x\rfloor + 1/2 - x}{x^{s+1}} \, dx\right|
  \le \int_a^b \frac{1}{x^{\sigma+1}} \, dx,
$$

  and evaluate the integral.

## Lemma: ZetaSum-aux2 {#ZetaSum_aux2 lean="ZetaSum_aux2"}

Let $N$ be a natural number and $s\in \mathbb{C}$, $\Re(s)>1$.
  Then
  
$$
\sum_{N < n} \frac{1}{n^s} =  \frac{- N^{1-s}}{1-s} + \frac{-N^{-s}}{2}
    + s \int_N^\infty \frac{\lfloor x\rfloor + 1/2 - x}{x^{s+1}} \, dx.
$$

### Proof {uses="ZetaSum_aux1"}

Apply Lemma [ZetaSum-aux1](#ZetaSum_aux1) with $a=N$ and $b\to \infty$.

## Lemma: ZetaBnd-aux1b {#ZetaBnd_aux1b lean="ZetaBnd_aux1b"}

For any $N\ge1$ and $s = \sigma + tI \in \mathbb{C}$, $\sigma > 0$,
  
$$
\left| \int_N^\infty \frac{\lfloor x\rfloor + 1/2 - x}{x^{s+1}} \, dx \right|
  \le \frac{N^{-\sigma}}{\sigma}.
$$

### Proof {uses="ZetaBnd_aux1a"}

Apply Lemma [ZetaBnd-aux1a](#ZetaBnd_aux1a) with $a=N$ and $b\to \infty$.

## Lemma: ZetaBnd-aux1 {#ZetaBnd_aux1 lean="ZetaBnd_aux1"}

For any $N\ge1$ and $s = \sigma + tI \in \mathbb{C}$, $\sigma=\in(0,2], 2 < |t|$,
  
$$
\left| s\int_N^\infty \frac{\lfloor x\rfloor + 1/2 - x}{x^{s+1}} \, dx \right|
  \le 2 |t| \frac{N^{-\sigma}}{\sigma}.
$$

### Proof {uses="ZetaBnd_aux1b"}

Apply Lemma [ZetaBnd-aux1b](#ZetaBnd_aux1b) and estimate $|s|\ll |t|$.

Big-Oh version of Lemma [ZetaBnd-aux1](#ZetaBnd_aux1).

## Lemma: ZetaBnd-aux1p {#ZetaBnd_aux1p lean="ZetaBnd_aux1p"}

For any $N\ge1$ and $s = \sigma + tI \in \mathbb{C}$, $\sigma=\in(0,2], 2 < |t|$,
  
$$
\left| s\int_N^\infty \frac{\lfloor x\rfloor + 1/2 - x}{x^{s+1}} \, dx \right|
  \ll |t| \frac{N^{-\sigma}}{\sigma}.
$$

### Proof {uses="ZetaBnd_aux1b"}

Apply Lemma [ZetaBnd-aux1b](#ZetaBnd_aux1b) and estimate $|s|\ll |t|$.

## Theorem: HolomorphicOn-riemannZeta0 {#HolomorphicOn_riemannZeta0 lean="HolomorphicOn_riemannZeta0" uses="riemannZeta0"}

For any $N\ge1$, the function $\zeta_0(N,s)$ is holomorphic on $\{s\in \mathbb{C}\mid \Re(s)>0 ∧ s \ne 1\}$.

### Proof

The function $\zeta_0(N,s)$ is a finite sum of entire functions, plus an integral
  that's absolutely convergent on $\{s\in \mathbb{C}\mid \Re(s)>0 ∧ s \ne 1\}$ by Lemma [ZetaBnd-aux1b](#ZetaBnd_aux1b).

## Lemma: isPathConnected-aux {#isPathConnected_aux lean="isPathConnected_aux"}

The set $\{s\in \mathbb{C}\mid \Re(s)>0 ∧ s \ne 1\}$ is path-connected.

### Proof

Construct explicit paths from $2$ to any point, either a line segment or two joined ones.

## Lemma: Zeta0EqZeta {#Zeta0EqZeta lean="Zeta0EqZeta" uses="riemannZeta0"}

For $\Re(s)>0$, $s\ne1$, and for any $N$,
  
$$
\zeta_0(N,s) = \zeta(s).
$$

### Proof {uses="isPathConnected_aux, ZetaSum_aux2, HolomorphicOn_riemannZeta0"}

Use Lemma [ZetaSum-aux2](#ZetaSum_aux2) and the Definition [riemannZeta0](#riemannZeta0).

## Lemma: ZetaBnd-aux2 {#ZetaBnd_aux2 lean="ZetaBnd_aux2"}

Given $n ≤ t$ and $\sigma$ with $1-A/\log t \le \sigma$, we have
  that
  
$$
|n^{-s}| \le n^{-1} e^A.
$$

### Proof

Use $|n^{-s}| = n^{-\sigma}
  = e^{-\sigma \log n}
  \le
  \exp(-\left(1-\frac{A}{\log t}\right)\log n)
  \le
  n^{-1} e^A$,
  since $n\le t$.

## Lemma: ZetaUpperBnd {#ZetaUpperBnd lean="ZetaUpperBnd"}

For any $s = \sigma + tI \in \mathbb{C}$, $1/2 \le \sigma\le 2, 3 < |t|$
  and any $0 < A < 1$ sufficiently small, and $1-A/\log |t| \le \sigma$, we have
  
$$
|\zeta(s)| \ll \log t.
$$

### Proof {uses="ZetaBnd_aux2, riemannZeta0, ZetaBnd_aux1, Zeta0EqZeta"}

First replace $\zeta(s)$ by $\zeta_0(N,s)$ for $N = \lfloor |t| \rfloor$.
  We estimate:
  
$$
|\zeta_0(N,s)| \ll
  \sum_{1\le n \le |t|} |n^{-s}|
  +
  \frac{- |t|^{1-\sigma}}{|1-s|} + \frac{-|t|^{-\sigma}}{2} +
  |t| \cdot |t| ^ {-σ} / σ
$$

  
$$
\ll
  e^A \sum_{1\le n < |t|} n^{-1}
  +|t|^{1-\sigma}
$$

  ,
  where we used Lemma [ZetaBnd-aux2](#ZetaBnd_aux2) and Lemma [ZetaBnd-aux1](#ZetaBnd_aux1).
  The first term is $\ll \log |t|$.
  For the second term, estimate
  
$$
|t|^{1-\sigma}
  \le |t|^{1-(1-A/\log |t|)}
  = |t|^{A/\log |t|} \ll 1.
$$

## Lemma: DerivUpperBnd-aux7 {#DerivUpperBnd_aux7 lean="DerivUpperBnd_aux7"}

For any $s = \sigma + tI \in \mathbb{C}$, $1/2 \le \sigma\le 2, 3 < |t|$, and any $0 < A < 1$
  sufficiently small, and $1-A/\log |t| \le \sigma$, we have
  
$$
\left\|s \cdot \int_{N}^{\infty}
    \left(\left\lfloor x \right\rfloor + \frac{1}{2} - x\right) \cdot x^{-s-1} \cdot (-\log x)
  \right\|
  \le 2 \cdot |t| \cdot N^{-\sigma} / \sigma \cdot \log |t|.
$$

### Proof

Estimate $|s|= |\sigma + tI|$ by $|s|\le 2 +|t| \le 2|t|$ (since $|t|>3$).
  Estimating $|\left\lfloor x \right\rfloor+1/2-x|$ by $1$,
  and using $|x^{-s-1}| = x^{-\sigma-1}$, we have
  
$$
\left\| s \cdot \int_{N}^{\infty}
    \left(\left\lfloor x \right\rfloor + \frac{1}{2} - x\right) \cdot x^{-s-1} \cdot (-\log x)
  \right\|
  \le 2 \cdot |t|
  \int_{N}^{\infty} x^{-\sigma} \cdot (\log x).
$$

  For the last integral, integrate by parts, getting:
  
$$
\int_{N}^{\infty} x^{-\sigma-1} \cdot (\log x) =
  \frac{1}{\sigma}N^{-\sigma} \cdot \log N + \frac1{\sigma^2} \cdot N^{-\sigma}.
$$

  Now use $\log N \le \log |t|$ to get the result.

## Lemma: ZetaDerivUpperBnd {#ZetaDerivUpperBnd lean="ZetaDerivUpperBnd"}

For any $s = \sigma + tI \in \mathbb{C}$, $1/2 \le \sigma\le 2, 3 < |t|$,
  there is an $A>0$ so that for $1-A/\log t \le \sigma$, we have
  
$$
|\zeta'(s)| \ll \log^2 t.
$$

### Proof {uses="ZetaBnd_aux2, ZetaUpperBnd, DerivUpperBnd_aux7, riemannZeta0, ZetaBnd_aux1, Zeta0EqZeta"}

First replace $\zeta(s)$ by $\zeta_0(N,s)$ for $N = \lfloor |t| \rfloor$.
  Differentiating term by term, we get:
  
$$
\zeta'(s) = -\sum_{1\le n < N} n^{-s} \log n
  + \frac{N^{1 - s}}{(1 - s)^2} + \frac{N^{1 - s} \log N} {1 - s}
  + \frac{N^{-s}\log N}{2} +
  \int_N^\infty \frac{\lfloor x\rfloor + 1/2 - x}{x^{s+1}} \, dx
  -s \int_N^\infty \log x \frac{\lfloor x\rfloor + 1/2 - x}{x^{s+1}} \, dx
  .
$$

  Estimate as before, with an extra factor of $\log |t|$.

## Lemma: ZetaNear1BndFilter {#ZetaNear1BndFilter lean="ZetaNear1BndFilter"}

As $\sigma\to1^+$,
  
$$
|\zeta(\sigma)| \ll 1/(\sigma-1).
$$

### Proof

Zeta has a simple pole at $s=1$. Equivalently, $\zeta(s)(s-1)$ remains bounded near $1$.
  Lots of ways to prove this.
  Probably the easiest one: use the expression for $\zeta_0 (N,s)$ with $N=1$ (the term $N^{1-s}/(1-s)$ being the only unbounded one).

## Lemma: ZetaNear1BndExact {#ZetaNear1BndExact lean="ZetaNear1BndExact"}

There exists a $c>0$ such that for all $1 < \sigma ≤ 2$,
  
$$
|\zeta(\sigma)| ≤ c/(\sigma-1).
$$

### Proof {uses="ZetaNear1BndFilter"}

Split into two cases, use Lemma [ZetaNear1BndFilter](#ZetaNear1BndFilter) for $\sigma$ sufficiently small
  and continuity on a compact interval otherwise.

## Lemma: ZetaLowerBound3 {#ZetaLowerBound3 lean="ZetaLowerBound3"}

There exists a $c>0$ such that for all $1 < \sigma <= 2$ and $3 < |t|$,
  
$$
c \frac{(\sigma-1)^{3/4}}{(\log |t|)^{1/4}} \le |\zeta(\sigma + tI)|.
$$

### Proof {uses="ZetaUpperBnd, ZetaNear1BndExact"}

Combine Lemma (ZetaLowerBound2) with upper bounds for
  $|\zeta(\sigma)|$ (from Lemma [ZetaNear1BndExact](#ZetaNear1BndExact)) and
  $|\zeta(\sigma+2it)|$ (from Lemma [ZetaUpperBnd](#ZetaUpperBnd)).

## Lemma: ZetaInvBound1 {#ZetaInvBound1 lean="ZetaInvBound1"}

For all $\sigma>1$,
  
$$
1/|\zeta(\sigma+it)| \le |\zeta(\sigma)|^{3/4}|\zeta(\sigma+2it)|^{1/4}
$$

### Proof

The identity
  
$$
1 \le |\zeta(\sigma)|^3 |\zeta(\sigma+it)|^4 |\zeta(\sigma+2it)|
$$

  for $\sigma>1$
  is already proved by Michael Stoll in the EulerProducts PNT file.

## Lemma: ZetaInvBound2 {#ZetaInvBound2 lean="ZetaInvBound2"}

For $\sigma>1$ (and $\sigma \le 2$),
  
$$
1/|\zeta(\sigma+it)| \ll (\sigma-1)^{-3/4}(\log |t|)^{1/4},
$$

  as $|t|\to\infty$.

### Proof {uses="ZetaUpperBnd, ZetaInvBound1, ZetaNear1BndExact"}

Combine Lemma [ZetaInvBound1](#ZetaInvBound1) with the bounds in Lemmata [ZetaNear1BndExact](#ZetaNear1BndExact) and
  [ZetaUpperBnd](#ZetaUpperBnd).

## Lemma: Zeta-eq-int-derivZeta {#Zeta_eq_int_derivZeta lean="Zeta_eq_int_derivZeta"}

For any $t\ne0$ (so we don't pass through the pole), and $\sigma_1 < \sigma_2$,
  
$$
\int_{\sigma_1}^{\sigma_2}\zeta'(\sigma + it) dt =
  \zeta(\sigma_2+it) - \zeta(\sigma_1+it).
$$

### Proof

This is the fundamental theorem of calculus.

## Lemma: Zeta-diff-Bnd {#Zeta_diff_Bnd lean="Zeta_diff_Bnd"}

For any $A>0$ sufficiently small, there is a constant $C>0$ so that
  whenever $1- A / \log t \le \sigma_1 < \sigma_2\le 2$ and $3 < |t|$, we have that:
  
$$
|\zeta (\sigma_2 + it) - \zeta (\sigma_1 + it)|
  \le C (\log |t|)^2 (\sigma_2 - \sigma_1).
$$

### Proof {uses="Zeta_eq_int_derivZeta, ZetaDerivUpperBnd"}

Use Lemma [Zeta-eq-int-derivZeta](#Zeta_eq_int_derivZeta) and
  estimate trivially using Lemma [ZetaDerivUpperBnd](#ZetaDerivUpperBnd).

## Lemma: ZetaInvBnd {#ZetaInvBnd lean="ZetaInvBnd"}

For any $A>0$ sufficiently small, there is a constant $C>0$ so that
  whenever $1- A / \log^9 |t| \le \sigma < 1+A/\log^9 |t|$ and $3 < |t|$, we have that:
  
$$
1/|\zeta(\sigma+it)| \le C \log^7 |t|.
$$

### Proof {uses="ZetaInvBound2, Zeta_diff_Bnd"}

Let $\sigma$ be given in the prescribed range, and set $\sigma' := 1+ A / \log^9 |t|$.
  Then
  
$$
|\zeta(\sigma+it)| \ge
  |\zeta(\sigma'+it)| - |\zeta(\sigma+it) - \zeta(\sigma'+it)|
  \ge
  C (\sigma'-1)^{3/4}\log |t|^{-1/4} - C \log^2 |t| (\sigma'-\sigma)
$$

  
$$
\ge
  C A^{3/4} \log |t|^{-7} - C \log^2 |t| (2 A / \log^9 |t|),
$$

  where we used Lemma [ZetaInvBound2](#ZetaInvBound2)  and Lemma [Zeta-diff-Bnd](#Zeta_diff_Bnd).
  Now by making $A$ sufficiently small (in particular, something like $A = 1/16$ should work), we can guarantee that
  
$$
|\zeta(\sigma+it)| \ge \frac C 2 (\log |t|)^{-7},
$$

  as desired.

Annoyingly, it is not immediate from this that $\zeta$ doesn't vanish there! That's because
$1/0 = 0$ in Lean. So we give a second proof of the same fact (refactor this later), with a lower
 bound on $\zeta$ instead of upper bound on $1 / \zeta$.

## Lemma: ZetaLowerBnd {#ZetaLowerBnd lean="ZetaLowerBnd"}

For any $A>0$ sufficiently small, there is a constant $C>0$ so that
  whenever $1- A / \log^9 |t| \le \sigma < 1$ and $3 < |t|$, we have that:
  
$$
|\zeta(\sigma+it)| \ge C \log^7 |t|.
$$

### Proof {uses="ZetaLowerBound3, Zeta_diff_Bnd"}

Follow same argument.

Now we get a zero free region.

## Lemma: ZetaZeroFree {#ZetaZeroFree lean="ZetaZeroFree"}

There is an $A>0$ so that for $1-A/\log^9 |t| \le \sigma < 1$ and $3 < |t|$,
  
$$
\zeta(\sigma+it) \ne 0.
$$

### Proof {uses="ZetaLowerBnd"}

Apply Lemma [ZetaLowerBnd](#ZetaLowerBnd).

## Lemma: LogDerivZetaBnd {#LogDerivZetaBnd lean="LogDerivZetaBnd"}

There is an $A>0$ so that for $1-A/\log^9 |t| \le \sigma < 1+A/\log^9 |t|$ and $3 < |t|$,
  
$$
|\frac {\zeta'}{\zeta} (\sigma+it)| \ll \log^9 |t|.
$$

### Proof {uses="ZetaDerivUpperBnd, ZetaInvBnd"}

Combine the bound on $|\zeta'|$ from Lemma [ZetaDerivUpperBnd](#ZetaDerivUpperBnd) with the
  bound on $1/|\zeta|$ from Lemma [ZetaInvBnd](#ZetaInvBnd).

## Theorem: ZetaNoZerosOn1Line {#ZetaNoZerosOn1Line lean="ZetaNoZerosOn1Line"}

The zeta function does not vanish on the 1-line.

### Proof

This fact is already proved in Stoll's work.

Then, since $\zeta$ doesn't vanish on the 1-line, there is a $\sigma<1$ (depending on $T$), so that
the box $[\sigma,1] \times_{ℂ} [-T,T]$ is free of zeros of $\zeta$.

## Lemma: ZetaNoZerosInBox {#ZetaNoZerosInBox lean="ZetaNoZerosInBox"}

For any $T>0$, there is a constant $\sigma<1$ so that
  
$$
\zeta(\sigma'+it) \ne 0
$$

  for all $|t| \leq T$ and $\sigma' \ge \sigma$.

### Proof

Assume not. Then there is a sequence $|t_n| \le T$ and $\sigma_n \to 1$ so that
  $\zeta(\sigma_n + it_n) = 0$.
  By compactness, there is a subsequence $t_{n_k} \to t_0$ along which
  $\zeta(\sigma_{n_k} + it_{n_k}) = 0$.
  If $t_0\ne0$, use the continuity of $\zeta$ to get that $\zeta(1 + it_0) = 0$;
  this is a contradiction.
  If $t_0=0$, $\zeta$ blows up near $1$, so can't be zero nearby.

We now prove that there's an absolute constant $\sigma_0$ so that $\zeta'/\zeta$ is holomorphic on
a rectangle $[\sigma_2,2] \times_{ℂ} [-3,3] \setminus \{1\}$.

## Lemma: LogDerivZetaHolcSmallT {#LogDerivZetaHolcSmallT lean="LogDerivZetaHolcSmallT"}

There is a $\sigma_2 < 1$ so that the function
  
$$
\frac {\zeta'}{\zeta}(s)
$$

  is holomorphic on $\{ \sigma_2 \le \Re s \le 2, |\Im s| \le 3 \} \setminus \{1\}$.

### Proof {uses="ZetaNoZerosInBox"}

The derivative of $\zeta$ is holomorphic away from $s=1$; the denominator $\zeta(s)$ is nonzero
  in this range by Lemma [ZetaNoZerosInBox](#ZetaNoZerosInBox).

## Lemma: LogDerivZetaHolcLargeT {#LogDerivZetaHolcLargeT lean="LogDerivZetaHolcLargeT"}

There is an $A>0$ so that for all $T>3$, the function
  $
  \frac {\zeta'}{\zeta}(s)
  $
  is holomorphic on $\{1-A/\log^9 T \le \Re s \le 2, |\Im s|\le T \}\setminus\{1\}$.

### Proof {uses="ZetaNoZerosInBox, ZetaZeroFree"}

The derivative of $\zeta$ is holomorphic away from $s=1$; the denominator $\zeta(s)$ is nonzero
  in this range by Lemma [ZetaZeroFree](#ZetaZeroFree).

## Lemma: LogDerivZetaBndUnif {#LogDerivZetaBndUnif lean="LogDerivZetaBndUnif"}

There exist $A, C > 0$ such that
  
$$
|\frac{\zeta'}{\zeta}(\sigma + it)|\leq C \log |t|^9
$$

  whenever $|t|>3$ and $\sigma > 1 - A/\log |t|^9$.

### Proof {uses="riemannZetaLogDerivResidue, LogDerivZetaBnd"}

For $\sigma$ close to $1$ use Lemma [LogDerivZetaBnd](#LogDerivZetaBnd), otherwise estimate trivially.

**Proof of Medium PNT**

The approach here is completely standard. We follow the use of
$\mathcal{M}(\widetilde{1_{\epsilon}})$ as in [Kontorovich 2015].

## Definition: ChebyshevPsi {#ChebyshevPsi lean="ChebyshevPsi"}

The (second) Chebyshev Psi function is defined as
  
$$
\psi(x) := \sum_{n \le x} \Lambda(n),
$$

  where $\Lambda(n)$ is the von Mangoldt function.

It has already been established that zeta doesn't vanish on the 1 line, and has a pole at $s=1$
of order 1.
We also have the following.

## Theorem: LogDerivativeDirichlet {#LogDerivativeDirichlet lean="LogDerivativeDirichlet"}

We have that, for $\Re(s)>1$,
  
$$
-\frac{\zeta'(s)}{\zeta(s)} = \sum_{n=1}^\infty \frac{\Lambda(n)}{n^s}.
$$

### Proof

Already in Mathlib.

The main object of study is the following inverse Mellin-type transform, which will turn out to
be a smoothed Chebyshev function.

## Definition: SmoothedChebyshev {#SmoothedChebyshev lean="SmoothedChebyshev" uses="Smooth1, VerticalIntegral"}

Fix $\epsilon>0$, and a bumpfunction supported in $[1/2,2]$. Then we define the smoothed
  Chebyshev function $\psi_{\epsilon}$ from $\mathbb{R}_{>0}$ to $\mathbb{C}$ by
  
$$
\psi_{\epsilon}(X) = \frac{1}{2\pi i}\int_{(\sigma)}\frac{-\zeta'(s)}{\zeta(s)}
  \mathcal{M}(\widetilde{1_{\epsilon}})(s)
  X^{s}ds,
$$

  where we'll take $\sigma = 1 + 1 / \log X$.

## Lemma: SmoothedChebyshevDirichlet-aux-integrable {#SmoothedChebyshevDirichlet_aux_integrable lean="SmoothedChebyshevDirichlet_aux_integrable" uses="Smooth1"}

Fix a nonnegative, continuously differentiable function $F$ on $\mathbb{R}$ with support in
  $[1/2,2]$, and total mass one, $\int_{(0,\infty)} F(x)/x dx = 1$. Then for any $\epsilon>0$,
  and $\sigma\in (1, 2]$, the function
  
$$
x \mapsto\mathcal{M}(\widetilde{1_{\epsilon}})(\sigma + ix)
$$

  is integrable on $\mathbb{R}$.

### Proof {uses="Smooth1Nonneg, Smooth1Properties_above, Smooth1ContinuousAt, Smooth1LeOne, MellinOfSmooth1b"}

By Lemma [MellinOfSmooth1b](#MellinOfSmooth1b) the integrand is $O(1/t^2)$ as $t\rightarrow \infty$ and hence
  the function is integrable.

## Lemma: SmoothedChebyshevDirichlet-aux-tsum-integral {#SmoothedChebyshevDirichlet_aux_tsum_integral lean="SmoothedChebyshevDirichlet_aux_tsum_integral" uses="Smooth1"}

Fix a nonnegative, continuously differentiable function $F$ on $\mathbb{R}$ with support in
  $[1/2,2]$, and total mass one, $\int_{(0,\infty)} F(x)/x dx = 1$. Then for any $\epsilon>0$ and
  $\sigma\in(1,2]$, the function
  $x \mapsto \sum_{n=1}^\infty \frac{\Lambda(n)}{n^{\sigma+it}}
  \mathcal{M}(\widetilde{1_{\epsilon}})(\sigma+it) x^{\sigma+it}$ is equal to
  $\sum_{n=1}^\infty \int_{(0,\infty)} \frac{\Lambda(n)}{n^{\sigma+it}}
  \mathcal{M}(\widetilde{1_{\epsilon}})(\sigma+it) x^{\sigma+it}$.

### Proof {uses="Smooth1Nonneg, Smooth1Properties_above, Smooth1ContinuousAt, SmoothedChebyshevDirichlet_aux_integrable, Smooth1LeOne"}

Interchange of summation and integration.

## Theorem: SmoothedChebyshevDirichlet {#SmoothedChebyshevDirichlet lean="SmoothedChebyshevDirichlet" uses="SmoothedChebyshev, Smooth1"}

We have that
  
$$
\psi_{\epsilon}(X) = \sum_{n=1}^\infty \Lambda(n)\widetilde{1_{\epsilon}}(n/X).
$$

### Proof {uses="Smooth1Nonneg, Smooth1Properties_above, Smooth1ContinuousAt, SmoothedChebyshevDirichlet_aux_integrable, LogDerivativeDirichlet, Smooth1LeOne, SmoothedChebyshevDirichlet_aux_tsum_integral"}

We have that
  
$$
\psi_{\epsilon}(X) = \frac{1}{2\pi i}\int_{(2)}\sum_{n=1}^\infty \frac{\Lambda(n)}{n^s}
  \mathcal{M}(\widetilde{1_{\epsilon}})(s)
  X^{s}ds.
$$

  We have enough decay (thanks to quadratic decay of $\mathcal{M}(\widetilde{1_{\epsilon}})$) to
  justify the interchange of summation and integration. We then get
  
$$
\psi_{\epsilon}(X) =
  \sum_{n=1}^\infty \Lambda(n)\frac{1}{2\pi i}\int_{(2)}
  \mathcal{M}(\widetilde{1_{\epsilon}})(s)
  (n/X)^{-s}
  ds
$$

  and apply the Mellin inversion formula.

The smoothed Chebyshev function is close to the actual Chebyshev function.

## Theorem: SmoothedChebyshevClose {#SmoothedChebyshevClose lean="SmoothedChebyshevClose" uses="SmoothedChebyshev"}

We have that
  
$$
\psi_{\epsilon}(X) = \psi(X) + O(\epsilon X \log X).
$$

### Proof {uses="Smooth1Nonneg, SmoothedChebyshevDirichlet, Smooth1Properties_above, Smooth1Properties_below, Smooth1, Smooth1LeOne"}

Take the difference. By Lemma [Smooth1Properties-above](#Smooth1Properties_above) and [Smooth1Properties-below](#Smooth1Properties_below),
  the sums agree except when $1-c \epsilon \leq n/X \leq 1+c \epsilon$. This is an interval of
  length $\ll \epsilon X$, and the summands are bounded by $\Lambda(n) \ll \log X$.

Returning to the definition of $\psi_{\epsilon}$, fix a large $T$ to be chosen later, and set
$\sigma_0 = 1 + 1 / log X$,
$\sigma_1 = 1- A/ \log T^9$, and
$\sigma_2<\sigma_1$ a constant.
Pull
contours (via rectangles!) to go
from $\sigma_0-i\infty$ up to $\sigma_0-iT$, then over to $\sigma_1-iT$, up to $\sigma_1-3i$,
over to $\sigma_2-3i$, up to $\sigma_2+3i$, back over to $\sigma_1+3i$, up to $\sigma_1+iT$,
over to $\sigma_0+iT$, and finally up to $\sigma_0+i\infty$.

In the process, we will pick up the residue at $s=1$.
We will do this in several stages. Here the interval integrals are defined as follows:

## Definition: I₁ {#I1 lean="I₁" uses="Smooth1"}

$$
I_1(\nu, \epsilon, X, T) := \frac{1}{2\pi i} \int_{-\infty}^{-T}
  \left(
  \frac{-\zeta'}\zeta(\sigma_0 + t i)
  \right)
   \mathcal M(\widetilde 1_\epsilon)(\sigma_0 + t i)
  X^{\sigma_0 + t i}
  \ i \ dt
$$

## Definition: I₂ {#I2 lean="I₂" uses="Smooth1"}

$$
I_2(\nu, \epsilon, X, T, \sigma_1) := \frac{1}{2\pi i} \int_{\sigma_1}^{\sigma_0}
  \left(
  \frac{-\zeta'}\zeta(\sigma - i T)
  \right)
    \mathcal M(\widetilde 1_\epsilon)(\sigma - i T)
  X^{\sigma - i T} \ d\sigma
$$

## Definition: I₃₇ {#I37 lean="I₃₇" uses="Smooth1"}

$$
I_{37}(\nu, \epsilon, X, T, \sigma_1) := \frac{1}{2\pi i} \int_{-T}^{T}
  \left(
  \frac{-\zeta'}\zeta(\sigma_1 + t i)
  \right)
    \mathcal M(\widetilde 1_\epsilon)(\sigma_1 + t i)
  X^{\sigma_1 + t i} \ i \ dt
$$

## Definition: I₈ {#I8 lean="I₈" uses="Smooth1"}

$$
I_8(\nu, \epsilon, X, T, \sigma_1) := \frac{1}{2\pi i} \int_{\sigma_1}^{\sigma_0}
  \left(
  \frac{-\zeta'}\zeta(\sigma + T i)
  \right)
    \mathcal M(\widetilde 1_\epsilon)(\sigma + T i)
  X^{\sigma + T i} \ d\sigma
$$

## Definition: I₉ {#I9 lean="I₉" uses="Smooth1"}

$$
I_9(\nu, \epsilon, X, T) := \frac{1}{2\pi i} \int_{T}^{\infty}
  \left(
  \frac{-\zeta'}\zeta(\sigma_0 + t i)
  \right)
    \mathcal M(\widetilde 1_\epsilon)(\sigma_0 + t i)
  X^{\sigma_0 + t i} \ i \ dt
$$

## Definition: I₃ {#I3 lean="I₃" uses="Smooth1"}

$$
I_3(\nu, \epsilon, X, T, \sigma_1) := \frac{1}{2\pi i} \int_{-T}^{-3}
  \left(
  \frac{-\zeta'}\zeta(\sigma_1 + t i)
  \right)
    \mathcal M(\widetilde 1_\epsilon)(\sigma_1 + t i)
  X^{\sigma_1 + t i} \ i \ dt
$$

## Definition: I₇ {#I7 lean="I₇" uses="Smooth1"}

$$
I_7(\nu, \epsilon, X, T, \sigma_1) := \frac{1}{2\pi i} \int_{3}^{T}
  \left(
  \frac{-\zeta'}\zeta(\sigma_1 + t i)
  \right)
    \mathcal M(\widetilde 1_\epsilon)(\sigma_1 + t i)
  X^{\sigma_1 + t i} \ i \ dt
$$

## Definition: I₄ {#I4 lean="I₄" uses="Smooth1"}

$$
I_4(\nu, \epsilon, X, \sigma_1, \sigma_2) := \frac{1}{2\pi i} \int_{\sigma_2}^{\sigma_1}
  \left(
  \frac{-\zeta'}\zeta(\sigma - 3 i)
  \right)
    \mathcal M(\widetilde 1_\epsilon)(\sigma - 3 i)
  X^{\sigma - 3 i} \ d\sigma
$$

## Definition: I₆ {#I6 lean="I₆" uses="Smooth1"}

$$
I_6(\nu, \epsilon, X, \sigma_1, \sigma_2) := \frac{1}{2\pi i} \int_{\sigma_2}^{\sigma_1}
  \left(
  \frac{-\zeta'}\zeta(\sigma + 3 i)
  \right)
    \mathcal M(\widetilde 1_\epsilon)(\sigma + 3 i)
  X^{\sigma + 3 i} \ d\sigma
$$

## Definition: I₅ {#I5 lean="I₅" uses="Smooth1"}

$$
I_5(\nu, \epsilon, X, \sigma_2) := \frac{1}{2\pi i} \int_{-3}^{3}
  \left(
  \frac{-\zeta'}\zeta(\sigma_2 + t i)
  \right)
    \mathcal M(\widetilde 1_\epsilon)(\sigma_2 + t i)
  X^{\sigma_2 + t i} \ i \ dt
$$

## Lemma: dlog-riemannZeta-bdd-on-vertical-lines {#dlog_riemannZeta_bdd_on_vertical_lines lean="dlog_riemannZeta_bdd_on_vertical_lines"}

For $\sigma_0 > 1$, there exists a constant $C > 0$ such that
  
$$
\forall t \in \mathbb{R}, \quad
  \left\| \frac{\zeta'(\sigma_0 + t i)}{\zeta(\sigma_0 + t i)} \right\| \leq C.
$$

### Proof

Write as Dirichlet series and estimate trivially using Theorem [LogDerivativeDirichlet](#LogDerivativeDirichlet).

## Lemma: SmoothedChebyshevPull1-aux-integrable {#SmoothedChebyshevPull1_aux_integrable lean="SmoothedChebyshevPull1_aux_integrable" uses="Smooth1"}

The integrand 
$$
\zeta'(s)/\zeta(s)\mathcal{M}(\widetilde{1_{\epsilon}})(s)X^{s}
$$

  is integrable on the contour $\sigma_0 + t i$ for $t \in \mathbb{R}$ and $\sigma_0 > 1$.

### Proof {uses="dlog_riemannZeta_bdd_on_vertical_lines, SmoothedChebyshevDirichlet_aux_integrable"}

The $\zeta'(s)/\zeta(s)$ term is bounded, as is $X^s$, and the smoothing function
  $\mathcal{M}(\widetilde{1_{\epsilon}})(s)$
  decays like $1/|s|^2$ by Theorem [MellinOfSmooth1b](#MellinOfSmooth1b).
  Actually, we already know that
  $\mathcal{M}(\widetilde{1_{\epsilon}})(s)$
  is integrable from Theorem [SmoothedChebyshevDirichlet-aux-integrable](#SmoothedChebyshevDirichlet_aux_integrable),
  so we should just need to bound the rest.

## Lemma: BddAboveOnRect {#BddAboveOnRect lean="BddAboveOnRect"}

Let $g : \mathbb{C} \to \mathbb{C}$ be a holomorphic function on a rectangle, then $g$ is bounded above on the rectangle.

### Proof

Use the compactness of the rectangle and the fact that holomorphic functions are continuous.

## Theorem: SmoothedChebyshevPull1 {#SmoothedChebyshevPull1 lean="SmoothedChebyshevPull1" uses="I1, SmoothedChebyshev, I37, I9, Smooth1, I2, I8"}

We have that
  
$$
\psi_{\epsilon}(X) =
  \mathcal{M}(\widetilde{1_{\epsilon}})(1)
  X^{1} +
  I_1 - I_2 +I_{37} + I_8 + I_9
  .
$$

### Proof {uses="Smooth1Nonneg, ResidueMult, SmoothedChebyshevPull1_aux_integrable, ResidueTheoremOnRectangleWithSimplePole, BddAbove_to_IsBigO, riemannZetaLogDerivResidue, Smooth1Properties_above, existsDifferentiableOn_of_bddAbove, Smooth1ContinuousAt, Smooth1LeOne, RectangleIntegral, VerticalIntegral"}

Pull rectangle contours and evaluate the pole at $s=1$.

Next pull contours to another box.

## Lemma: SmoothedChebyshevPull2 {#SmoothedChebyshevPull2 lean="SmoothedChebyshevPull2" uses="I3, I37, I4, Smooth1, I6, I7, I5"}

We have that
  
$$
I_{37} =
  I_3 - I_4 + I_5 + I_6 + I_7
  .
$$

### Proof {uses="Smooth1Nonneg, HolomorphicOn.vanishesOnRectangle, Smooth1Properties_above, Smooth1ContinuousAt, Smooth1LeOne, RectangleIntegral"}

Mimic the proof of Lemma [SmoothedChebyshevPull1](#SmoothedChebyshevPull1).

We insert this information in $\psi_{\epsilon}$. We add and subtract the integral over the box
$[1-\delta,2] \times_{ℂ} [-T,T]$, which we evaluate as follows

## Theorem: ZetaBoxEval {#ZetaBoxEval lean="ZetaBoxEval" uses="Smooth1"}

For all $\epsilon > 0$ sufficiently close to $0$, the rectangle integral over $[1-\delta,2] \times_{ℂ} [-T,T]$ of the integrand in
  $\psi_{\epsilon}$ is
  
$$
\frac{X^{1}}{1}\mathcal{M}(\widetilde{1_{\epsilon}})(1)
  = X(1+O(\epsilon))
  ,
$$

  where the implicit constant is independent of $X$.

### Proof {uses="MellinOfSmooth1c"}

Unfold the definitions and apply Lemma [MellinOfSmooth1c](#MellinOfSmooth1c).

It remains to estimate all of the integrals.

This auxiliary lemma is useful for what follows.

## Lemma: IBound-aux1 {#IBound_aux1 lean="IBound_aux1"}

Given a natural number $k$ and a real number $X_0 > 0$, there exists $C \geq 1$ so that for all $X \geq X_0$,
  
$$
\log^k X \le C \cdot X.
$$

### Proof

We use the fact that $\log^k X / X$ goes to $0$ as $X \to \infty$.
  Then we use the extreme value theorem to find a constant $C$ that works for all $X \geq X_0$.

## Lemma: I1Bound {#I1Bound lean="I1Bound" uses="I1"}

We have that
  
$$
\left|I_{1}(\nu, \epsilon, X, T)\
  \right| \ll \frac{X}{\epsilon T}
  .
$$

  Same with $I_9$.

### Proof {uses="SmoothedChebyshevPull1_aux_integrable, riemannZetaLogDerivResidue, Smooth1, MellinOfSmooth1b"}

Unfold the definitions and apply the triangle inequality.
  
$$
\left|I_{1}(\nu, \epsilon, X, T)\right| =
  \left|
  \frac{1}{2\pi i} \int_{-\infty}^{-T}
  \left(
  \frac{-\zeta'}\zeta(\sigma_0 + t i)
  \right)
   \mathcal M(\widetilde 1_\epsilon)(\sigma_0 + t i)
  X^{\sigma_0 + t i}
  \ i \ dt
  \right|
$$

  By Theorem [dlog-riemannZeta-bdd-on-vertical-lines](#dlog_riemannZeta_bdd_on_vertical_lines) (once fixed!!),
  $\zeta'/\zeta (\sigma_0 + t i)$ is bounded by $\zeta'/\zeta(\sigma_0)$, and
  Theorem [riemannZetaLogDerivResidue](#riemannZetaLogDerivResidue) gives $\ll 1/(\sigma_0-1)$ for the latter. This gives:
  
$$
\leq
  \frac{1}{2\pi}
  \left|
   \int_{-\infty}^{-T}
  C \log X\cdot
   \frac{C'}{\epsilon|\sigma_0 + t i|^2}
  X^{\sigma_0}
  \ dt
  \right|
  ,
$$

  where we used Theorem [MellinOfSmooth1b](#MellinOfSmooth1b).
  Continuing the calculation, we have
  
$$
\leq
  \log X \cdot
  C'' \frac{X^{\sigma_0}}{\epsilon}
  \int_{-\infty}^{-T}
  \frac{1}{t^2}
  \ dt
  \ \leq \
  C''' \frac{X\log X}{\epsilon T}
  ,
$$

  where we used that $\sigma_0=1+1/\log X$, and $X^{\sigma_0} = X\cdot X^{1/\log X}=e \cdot X$.

## Lemma: I2Bound {#I2Bound lean="I2Bound" uses="I2"}

Assuming a bound of the form of Lemma [LogDerivZetaBndUnif](#LogDerivZetaBndUnif) we have that
  
$$
\left|I_{2}(\nu, \epsilon, X, T)\right| \ll \frac{X}{\epsilon T}
  .
$$

### Proof {uses="Smooth1, IBound_aux1, MellinOfSmooth1b"}

Unfold the definitions and apply the triangle inequality.
  
$$
\left|I_{2}(\nu, \epsilon, X, T, \sigma_1)\right| =
  \left|\frac{1}{2\pi i} \int_{\sigma_1}^{\sigma_0}
  \left(\frac{-\zeta'}\zeta(\sigma - T i) \right) \cdot
  \mathcal M(\widetilde 1_\epsilon)(\sigma - T i) \cdot
  X^{\sigma - T i}
   \ d\sigma
  \right|
$$

  
$$
\leq
  \frac{1}{2\pi}
  \int_{\sigma_1}^{\sigma_0}
  C \cdot \log T ^ 9
  \frac{C'}{\epsilon|\sigma - T i|^2}
  X^{\sigma_0}
   \ d\sigma
   \leq
  C'' \cdot \frac{X\log T^9}{\epsilon T^2}
  ,
$$

  where we used Theorems [MellinOfSmooth1b](#MellinOfSmooth1b), the hypothesised bound on zeta and the fact that
  $X^\sigma \le X^{\sigma_0} = X\cdot X^{1/\log X}=e \cdot X$.
  Since $T>3$, we have $\log T^9 \leq C''' T$.

## Lemma: I8I2 {#I8I2 lean="I8I2" uses="I2, I8"}

Symmetry between $I_2$ and $I_8$:
  
$$
I_8(\nu, \epsilon, X, T) = -\overline{I_2(\nu, \epsilon, X, T)}
  .
$$

### Proof {uses="Smooth1, intervalIntegral_conj, deriv_riemannZeta_conj"}

This is a direct consequence of the definitions of $I_2$ and $I_8$.

## Lemma: I8Bound {#I8Bound lean="I8Bound" uses="I8"}

We have that
  
$$
\left|I_{8}(\nu, \epsilon, X, T)\right| \ll \frac{X}{\epsilon T}
  .
$$

### Proof {uses="I2, I8I2, I2Bound"}

We deduce this from the corresponding bound for $I_2$, using the symmetry between $I_2$ and $I_8$.

## Lemma: log-pow-over-xsq-integral-bounded {#log_pow_over_xsq_integral_bounded lean="log_pow_over_xsq_integral_bounded"}

For every $n$ there is some absolute constant $C>0$ such that
  
$$
\int_3^T \frac{(\log x)^9}{x^2}dx < C
$$

### Proof

Induct on n and just integrate by parts.

## Lemma: I3Bound {#I3Bound lean="I3Bound" uses="I3"}

Assuming a bound of the form of Lemma [LogDerivZetaBndUnif](#LogDerivZetaBndUnif) we have that
  
$$
\left|I_{3}(\nu, \epsilon, X, T)\right| \ll \frac{X}{\epsilon}\, X^{-\frac{A}{(\log T)^9}}
  .
$$

  Same with $I_7$.

### Proof {uses="Smooth1, MellinOfSmooth1b, log_pow_over_xsq_integral_bounded"}

Unfold the definitions and apply the triangle inequality.
  
$$
\left|I_{3}(\nu, \epsilon, X, T, \sigma_1)\right| =
  \left|\frac{1}{2\pi i} \int_{-T}^3
  \left(\frac{-\zeta'}\zeta(\sigma_1 + t i) \right)
  \mathcal M(\widetilde 1_\epsilon)(\sigma_1 + t i)
  X^{\sigma_1 + t i}
  \ i \ dt
  \right|
$$

  
$$
\leq
  \frac{1}{2\pi}
  \int_{-T}^3
  C \cdot \log t ^ 9
  \frac{C'}{\epsilon|\sigma_1 + t i|^2}
  X^{\sigma_1}
   \ dt
  ,
$$

  where we used Theorems [MellinOfSmooth1b](#MellinOfSmooth1b) and the hypothesised bound on zeta.
  Now we estimate $X^{\sigma_1} = X \cdot X^{-A/ \log T^9}$, and the integral is absolutely bounded.

## Lemma: I4Bound {#I4Bound lean="I4Bound" uses="I4"}

We have that
  
$$
\left|I_{4}(\nu, \epsilon, X, \sigma_1, \sigma_2)\right| \ll \frac{X}{\epsilon}\,
   X^{-\frac{A}{(\log T)^9}}
  .
$$

  Same with $I_6$.

### Proof {uses="Smooth1, MellinOfSmooth1b"}

The analysis of $I_4$ is similar to that of $I_2$, (in Lemma [I2Bound](#I2Bound)) but even easier.
  Let $C$ be the sup of $-\zeta'/\zeta$ on the curve $\sigma_2 + 3 i$ to $1+ 3i$ (this curve is compact, and away from the pole at $s=1$).
  Apply Theorem [MellinOfSmooth1b](#MellinOfSmooth1b) to get the bound $1/(\epsilon |s|^2)$, which is bounded by $C'/\epsilon$.
  And $X^s$ is bounded by $X^{\sigma_1} = X \cdot X^{-A/ \log T^9}$.
  Putting these together gives the result.

## Lemma: I5Bound {#I5Bound lean="I5Bound" uses="I5"}

We have that
  
$$
\left|I_{5}(\nu, \epsilon, X, \sigma_2)\right| \ll \frac{X^{\sigma_2}}{\epsilon}.
$$

### Proof {uses="Smooth1, MellinOfSmooth1b"}

Here $\zeta'/\zeta$ is absolutely bounded on the compact interval $\sigma_2 + i [-3,3]$, and
  $X^s$ is bounded by $X^{\sigma_2}$. Using Theorem [MellinOfSmooth1b](#MellinOfSmooth1b) gives the bound $1/(\epsilon |s|^2)$, which is bounded by $C'/\epsilon$.
  Putting these together gives the result.

**MediumPNT**

## Theorem: MediumPNT {#MediumPNT lean="MediumPNT"}

We have
  
$$
\sum_{n \leq x} \Lambda(n) = x + O(x \exp(-c(\log x)^{1/10})).
$$

### Proof {uses="LogDerivZetaHolcSmallT, I3Bound, I4, I2, I6, intervalIntegral_conj, I5Bound, SmoothedChebyshevClose, I3, I1, Smooth1Nonneg, MellinOfSmooth1c, Smooth1ContinuousAt, LogDerivZetaBndUnif, I1Bound, I37, I9, LogDerivZetaHolcLargeT, Smooth1Properties_above, Smooth1, I8, I2Bound, I5, SmoothedChebyshev, SmoothedChebyshevPull2, I8Bound, SmoothExistence, I4Bound, deriv_riemannZeta_conj, I7, Smooth1LeOne, SmoothedChebyshevPull1"}

Evaluate the integrals.

