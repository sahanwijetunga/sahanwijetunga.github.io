---
layout: archive
title: "Formalization"
permalink: /formalization/
author_profile: true
---

VERSEIM (Tufts) REU Summer 2025
======
I participated in an REU at Tufts in Summer 2025, under [Dr. George Mcninch](https://gmcninch.math.tufts.edu/). See also [his page](https://gmcninch.math.tufts.edu/posts/2025-07--formalization-REU.html) on the REU, and the [general REU website](https://sites.tufts.edu/verseimreu/). 

Most of our work is contained in [this GitHub repository](https://github.com/gmcninch-tufts/VERSEIM-2025). See the repo for more info and our full results as a group. 

In the first few weeks George taught us the basics of Lean 4 through [Mathematics in Lean](https://leanprover-community.github.io/mathematics_in_lean/index.html) and [additional content](https://github.com/gmcninch-tufts/VERSEIM-2025/tree/main/VERSEIM2025/Introduction) he created. 

Afterwards I went through some of [Theorem Proving in Lean](https://lean-lang.org/theorem_proving_in_lean4/), and then constructed the Gram-Schmidt algorithm in Lean. This is already in mathlib (see [Mathlib.Analysis.InnerProductSpace.GramSchmidtOrtho](https://leanprover-community.github.io/mathlib4_docs/Mathlib/Analysis/InnerProductSpace/GramSchmidtOrtho.html)) implemented using [Inner Product Spaces](https://leanprover-community.github.io/mathlib4_docs/Mathlib/Analysis/InnerProductSpace/Defs.html#InnerProductSpace), whereas my results use [Bilinear Forms](https://leanprover-community.github.io/mathlib4_docs/Mathlib/LinearAlgebra/BilinearMap.html#LinearMap.BilinForm) with added predicates. It was useful to read their implementation of things after I did mine, though I don't intend to add mine to mathlib. 

George implemented some stuff over bilinear forms [here](https://github.com/gmcninch-tufts/VERSEIM-2025/blob/main/VERSEIM2025/Forms/Bilinear.lean), and I generalized [isCompl_orthogonal_of_restrict_nondegenerate](https://leanprover-community.github.io/mathlib4_docs/Mathlib/LinearAlgebra/BilinearForm/Orthogonal.html#LinearMap.BilinForm.isCompl_orthogonal_of_restrict_nondegenerate) to drop the reflexitivity requirement. There's some other definitions and results in the file and [Isometries](https://github.com/gmcninch-tufts/VERSEIM-2025/blob/main/VERSEIM2025/Forms/Isometries.lean) which make things convenient to state elsewhere in the REU project. 

I implemented definitions for Hyperbolic Spaces, namely vector spaces \\(V\\) equipped with a bilinear form \\(B\\) that is a direct sum of Hyperbolic 2-spaces, those with a basis \\((e,f)\\) with \\(B(e,e)=B(f,f)=0\\) and \\(B(e,f)=1\\) (\\(B(f,e)\\) is left unspecified, however if the form is alternating or symmetric the value is forced). 

The (immediate) relevance of this is that any nondegenerate finite dimensional alternating form is hyperbolic, which lets us prove that any two finite dimensional alternating forms of equal dimension are isomorphic and that any nondegenerate symmmetric form is the direct sum of an anisotropic (definite) part and a hyperbolic part (yielding a corresponding isomorphism result for algebraically closed fields). This is implemented in the respective files under [Hyperbolic](https://github.com/gmcninch-tufts/VERSEIM-2025/tree/main/VERSEIM2025/Forms/Hyperbolic). 

At the suggestion of George, I next formalized Cassels-Pfister Theorem (see Theorem 17.3 of [The Algebraic and Geometric Theory
of Quadratic Forms](https://www.math.ucla.edu/~merkurev/Book/Kniga-final/Kniga.pdf)), namely that the values taken by the extension of a quadratic map \\(φ: V → F\\) to \\(V(X) → F(X)\\) that are in \\(F[X]\\) are taken by the extension \\(V[X] → F[X]\\) as well. This used the following notable tools: 
  * Compatibility of \\(V[X]\\) and \\(V(X)\\), viewed as extension by scalars of \\(V\\) by \\(F[X]\\) and \\(F(X)\\), and extending quadratic forms by scalars (mostly done in mathlib, abusing bilinear forms, which forces a requirement of characteristic not 2)
  * An \\(F[X]\\)-linear isomorphism between \\(V[X]\\) viewed as extension by scalars and as formal polynomials with coefficients in \\(V\\), implemented by George [here](https://github.com/gmcninch-tufts/VERSEIM-2025/blob/main/VERSEIM2025/Forms/RationalFunctionFields/PolynomialModule.lean)
  * Definition and results for degree over \\(V[X]\\), done [here](https://github.com/gmcninch-tufts/VERSEIM-2025/tree/main/VERSEIM2025/PolynomialModuleDegree). This is already defined in mathlib for rings but not for modules. 
  * Compatibility of degree over \\(V[X]\\) and \\(F[X]\\) when extending quadratic forms by scalars, done [here](https://github.com/gmcninch-tufts/VERSEIM-2025/blob/main/VERSEIM2025/Forms/RationalFunctionFields/Basics.lean)
  * Quotienting a quadratic form to achieve a regular one, done [here](https://github.com/gmcninch-tufts/VERSEIM-2025/blob/main/VERSEIM2025/Forms/QuadraticNondegenerate.lean)

The actual theorem is proved [here](https://github.com/gmcninch-tufts/VERSEIM-2025/blob/main/VERSEIM2025/Forms/RationalFunctionFields/CasselsPfister.lean). A nice immediate corollary is that a sum of \\(n\\) squares in \\(F(X)\\) which lies in \\(F[X]\\) is also a sum of \\(n\\) squares in \\(F[X]\\), implemented [here](https://github.com/gmcninch-tufts/VERSEIM-2025/blob/main/VERSEIM2025/Forms/RationalFunctionFields/Results.lean). 

We will likely clean up some of the results which aren't in mathlib already, and work on adding them to mathlib in a separate repository. 

Fun note: I did submit one minor documentation change to mathlib during the REU, [which did get merged](https://github.com/leanprover-community/mathlib4/commit/f348f3598ef381bfe6410ad8f5ac3e4a01614e83). 