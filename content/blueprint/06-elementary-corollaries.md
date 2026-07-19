---
title: 'Elementary Corollaries'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

## Lemma: finsum-range-eq-sum-range {#finsum_range_eq_sum_range lean="finsum_range_eq_sum_range"}

For any arithmetic function $f$ and real number $x$, one has
  
$$
\sum_{n \leq x} f(n) = \sum_{n \leq ⌊x⌋_+} f(n)
$$

  and
  
$$
\sum_{n < x} f(n) = \sum_{n < ⌈x⌉_+} f(n).
$$

### Proof

Straightforward.

## Theorem: chebyshev-asymptotic {#chebyshev-asymptotic lean="chebyshev_asymptotic"}

One has
  
$$
\sum_{p \leq x} \log p = x + o(x).
$$

### Proof {uses="WeakPNT"}

From the prime number theorem we already have
  
$$
\sum_{n \leq x} \Lambda(n) = x + o(x)
$$

  so it suffices to show that
  
$$
\sum_{j \geq 2} \sum_{p^j \leq x} \log p = o(x).
$$

  Only the terms with $j \leq \log x / \log 2$ contribute, and each $j$ contributes at most
  $\sqrt{x} \log x$ to the sum, so the left-hand side is $O( \sqrt{x} \log^2 x ) = o(x)$ as
  required.

## Corollary: primorial-bounds {#primorial_bounds lean="primorial_bounds"}

We have
    
$$
\prod_{p \leq x} p = \exp( x + o(x) )
$$

### Proof {uses="chebyshev-asymptotic"}

Exponentiate Theorem (chebyshev_asymptotic).

## Theorem: pi-asymp {#pi_asymp lean="pi_asymp"}

There exists a function $c(x)$ such that $c(x) = o(1)$ as $x \to \infty$ and
  
$$
\pi(x) = (1 + c(x)) \int_2^x \frac{dt}{\log t}
$$

  for all $x$ large enough.

### Proof {uses="chebyshev-asymptotic"}

We have the identity
  
$$
\pi(x) = \frac{1}{\log x} \sum_{p \leq x} \log p
  + \int_2^x (\sum_{p \leq t} \log p) \frac{dt}{t \log^2 t}
$$

  as can be proven by interchanging the sum and integral and using the fundamental theorem of
  calculus.  For any $\varepsilon$, we know from Theorem (chebyshev_asymptotic) that there is $x_\varepsilon$
  such that $\sum_{p \leq t} \log p = t + O(\varepsilon t)$ for $t \geq x_\varepsilon$, hence for $x \geq x_\varepsilon$
  
$$
\pi(x) = \frac{1}{\log x} (x + O(\varepsilon x))
  + \int_{x_\varepsilon}^x (t + O(\varepsilon t)) \frac{dt}{t \log^2 t} + O_\varepsilon(1)
$$

  where the $O_\varepsilon(1)$ term can depend on $x_\varepsilon$ but is independent of $x$.  One can evaluate
  this after an integration by parts as
  
$$
\pi(x) = (1+O(\varepsilon)) \int_{x_\varepsilon}^x \frac{dt}{\log t} + O_\varepsilon(1)
$$

  
$$
= (1+O(\varepsilon)) \int_{2}^x \frac{dt}{\log t}
$$

  for $x$ large enough, giving the claim.

## Corollary: pi-alt {#pi_alt lean="pi_alt"}

One has
  
$$
\pi(x) = (1+o(1)) \frac{x}{\log x}
$$

  as $x \to \infty$.

### Proof {uses="pi_asymp"}

An integration by parts gives
  
$$
\int_2^x \frac{dt}{\log t} = \frac{x}{\log x} - \frac{2}{\log 2} +
  \int_2^x \frac{dt}{\log^2 t}.
$$

  We have the crude bounds
  
$$
\int_2^{\sqrt{x}} \frac{dt}{\log^2 t} = O( \sqrt{x} )
$$

  and
  
$$
\int_{\sqrt{x}}^x \frac{dt}{\log^2 t} = O( \frac{x}{\log^2 x} )
$$

  and combining all this we obtain
  
