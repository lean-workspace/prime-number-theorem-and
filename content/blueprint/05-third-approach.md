---
title: 'Third Approach'
type: "blueprint-chapter"
tags:
  - "blueprint"
---

**Hadamard factorization**

In this file, we prove the Hadamard Factorization theorem for functions of finite order,
and prove that the zeta function is such.

**Hoffstein-Lockhart**

In this file, we use the Hoffstein-Lockhart construction to prove a zero-free region for zeta.

Hoffstein-Lockhart + Goldfeld-Hoffstein-Liemann

Instead of the ``slick'' identity $3+4\cos\theta+\cos2\theta=2(\cos\theta+1)^2\ge0$, we use the
following more robust identity.

## Theorem: HLineq {#thm:HLineq}

For any $p>0$ and $t\in\mathbb{R}$,

$$
3+p^{2it}+p^{-2it}+2p^{it}+2p^{-it} \ge 0.
$$

### Proof

This follows immediately from the identity

$$
|1+p^{it}+p^{-it}|^2=1+p^{2it}+p^{-2it}+2p^{it}+2p^{-it}+2.
$$

[Note: identities of this type will work in much greater generality, especially for
higher degree $L$-functions.]

This means that, for fixed $t$, we define the following alternate function.

## Definition: FsigmaDef {#FsigmaDef}

For $\sigma>1$ and $t\in\mathbb{R}$, define

$$
F(\sigma) := \zeta^3(\sigma)\zeta^2(\sigma+it)\zeta^2(\sigma-it)\zeta(\sigma+2it)\zeta(\sigma-2it).
$$

## Theorem: FsigmaThm {#FsigmaThm}

Then $F$ is real-valued, and
whence $F(\sigma)\ge1$ there.

### Proof {uses="thm:HLineq, FsigmaDef"}

