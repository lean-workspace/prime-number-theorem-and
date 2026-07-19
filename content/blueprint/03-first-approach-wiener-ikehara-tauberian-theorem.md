---
title: 'First approach: Wiener-Ikehara Tauberian theorem'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

**A Fourier-analytic proof of the Wiener-Ikehara theorem**

The Fourier transform of an absolutely integrable function $\psi: \mathbb{R} \to \mathbb{C}$ is defined by the
formula 
$$
\hat \psi(u) := \int_\mathbb{R} e(-tu) \psi(t)\ dt
$$
 where $e(\theta) := e^{2\pi i \theta}$.

Let $f: \mathbb{N} \to \mathbb{C}$ be an arithmetic function such that $\sum_{n=1}^\infty \frac{|f(n)|}{n^\sigma} <
\infty$ for all $\sigma>1$.  Then the Dirichlet series

$$
F(s) := \sum_{n=1}^\infty \frac{f(n)}{n^s}
$$

is absolutely convergent for $\sigma>1$.

## Lemma: first-fourier {#first-fourier lean="first_fourier"}

If $\psi: \mathbb{R} \to \mathbb{C}$ is integrable and $x > 0$, then for any $\sigma>1$
  
$$
\sum_{n=1}^\infty \frac{f(n)}{n^\sigma} \hat \psi( \frac{1}{2\pi} \log \frac{n}{x} ) =
  \int_\mathbb{R} F(\sigma + it) \psi(t) x^{it}\ dt.
$$

### Proof

By the definition of the Fourier transform, the left-hand side expands as
  
$$
\sum_{n=1}^\infty \int_\mathbb{R} \frac{f(n)}{n^\sigma} \psi(t) e( - \frac{1}{2\pi} t \log
  \frac{n}{x})\ dt
$$

  while the right-hand side expands as
  
$$
\int_\mathbb{R} \sum_{n=1}^\infty \frac{f(n)}{n^{\sigma+it}} \psi(t) x^{it}\ dt.
$$

  Since
  
$$
\frac{f(n)}{n^\sigma} \psi(t) e( - \frac{1}{2\pi} t \log \frac{n}{x}) =
  \frac{f(n)}{n^{\sigma+it}} \psi(t) x^{it}
$$

  the claim then follows from Fubini's theorem.

## Lemma: second-fourier {#second-fourier lean="second_fourier"}

If $\psi: \mathbb{R} \to \mathbb{C}$ is absolutely integrable and $x > 0$, then for any $\sigma>1$
  
$$
\int_{-\log x}^\infty e^{-u(\sigma-1)} \hat \psi(\frac{u}{2\pi})\ du =
  x^{\sigma - 1} \int_\mathbb{R} \frac{1}{\sigma+it-1} \psi(t) x^{it}\ dt.
$$

### Proof

The left-hand side expands as
  
$$
\int_{-\log x}^\infty \int_\mathbb{R} e^{-u(\sigma-1)} \psi(t) e(-\frac{tu}{2\pi})\ dt\ du
$$

  so by Fubini's theorem it suffices to verify the identity
  
$$
\begin{align*}
  \int_{-\log x}^\infty e^{-u(\sigma-1)} e(-\frac{tu}{2\pi})\ du
  &= \int_{-\log x}^\infty e^{(it - \sigma + 1)u}\ du \\
  &= \frac{1}{it - \sigma + 1} e^{(it - \sigma + 1)u}\ \Big|_{-\log x}^\infty \\
  &= x^{\sigma - 1} \frac{1}{\sigma+it-1} x^{it}
  \end{align*}
$$

Now let $A \in \mathbb{C}$, and suppose that there is a continuous function $G(s)$ defined on
$\mathrm{Re} s \geq 1$ such that $G(s) = F(s) - \frac{A}{s-1}$ whenever $\mathrm{Re} s > 1$.
We also make the Chebyshev-type hypothesis

$$
\begin{equation*}
\sum_{n \leq x} |f(n)| \ll x
\end{equation*}
$$

