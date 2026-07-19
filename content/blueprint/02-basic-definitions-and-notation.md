---
title: 'Basic definitions and notation'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

## Definition: First prime gap {#first-gap-def lean="first_gap"}

$P(g)$ is the first prime $p_n$ for which the prime gap
  $p_{n+1}-p_n$ is equal to $g$, or $0$ if no such gap
  exists.

## Definition: pi {#pi-def lean="pi"}

$\pi(x)$ is the number of primes less than or equal to
  $x$.

## Definition: pi star {#pi-star-def lean="pi_star" uses="pi-def"}

$\pi^*(x) = \sum_{k \geq 1} \pi(x^{1/k}) / k$.

## Definition: li and Li {#li-def lean="li, Li"}

$\mathrm{li}(x) = \int_0^x \frac{dt}{\log t}$ (in the
  principal value sense) and
  $\mathrm{Li}(x) = \int_2^x \frac{dt}{\log t}$.

## Definition: Equation (2) of FKS2 {#Epsi-def lean="Eψ"}

$E_\psi(x) = |\psi(x) - x| / x$

## Definition: Definitions 1, 5, FKS2 {#classical-bound-psi lean="Eψ.classicalBound" uses="Epsi-def"}

We say that $E_\psi$ satisfies a _classical bound_
  with parameters $A, B, C, R, x_0$ if for all
  $x \geq x_0$ we have
  
$$
E_\psi(x) \leq A \left(\frac{\log x}{R}\right)^B
     \exp\left(-C \left(\frac{\log x}{R}\right)^{1/2}
     \right).
$$

  We say that it obeys a _numerical bound_ with
  parameter $\varepsilon(x_0)$ if for all $x \geq x_0$
  we have
  
$$
E_\psi(x) \leq \varepsilon(x_0).
$$

## Definition: Equation (1) of FKS2 {#Epi-def lean="Eπ" uses="pi-def, li-def"}

$E_\pi(x) = |\pi(x) - \mathrm{Li}(x)| /
  (x / \log x)$.

## Definition: Equation (2) of FKS2 {#Etheta-def lean="Eθ"}

$E_\theta(x) = |\theta(x) - x| / x$

## Definition: Definitions 1, 5, FKS2 {#classical-bound-theta lean="Eθ.classicalBound" uses="Etheta-def"}

We say that $E_\theta$ satisfies a _classical bound_
  with parameters $A, B, C, R, x_0$ if for all
  $x \geq x_0$ we have
  
$$
E_\theta(x) \leq A \left(\frac{\log x}{R}\right)^B
     \exp\left(-C \left(\frac{\log x}{R}\right)^{1/2}
     \right).
$$

  We say that it obeys a _numerical bound_ with
  parameter $\varepsilon(x_0)$ if for all $x \geq x_0$
  we have
  
$$
E_\theta(x) \leq \varepsilon(x_0).
$$

## Definition: Definitions 1, 5, FKS2 {#classical-bound-pi lean="Eπ.classicalBound" uses="Epi-def"}

We say that $E_\pi$ satisfies a _classical bound_
  with parameters $A, B, C, R, x_0$ if for all
  $x \geq x_0$ we have
  
$$
E_\pi(x) \leq A \left(\frac{\log x}{R}\right)^B
     \exp\left(-C \left(\frac{\log x}{R}\right)^{1/2}
     \right).
$$

  We say that it obeys a _numerical bound_ with
  parameter $\varepsilon(x_0)$ if for all $x \geq x_0$
  we have
  
$$
E_\pi(x) \leq \varepsilon(x_0).
$$

## Lemma: Admissible bound decreasing for large x {#admissible-bound-monotone lean="admissible_bound.mono" discussion="900"}

If $A,B,C,R > 0$ then the classical bound is monotone
  decreasing for $x \geq \exp( R (2B/C)^2 )$.

### Proof

Differentiate the bound and check the
  sign.

## Lemma: Classic bound implies numerical bound {#classical-to-numeric lean="Eψ.classicalBound.to_numericalBound, Eθ.classicalBound.to_numericalBound, Eπ.classicalBound.to_numericalBound" uses="Epsi-def, classical-bound-psi, classical-bound-theta, Etheta-def, classical-bound-pi, Epi-def" discussion="901"}

A classical bound for $x \geq x_0$ implies a numerical
  bound for $x \geq \max(x_0,
  \exp( R (2B/C)^2  ))$.

### Proof {uses="admissible-bound-monotone, admissible-bound-monotone, admissible-bound-monotone"}

Immediate from previous lemma