That
$\log F(\sigma)\ge0$ for $\sigma>1$ follows from
Theorem [HLineq](#thm:HLineq).

[Note: I often prefer to avoid taking logs of functions that, even if real-valued, have to be
justified as being such. Instead, I like to start with ``logF'' as a convergent
Dirichlet series, show that it is real-valued and non-negative, and then exponentiate...]

From this and Hadamard factorization, we deduce the following.

## Theorem: StrongZeroFree {#thm:StrongZeroFree}

There is a constant $c>0$, so that $\zeta(s)$ does not vanish in
the region $\sigma>1-\frac{c}{\log t}$, and moreover,

$$
-\frac{\zeta'}{\zeta}(\sigma+it) \ll (\log t)^2
$$

there.

### Proof {uses="FsigmaThm"}

Use Theorem [FsigmaThm](#FsigmaThm) and Hadamard factorization.

This allows us to quantify precisely the relationship between $T$ and $\delta$ in
Theorem [ZetaNoZerosInBox](#ZetaNoZerosInBox)....

**Strong PNT**

## Lemma: AnalyticOn.norm-le-of-norm-le-on-sphere {#AnalyticOn.norm_le_of_norm_le_on_sphere lean="AnalyticOn.norm_le_of_norm_le_on_sphere"}

An application of the Maximum modulus principle.

### Proof

This is standard in the literature.

## Theorem: borelCaratheodory' {#borelCaratheodory' lean="borelCaratheodory'"}

An application of
    `Complex.borelCaratheodory_zero`.

### Proof

This is standard in the literature.

This upstreamed from https://github.com/math-inc/strongpnt/tree/main

## Lemma: cauchy-formula-deriv {#cauchy_formula_deriv lean="cauchy_formula_deriv"}

Let $f$ be analytic on $|z|\leq R$. For any $z$ with $|z|\leq r$ and any $r'$
    with $0 < r < r' < R$ we have
    
$$
f'(z)=\frac{1}{2\pi i}\oint_{|w|=r'}\frac{f(w)}{(w-z)^2}\,dw=\frac{1}{2\pi}
    \int_0^{2\pi}\frac{r'e^{it}\,f(r'e^{it})}{(r'e^{it}-z)^2}\,dt.
$$

### Proof

This is just Cauchy's integral formula for derivatives.

## Lemma: DerivativeBound {#DerivativeBound lean="DerivativeBound"}

Let $R,\,M>0$ and $0 < r < r' < R$. Let $f$ be analytic on $|z|\leq R$ such that
    $f(0)=0$ and suppose $\Re f(z)\leq M$ for all $|z|\leq R$. Then we have that
    
$$
|f'(z)|\leq\frac{2M(r')^2}{(R-r')(r'-r)^2}
$$

    for all $|z|\leq r$.

### Proof {uses="cauchy_formula_deriv, borelCaratheodory'"}

By Lemma [cauchy-formula-deriv](#cauchy_formula_deriv) we know that
    
$$
f'(z)=\frac{1}{2\pi i}\oint_{|w|=r'}\frac{f(w)}{(w-z)^2}\,dw
      =\frac{1}{2\pi }\int_0^{2\pi}\frac{r'e^{it}\,f(r'e^{it})}{(r'e^{it}-z)^2}\,dt.
$$

    Thus,
    
$$
        |f'(z)|=\left|\frac{1}{2\pi}\int_0^{2\pi}
          \frac{r'e^{it}\,f(r'e^{it})}{(r'e^{it}-z)^2}\,dt\right|
          \leq\frac{1}{2\pi}\int_0^{2\pi}
          \left|\frac{r'e^{it}\,f(r'e^{it})}{(r'e^{it}-z)^2}\right|\,dt.
$$

    Now applying Theorem [borelCaratheodory'](#borelCaratheodory'), and noting that
    $r'-r\leq|r'e^{it}-z|$, we have that
    
$$
\left|\frac{r'e^{it}\,f(r'e^{it})}{(r'e^{it}-z)^2}\right|
      \leq\frac{2M(r')^2}{(R-r')(r'-r)^2}.
$$

    Substituting this into Equation ((pickupPoint1)) and evaluating the integral
    completes the proof.

## Theorem: BorelCaratheodoryDeriv {#BorelCaratheodoryDeriv lean="BorelCaratheodoryDeriv"}

Let $R,\,M>0$. Let $f$ be analytic on $|z|\leq R$ such that $f(0)=0$ and suppose
    $\Re f(z)\leq M$ for all $|z|\leq R$. Then for any $0 < r < R$,
    
$$
|f'(z)|\leq\frac{16MR^2}{(R-r)^3}
$$

    for all $|z|\leq r$.

### Proof {uses="DerivativeBound"}

Using Lemma [DerivativeBound](#DerivativeBound) with $r'=(R+r)/2$, and noting that $r < R$,
    we have that
    
$$
|f'(z)|\leq\frac{4M(R+r)^2}{(R-r)^3}\leq\frac{16MR^2}{(R-r)^3}.
$$

## Definition: TaxicabIntegral {#TaxicabIntegral}

Let $0 < R$. Let $f:\overline{\mathbb{D}_R}\to\mathbb{C}$ be analytic on neighborhoods of points
  in $\overline{\mathbb{D}_R}$. Define the functon $I_f:\mathbb{D}_R\to\mathbb{C}$ by
    
$$
I_f(z)=z\int_0^1f(tz)\,dt.
$$

## Theorem: LogOfAnalyticFunction {#LogOfAnalyticFunction lean="LogOfAnalyticFunction"}

Let $0<r<R$. Let $B:\overline{\mathbb{D}_{R}}\to\mathbb{C}$ be analytic on neighborhoods of
    points in $\overline{\mathbb{D}_{R}}$ with $B(z)\neq 0$ for all
    $z\in\overline{\mathbb{D}_{R}}$.Then there exists $J_B:\mathbb{D}_R\to\mathbb{C}$ that is
    analytic on neighborhoods of points in $\mathbb{D}_R$ such that
    
- $J_B(0)=0$
- $J_B'(z)=B'(z)/B(z)$ for all $z\in\overline{\mathbb{D}_r}$
- $\log|B(z)|-\log|B(0)|=\mathfrak{R}J_B(z)$ for all $z\in\mathbb{D}_R$.

### Proof

We let $J_B(z)=I_{B'/B}(z)$. Then clearly, $J_B(0)=0$. Now note that
    
$$
\begin{aligned}
        I_{B'/B}(z)=z\int_0^1(B'/B)(tz)\,dt=\int_0^z(B'/B)(u)\,du.
    \end{aligned}
$$

    Thus by the fundamental theorem of calculus we have that $J_B'(z)=B'(z)/B(z)$. Now let
    $H(z)=\exp(J_B(z))/B(z)$ and note that
    
$$
H'(z)=(B(z)\,J_B'(z)-B'(z))\left(\frac{\exp(J_B(z))}{(B(z))^2}\right).
$$

    Thus, $H$ is constant since we know that $B(z)\,J_B'(z)-B(z)=0$ from $J_B'(z)=B'(z)/B(z)$. So
    since $H(0)=\exp(J_B(0))/B(0)=1/B(0)$ we know $H(z)=1/B(0)$ for all $z$. So we have,
    
$$
\frac{1}{B(0)}=\frac{\exp(J_B(z))}{B(z)}\implies\left|\frac{B(z)}{B(0)}\right|
      =\exp(\mathfrak{R}J_B(z)).
$$

    Taking the logarithm of both sides completes the proof.

## Theorem: LogOfAnalyticFunction' {#LogOfAnalyticFunction' lean="LogOfAnalyticFunction'"}

A wrapper of the above theorem that will be useful later on.

### Proof {uses="LogOfAnalyticFunction"}

See above.

## Definition: SetOfZeros {#SetOfZeros lean="SetOfZeros"}

Let $R>0$ and $f:\mathbb{C}\to\mathbb{C}$. Define the set of zeros
    $\mathcal{K}_f(R)=\{\rho\in\mathbb{C}:|\rho|\leq R,\,f(\rho)=0\}$.

## Definition: ZeroOrder {#ZeroOrder}

Let $f:\mathbb{C}\to\mathbb{C}$.
  We define $m_f(\rho)$ as the order of the zero $\rho$ w.r.t $f$.

In LEAN, this corresponds exactly with analyticOrderAt/analyticOrderNatAt.

## Definition: ZeroFactor {#ZeroFactor lean="ZeroFactor"}

Let $f:\mathbb{C}\to\mathbb{C}$ and $\rho\in\mathbb{C}$. Then there exists $h_\rho$ such that
    
$$
f(z)=(z-\rho)^{m_f(\rho)}\,h_\rho(z).
$$

    In LEAN, this corresponds exactly with (-.analyticOrderAt-ne-top.mp -).choose,
    but this serves as a wrapper of that with the necessary conditions.

## Lemma: ZeroFactorization {#ZeroFactorization lean="ZeroFactorization" uses="SetOfZeros, ZeroFactor"}

Let $f:\mathbb{C}\to\mathbb{C}$ be analytic on $\overline{\mathbb{D}_1}$ with $f(0)\neq 0$.
    For all $\rho\in\mathcal{K}_f(R)$ with $R<1$ there exists $h_\rho(z)$ such that
    $h_\rho(z)$ is analytic at $\rho$, $h_\rho(\rho)\neq 0$, and
    $f(z)=(z-\rho)^{m_f(\rho)}\,h_\rho(z)$.

### Proof

Since $f$ is analytic on neighborhoods of points in $\overline{\mathbb{D}_1}$ we know
    that there exists a series expansion about $\rho$:
    
$$
f(z)=\sum_{0\leq n}a_n\,(z-\rho)^n.
$$

    Now if we let $m$ be the smallest number such that $a_m\neq 0$, then
    
$$
f(z)=\sum_{0\leq n}a_n\,(z-\rho)^n=\sum_{m\leq n}a_n\,(z-\rho)^n
      =(z-\rho)^m\sum_{m\leq n}a_n\,(z-\rho)^{n-m}=(z-\rho)^m\,h_\rho(z).
$$

    Trivially, $h_\rho(z)$ is analytic at $\rho$ (we have written down the series
    expansion); now note that
    
$$
h_\rho(\rho)=\sum_{m\leq n}a_n(\rho-\rho)^{n-m}=\sum_{m\leq n}a_n0^{n-m}=a_m\neq 0.
$$

## Definition: CFunction {#CFunction lean="Cf" uses="SetOfZeros, ZeroFactor"}

Let $0 < r < 1$, and $f:\mathbb{C}\to\mathbb{C}$ be analytic on $\overline{\mathbb{D}_1}$ with
    $f(0)\neq 0$. We define a function $C_f:\mathbb{C}\to\mathbb{C}$ as follows. This function is
    constructed by dividing $f(z)$ by a polynomial whose roots are the zeros of $f$ inside
    $\overline{\mathbb{D}_r}$.
    
$$
C_f(z)=\begin{cases}
        \displaystyle\frac{f(z)}{\prod_{\rho\in\mathcal{K}_f(r)}(z-\rho)^{m_f(\rho)}}
          \qquad\text{for }z\not\in\mathcal{K}_f(r) \\
        \displaystyle\frac{h_z(z)}{\prod_{\rho\in\mathcal{K}_f(r)\setminus\{z\}}
          (z-\rho)^{m_f(\rho)}}\qquad\text{for }z\in\mathcal{K}_f(r)
    \end{cases}
$$

    where $h_z(z)$ comes from Lemma [ZeroFactorization](#ZeroFactorization).

## Lemma: CfAnalytic {#CfAnalytic lean="CfAnalytic" uses="CFunction"}

If $f:\mathbb{C}\to\mathbb{C}$ is analytic on $\overline{\mathbb{D}_1}$ then so too is $C_f$.

### Proof {uses="ZeroFactorization, SetOfZeros, ZeroFactor"}

Look at the definition of $C_f$ and apply ZeroFactorization.

## Definition: BlaschkeB {#BlaschkeB lean="BlaschkeB" uses="CFunction, SetOfZeros"}

Let $0 < r < R < 1$, and $f:\mathbb{C}\to\mathbb{C}$ be analytic $\overline{\mathbb{D}_1}$ with
    $f(0)\neq 0$. We define a function $B_f:\mathbb{C}\to\mathbb{C}$ as follows.
    
$$
B_f(z)=C_f(z)\prod_{\rho\in\mathcal{K}_f(r)}
      \left(R-\frac{z\overline{\rho}}{R}\right)^{m_f(\rho)}
$$

## Lemma: BlaschkeAnalytic {#BlaschkeAnalytic lean="BlaschkeAnalytic" uses="BlaschkeB, SetOfZeros"}

If $f:\mathbb{C}\to\mathbb{C}$ is analytic on $\overline{\mathbb{D}_R}$ then so too is $B_f$.

### Proof {uses="CFunction, CfAnalytic"}

Expand out $B_f$ as a product, and observe that each part is analytic on $\overline{\mathbb{D}_R}$.

## Lemma: BlaschkeOfZero {#BlaschkeOfZero lean="BlaschkeOfZero" uses="BlaschkeB, SetOfZeros"}

Let $0 < r < R<1$, and $f:\mathbb{C}\to\mathbb{C}$ be analytic on $\overline{\mathbb{D}_1}$ with
    $f(0)\neq 0$. Then
    
$$
|B_f(0)|=|f(0)|\prod_{\rho\in\mathcal{K}_f(r)}
      \left(\frac{R}{|\rho|}\right)^{m_f(\rho)}.
$$

### Proof {uses="CFunction, ZeroFactor"}

Since $f(0)\neq 0$, we know that $0\not\in\mathcal{K}_f(r)$. Thus,
    
$$
C_f(0)=\frac{f(0)}{\displaystyle\prod_{\rho\in\mathcal{K}_f(r)}(-\rho)^{m_f(\rho)}}.
$$

    Thus, substituting this into Definition [BlaschkeB](#BlaschkeB),
    
$$
|B_f(0)|=|C_f(0)|\prod_{\rho\in\mathcal{K}_f(r)}R^{m_f(\rho)}
      =|f(0)|\prod_{\rho\in\mathcal{K}_f(r)}\left(\frac{R}{|\rho|}\right)^{m_f(\rho)}.
$$

## Lemma: norm-fOfZero-le-norm-BlaschkeOfZero {#norm_fOfZero_le_norm_BlaschkeOfZero lean="norm_fOfZero_le_norm_BlaschkeOfZero" uses="BlaschkeB, SetOfZeros"}

Let $0 < r < R<1$, and $f:\mathbb{C}\to\mathbb{C}$ be analytic on $\overline{\mathbb{D}_1}$ with
    $f(0)\neq 0$. Then
    
$$
|f(0)|\leq|B_f(0)|.
$$

### Proof {uses="BlaschkeOfZero"}

Applying lemma [BlaschkeOfZero](#BlaschkeOfZero) we know that
    
$$
|B_f(0)|=|f(0)|\prod_{\rho\in\mathcal{K}_f(r)}
      \left(\frac{R}{|\rho|}\right)^{m_f(\rho)}.
$$

    Note that for all $\rho\in\mathcal{K}_f(r)$ that $1<R/|\rho|$ since $r<R$.
    Thus, the result follows.

## Lemma: DiskBound {#DiskBound lean="DiskBound" uses="BlaschkeB, SetOfZeros"}

Let $0 < r < R<1$. If $f:\mathbb{C}\to\mathbb{C}$ is a function analytic on
    $\overline{\mathbb{D}_1}$ with $f(0)\neq0$ such that $|f(z)|\leq B$ for $|z|\leq R$,
    then $|B_f(z)|\leq B$ for $|z|\leq R$ also.

### Proof {uses="CFunction, AnalyticOn.norm_le_of_norm_le_on_sphere, ZeroFactor, BlaschkeAnalytic"}

For $|z|=R$, we know that $z\not\in\mathcal{K}_f(r)$. Thus,
    
$$
C_f(z)=\frac{f(z)}{\displaystyle\prod_{\rho\in\mathcal{K}_f(r)}(z-\rho)^{m_f(\rho)}}.
$$

    Thus, substituting this into Definition [BlaschkeB](#BlaschkeB),
    
$$
|B_f(z)|=|f(z)|\prod_{\rho\in\mathcal{K}_f(r)}
      \left|\frac{R-z\overline{\rho}/R}{z-\rho}\right|^{m_f(\rho)}.
$$

    But note that
    
$$
\left|\frac{R-z\overline{\rho}/R}{z-\rho}\right|
      =\frac{|R^2-z\overline{\rho}|/R}{|z-\rho|}
      =\frac{|z|\cdot|\overline{z-\rho}|/R}{|z-\rho|}=1.
$$

    So we have that $|B_f(z)|=|f(z)|\leq B$ when $|z|=R$. Now by the maximum modulus
    principle, we know that the maximum of $|B_f|$ must occur on the boundary where
    $|z|=R$. Thus $|B_f(z)|\leq B$ for all $|z|\leq R$.

## Lemma: BlaschkeNonZero {#BlaschkeNonZero lean="BlaschkeNonzero" uses="BlaschkeB, SetOfZeros"}

Let $0 < r < R<1$ and $f:\overline{\mathbb{D}_1}\to\mathbb{C}$ be analytic on
    neighborhoods of points in $\overline{\mathbb{D}_1}$ with $f(0)\neq 0$. Then $B_f(z)\neq 0$
    for all $z\in\overline{\mathbb{D}_r}$.

### Proof {uses="CFunction, ZeroFactorization, ZeroFactor"}

Suppose that $z\in\mathcal{K}_f(r)$. Then we have that
    
$$
C_f(z)=\frac{h_z(z)}{\displaystyle\prod_{\rho\in\mathcal{K}_f(r)\setminus\{z\}}
      (z-\rho)^{m_f(\rho)}}.
$$

    where $h_z(z)\neq 0$ according to Lemma [ZeroFactorization](#ZeroFactorization). Thus, substituting
    this into Definition [BlaschkeB](#BlaschkeB),
    
$$
        |B_f(z)|=|h_z(z)|\cdot\left|R-\frac{|z|^2}{R}\right|^{m_f(z)}
          \prod_{\rho\in\mathcal{K}_f(r)\setminus\{z\}}
          \left|\frac{R-z\overline{\rho}/R}{z-\rho}\right|^{m_f(\rho)}.
$$

    Trivially, $|h_z(z)|\neq 0$. Now note that
    
$$
\left|R-\frac{|z|^2}{R}\right|=0\implies|z|=R.
$$

    However, this is a contradiction because $z\in\overline{\mathbb{D}_r}$ tells us that
    $|z|\leq r < R$. Similarly, note that
    
$$
\left|\frac{R-z\overline{\rho}/R}{z-\rho}\right|=0\implies|z|=\frac{R^2}{|\overline{\rho}|}.
$$

    However, this is also a contradiction because $\rho\in\mathcal{K}_f(r)$ tells us that
    $R < R^2/|\overline{\rho}|=|z|$, but $z\in\overline{\mathbb{D}_r}$ tells us that
    $|z|\leq r < R$. So, we know that
    
$$
\left|R-\frac{|z|^2}{R}\right|\neq 0\qquad\text{and}\qquad
      \left|\frac{R-z\overline{\rho}/R}{z-\rho}\right|\neq 0
      \quad\text{for all}\quad\rho\in\mathcal{K}_f(r)\setminus\{z\}.
$$

    Applying this to Equation ((pickupPoint2)) we have that $|B_f(z)|\neq 0$.
    So, $B_f(z)\neq 0$.

    Now suppose that $z\not\in\mathcal{K}_f(r)$. Then we have that
    
$$
C_f(z)=\frac{f(z)}{\displaystyle\prod_{\rho\in\mathcal{K}_f(r)}(z-\rho)^{m_f(\rho)}}.
$$

    Thus, substituting this into Definition [BlaschkeB](#BlaschkeB),
    
$$
        |B_f(z)|=|f(z)|\prod_{\rho\in\mathcal{K}_f(r)}
          \left|\frac{R-z\overline{\rho}/R}{z-\rho}\right|^{m_f(\rho)}.
$$

    We know that $|f(z)|\neq 0$ since $z\not\in\mathcal{K}_f(r)$. Now note that
    
$$
\left|\frac{R-z\overline{\rho}/R}{z-\rho}\right|=0\implies|z|=\frac{R^2}{|\overline{\rho}|}.
$$

    However, this is a contradiction because $\rho\in\mathcal{K}_f(r)$ tells us that
    $R < R^2/|\overline{\rho}|=|z|$, but $z\in\overline{\mathbb{D}_r}$ tells us that
    $|z|\leq r < R$. So, we know that
    
$$
\left|\frac{R-z\overline{\rho}/R}{z-\rho}\right|\neq 0
      \quad\text{for all}\quad\rho\in\mathcal{K}_f(r).
$$

    Applying this to Equation ((pickupPoint3)) we have that $|B_f(z)|\neq 0$.
    So, $B_f(z)\neq 0$.

    We have shown that $B_f(z)\neq 0$ for both $z\in\mathcal{K}_f(r)$ and
    $z\not\in\mathcal{K}_f(r)$, so the result follows.

## Theorem: ZerosBound {#ZerosBound lean="ZerosBound" uses="SetOfZeros"}

Let $0< r < R<1$. If $f:\mathbb{C}\to\mathbb{C}$ is a function analytic on
    neighborhoods of points in $\overline{\mathbb{D}_1}$ with $f(0)=1$ and $|f(z)|\leq B$
    for $|z|\leq R$, then
    
$$
\sum_{\rho\in\mathcal{K}_f(r)}m_f(\rho)\leq\frac{\log B}{\log(R/r)}.
$$

### Proof {uses="BlaschkeB, DiskBound, BlaschkeOfZero"}

Since $f(0)=1$, by Lemma [BlaschkeOfZero](#BlaschkeOfZero) we know that
    
$$
|B_f(0)|
      =|f(0)|\prod_{\rho\in\mathcal{K}_f(r)}\left(\frac{R}{|\rho|}\right)^{m_f(\rho)}
      =\prod_{\rho\in\mathcal{K}_f(r)}\left(\frac{R}{|\rho|}\right)^{m_f(\rho)}.
$$

    Thus, substituting this into Definition [BlaschkeB](#BlaschkeB),
    
$$
(R/r)^{\sum_{\rho\in\mathcal{K}_f(r)}m_f(\rho)}
      =\prod_{\rho\in\mathcal{K}_f(r)}\left(\frac{R}{r}\right)^{m_f(\rho)}
      \leq\prod_{\rho\in\mathcal{K}_f(r)}\left(\frac{R}{|\rho|}\right)^{m_f(\rho)}
      =|B_f(0)|\leq B
$$

    whereby Lemma [DiskBound](#DiskBound) we know that $|B_f(z)|\leq B$ for all $|z|\leq R$.
    Taking the logarithm of both sides and rearranging gives the desired result.

## Definition: JBlaschke {#JBlaschke lean="JBlaschke" uses="BlaschkeNonZero, BlaschkeB, SetOfZeros, BlaschkeAnalytic, LogOfAnalyticFunction'"}

Let $0 < r < R<1$. If $f:\mathbb{C}\to\mathbb{C}$ is a function analytic on
    neighborhoods of points in $\overline{\mathbb{D}_1}$ with $f(0)=1$, define
    $L_f(z)=J_{B_f}(z)$ where $J$ is from Theorem [LogOfAnalyticFunction](#LogOfAnalyticFunction) and $B_f$
    is from Definition [BlaschkeB](#BlaschkeB).

## Theorem: JBlaschkeDerivBound {#JBlaschkeDerivBound lean="JBlaschkeDerivBound" uses="SetOfZeros, JBlaschke"}

Let $B>1$ and $0 < r' < r < R<1$. If $f:\mathbb{C}\to\mathbb{C}$ is a function analytic
    on neighborhoods of points in $\overline{\mathbb{D}_1}$ with $f(0)=1$ and $|f(z)|\leq B$
    for all $|z|\leq R$, then for all $|z|\leq r'$
    
$$
|L_f'(z)|\leq\frac{16\log(B)\,r^2}{(r-r')^3}.
$$

### Proof {uses="BlaschkeNonZero, BlaschkeB, norm_fOfZero_le_norm_BlaschkeOfZero, DiskBound, BlaschkeAnalytic, LogOfAnalyticFunction', BorelCaratheodoryDeriv"}

By Lemma [DiskBound](#DiskBound) we immediately know that $|B_f(z)|\leq B$ for all $|z|\leq R$.
    Now since $L_f=J_{B_f}$ by Definition [JBlaschke](#JBlaschke), by Theorem
    [LogOfAnalyticFunction](#LogOfAnalyticFunction) we know that
    
$$
L_f(0)=0\qquad\text{and}\qquad
      \Re L_f(z)=\log|B_f(z)|-\log|B_f(0)|\leq\log|B_f(z)|\leq\log B
$$

    for all $|z|\leq r$. Note that in the above
    
$$
0=\log|f(0)|\leq\log|B_f(0)|
$$

    because of Lemma [norm-fOfZero-le-norm-BlaschkeOfZero](#norm_fOfZero_le_norm_BlaschkeOfZero). So by Theorem [BorelCaratheodoryDeriv](#BorelCaratheodoryDeriv), it follows that
    
$$
|L_f'(z)|\leq\frac{16\log(B)\,r^2}{(r-r')^3}
$$

    for all $|z|\leq r'$.

## Theorem: FinalBound {#FinalBound lean="FinalBound" uses="SetOfZeros"}

Let $B>1$ and $0 < r' < r < R' < R<1$. If $f:\mathbb{C}\to\mathbb{C}$ is a function
    analytic on neighborhoods of points in $\overline{\mathbb{D}_1}$ with $f(0)=1$ and
    $|f(z)|\leq B$ for all $|z|\leq R$, then for all
    $z\in\overline{\mathbb{D}_{r'}}\setminus\mathcal{K}_f(R')$ we have
    
$$
\left|\frac{f'}{f}(z)-\sum_{\rho\in\mathcal{K}_f(r)}\frac{m_f(\rho)}{z-\rho}\right|
      \leq\left(\frac{16r^2}{(r-r')^3}+\frac{1}{(R^2/R'-R')\,\log(R/R')}\right)\log B.
$$

### Proof {uses="BlaschkeNonZero, BlaschkeB, ZerosBound, CFunction, JBlaschke, ZeroFactor, JBlaschkeDerivBound, BlaschkeAnalytic, LogOfAnalyticFunction'"}

Since $z\in\overline{\mathbb{D}_{r'}}\setminus\mathcal{K}_f(R')$ we know that
    $z\not\in\mathcal{K}_f(R')$; thus, by Definition [CFunction](#CFunction) we know that
    
$$
C_f(z)=\frac{f(z)}{\displaystyle\prod_{\rho\in\mathcal{K}_f(r)}(z-\rho)^{m_f(\rho)}}.
$$

    Substituting this into Definition [BlaschkeB](#BlaschkeB) we have that
    
$$
B_f(z)=f(z)\prod_{\rho\in\mathcal{K}_f(r)}
      \left(\frac{R-z\overline{\rho}/R}{z-\rho}\right)^{m_f(\rho)}.
$$

    Taking the complex logarithm of both sides we have that
    
$$
\mathrm{Log}\,B_f(z)=\mathrm{Log}\,f(z)
      +\sum_{\rho\in\mathcal{K}_f(r)}m_f(\rho)\,\mathrm{Log}(R-z\overline{\rho}/R)
      -\sum_{\rho\in\mathcal{K}_f(r)}m_f(\rho)\,\mathrm{Log}(z-\rho).
$$

    Taking the derivative of both sides we have that
    
$$
\frac{B_f'}{B_f}(z)=\frac{f'}{f}(z)
      +\sum_{\rho\in\mathcal{K}_f(r)}\frac{m_f(\rho)}{z-R^2/\overline{\rho}}
      -\sum_{\rho\in\mathcal{K}_f(r)}\frac{m_f(\rho)}{z-\rho}.
$$

    By Definition [JBlaschke](#JBlaschke) and Theorem [LogOfAnalyticFunction](#LogOfAnalyticFunction),
    since $L_f(z)=J_{B_f}(z)$ we have $L_f'(z)=J'_{B_f}(z)=(B_f'/B_f)(z)$. Thus,
    
$$
\frac{f'}{f}(z)-\sum_{\rho\in\mathcal{K}_f(r)}\frac{m_f(\rho)}{z-\rho}
      =L_f'(z)-\sum_{\rho\in\mathcal{K}_f(r)}\frac{m_f(\rho)}{z-R^2/\overline{\rho}}.
$$

    Now since $z\in\overline{\mathbb{D}_{r'}}\subseteq\overline{\mathbb{D}_{R'}}$ and $\rho\in\mathcal{K}_f(r)\subseteq\mathcal{K}_f(R')$, we know that
    $R^2/R'-R'\leq|z-R^2/\overline{\rho}|$. Thus by the triangle inequality we have
    
$$
\left|\frac{f'}{f}(z)-\sum_{\rho\in\mathcal{K}_f(r)}\frac{m_f(\rho)}{z-\rho}\right|
      \leq|L_f'(z)|+\left(\frac{1}{R^2/R'-R'}\right)\sum_{\rho\in\mathcal{K}_f(r)}m_f(\rho).
$$

    Now by Theorem [ZerosBound](#ZerosBound) and [JBlaschkeDerivBound](#JBlaschkeDerivBound) we get our desired result
    with a little algebraic manipulation.

API analogous to HasProd.norm, Multipliable.norm, Multipliable.norm-tprod

## Theorem: ZetaFixedLowerBound {#ZetaFixedLowerBound lean="ZetaFixedLowerBound"}

For all $t\in\mathbb{R}$ one has
    
$$
|\zeta(3/2+it)|\geq\frac{\zeta(3)}{\zeta(3/2)}.
$$

### Proof

From the Euler product expansion of $\zeta$, we have that for $\Re s>1$
    
$$
\zeta(s)=\prod_p\frac{1}{1-p^{-s}}.
$$

    Thus, we have that
    
$$
\frac{\zeta(2s)}{\zeta(s)}=\prod_p\frac{1-p^{-s}}{1-p^{-2s}}=\prod_p\frac{1}{1+p^{-s}}.
$$

    Now note that $|1-p^{-(3/2+it)}|\leq 1+|p^{-(3/2+it)}|=1+p^{-3/2}$. Thus,
    
$$
|\zeta(3/2+it)|=\prod_p\frac{1}{|1-p^{-(3/2+it)}|}
      \geq\prod_p\frac{1}{1+p^{-3/2}}=\frac{\zeta(3)}{\zeta(3/2)}
$$

    for all $t\in\mathbb{R}$ as desired.

## Definition: riemannZeta1 {#riemannZeta1 lean="riemannZeta1"}

Let
    
$$
\zeta_1(s)=1+\frac{1}{s-1}-s\int_1^\infty\{x\}\,x^{-s}\,\frac{dx}{x}.
$$

## Theorem: Zeta1AltFormula {#Zeta1AltFormula lean="Zeta1AltFormula" uses="riemannZeta1, riemannZeta0"}

We have that
    
$$
\zeta_1(s)=\zeta_0(1,s)
$$

    where $\zeta_0(1,s)$ comes from Definition [riemannZeta0](#riemannZeta0).

### Proof

Note that
    
$$
\zeta_0(1,s)=1+\frac{-1}{1-s}+\frac{-1}{2}+s\int_1^\infty\frac{\lfloor x\rfloor+1/2-x}{x^{s+1}}\,dx.
$$

    With minor simplifications we have
    
$$
\zeta_0(1,s)=1+\frac{1}{s-1}-\frac{1}{2}+\frac{s}{2}\int_1^\infty x^{-s-1}\,dx-s\int_1^\infty\{x\}\,x^{-s-1}\,dx.
$$

    The first integral evaluates to $1/s$ (when $0<\mathfrak{R}s$), so this term when multiplied by the $s/2$ cancels with the $-1/2$. This exactly gives $\zeta_1$.

## Theorem: ZetaAltFormula {#ZetaAltFormula lean="ZetaAltFormula" uses="riemannZeta1"}

We have that
    
$$
\zeta(s)=\zeta_1(s)
$$

    for all $s\in S$ with $S=\{s\in\mathbb{C}:0<\mathfrak{R}s,\,s\neq 1\}$.

### Proof {uses="riemannZeta0, Zeta1AltFormula, Zeta0EqZeta"}

This immediately follows from Lemmas [Zeta1AltFormula](#Zeta1AltFormula) and [Zeta0EqZeta](#Zeta0EqZeta).

## Theorem: GlobalBound {#GlobalBound lean="GlobalBound"}

For all $s\in\mathbb{C}$ with $|s|\leq 1$ and $t\in\mathbb{R}$ with $|t|\geq 2$, we have that
    
$$
|\zeta(s+3/2+it)|\leq 7+2\,|t|.
$$

### Proof {uses="ZetaAltFormula, riemannZeta1"}

For the sake of clearer proof writing let $z=s+3/2+it$. Since $|s|\leq 1$ we know that
    $1/2\leq\mathfrak{R}z$; additionally, as $|t|\geq 2$, we know $1\leq|\mathfrak{I}z|$.
    So, $z\in S$. Thus, from Lemma [ZetaAltFormula](#ZetaAltFormula) we know that
    
$$
|\zeta(z)|\leq 1+\frac{1}{|z-1|}
      +|z|\cdot\left|\int_1^\infty\{x\}\,x^{-z}\,\frac{dx}{x}\right|
$$

    by applying the triangle inequality. Now note that $|z-1|\geq 1$. Likewise,
    
$$
|z|\cdot\left|\int_1^\infty\{x\}\,x^{-z}\,\frac{dx}{x}\right|
      \leq|z|\int_1^\infty|\{x\}\,x^{-z-1}|\,dx
      \leq|z|\int_1^\infty x^{-\Re z-1}\,dx=\frac{|z|}{\Re z}\leq 2\,|z|.
$$

    Thus we have that,
    
$$
|\zeta(s+3/2+it)|=|\zeta(z)|\leq 1+1+2\,|z|=2+2\,|s+3/2+it|
      \leq2+2\,|s|+3+2\,|it|\leq 7+2\,|t|.
$$

## Theorem: LogDerivZetaFinalBound {#LogDerivZetaFinalBound}

Let $t\in\mathbb{R}$ with $|t|\geq 2$ and $0 < r' < r < R' < R<1$. If
    $f(z)=\zeta(z+3/2+it)$, then for all
    $z\in\overline{\mathbb{D}_{r'}}\setminus\mathcal{K}_f(R')$ we have that
    
$$
\left|\frac{f'}{f}(z)-\sum_{\rho\in\mathcal{K}_f(r)}\frac{m_f(\rho)}{z-\rho}\right|
      \ll\left(\frac{16r^2}{(r-r')^3}+\frac{1}{(R^2/R'-R')\,\log(R/R')}\right)\log|t|.
$$

### Proof {uses="ZetaFixedLowerBound, GlobalBound, FinalBound"}

Let $g(z)=\zeta(z+3/2+it)/\zeta(3/2+it)$. Note that $g(0)=1$ and for $|z|\leq R$
    
$$
|g(z)|=\frac{|\zeta(z+3/2+it)|}{|\zeta(3/2+it)|}
      \leq\frac{\zeta(3/2)}{\zeta(3)}\cdot(7+2\,|t|)\leq\frac{13\,\zeta(3/2)}{3\,\zeta(3)}\,|t|
$$

    by Theorems [ZetaFixedLowerBound](#ZetaFixedLowerBound) and [GlobalBound](#GlobalBound). Thus by Theorem
    [FinalBound](#FinalBound) we have that
    
$$
\left|\frac{g'}{g}(z)-\sum_{\rho\in\mathcal{K}_g(r)}\frac{m_g(\rho)}{z-\rho}\right|
      \leq\left(\frac{16r^2}{(r-r')^3}+\frac{1}{(R^2/R'-R')\,\log(R/R')}\right)
      \left(\log|t|+\log\left(\frac{13\,\zeta(3/2)}{3\,\zeta(3)}\right)\right).
$$

    Now note that $f'/f=g'/g$, $\mathcal{K}_f(r)=\mathcal{K}_g(r)$, and
    $m_g(\rho)=m_f(\rho)$ for all $\rho\in\mathcal{K}_f(r)$. Thus we have that,
    
$$
\left|\frac{f'}{f}(z)-\sum_{\rho\in\mathcal{K}_f(r)}\frac{m_f(\rho)}{z-\rho}\right|
      \ll\left(\frac{16r^2}{(r-r')^3}+\frac{1}{(R^2/R'-R')\,\log(R/R')}\right)\log|t|
$$

    where the implied constant $C$ is taken to be
    
$$
C\geq 1+\frac{\log((13\,\zeta(3/2))/(3\,\zeta(3)))}{\log 2}.
$$

## Definition: ZeroWindows {#ZeroWindows}

Let $\mathcal{Z}_t=\{\rho\in\mathbb{C}:\zeta(\rho)=0,\,|\rho-(3/2+it)|\leq 3/4\}$.

## Lemma: SumBoundI {#SumBoundI}

For all $\delta\in (0,1)$ and $t\in\mathbb{R}$ with $|t|\geq 2$ we have
    
$$
\left|\frac{\zeta'}{\zeta}(1+\delta+it)
      -\sum_{\rho\in\mathcal{Z}_t}\frac{m_\zeta(\rho)}{1+\delta+it-\rho}\right|\ll\log|t|.
$$

### Proof {uses="LogDerivZetaFinalBound"}

We apply Theorem [LogDerivZetaFinalBound](#LogDerivZetaFinalBound) where $r'=2/3$, $r=3/4$, $R'=5/6$, and
    $R=8/9$. Thus, for all $z\in\overline{\mathbb{D}_{2/3}}\setminus\mathcal{K}_f(5/6)$
    we have that
    
$$
\left|\frac{\zeta'}{\zeta}(z+3/2+it)
      -\sum_{\rho\in\mathcal{K}_f(3/4)}\frac{m_f(\rho)}{z-\rho}\right|\ll\log|t|
$$

    where $f(z)=\zeta(z+3/2+it)$ for $t\in\mathbb{R}$ with $|t|\geq 2$. Now if we let
    $z=-1/2+\delta$, then $z\in(-1/2,1/2)\subseteq\overline{\mathbb{D}_{2/3}}$.
    Additionally, $f(z)=\zeta(1+\delta+it)$, where $1+\delta+it$ lies in the zero-free
    region where $\sigma>1$. Thus, $z\not\in\mathcal{K}_f(5/6)$. So,
    
$$
\left|\frac{\zeta'}{\zeta}(1+\delta+it)
      -\sum_{\rho\in\mathcal{K}_f(3/4)}\frac{m_f(\rho)}{-1/2+\delta-\rho}\right|
      \ll\log|t|.
$$

    But now note that if $\rho\in\mathcal{K}_f(3/4)$, then $\zeta(\rho+3/2+it)=0$ and
    $|\rho|\leq 3/4$. Thus, $\rho+3/2+it\in\mathcal{Z}_t$ (the argument works in reverse as well).
    Additionally, note that $m_f(\rho)=m_\zeta(\rho+3/2+it)$. So changing variables using these
    facts gives us that
    
$$
\left|\frac{\zeta'}{\zeta}(1+\delta+it)
      -\sum_{\rho\in\mathcal{Z}_t}\frac{m_\zeta(\rho)}{1+\delta+it-\rho}\right|
      \ll\log|t|.
$$

## Lemma: ShiftTwoBound {#ShiftTwoBound}

For all $\delta\in (0,1)$ and $t\in\mathbb{R}$ with $|t|\geq 2$ we have
    
$$
-\Re \left(\frac{\zeta'}{\zeta}(1+\delta+2it)\right)\ll\log|t|.
$$

### Proof {uses="SumBoundI"}

Note that, for $\rho\in\mathcal{Z}_{2t}$
    
$$
\begin{aligned}
        \Re \left(\frac{1}{1+\delta+2it-\rho}\right)
          &=\Re \left(\frac{1+\delta-2it-\overline{\rho}}
            {(1+\delta+2it-\rho)(1+\delta-2it-\overline{\rho})}\right) \\
          &=\frac{\Re (1+\delta-2it-\overline{\rho})}{|1+\delta+2it-\rho|^2}
            =\frac{1+\delta-\Re \rho}{(1+\delta-\Re \rho)^2+(2t-\mathfrak{I}\rho)^2}.
    \end{aligned}
$$

    Now since $\rho\in\mathcal{Z}_{2t}$, we have that $|\rho-(3/2+2it)|\leq 3/4$. So,
    we have $\Re \rho\in[3/4,9/4]$ and $\mathfrak{I}\rho\in[2t-3/4,2t+3/4]$. Additionally,
    we know that $\zeta(\rho)=0$. This implies the stronger condition that $\Re \rho\in[3/4,1]$.
    Thus,
    
$$
\delta\leq 1+\delta-\Re \rho\qquad\text{and}\qquad
      (1+\delta-\Re \rho)^2+(2t-\mathfrak{I}\rho)^2\leq 25/16+9/16=17/8.
$$

    Which implies that
    
$$
        0<\frac{8}{17}\,\delta
          \leq\frac{1+\delta-\Re \rho}{(1+\delta-\Re \rho)^2+(2t-\mathfrak{I}\rho)^2}
          =\Re \left(\frac{1}{1+\delta+2it-\rho}\right).
$$

    Note that, from Lemma [SumBoundI](#SumBoundI), we have
    
$$
\sum_{\rho\in\mathcal{Z}_{2t}}m_\zeta(\rho)\,
      \Re \left(\frac{1}{1+\delta+2it-\rho}\right)
      -\Re \left(\frac{\zeta'}{\zeta}(1+\delta+2it)\right)
      \leq\left|\frac{\zeta'}{\zeta}(1+\delta+2it)
      -\sum_{\rho\in\mathcal{Z}_{2t}}\frac{m_\zeta(\rho)}{1+\delta+2it-\rho}\right|
      \ll\log|2t|.
$$

    Since $m_\zeta(\rho)\geq 0$ for all $\rho\in\mathcal{Z}_{2t}$, the inequality from
    Equation ((pickupPoint4)) tells us that by subtracting the sum from both sides
    we have
    
$$
-\Re \left(\frac{\zeta'}{\zeta}(1+\delta+2it)\right)\ll\log|2t|.
$$

    Noting that $\log|2t|=\log(2)+\log|t|\leq2\log|t|$ completes the proof.

## Lemma: ShiftOneBound {#ShiftOneBound}

There exists $C>0$ such that for all $\delta\in(0,1)$ and $t\in\mathbb{R}$ with
    $|t|\geq 3$; if $\zeta(\rho)=0$ with $\rho=\sigma+it$, then
    
$$
-\Re \left(\frac{\zeta'}{\zeta}(1+\delta+it)\right)
      \leq -\frac{1}{1+\delta-\sigma}+C\log|t|.
$$

### Proof {uses="SumBoundI"}

Note that for $\rho'\in\mathcal{Z}_t$
    
$$
\begin{aligned}
        \Re \left(\frac{1}{1+\delta+it-\rho'}\right)
          &=\Re \left(\frac{1+\delta-it-\overline{\rho'}}
            {(1+\delta+it-\rho')(1+\delta-it-\overline{\rho'})}\right) \\
          &=\frac{\Re (1+\delta-it-\overline{\rho'})}{|1+\delta+it-\rho'|^2}
            =\frac{1+\delta-\Re \rho'}{(1+\delta-\Re \rho')^2+(t-\mathfrak{I}\rho')^2}.
    \end{aligned}
$$

    Now since $\rho'\in\mathcal{Z}_t$, we have that $|\rho'-(3/2+it)|\leq 3/4$. So, we
    have $\Re \rho'\in[3/4,9/4]$ and $\mathfrak{I}\rho'\in[t-3/4,t+3/4]$. Additionally, we know
    that $\zeta(\rho')=0$. This implies the stronger condition that $\Re \rho'\in[3/4,1]$. Thus,
    
$$
\delta\leq 1+\delta-\Re \rho'\qquad\text{and}\qquad
      (1+\delta-\Re \rho')^2+(t-\mathfrak{I}\rho')^2\leq 25/16+9/16=17/8.
$$

    Which implies that
    
$$
        0<\frac{8}{17}\,\delta
          \leq\frac{1+\delta-\Re \rho'}{(1+\delta-\Re \rho')^2+(t-\mathfrak{I}\rho')^2}
          =\Re \left(\frac{1}{1+\delta+it-\rho'}\right).
$$

    Note that, from Lemma [SumBoundI](#SumBoundI), we have
    
$$
\sum_{\rho'\in\mathcal{Z}_t}m_\zeta(\rho')\,
      \Re \left(\frac{1}{1+\delta+it-\rho'}\right)
      -\Re \left(\frac{\zeta'}{\zeta}(1+\delta+it)\right)
      \leq\left|\frac{\zeta'}{\zeta}(1+\delta+it)
      -\sum_{\rho'\in\mathcal{Z}_t}\frac{m_\zeta(\rho')}{1+\delta+it-\rho'}\right|
      \ll\log|t|.
$$

    Since $m_\zeta(\rho')\geq 0$ for all $\rho'\in\mathcal{Z}_t$, the inequality from
    Equation ((pickupPoint5)) tells us that by subtracting the sum over all
    $\rho'\in\mathcal{Z}_t\setminus\{\rho\}$ from both sides we have
    
$$
\frac{m_\zeta(\rho)}{\Re (1+\delta+it-\rho)}
      -\Re \left(\frac{\zeta'}{\zeta}(1+\delta+it)\right)\ll\log|t|.
$$

    But of course we have that $\Re (1+\delta+it-\rho)=1+\delta-\sigma$. So subtracting
    this term from both sides and recalling the implied constant we have
    
$$
-\Re \left(\frac{\zeta'}{\zeta}(1+\delta+it)\right)
      \leq -\frac{m_\zeta(\rho)}{1+\delta-\sigma}+C\log|t|.
$$

    We have that $\sigma\leq 1$ since $\zeta$ is zero free on the right half plane
    $\sigma>1$. Thus $0<1+\delta-\sigma$. Noting this in combination with the fact that
    $1\leq m_\zeta(\rho)$ completes the proof.

## Lemma: ShiftZeroBound {#ShiftZeroBound}

For all $\delta\in(0,1)$ we have
    
$$
-\Re \left(\frac{\zeta'}{\zeta}(1+\delta)\right)\leq\frac{1}{\delta}+O(1).
$$

### Proof {uses="riemannZetaLogDerivResidue"}

From Theorem [riemannZetaLogDerivResidue](#riemannZetaLogDerivResidue) we know that
    
$$
-\frac{\zeta'}{\zeta}(s)=\frac{1}{s-1}+O(1).
$$

    Changing variables $s\mapsto 1+\delta$ and applying the triangle inequality we have that
    
$$
-\Re \left(\frac{\zeta'}{\zeta}(1+\delta)\right)\leq\left|
      -\frac{\zeta'}{\zeta}(1+\delta)\right|\leq\frac{1}{\delta}+O(1).
$$

## Theorem: ZeroInequality {#ZeroInequality lean="ZeroInequality"}

There exists a constant $0 < E<1$ such that for all $\rho=\sigma+it$ with $\zeta(\rho)=0$
    and $|t|\geq 2$, one has
    
$$
\sigma\leq 1-\frac{E}{\log|t|}.
$$

### Proof {uses="ShiftOneBound, ShiftTwoBound, ShiftZeroBound, LogDerivativeDirichlet"}

From Theorem [LogDerivativeDirichlet](#LogDerivativeDirichlet) when $\Re s>1$ we have
    
$$
-\frac{\zeta'}{\zeta}(s)=\sum_{1\leq n}\frac{\Lambda(n)}{n^s}.
$$

    Thus,
    
$$
-3\,\frac{\zeta'}{\zeta}(1+\delta)
        -4\,\frac{\zeta'}{\zeta}(1+\delta+it)
        -\frac{\zeta'}{\zeta}(1+\delta+2it)
        =\sum_{1\leq n}\Lambda(n)\,n^{-(1+\delta)}\left(3+4n^{-it}+n^{-2it}\right).
$$

    Now applying Euler's identity
    
$$
\begin{aligned}
        -3\,\Re \left(\frac{\zeta'}{\zeta}(1+\delta)\right)&
            -4\,\Re \left(\frac{\zeta'}{\zeta}(1+\delta+it)\right)
            -\Re \left(\frac{\zeta'}{\zeta}(1+\delta+2it)\right) \\
        &\qquad\qquad\qquad=\sum_{1\leq n}\Lambda(n)\,n^{-(1+\delta)}
            \left(3+4\cos(-it\log n)+\cos(-2it\log n)\right)
    \end{aligned}
$$

    By Lemma (ThreeFourOneTrigIdentity) we know that the series on the right hand side
    is bounded below by $0$, and by Lemmas [ShiftTwoBound](#ShiftTwoBound), [ShiftOneBound](#ShiftOneBound),
    and [ShiftZeroBound](#ShiftZeroBound) we have an upper bound on the left hand side. So,
    
$$
0\leq\frac{3}{\delta}+3A-\frac{4}{1+\delta-\sigma}+4B\log|t|+C\log|t|
$$

    where $A$, $B$, and $C$ are the implied constants coming from Lemmas
    [ShiftZeroBound](#ShiftZeroBound), [ShiftOneBound](#ShiftOneBound), and [ShiftTwoBound](#ShiftTwoBound) respectively.
    By choosing $D\geq 3A/\log 2+4B+C$ we have
    
$$
\frac{4}{1+\delta-\sigma}\leq\frac{3}{\delta}+D\log|t|
$$

    by some manipulation. Now if we choose $\delta=(2D\log|t|)^{-1}$ then we have
    
$$
\frac{4}{1-\sigma+1/(2D\log|t|)}\leq7D\log|t|.
$$

    So with some manipulation we have that
    
$$
\sigma\leq 1-\frac{1}{14D\log|t|}.
$$

    This is exactly the desired result with the constant $E=(14D)^{-1}$

## Definition: DeltaT {#DeltaT lean="DeltaT" uses="ZeroInequality"}

Let $\delta_t=E/\log|t|$ where $E$ is the constant coming from Theorem [ZeroInequality](#ZeroInequality).

## Lemma: DeltaRange {#DeltaRange lean="DeltaRange" uses="DeltaT"}

For all $t\in\mathbb{R}$ with $|t|\geq 2$ we have that 
$$
\delta_t<1/14.
$$

### Proof {uses="ShiftOneBound, ZeroInequality, ShiftTwoBound, ShiftZeroBound, SumBoundI, LogDerivZetaFinalBound"}

Note that $\delta_t=E/\log|t|$ where $E$ is the implied constant from
    Lemma [ZeroInequality](#ZeroInequality). But we know that $E=(14D)^{-1}$ where $D\geq 3A/\log 2+4B+C$
    where $A$, $B$, and $C$ are the constants coming from
    Lemmas [ShiftZeroBound](#ShiftZeroBound), [ShiftOneBound](#ShiftOneBound), and [ShiftTwoBound](#ShiftTwoBound) respectively. Thus,
    
$$
E\leq\frac{1}{14\,(3A/\log 2+4B+C)}.
$$

    But note that $A\geq 0$ and $B\geq 0$ by Lemmas [ShiftZeroBound](#ShiftZeroBound) and [ShiftOneBound](#ShiftOneBound)
    respectively. However, we have that
    
$$
C\geq 2+\frac{2\log((13\,\zeta(3/2))/(3\,\zeta(3)))}{\log 2}
$$

    by Theorem [LogDerivZetaFinalBound](#LogDerivZetaFinalBound) with Lemmas [SumBoundI](#SumBoundI) and [ShiftTwoBound](#ShiftTwoBound).
    So, by a very lazy estimate we have $C\geq 2$ and $E\leq 1/28$. Thus,
    
$$
\delta_t=\frac{E}{\log|t|}\leq\frac{1}{28\,\log2}<\frac{1}{14}.
$$

## Lemma: SumBoundII {#SumBoundII}

For all $t\in\mathbb{R}$ with $|t|\geq 2$ and $z=\sigma+it$
    where $1-\delta_t/3\leq\sigma\leq 3/2$, we have that
    
$$
\left|\frac{\zeta'}{\zeta}(z)
      -\sum_{\rho\in\mathcal{Z}_t}\frac{m_\zeta(\rho)}{z-\rho}\right|\ll\log|t|.
$$

### Proof {uses="DeltaRange, LogDerivZetaFinalBound, ZeroInequality"}

By Lemma [DeltaRange](#DeltaRange) we have that
    
$$
-11/21<-1/2-\delta_t/3\leq\sigma-3/2\leq0.
$$

    We apply Theorem [LogDerivZetaFinalBound](#LogDerivZetaFinalBound) where $r'=2/3$, $r=3/4$, $R'=5/6$, and $R=8/9$.
    Thus for all $z\in\overline{\mathbb{D}_{2/3}}\setminus\mathcal{K}_f(5/6)$ we have that
    
$$
\left|\frac{\zeta'}{\zeta}(z+3/2+it)
      -\sum_{\rho\in\mathcal{K}_f(3/4)}\frac{m_f(\rho)}{z-\rho}\right|\ll\log|t|
$$

    where $f(z)=\zeta(z+3/2+it)$ for $t\in\mathbb{R}$ with $|t|\geq 2$.
    Now if we let $z=\sigma-3/2$, then $z\in(-11/21,0)\subseteq\overline{\mathbb{D}_{2/3}}$.
    Additionally, $f(z)=\zeta(\sigma+it)$, where $\sigma+it$ lies in the zero free region given by
    Lemma [ZeroInequality](#ZeroInequality) since $\sigma\geq 1-\delta_t/3\geq 1-\delta_t$.
    Thus, $z\not\in\mathcal{K}_f(5/6)$. So,
    
$$
\left|\frac{\zeta'}{\zeta}(\sigma+it)
      -\sum_{\rho\in\mathcal{K}_f(3/4)}\frac{m_f(\rho)}{\sigma-3/2-\rho}\right|\ll\log|t|.
$$

    But now note that if $\rho\in\mathcal{K}_f(3/4)$, then $\zeta(\rho+3/2+it)=0$
    and $|\rho|\leq 3/4$ (and the argument works in reverse). Additionally, note that
    $m_f(\rho)=m_\zeta(\rho+3/2+it)$. So changing variables using these facts gives us that
    
$$
\left|\frac{\zeta'}{\zeta}(\sigma+it)
      -\sum_{\rho\in\mathcal{Z}_t}\frac{m_\zeta(\rho)}{\sigma+it-\rho}\right|\ll\log|t|.
$$

## Lemma: GapSize {#GapSize}

Let $t\in\mathbb{R}$ with $|t|\geq 3$ and $z=\sigma+it$ where $1-\delta_t/3\leq\sigma\leq 3/2$.
   Additionally, let $\rho\in\mathcal{Z}_t$. Then we have that
   
$$
|z-\rho|\geq\delta_t/6.
$$

### Proof {uses="ZeroInequality"}

Let $\rho=\sigma'+it'$ and note that since $\rho\in\mathcal{Z}_t$, we have $t'\in(t-3/4,t+3/4)$.
    Thus, if $t>1$ we have
    
$$
\log|t'|\leq\log|t+3/4|\leq\log|2t|=\log 2+\log|t|\leq 2\log|t|.
$$

    And otherwise if $t<-1$ we have
    
$$
\log|t'|\leq\log|t-3/4|\leq\log|2t|=\log 2+\log|t|\leq 2\log|t|.
$$

    So by taking reciprocals and multiplying through by a constant we have
    that $\delta_t\leq2\delta_{t'}$. Now note that since $\rho\in\mathcal{Z}_t$
    we know that $\sigma'\leq 1-\delta_{t'}$ by Theorem [ZeroInequality](#ZeroInequality)
    (here we use the fact that $|t|\geq 3$ to give us that $|t'|\geq 2$). Thus,
    
$$
\delta_t/6\leq\delta_{t'}-\delta_t/3
      =1-\delta_t/3-(1-\delta_{t'})\leq\sigma-\sigma'\leq|z-\rho|.
$$

## Lemma: LogDerivZetaUniformLogSquaredBoundStrip {#LogDerivZetaUniformLogSquaredBoundStrip lean="LogDerivZetaUniformLogSquaredBoundStrip" uses="ZeroInequality"}

There exists a constant $F\in(0,1/2)$ such that
    for all $t\in\mathbb{R}$ with $|t|\geq 3$ one has
    
$$
1-\frac{F}{\log|t|}\leq\sigma\leq 3/2
      \implies\left|\frac{\zeta'}{\zeta}(\sigma+it)\right|\ll\log^2|t|
$$

    where the implied constant is uniform in $\sigma$.

### Proof {uses="ZeroInequality, ZerosBound, GlobalBound, ZetaFixedLowerBound, SumBoundII, GapSize"}

Take $F=E/3$ where $E$ comes from Theorem [ZeroInequality](#ZeroInequality).
    Then we have that $\sigma\geq 1-\delta_t/3$. So, we apply Lemma [SumBoundII](#SumBoundII),
    which gives us that
    
$$
\left|\frac{\zeta'}{\zeta}(z)
      -\sum_{\rho\in\mathcal{Z}_t}\frac{m_\zeta(\rho)}{z-\rho}\right|\ll\log|t|.
$$

    Using the reverse triangle inequality and rearranging, we have that
    
$$
\left|\frac{\zeta'}{\zeta}(z)\right|
      \leq\sum_{\rho\in\mathcal{Z}_t}\frac{m_\zeta(\rho)}{|z-\rho|}+C\,\log|t|
$$

    where $C$ is the implied constant in Lemma [SumBoundII](#SumBoundII).
    Now applying Lemma [GapSize](#GapSize) we have that
    
$$
\left|\frac{\zeta'}{\zeta}(z)\right|
      \leq\frac{6}{\delta_t}\sum_{\rho\in\mathcal{Z}_t}m_\zeta(\rho)+C\,\log|t|.
$$

    Now let $f(z)=\zeta(z+3/2+it)/\zeta(3/2+it)$ with $\rho=\rho'+3/2+it$.
    Then if $\rho\in\mathcal{Z}_t$ we have that
    
$$
0=\zeta(\rho)=\zeta(\rho'+3/2+it)=f(\rho')
$$

    with the same multiplicity of zero, that is $m_\zeta(\rho)=m_f(\rho')$.
    And also if $\rho\in\mathcal{Z}_t$ then
    
$$
3/4\geq|\rho-(3/2+it)|=|\rho'|.
$$

    Thus we change variables to have that
    
$$
\left|\frac{\zeta'}{\zeta}(z)\right|
      \leq\frac{6}{\delta_t}\sum_{\rho'\in\mathcal{K}_f(3/4)}m_f(\rho')+C\,\log|t|.
$$

    Now note that $f(0)=1$ and for $|z|\leq 8/9$ we have
    
$$
|f(z)|=\frac{|\zeta(z+3/2+it)|}{|\zeta(3/2+it)|}
      \leq\frac{\zeta(3/2)}{\zeta(3)}\cdot(7+2\,|t|)\leq\frac{13\,\zeta(3/2)}{3\,\zeta(3)}\,|t|
$$

    by Theorems [ZetaFixedLowerBound](#ZetaFixedLowerBound) and [GlobalBound](#GlobalBound).
    Thus by Theorem [ZerosBound](#ZerosBound) we have that
    
$$
\sum_{\rho'\in\mathcal{K}_f(3/4)}m_f(\rho')
      \leq\frac{\log|t|+\log(13\,\zeta(3/2)/(3\,\zeta(3)))}{\log((8/9)/(3/4))}\leq D\log|t|
$$

    where $D$ is taken to be sufficiently large.
    Recall, by definition that, $\delta_t=E/\log|t|$ with $E$ coming from
    Theorem [ZeroInequality](#ZeroInequality). By using this fact and the above, we have that
    
$$
\left|\frac{\zeta'}{\zeta}(z)\right|\ll\log^2|t|+\log|t|
$$

    where the implied constant is taken to be bigger than $\max(6D/E,C)$.
    We know that the RHS is bounded above by $\ll\log^2|t|$; so the result follows.

## Theorem: LogDerivZetaUniformLogSquaredBound {#LogDerivZetaUniformLogSquaredBound lean="LogDerivZetaUniformLogSquaredBound" uses="LogDerivZetaUniformLogSquaredBoundStrip, ZeroInequality"}

There exists a constant $F\in(0,1/2)$ such that for all $t\in\mathbb{R}$ with $|t|\geq 3$ one has
    
$$
1-\frac{F}{\log|t|}\leq\sigma\implies\left|\frac{\zeta'}{\zeta}(\sigma+it)\right|\ll\log^2|t|
$$

    where the implied constant is uniform in $\sigma$.

### Proof {uses="LogDerivZetaUniformLogSquaredBoundStrip, riemannZetaLogDerivResidue, LogDerivativeDirichlet"}

Note that
    
$$
\left|\frac{\zeta'}{\zeta}(\sigma+it)\right|
      =\sum_{1\leq n}\frac{\Lambda(n)}{|n^{\sigma+it}|}=\sum_{1\leq n}\frac{\Lambda(n)}{n^\sigma}
      =-\frac{\zeta'}{\zeta}(\sigma)\leq\left|\frac{\zeta'}{\zeta}(\sigma)\right|.
$$

    From Theorem [riemannZetaLogDerivResidue](#riemannZetaLogDerivResidue), and applying the triangle inequality we know that
    
$$
\left|\frac{\zeta'}{\zeta}(s)\right|\leq\frac{1}{|s-1|}+C.
$$

    where $C>0$ is some constant. Thus, for $\sigma\geq 3/2$ we have that
    
$$
\left|\frac{\zeta'}{\zeta}(\sigma+it)\right|
      \leq\left|\frac{\zeta'}{\zeta}(\sigma)\right|
      \leq\frac{1}{\sigma-1}+C\leq 2+C\ll 1\ll\log^2|t|.
$$

    Putting this together with Lemma [LogDerivZetaUniformLogSquaredBoundStrip](#LogDerivZetaUniformLogSquaredBoundStrip)
    completes the proof.

## Theorem: LogDerivZetaLogSquaredBoundSmallt {#LogDerivZetaLogSquaredBoundSmallt lean="LogDerivZetaLogSquaredBoundSmallt" uses="LogDerivZetaUniformLogSquaredBoundStrip, ZeroInequality"}

For $T>0$ and $\sigma'=1-\delta_T/3=1-F/\log T$, if $|t|\leq T$ then we have that
    
$$
\left|\frac{\zeta'}{\zeta}(\sigma'+it)\right|\ll\log^2(2+T).
$$

### Proof {uses="LogDerivZetaUniformLogSquaredBound, riemannZetaLogDerivResidue"}

Note that if $|t|\geq 3$ then from Theorem [LogDerivZetaUniformLogSquaredBound](#LogDerivZetaUniformLogSquaredBound) we have that
    
$$
\left|\frac{\zeta'}{\zeta}(\sigma'+it)\right|\ll\log^2|t|\leq\log^2T\leq\log^2(2+T).
$$

    Otherwise, if $|t|\leq 3$, then from Theorem [riemannZetaLogDerivResidue](#riemannZetaLogDerivResidue)
    and applying the triangle inequality we know
    
$$
\left|\frac{\zeta'}{\zeta}(\sigma'+it)\right|
      \leq\frac{1}{|(\sigma'-1)+it|}+C\leq\frac{\log T}{F}+C
$$

    where $C\geq 0$. Thus, we have that
    
$$
\left|\frac{\zeta'}{\zeta}(\sigma'+it)\right|
      \leq\left(\frac{\log T}{F\,\log 2}+\frac{C}{\log 2}\right)\,\log(2+|t|)
      \leq\left(\frac{\log(2+T)}{F\,\log 2}+\frac{C}{\log 2}\right)\log(2+T)
      \ll\log^2(2+T).
$$

From here out we closely follow our previous proof of the Medium PNT and we modify it
using our new estimate in Theorem [LogDerivZetaUniformLogSquaredBound](#LogDerivZetaUniformLogSquaredBound).
Recall Definition [SmoothedChebyshev](#SmoothedChebyshev); for fixed $\varepsilon>0$
and a bump function $\nu$ supported on $[1/2,2]$ we have

$$
\psi_\varepsilon(X)
  =\frac{1}{2\pi i}\int_{(\sigma)}\left(-\frac{\zeta'}{\zeta}(s)\right)
  \,\mathcal{M}(\tilde{1}_\varepsilon)(s)\,X^s\,ds
$$

where $\sigma=1+1/\log X$. Let $T>3$ be a large constant to be chosen later,
and we take $\sigma'=1-\delta_T/3=1-F/\log T$ with $F$ coming from
Theorem [LogDerivZetaUniformLogSquaredBound](#LogDerivZetaUniformLogSquaredBound). We integrate along the $\sigma$ vertical line,
and we pull contours  accumulating the pole at $s=1$ when we integrate along the curves

- $I_1$: $\sigma-i\infty$ to $\sigma-iT$
- $I_2$: $\sigma'-iT$ to $\sigma-iT$
- $I_3$: $\sigma'-iT$ to $\sigma'+iT$
- $I_4$: $\sigma'+iT$ to $\sigma+iT$
- $I_5$: $\sigma+iT$ to $\sigma+i\infty$.

## Definition: I1New {#I1New lean="I1New" uses="Smooth1"}

Let
    
$$
I_1(\nu,\varepsilon,X,T)=
      \frac{1}{2\pi i}\int_{-\infty}^{-T}\left(-\frac{\zeta'}{\zeta}(\sigma+it)\right)
      \,\mathcal{M}(\tilde{1}_\varepsilon)(\sigma+it)\,X^{\sigma+it}\,dt.
$$

## Definition: I5New {#I5New lean="I5New" uses="Smooth1"}

Let
    
$$
I_5(\nu,\varepsilon,X,T)=
      \frac{1}{2\pi i}\int_T^\infty\left(-\frac{\zeta'}{\zeta}(\sigma+it)\right)
      \,\mathcal{M}(\tilde{1}_\varepsilon)(\sigma+it)\,X^{\sigma+it}\,dt.
$$

## Lemma: I1NewBound {#I1NewBound lean="I1NewBound" uses="I1New"}

We have that
    
$$
|I_1(\nu,\varepsilon,X,T)|\ll\frac{X}{\varepsilon\sqrt{T}}.
$$

### Proof {uses="LogDerivZetaUniformLogSquaredBound, LogDerivZetaUniformLogSquaredBoundStrip, ZeroInequality, Smooth1, MellinOfSmooth1b"}

Note that $|I_1(\nu,\varepsilon,X,T)|=$
    
$$
\left|\frac{1}{2\pi i}\int_{-\infty}^{-T}\left(-\frac{\zeta'}{\zeta}(\sigma+it)\right)
      \,\mathcal{M}(\tilde{1}_\varepsilon)(\sigma+it)\,X^{\sigma+it}\,dt\right|
      \ll\int_{-\infty}^{-T}\left|\frac{\zeta'}{\zeta}(\sigma+it)\right|
      \cdot|\mathcal{M}(\tilde{1}_\varepsilon)(\sigma+it)|\cdot X^\sigma\,dt.
$$

    Applying Theorem [LogDerivZetaUniformLogSquaredBound](#LogDerivZetaUniformLogSquaredBound) and Lemma [MellinOfSmooth1b](#MellinOfSmooth1b),
    we have that
    
$$
|I_1(\nu,\varepsilon,X,T)|
      \ll\int_{-\infty}^{-T}\log^2|t|\cdot\frac{X^\sigma}{\varepsilon\,|\sigma+it|^2}\,dt
      \ll\frac{X}{\varepsilon}\int_T^\infty\frac{\sqrt{t}\,dt}{t^2}
      \ll\frac{X}{\varepsilon\sqrt{T}}.
$$

    Here we are using the fact that $\log^2 t$ grows slower than $\sqrt{t}$,
    $|\sigma+it|^2\geq t^2$, and $X^\sigma=X\cdot X^{1/\log X}=eX$.

## Lemma: I5NewBound {#I5NewBound lean="I5NewBound" uses="I5New"}

We have that
    
$$
|I_5(\nu,\varepsilon,X,T)|\ll\frac{X}{\varepsilon\sqrt{T}}.
$$

### Proof {uses="Smooth1, deriv_riemannZeta_conj, I1NewBound, I1New"}

By symmetry, note that
    
$$
|I_1(\nu,\varepsilon,X,T)|=|\overline{I_5(\nu,\varepsilon,X,T)}|=|I_5(\nu,\varepsilon,X,T)|.
$$

    Applying Lemma [I1NewBound](#I1NewBound) completes the proof.

## Definition: I2New {#I2New lean="I2New" uses="Smooth1"}

Let
    
$$
I_2(\nu,\varepsilon,X,T)
      =\frac{1}{2\pi i}\int_{\sigma'}^\sigma\left(-\frac{\zeta'}{\zeta}(\sigma_0-iT)\right)
      \,\mathcal{M}(\tilde{1}_\varepsilon)(\sigma_0-iT)\,X^{\sigma_0-iT}\,d\sigma_0.
$$

## Definition: I4New {#I4New lean="I4New" uses="Smooth1"}

Let
    
$$
I_4(\nu,\varepsilon,X,T)
    =\frac{1}{2\pi i}\int_{\sigma'}^\sigma\left(-\frac{\zeta'}{\zeta}(\sigma_0+iT)\right)
    \,\mathcal{M}(\tilde{1}_\varepsilon)(\sigma_0+iT)\,X^{\sigma_0+iT}\,d\sigma_0.
$$

## Lemma: I2NewBound {#I2NewBound lean="I2NewBound" uses="LogDerivZetaUniformLogSquaredBoundStrip, ZeroInequality, I2New"}

We have that
    
$$
|I_2(\nu,\varepsilon,X,T)|\ll\frac{X}{\varepsilon\sqrt{T}}.
$$

### Proof {uses="LogDerivZetaUniformLogSquaredBound, MellinOfSmooth1b"}

Note that $|I_2(\nu,\varepsilon,X,T)|=$
    
$$
\left|\frac{1}{2\pi i}\int_{\sigma'}^\sigma\left(-\frac{\zeta'}{\zeta}(\sigma_0-iT)\right)
      \,\mathcal{M}(\tilde{1}_\varepsilon)(\sigma_0-iT)\,X^{\sigma_0-iT}\,d\sigma_0\right|
      \ll\int_{\sigma'}^\sigma\left|\frac{\zeta'}{\zeta}(\sigma_0-iT)\right|
      \cdot|\mathcal{M}(\tilde{1}_\varepsilon)(\sigma_0-iT)|\cdot X^{\sigma_0}\,d\sigma_0.
$$

    Applying Theorem [LogDerivZetaUniformLogSquaredBound](#LogDerivZetaUniformLogSquaredBound) and Lemma [MellinOfSmooth1b](#MellinOfSmooth1b),
    we have that
    
$$
|I_2(\nu,\varepsilon,X,T)|\ll\int_{\sigma'}^\sigma\log^2 T
      \cdot\frac{X^{\sigma_0}}{\varepsilon\,|\sigma_0-iT|^2}\,d\sigma_0
      \ll\frac{X\,\log^2T}{\varepsilon\,T^2}\int_{\sigma'}^\sigma d\,\sigma_0
      =\frac{X\,\log^2T}{\varepsilon\,T^2}\,(\sigma-\sigma').
$$

    Here we are using the fact that $X^{\sigma_0}\leq X^\sigma=X\cdot X^{1/\log X}=eX$
    and $|\sigma_0-iT|^2\geq T^2$. Now note that
    
$$
|I_2(\nu,\varepsilon,X,T)|\ll\frac{X\,\log^2T}{\varepsilon\,T^2}\,(\sigma-\sigma')
      =\frac{X\,\log^2T}{\varepsilon\,T^2\,\log X}+\frac{FX\,\log T}{\varepsilon\,T^2}
      \ll\frac{X}{\varepsilon\sqrt{T}}.
$$

    Here we are using the fact that $\log T\ll T^{3/2}$, $\log^2T\ll T^{3/2}$, and $X/\log X\ll X$.

## Lemma: I4NewBound {#I4NewBound lean="I4NewBound" uses="LogDerivZetaUniformLogSquaredBoundStrip, ZeroInequality, I4New"}

We have that
    
$$
|I_4(\nu,\varepsilon,X,T)|\ll\frac{X}{\varepsilon\sqrt{T}}.
$$

### Proof {uses="I2NewBound, I2New, Smooth1, intervalIntegral_conj, deriv_riemannZeta_conj"}

By symmetry, note that
    
$$
|I_2(\nu,\varepsilon,X,T)|=|\overline{I_4(\nu,\varepsilon,X,T)}|=|I_4(\nu,\varepsilon,X,T)|.
$$

    Applying Lemma [I2NewBound](#I2NewBound) completes the proof.

## Definition: I3New {#I3New lean="I3New" uses="Smooth1"}

Let
    
$$
I_3(\nu,\varepsilon,X,T)
      =\frac{1}{2\pi i}\int_{-T}^T\left(-\frac{\zeta'}{\zeta}(\sigma'+it)\right)
      \,\mathcal{M}(\tilde{1}_\varepsilon)(\sigma'+it)\,X^{\sigma'+it}\,dt.
$$

## Lemma: I3NewBound {#I3NewBound lean="I3NewBound" uses="LogDerivZetaUniformLogSquaredBoundStrip, ZeroInequality, I3New"}

We have that
    
$$
|I_3(\nu,\varepsilon,X,T)|\ll\frac{X^{1-F/\log T}\sqrt{T}}{\varepsilon}.
$$

### Proof {uses="LogDerivZetaLogSquaredBoundSmallt, DeltaRange, MellinOfSmooth1b"}

Note that $|I_3(\nu,\varepsilon,X,T)|=$
    
$$
\left|\frac{1}{2\pi i}\int_{-T}^T\left(-\frac{\zeta'}{\zeta}(\sigma'+it)\right)
      \,\mathcal{M}(\tilde{1}_\varepsilon)(\sigma'+it)\,X^{\sigma'+it}\,dt\right|
      \ll\int_{-T}^T\left|\frac{\zeta'}{\zeta}(\sigma'+it)\right|
      \cdot|\mathcal{M}(\tilde{1}_\varepsilon)(\sigma'+it)|\cdot X^{\sigma'}\,dt.
$$

    Applying Theorem [LogDerivZetaLogSquaredBoundSmallt](#LogDerivZetaLogSquaredBoundSmallt) and Lemma [MellinOfSmooth1b](#MellinOfSmooth1b),
    we have that
    
$$
|I_3(\nu,\varepsilon,X,T)|\ll\int_{-T}^T\log^2(2+T)
      \cdot\frac{X^{\sigma'}}{\varepsilon\,|\sigma'+it|^2}\,dt
      \ll\frac{X^{1-F/\log T}\,\sqrt{T}}{\varepsilon}\int_0^T\frac{dt}{|\sigma'+it|^2}.
$$

    Here we are using the fact that this integrand is symmetric in $t$ about $0$
    and that $\log^2(2+T)\ll\sqrt{T}$ for sufficiently large $T$. Now note that,
    by Lemma [DeltaRange](#DeltaRange), we have
    
$$
\frac{1}{|\sigma'+it|^2}=\frac{1}{(1-\delta_T/3)^2+t^2}<\frac{1}{(41/42)^2+t^2}.
$$

    Thus,
    
$$
|I_3(\nu,\varepsilon,X,T)|
      \ll\frac{X^{1-F/\log T}\sqrt{T}}{\varepsilon}\int_0^T\frac{dt}{|\sigma'+it|^2}
      \leq\frac{X^{1-F/\log T}\sqrt{T}}{\varepsilon}\int_0^\infty\frac{dt}{(41/42)^2+t^2}.
$$

    The integral on the right hand side evaluates to $21\pi/41$, which is just a constant,
    so the desired result follows.

## Theorem: SmoothedChebyshevPull3 {#SmoothedChebyshevPull3 lean="SmoothedChebyshevPull3" uses="I4New, I3New, SmoothedChebyshev, I2New, Smooth1, I1New, I5New"}

We have that
    
$$
\psi_\varepsilon(X)=\mathcal{M}(\tilde{1}_\varepsilon)(1)\,X^1+I_1-I_2+I_3+I_4+I_5.
$$

### Proof {uses="Smooth1Nonneg, ResidueMult, SmoothedChebyshevPull1_aux_integrable, ResidueTheoremOnRectangleWithSimplePole, BddAbove_to_IsBigO, riemannZetaLogDerivResidue, Smooth1Properties_above, existsDifferentiableOn_of_bddAbove, Smooth1ContinuousAt, Smooth1LeOne, RectangleIntegral, VerticalIntegral"}

Pull contours and accumulate the pole of $\zeta'/\zeta$ at $s=1$.

## Theorem: StrongPNT {#StrongPNT}

We have
    
$$
\sum_{n\leq x}\Lambda(n)=x+O\left(x\exp(-c\sqrt{\log x})\right).
$$

### Proof {uses="SmoothedChebyshevClose, SmoothedChebyshevPull3, MellinOfSmooth1c, I1NewBound, I2NewBound, I3NewBound, I4NewBound, I5NewBound"}

By Theorem [SmoothedChebyshevClose](#SmoothedChebyshevClose) and [SmoothedChebyshevPull3](#SmoothedChebyshevPull3) we have that
    
$$
\mathcal{M}(\tilde{1}_\varepsilon)(1)\,x^1+I_1-I_2+I_3+I_4+I_5
      =\psi(x)+O(\varepsilon x\log x).
$$

    Applying Theorem [MellinOfSmooth1c](#MellinOfSmooth1c) and Lemmas [I1NewBound](#I1NewBound), [I2NewBound](#I2NewBound),
    [I3NewBound](#I3NewBound), [I4NewBound](#I4NewBound), and [I5NewBound](#I5NewBound) we have that
    
$$
\psi(x)=x+O(\varepsilon x)+O(\varepsilon x\log x)
      +O\left(\frac{x}{\varepsilon\sqrt{T}}\right)
      +O\left(\frac{x^{1-F/\log T}\sqrt{T}}{\varepsilon}\right).
$$

    We absorb the $O(\varepsilon x)$ term into the $O(\varepsilon x\log x)$ term and
    balance the last two terms in $T$.
    
$$
\frac{x}{\varepsilon\sqrt{T}}
      =\frac{x^{1-F/\log T}\sqrt{T}}{\varepsilon}\implies T
      =\exp(\sqrt{F\log x}).
$$

    Thus,
    
$$
\psi(x)=x+O(\varepsilon x\log x)
      +O\left(\frac{x}{\displaystyle\varepsilon\exp((1/2)\cdot\sqrt{F\log x})}\right).
$$

    Now we balance the last two terms in $\varepsilon$.
    
$$
\varepsilon x\log x
      =\frac{x}{\displaystyle\varepsilon\exp((1/2)\cdot\sqrt{F\log x})}
      \implies\varepsilon\log x
      =\frac{\displaystyle\sqrt{\log x}}{\displaystyle\exp((1/4)\cdot\sqrt{F\log x})}.
$$

    Thus,
    
$$
\psi(x)=x+O\left(x\exp(-(\sqrt{F}/4)\cdot\sqrt{\log x})\sqrt{\log x}\right).
$$

    Absorbing the $\displaystyle\sqrt{\log x}$ into the
    $\displaystyle\exp(-(\sqrt{F}/4)\cdot\sqrt{\log x})$ completes the proof.