for all $x \geq 1$ (this hypothesis is not strictly necessary, but simplifies the arguments and
can be obtained fairly easily in applications).

## Lemma: Preliminary decay bound I {#prelim-decay lean="prelim_decay"}

\discussion{561}

If $\psi:\mathbb{R} \to \mathbb{C}$ is absolutely integrable then 
$$
|\hat \psi(u)| \leq \| \psi \|_1
$$

  for all $u \in \mathbb{R}$. where $C$ is an absolute constant.

### Proof

Immediate from the triangle inequality.

## Lemma: Preliminary decay bound II {#prelim-decay-2 lean="prelim_decay_2"}

\discussion{562}

If $\psi:\mathbb{R} \to \mathbb{C}$ is absolutely integrable and of bounded variation, then

$$
|\hat \psi(u)| \leq \| \psi \|_{TV} / 2\pi |u|
$$

for all non-zero $u \in \mathbb{R}$.

### Proof

By Lebesgue--Stiejtes integration by parts we have

$$
2\pi i u \hat \psi(u) = \int _\mathbb{R} e(-tu) d\psi(t)
$$

and the claim then follows from the triangle inequality.

## Lemma: Preliminary decay bound III {#prelim-decay-3 lean="prelim_decay_3"}

\discussion{563}

If $\psi:\mathbb{R} \to \mathbb{C}$ is absolutely integrable, absolutely continuous, and $\psi'$ is of bounded
variation, then

$$
|\hat \psi(u)| \leq \| \psi' \|_{TV} / (2\pi |u|)^2
$$

for all non-zero $u \in \mathbb{R}$.

### Proof {uses="prelim-decay-2"}

Should follow from previous lemma.

## Lemma: Decay bound, alternate form {#decay-alt lean="decay_alt"}

\discussion{564}

If $\psi:\mathbb{R} \to \mathbb{C}$ is absolutely
integrable, absolutely continuous, and $\psi'$ is of bounded variation, then

