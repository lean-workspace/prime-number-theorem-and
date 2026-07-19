---
title: "PNT+ blueprint"
description: "Companion blueprint for AlexKontorovich/PrimeNumberTheoremAnd — the Prime Number Theorem and explicit analytic number theory in Lean, statuses computed from the kernel."
type: "blueprint-index"
tags:
  - "blueprint"
---

Companion blueprint for
[AlexKontorovich/PrimeNumberTheoremAnd](https://github.com/AlexKontorovich/PrimeNumberTheoremAnd),
the ongoing Lean 4 formalization of the **Prime Number Theorem** (with
classical error term) and its extensions — three proof approaches
(Wiener-Ikehara, Perron-formula, and Hadamard-factorization routes),
elementary corollaries, and the Integrated Explicit Analytic Number Theory
network's explicit-estimates program (Rosser-Schoenfeld, Chebyshev bounds,
Bombieri-Vinogradov, and more).

The mathematics is the work of the upstream project's
[contributors](https://github.com/AlexKontorovich/PrimeNumberTheoremAnd/graphs/contributors),
organized by Alex Kontorovich. The prose here is converted from the
upstream blueprint sources (Apache-2.0); the license is carried in
`UPSTREAM-LICENSE.txt`.

Upstream authors its formal statements next to the Lean code as
[LeanArchitect](https://github.com/hanwenzhu/LeanArchitect) `@[blueprint]`
attributes; this migration ran that generation (`lake build
PrimeNumberTheoremAnd:blueprint`) and inlined the generated nodes — 48
`\inputleanmodule` expansions across 194 module tables — so the chapters
here carry the same statements as the published blueprint. Statuses,
dependency edges, and source snippets are recomputed from the compiled
environment on every sync — nothing here is hand-maintained:

```bash
lake exe cache get                       # prebuilt mathlib
lake build +PrimeNumberTheoremAnd        # compile the pinned upstream library
npm run blueprint:sync                   # extract kernel truth + regenerate the canvas
```

The original leanblueprint site remains at
[alexkontorovich.github.io/PrimeNumberTheoremAnd/blueprint](https://alexkontorovich.github.io/PrimeNumberTheoremAnd/blueprint/).
This mirror currently scopes to the core Prime Number Theorem arc —
chapters 1-6 (246 items): definitions, the three proof approaches
(Wiener-Ikehara, Perron-formula contour route, Hadamard factorization),
and the elementary corollaries. The upstream explicit-estimates program
(chapters 7-13, ~570 more items) is converted and staged, to be enabled
in a later pass — the full blueprint is the largest in the ecosystem.
