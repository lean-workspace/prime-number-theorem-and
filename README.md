# PrimeNumberTheoremAnd — Lean Workspace

Interactive blueprint companion for
[AlexKontorovich/PrimeNumberTheoremAnd](https://github.com/AlexKontorovich/PrimeNumberTheoremAnd),
the ongoing Lean 4 formalization of the Prime Number Theorem (with classical
error term) and its extensions — primes in arithmetic progressions, and
onward toward Chebotarev density. The upstream blueprint chapters render
here as native chapters whose statuses, dependency edges, and source
snippets are recomputed from the compiled library — nothing is
hand-maintained.

```bash
lake exe cache get                       # prebuilt mathlib
lake build +PrimeNumberTheoremAnd        # compile the pinned upstream library
npm install && npm run dev               # site at http://localhost:8080
npm run blueprint:sync                   # refresh kernel statuses after Lean changes
```

## Attribution

The mathematics here is the work of the
[PrimeNumberTheoremAnd](https://github.com/AlexKontorovich/PrimeNumberTheoremAnd)
project — **"Prime Number Theorem And ..."** — by the upstream project's
[contributors](https://github.com/AlexKontorovich/PrimeNumberTheoremAnd/graphs/contributors),
organized by Alex Kontorovich.

The blueprint prose is converted from the upstream blueprint sources (the
narrative `blueprint.tex` plus statement nodes the upstream authors write
next to the Lean code as LeanArchitect `@[blueprint]` attributes), and the
Lean code is consumed as a pinned Lake dependency, both under the upstream
Apache-2.0 license (`UPSTREAM-LICENSE.txt`). The original leanblueprint
site: [alexkontorovich.github.io/PrimeNumberTheoremAnd/blueprint](https://alexkontorovich.github.io/PrimeNumberTheoremAnd/blueprint/).
This repository is a downstream mirror for the Lean Workspace toolchain,
not the upstream project.