$$
|\hat \psi(u)| \leq ( \|\psi\|_1 + \| \psi' \|_{TV} / (2\pi)^2) / (1+|u|^2)
$$

for all $u \in \mathbb{R}$.

### Proof {uses="prelim-decay-3, decay, prelim-decay"}

Should follow from previous lemmas.

## Lemma: Decay bounds {#decay lean="decay_bounds"}

If $\psi:\mathbb{R} \to \mathbb{C}$ is $C^2$ and obeys the bounds
    
$$
|\psi(t)|, |\psi''(t)| \leq A / (1 + |t|^2)
$$

    for all $t \in \mathbb{R}$, then
  
$$
|\hat \psi(u)| \leq C A / (1+|u|^2)
$$

  for all $u \in \mathbb{R}$, where $C$ is an absolute constant.

### Proof

From two integration by parts we obtain the identity
  
$$
(1+u^2) \hat \psi(u) = \int_{\bf R} (\psi(t) - \frac{u}{4\pi^2} \psi''(t)) e(-tu)\ dt.
$$

  Now apply the triangle inequality and the identity $\int_{\bf R} \frac{dt}{1+t^2}\ dt = \pi$ to
  obtain the claim with $C = \pi + 1 / 4 \pi$.

## Lemma: Limiting Fourier identity {#limiting lean="limiting_fourier"}

If $\psi: \mathbb{R} \to \mathbb{C}$ is $C^2$ and compactly supported and $x \geq 1$, then
  
$$
\sum_{n=1}^\infty \frac{f(n)}{n} \hat \psi( \frac{1}{2\pi} \log \frac{n}{x} )
    - A \int_{-\log x}^\infty \hat \psi(\frac{u}{2\pi})\ du
    = \int_\mathbb{R} G(1+it) \psi(t) x^{it}\ dt.
$$

### Proof {uses="second-fourier, first-fourier"}

By Lemma [first-fourier](#first-fourier) and Lemma [second-fourier](#second-fourier), we know that for any $\sigma>1$,
  we have
  
$$
\sum_{n=1}^\infty \frac{f(n)}{n^\sigma} \hat \psi( \frac{1}{2\pi} \log \frac{n}{x} )
    - A x^{1-\sigma} \int_{-\log x}^\infty e^{-u(\sigma-1)} \hat \psi(\frac{u}{2\pi})\ du
    = \int_\mathbb{R} G(\sigma+it) \psi(t) x^{it}\ dt.
$$

  Now take limits as $\sigma \to 1$ using dominated convergence together with (cheby)
  and Lemma [Decay bounds](#decay) to obtain the result.

## Corollary: Corollary of limiting identity {#limiting-cor lean="limiting_cor"}

With the hypotheses as above, we have
  
$$
\sum_{n=1}^\infty \frac{f(n)}{n} \hat \psi( \frac{1}{2\pi} \log \frac{n}{x} )
    = A \int_{-\infty}^\infty \hat \psi(\frac{u}{2\pi})\ du + o(1)
$$

  as $x \to \infty$.

### Proof {uses="limiting"}

Immediate from the Riemann-Lebesgue lemma, and also noting that
  $\int_{-\infty}^{-\log x} \hat \psi(\frac{u}{2\pi})\ du = o(1)$.

## Lemma: Smooth Urysohn lemma {#smooth-ury lean="smooth_urysohn"}

If $I$ is a closed interval contained in an open interval $J$, then there exists a smooth
  function $\Psi: \mathbb{R} \to \mathbb{R}$ with $1_I \leq \Psi \leq 1_J$.

### Proof

A standard analysis lemma, which can be proven by convolving $1_K$ with a smooth approximation
  to the identity for some interval $K$ between $I$ and $J$. Note that we have
  ``SmoothBumpFunction''s on smooth manifolds in Mathlib, so this shouldn't be too hard...

## Lemma: Limiting identity for Schwartz functions {#schwarz-id lean="limiting_cor_schwartz"}

The previous corollary also holds for functions $\psi$ that are assumed to be in the Schwartz
  class, as opposed to being $C^2$ and compactly supported.

### Proof {uses="limiting-cor, smooth-ury"}

For any $R>1$, one can use a smooth cutoff function (provided by Lemma [Smooth Urysohn lemma](#smooth-ury) to write
  $\psi = \psi_{\leq R} + \psi_{>R}$, where $\psi_{\leq R}$ is $C^2$ (in fact smooth) and compactly
  supported (on $[-R,R]$), and $\psi_{>R}$ obeys bounds of the form
  
$$
|\psi_{>R}(t)|, |\psi''_{>R}(t)| \ll R^{-1} / (1 + |t|^2)
$$

  where the implied constants depend on $\psi$.  By Lemma [Decay bounds](#decay) we then have
  
$$
\hat \psi_{>R}(u) \ll R^{-1} / (1+|u|^2).
$$

  Using this and (cheby) one can show that
  
$$
\sum_{n=1}^\infty \frac{f(n)}{n} \hat \psi_{>R}( \frac{1}{2\pi} \log \frac{n}{x} ),
    A \int_{-\infty}^\infty \hat \psi_{>R} (\frac{u}{2\pi})\ du \ll R^{-1}
$$

  (with implied constants also depending on $A$), while from Lemma [Corollary of limiting identity](#limiting-cor) one has
  
$$
\sum_{n=1}^\infty \frac{f(n)}{n} \hat \psi_{\leq R}( \frac{1}{2\pi} \log \frac{n}{x} )
    = A \int_{-\infty}^\infty \hat \psi_{\leq R} (\frac{u}{2\pi})\ du + o(1).
$$

  Combining the two estimates and letting $R$ be large, we obtain the claim.

## Lemma: Bijectivity of Fourier transform {#bij lean="fourier_surjection_on_schwartz"}

The Fourier transform is a bijection on the Schwartz class. [Note: only surjectivity is
  actually used.]

### Proof

This is a standard result in Fourier analysis.
  It can be proved here by appealing to Mellin inversion, Theorem (MellinInversion).
  In particular, given $f$ in the Schwartz class, let
  $F : \mathbb{R}_+ \to \mathbb{C} : x \mapsto f(\log x)$ be a function in the ``Mellin space''; then the
  Mellin transform of $F$ on the imaginary axis $s=it$ is the Fourier transform of $f$.
  The Mellin inversion theorem gives Fourier inversion.

## Corollary: Smoothed Wiener-Ikehara {#WienerIkeharaSmooth lean="wiener_ikehara_smooth"}

If $\Psi: (0,\infty) \to \mathbb{C}$ is smooth and compactly supported away from the origin, then,
  
$$
\sum_{n=1}^\infty f(n) \Psi( \frac{n}{x} ) = A x \int_0^\infty \Psi(y)\ dy + o(x)
$$

  as $x \to \infty$.

### Proof {uses="schwarz-id, bij"}

By Lemma [Bijectivity of Fourier transform](#bij), we can write
  
$$
y \Psi(y) = \hat \psi( \frac{1}{2\pi} \log y )
$$

  for all $y>0$ and some Schwartz function $\psi$.  Making this substitution, the claim is then
  equivalent after standard manipulations to
  
$$
\sum_{n=1}^\infty \frac{f(n)}{n} \hat \psi( \frac{1}{2\pi} \log \frac{n}{x} )
    = A \int_{-\infty}^\infty \hat \psi(\frac{u}{2\pi})\ du + o(1)
$$

  and the claim follows from Lemma [Limiting identity for Schwartz functions](#schwarz-id).

Now we add the hypothesis that $f(n) \geq 0$ for all $n$.

## Proposition: Wiener-Ikehara in an interval {#WienerIkeharaInterval lean="WienerIkeharaInterval"}

For any closed interval $I \subset (0,+\infty)$, we have
  
$$
\sum_{n=1}^\infty f(n) 1_I( \frac{n}{x} ) = A x |I|  + o(x).
$$

### Proof {uses="WienerIkeharaSmooth"}

Use Lemma [Smooth Urysohn lemma](#smooth-ury) to bound $1_I$ above and below by smooth compactly supported functions whose integral is close to the measure of $|I|$, and use the non-negativity of $f$.

## Corollary: Wiener-Ikehara Theorem (1) {#WienerIkehara lean="WienerIkeharaTheorem'"}

We have
  
$$
\sum_{n\leq x} f(n) = A x + o(x).
$$

### Proof {uses="WienerIkeharaInterval"}

Apply the preceding proposition with $I = [\varepsilon,1]$ and then send
  $\varepsilon$ to zero (using (cheby) to control the error).

**Weak PNT**

## Theorem: WeakPNT {#WeakPNT lean="WeakPNT"}

We have
  
$$
\sum_{n \leq x} \Lambda(n) = x + o(x).
$$

### Proof {uses="WienerIkehara"}

Already done by Stoll, assuming Wiener-Ikehara.

**Removing the Chebyshev hypothesis**

In this section we do *not* assume the bound (cheby), but instead derive it from the other hypotheses.

## Lemma: limiting-fourier-variant {#limiting-fourier-variant lean="limiting_fourier_variant"}

If $\psi: \mathbb{R} \to \mathbb{C}$ is $C^2$ and compactly supported with $f$ and $\hat \psi$ non-negative, and $0 < x$, then
  
$$
\sum_{n=1}^\infty \frac{f(n)}{n} \hat \psi( \frac{1}{2\pi} \log \frac{n}{x} ) - A \int_{-\log x}^\infty \hat \psi(\frac{u}{2\pi})\ du =  \int_\mathbb{R} G(1+it) \psi(t) x^{it}\ dt.
$$

### Proof {uses="second-fourier, first-fourier, decay"}

Repeat the proof of Lemma [limiting-fourier-variant](#limiting-fourier-variant), but use monotone convergence instead of dominated convergence.  (The proof should be simpler, as one no longer needs to establish domination for the sum.)

## Corollary: crude-upper-bound {#crude-upper-bound lean="crude_upper_bound"}

If $\psi: \mathbb{R} \to \mathbb{C}$ is $C^2$ and compactly supported with $f$ and $\hat \psi$ non-negative, then there exists a constant $B$ such that
  
$$
|\sum_{n=1}^\infty \frac{f(n)}{n} \hat \psi( \frac{1}{2\pi} \log \frac{n}{x} )| \leq B
$$

  for all $x > 0$.

### Proof {uses="limiting-fourier-variant"}

This readily follows from the previous lemma and the triangle inequality.

## Corollary: auto-cheby {#auto-cheby lean="auto_cheby"}

One has 
$$
\sum_{n \leq x} f(n) = O(x)
$$
 for all $x \geq 1$.

### Proof {uses="second-fourier, first-fourier, crude-upper-bound, WienerIkehara"}

By applying Corollary [crude-upper-bound](#crude-upper-bound) for a specific compactly supported function $\psi$,
  one can obtain a bound of the form $\sum_{(1-\varepsilon)x < n \leq x} f(n) = O(x)$ for all $x$
  and some absolute constant $\varepsilon$ (which can be made explicit).

  If $C$ is a sufficiently large constant, the claim $|\sum_{n \leq x} f(n)| \leq Cx$ can now be
  proven by strong induction on $x$, as the claim for $(1-\varepsilon)x$ implies the claim for $x$
  by the triangle inequality (and the claim is trivial for $x < 1$).

## Theorem: Wiener-Ikehara Theorem (2) {#WienerIkehara2 lean="WienerIkeharaTheorem''"}

We have 
$$
\sum_{n\leq x} f(n) = A x + o(x).
$$

### Proof {uses="auto-cheby, WienerIkehara"}

Use Corollary [auto-cheby](#auto-cheby) to remove the Chebyshev hypothesis in Theorem [Wiener-Ikehara Theorem (1)](#WienerIkehara).

**The prime number theorem in arithmetic progressions**

## Lemma: WeakPNT-character {#WeakPNT-character lean="WeakPNT_character"}

If $q ≥ 1$ and $a$ is coprime to $q$, and $\mathrm{Re} s > 1$, we have
  
$$
\sum_{n: n = a\ (q)} \frac{\Lambda(n)}{n^s} = - \frac{1}{\varphi(q)} \sum_{\chi\ (q)}
  \overline{\chi(a)} \frac{L'(s,\chi)}{L(s,\chi)}.
$$

### Proof

From the Fourier inversion formula on the multiplicative group $(\mathbb{Z}/q\mathbb{Z})^\times$, we have
  
$$
1_{n=a\ (q)} = \frac{\varphi(q)}{q} \sum_{\chi\ (q)} \overline{\chi(a)} \chi(n).
$$

  On the other hand, from standard facts about L-series we have for each character $\chi$ that
  
$$
\sum_{n} \frac{\Lambda(n) \chi(n)}{n^s} = - \frac{L'(s,\chi)}{L(s,\chi)}.
$$

  Combining these two facts, we obtain the claim.

## Proposition: WeakPNT-AP-prelim {#WeakPNT-AP-prelim lean="WeakPNT_AP_prelim"}

If $q ≥ 1$ and $a$ is coprime to $q$, the Dirichlet series
  $\sum_{n \leq x: n = a\ (q)} \frac{\Lambda(n)}{n^s}$ converges for $\mathrm{Re}(s) > 1$ to
  $\frac{1}{\varphi(q)} \frac{1}{s-1} + G(s)$ where $G$ has a continuous extension to
  $\mathrm{Re}(s)=1$.

### Proof {uses="ChebyshevPsi, WeakPNT-character"}

We expand out the left-hand side using Lemma [WeakPNT-character](#WeakPNT-character).  The contribution of the
  non-principal characters $\chi$ extend continuously to $\mathrm{Re}(s) = 1$ thanks to the
  non-vanishing of $L(s,\chi)$ on this line (which should follow from another component of
  this project), so it suffices to show that for the principal character $\chi_0$, that
  
$$
-\frac{L'(s,\chi_0)}{L(s,\chi_0)} - \frac{1}{s-1}
$$

  also extends continuously here.  But we already know that
  
$$
-\frac{\zeta'(s)}{\zeta(s)} - \frac{1}{s-1}
$$

  extends, and from Euler product machinery one has the identity
  
$$
\frac{L'(s,\chi_0)}{L(s,\chi_0)}
  = \frac{\zeta'(s)}{\zeta(s)} + \sum_{p|q} \frac{\log p}{p^s-1}.
$$

  Since there are only finitely many primes dividing $q$, and each summand $\frac{\log p}{p^s-1}$
  extends continuously, the claim follows.

## Theorem: WeakPNT-AP {#WeakPNT-AP lean="WeakPNT_AP"}

If $q ≥ 1$ and $a$ is coprime to $q$, we have
  
$$
\sum_{n \leq x: n = a\ (q)} \Lambda(n) = \frac{x}{\varphi(q)} + o(x).
$$

### Proof {uses="WienerIkehara2, WeakPNT-AP-prelim, WienerIkehara"}

Apply Theorem [Wiener-Ikehara Theorem (1)](#WienerIkehara) (or Theorem [Wiener-Ikehara Theorem (2)](#WienerIkehara2) to avoid
  checking the Chebyshev condition) using Proposition [WeakPNT-AP-prelim](#WeakPNT-AP-prelim).

**The Chebotarev density theorem: the case of cyclotomic extensions**

In this section, $K$ is a number field, $L = K(\mu_m)$ for some natural number $m$, and
$G = Gal(K/L)$.

The goal here is to prove the Chebotarev density theorem for the case of cyclotomic extensions.

## Lemma: Dedekind-factor {#Dedekind-factor}

We have

$$
\zeta_L(s) = \prod_{\chi} L(\chi,s)
$$

for $\Re(s) > 1$, where $\chi$ runs over homomorphisms from $G$ to $\mathbb{C}^\times$ and $L$ is the
Artin $L$-function.

### Proof

See Propositions 7.1.16, 7.1.19 of \url{https://www.math.ucla.edu/ sharifi/algnum.pdf}.

## Lemma: Simple pole {#Dedekind-pole}

$\zeta_L$ has a simple pole at $s=1$.

### Proof

See Theorem 7.1.12 of \url{https://www.math.ucla.edu/ sharifi/algnum.pdf}.

## Lemma: Dedekind-nonvanishing {#Dedekind-nonvanishing}

For any non-principal character
$\chi$ of $Gal(K/L)$, $L(\chi,s)$ does not vanish for $\Re(s)=1$.

### Proof {uses="Dedekind-factor, Dedekind-pole"}

For $s=1$, this will follow from
Lemmas [Dedekind-factor](#Dedekind-factor), [Simple pole](#Dedekind-pole). For the rest of the line, one should be able to
adapt the arguments for the Dirichet L-function.

**The Chebotarev density theorem: the case of abelian extensions**

(Use the arguments in Theorem 7.2.2 of \url{https://www.math.ucla.edu/ sharifi/algnum.pdf} to extend the
previous results to abelian extensions (actually just cyclic extensions would suffice))

**The Chebotarev density theorem: the general case**

(Use the arguments in Theorem 7.2.2 of \url{https://www.math.ucla.edu/ sharifi/algnum.pdf} to extend the
previous results to arbitrary extensions

## Lemma: PNT for one character {#Dedekind-PNT}

For any non-principal character $\chi$ of
$Gal(K/L)$, 
$$
\sum_{N \mathfrak{p} \leq x} \chi(\mathfrak{p}) \log N \mathfrak{p}  = o(x).
$$

### Proof {uses="Dedekind-nonvanishing"}

This should follow from Lemma [Dedekind-nonvanishing](#Dedekind-nonvanishing)
and the arguments for the Dirichlet L-function. (It may be more convenient to work with a
von Mangoldt type function instead of $\log N\mathfrak{p}$).