$$
\int_2^x \frac{dt}{\log t} = \frac{x}{\log x} + O( \frac{x}{\log^2 x} )
$$

  
$$
= (1+o(1)) \frac{x}{\log x}
$$

  and the claim then follows from Theorem [pi-asymp](#pi_asymp).

## Proposition: pn-asymptotic {#pn_asymptotic lean="pn_asymptotic"}

One has
    
$$
p_n = (1+o(1)) n \log n
$$

  as $n \to \infty$.

### Proof {uses="pi_alt"}

Use Corollary [pi-alt](#pi_alt) to show that $n=\pi(p_n)\sim p_n/\log p_n$
    Taking logs gives $\log n \sim \log p_n - \log\log p_n \sim \log p_n$.
    Multiplying these gives $p_n\sim n\log n$ from which the result follows.

## Corollary: pn-pn-plus-one {#pn_pn_plus_one lean="pn_pn_plus_one"}

We have $p_{n+1} - p_n = o(p_n)$
    as $n \to \infty$.

### Proof {uses="pn_asymptotic"}

Easy consequence of preceding proposition.

## Corollary: prime-between {#prime_between lean="prime_between"}

For every $\varepsilon>0$, there is a prime between $x$ and $(1+\varepsilon)x$ for
  all sufficiently large $x$.

### Proof {uses="pi_alt"}

Use Corollary [pi-alt](#pi_alt) to show that $\pi((1+\varepsilon)x) - \pi(x)$ goes to infinity
  as $x \to \infty$.

## Proposition: mun {#mun lean="sum_mobius_div_self_le"}

We have $|\sum_{n \leq x} \frac{\mu(n)}{n}| \leq 1$.

### Proof

From M\"obius inversion $1_{n=1} = \sum_{d|n} \mu(d)$ and summing we have
    
$$
1 = \sum_{d \leq x} \mu(d) \lfloor \frac{x}{d} \rfloor
$$

    for any $x \geq 1$. Since $\lfloor \frac{x}{d} \rfloor = \frac{x}{d} - \epsilon_d$ with
    $0 \leq \epsilon_d < 1$ and $\epsilon_x = 0$, we conclude that
    
$$
1 ≥ x \sum_{d \leq x} \frac{\mu(d)}{d} - (x - 1)
$$

    and the claim follows.

## Proposition: M\"obius form of prime number theorem {#mu-pnt lean="mu_pnt"}

We have $\sum_{n \leq x} \mu(n) = o(x)$.

### Proof {uses="WeakPNT, mun"}

From the Dirichlet convolution identity
    
$$
\mu(n) \log n = - \sum_{d|n} \mu(d) \Lambda(n/d)
$$

  and summing we obtain
  
$$
\sum_{n \leq x} \mu(n) \log n = - \sum_{d \leq x} \mu(d) \sum_{m \leq x/d} \Lambda(m).
$$

  For any $\varepsilon>0$, we have from the prime number theorem that
  
$$
\sum_{m \leq x/d} \Lambda(m) = x/d + O(\varepsilon x/d) + O_\varepsilon(1)
$$

  (divide into cases depending on whether $x/d$ is large or small compared to $\varepsilon$).
  We conclude that
  
$$
\sum_{n \leq x} \mu(n) \log n
    = - x \sum_{d \leq x} \frac{\mu(d)}{d} + O(\varepsilon x \log x) + O_\varepsilon(x).
$$

  Applying [mun](#mun) we conclude that
  
$$
\sum_{n \leq x} \mu(n) \log n = O(\varepsilon x \log x) + O_\varepsilon(x).
$$

  and hence
  
$$
\sum_{n \leq x} \mu(n) \log x
    = O(\varepsilon x \log x) + O_\varepsilon(x) + O( \sum_{n \leq x} (\log x - \log n) ).
$$

  From Stirling's formula one has
  
$$
\sum_{n \leq x} (\log x - \log n) = O(x)
$$

  thus
  
$$
\sum_{n \leq x} \mu(n) \log x = O(\varepsilon x \log x) + O_\varepsilon(x)
$$

  and thus
  
$$
\sum_{n \leq x} \mu(n) = O(\varepsilon x) + O_\varepsilon(\frac{x}{\log x}).
$$

  Sending $\varepsilon \to 0$ we obtain the claim.

## Proposition: lambda-pnt {#lambda-pnt lean="lambda_pnt"}

We have $\sum_{n \leq x} \lambda(n) = o(x)$.

### Proof {uses="WeakPNT, mu-pnt, mun"}

From the identity
    
$$
\lambda(n) = \sum_{d^2|n} \mu(n/d^2)
$$

  and summing, we have
  
$$
\sum_{n \leq x} \lambda(n) = \sum_{d \leq \sqrt{x}} \sum_{n \leq x/d^2} \mu(n).
$$

  For any $\varepsilon>0$, we have from Proposition [M\"obius form of prime number theorem](#mu-pnt) that
  
$$
\sum_{n \leq x/d^2} \mu(n) = O(\varepsilon x/d^2) + O_\varepsilon(1)
$$

  and hence on summing in $d$
  
$$
\sum_{n \leq x} \lambda(n) = O(\varepsilon x) + O_\varepsilon(x^{1/2}).
$$

  Sending $\varepsilon \to 0$ we obtain the claim.

## Proposition: Alternate M\"obius form of prime number theorem {#mu-pnt-alt lean="mu_pnt_alt"}

We have $\sum_{n \leq x} \mu(n)/n = o(1)$.

### Proof {uses="mu-pnt"}

As in the proof of Theorem [mun](#mun), we have
    
$$
1 = \sum_{d \leq x} \mu(d) \lfloor \frac{x}{d} \rfloor
$$

    
$$
= x \sum_{d \leq x} \frac{\mu(d)}{d} - \sum_{d \leq x} \mu(d) \{ \frac{x}{d} \}
$$

  so it will suffice to show that
  
$$
\sum_{d \leq x} \mu(d) \{ \frac{x}{d} \} = o(x).
$$

  Let $N$  be a natural number.  It suffices to show that
  
$$
\sum_{d \leq x} \mu(d) \{ \frac{x}{d} \} = O(x/N).
$$

  if $x$ is large enough depending on $N$.
  We can split the left-hand side as the sum of
  
$$
\sum_{d \leq x/N} \mu(d) \{ \frac{x}{d} \}
$$

  and
  
$$
\sum_{j=1}^{N-1} \sum_{x/(j+1) < d \leq x/j} \mu(d) (x/d - j).
$$

  The first term is clearly $O(x/N)$.  For the second term, we can use Theorem [M\"obius form of prime number theorem](#mu-pnt)
  and summation by parts (using the fact that $x/d-j$ is monotone and bounded) to find that
  
$$
\sum_{x/(j+1) < d \leq x/j} \mu(d) (x/d - j) = o(x)
$$

  for any given $j$, so in particular
  
$$
\sum_{x/(j+1) < d \leq x/j} \mu(d) (x/d - j) = O(x/N^2)
$$

  for all $j=1,\dots,N-1$ if $x$ is large enough depending on $N$.
  Summing all the bounds, we obtain the claim.

**Consequences of the PNT in arithmetic progressions**

## Theorem: Prime number theorem in AP {#chebyshev-asymptotic-pnt lean="chebyshev_asymptotic_pnt"}

If $a\ (q)$ is a primitive residue class, then one has
  
$$
\sum_{p \leq x: p = a\ (q)} \log p = \frac{x}{\phi(q)} + o(x).
$$

### Proof {uses="WeakPNT-AP, chebyshev-asymptotic"}

This is a routine modification of the proof of Theorem [chebyshev-asymptotic](#chebyshev-asymptotic).

## Corollary: Dirichlet's theorem {#dirichlet_thm lean="dirichlet_thm"}

Any primitive residue class contains an infinite number of primes.

### Proof {uses="chebyshev-asymptotic-pnt"}

If this were not the case, then the sum $\sum_{p \leq x: p = a\ (q)} \log p$
  would be bounded in $x$, contradicting Theorem [Prime number theorem in AP](#chebyshev-asymptotic-pnt).

**Consequences of the Chebotarev density theorem**

## Lemma: Cyclotomic Chebotarev {#Chebotarev-cyclic}

For any $a$ coprime to $m$,

$$
\sum_{N \mathfrak{p} \leq x; N \mathfrak{p} = a\ (m)} \log N \mathfrak{p}  =
\frac{1}{|G|} \sum_{N \mathfrak{p} \leq x} \log N \mathfrak{p}.
$$

### Proof {uses="Dedekind-PNT, WeakPNT-AP"}

This should follow from Lemma [PNT for one character](#Dedekind-PNT) by a Fourier expansion.

