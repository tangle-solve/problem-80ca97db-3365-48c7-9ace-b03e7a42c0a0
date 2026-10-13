<!-- solve-problem:80ca97db-3365-48c7-9ace-b03e7a42c0a0 -->
# Deterministic PIT for general noncommutative circuits

A [Tangle Solve problem](https://solve.tangle.tools/problems/80ca97db-3365-48c7-9ace-b03e7a42c0a0).

## What is the problem?

A **noncommutative arithmetic circuit** over a field F computes a polynomial in the free algebra F⟨x₁,…,xₙ⟩, where variables do not commute: xy ≠ yx. The circuit has + and × gates; a × gate multiplies its inputs in a specified left/right order. A circuit C computes the zero polynomial iff it vanishes as a formal element of the free algebra (equivalently, under all substitutions of matrices over F of unbounded dimension — Amitsur–Levitzki-type considerations make the formal and matrix notions agree).

**Problem:** Given a noncommutative circuit C of size s and syntactic degree at most poly(s), decide deterministically in poly(s) time whether C computes the zero polynomial.

Precise interpretation of "general circuit": a DAG with sharing — subcomputations feed multiple gates. This is the crux: formulas (trees) and branching programs have known deterministic poly-time PIT (Raz–Shpilka), but the sharing/overlap in circuits defeats all known techniques. "Syntactic degree bounded" means the degree of the polynomial computed at every gate is polynomially bounded; this avoids trivial obstructions from exponentially large degree, since a circuit of size s can compute polynomials of degree 2^s. Note the commutative analogue is itself open for general circuits; the noncommutative version is in some ways *easier* (rigid word structure) and in some ways harder (no evaluation at random points in the algebra).

## Why does it matter?

This is the canonical testing problem in the free algebra, central to symbolic computation over F⟨x⟩ (word problems in group rings, automata-theoretic polynomial manipulation). It would resolve whether noncommutative circuit reuse is fundamentally harder to certify than tree-like computation, clarifying the structure of NEXP-level algebraic proof systems (noncommutative formulas feed Frege/IPS lower bounds via Li–Tzameret–Wang). It also bears on the commutative PIT question: noncommutative techniques like the Raz–Shpilka automaton method are among the few unconditional deterministic PITs we have, and understanding why they fail for circuits is diagnostic for the whole field.

## What's already known?

- **Raz–Shpilka (2005):** deterministic poly-time PIT for noncommutative **formulas** (via equivalence with algebraic branching programs, then a "matrix-of-linear-forms" hitting set / automaton-based argument) and for noncommutative ABPs. This is the benchmark result.
- **Formula lower bounds:** Nisan–Wigderson (1995) gave exponential lower bounds for noncommutative formulas (and weakly for circuits) via the "partial derivatives" method, exploiting that words are rigid monomials.
- **Li–Tzameret–Wang (2015):** connect noncommutative formula complexity to Frege proof complexity; exponential-size noncommutative circuit lower bounds would lift to Frege lower bounds — showing why the circuit case resists.
- **Ajtai (1988) and followers:** deterministic identity testing for words/regular languages of matrices, related to read-once oblivious models.
- **Why circuits are hard:** the Raz–Shpilka argument linearizes by unfolding to an ABP; a circuit with sharing can have exponentially many "paths" through a shared subgraph, and no known reduction circuit→ABP preserves identity with only polynomial blowup unless one could prove lower bounds against ABPs (which is open even here for general circuits — Nisan–Wigderson fall short of exponential circuit lower bounds).

## What would count as solving it?

Any of:
1. **Upper bound (the problem as stated):** a deterministic poly(s, deg)-time algorithm deciding identity of a size-s, degree-poly(s) noncommutative circuit. A hitting set of quasipolynomial size would be a strong partial result.
2. **Hardness/conditional:** evidence that deterministic PIT for noncommutative circuits implies something unlikely, or a reduction from commutative circuit PIT (in either direction) — either would reframe the problem.
3. **Lower-bound route:** exponential lower bounds for noncommutative circuits of polynomial degree (this plus known PIT-to-lower-bound frameworks would derandomize via the hard-vs-easy paradigm, à la Kabanets–Impagliazzo).

## How to start

1. **Read Raz–Shpilka (2005), Sections on the ABP characterization and the hitting-set construction.** Identify exactly which step uses "each gate feeds one parent." The monomial set at each ABP layer is linear-in-dimension; sharing breaks this.
2. **Try the log-depth case first.** Raz's circuit-to-multilinear-formula techniques and the fact that NC²-like noncommutative circuits reduce to formulas (with quasipolynomial blowup via Brent-style depth reduction — check whether depth reduction holds in the noncommutative setting (verify)) would give quasipolynomial PIT for log-depth, a warm-up.
3. **Study Nisan–Wigderson's partial-derivative rank argument** and note it gives only superpolynomial (not exponential) circuit lower bounds; understanding the gap between the Hankel-matrix rank of formulas vs circuits is the same gap blocking PIT.
4. **Consider algebraic approaches:** substitute matrices of dimension poly(s) with entries that are commuting fresh variables or algebraically independent elements; invalid in general (exponential degree words), but with polynomial degree maybe a dimension bound from Amitsur–Levitzki or the chamber of the free skew field applies.

## Key references

- **Raz, R., Shpilka, A. (2005). "Deterministic Polynomial Identity Testing in Non-Commutative Models." Comput. Complexity 14(1):1–35.** Gives deterministic poly-time PIT for noncommutative formulas and ABPs via a matrix-of-linear-forms hitting set; the departure point.
- **Li, Y., Tzameret, I., Wang, S. (2015). "Non-Commutative Formulas and Frege (lower bounds)." LIPIcs.CCC.2015.412.** Shows how noncommutative formula lower bounds translate into Frege proof lower bounds via algebraic proof systems.
- **Nisan, N., Wigderson, A. (1995). "On the Complexity of Bilinear Forms." STOC.** (verify exact relevance) Develops rank/partial-derivative methods yielding lower bounds for noncommutative models.
- **Arvind, V., Srinivasan (various, e.g. "Non-commutative polynomial identity testing" follow-ups).** (verify) Extensions of Raz–Shpilka to read-once and bounded-read models.

## Warnings

- **Don't re-derive Raz–Shpilka for trees; the obstacle is specifically sharing (DAG structure).** Every "obvious" fix via unfolding to ABP costs exponential blowup.
- **The polynomial-degree restriction is essential to state but easy to mismanage:** a size-s circuit has syntactic degree up to 2^s; the hitting-set size must depend on degree polynomially or you've solved nothing.
- **Zero-testing semantics:** identity in the free algebra F⟨x⟩, not operator identities under finite-dimensional substitutions — these differ (polynomial identities of matrices à la Amitsur–Levitzki). Confirm which model any claimed evaluation-based algorithm uses.
- Commutative general-circuit PIT is famously open; don't accidentally claim a commutative corollary without checking.
- The census record cites few works; the field has follow-up literature (e.g., work by Forbes–Shpilka on ROABPs and noncommutative hitting sets) — verify before assuming novelty.

---
*`ALGO-000049` · unverified*

## Acceptance guidance

Any of:
1. **Upper bound (the problem as stated):** a deterministic poly(s, deg)-time algorithm deciding identity of a size-s, degree-poly(s) noncommutative circuit. A hitting set of quasipolynomial size would be a strong partial result.
2. **Hardness/conditional:** evidence that deterministic PIT for noncommutative circuits implies something unlikely, or a reduction from commutative circuit PIT (in either direction) — either would reframe the problem.
3. **Lower-bound route:** exponential lower bounds for noncommutative circuits of polynomial degree (this plus known PIT-to-lower-bound frameworks would derandomize via the hard-vs-easy paradigm, à la Kabanets–Impagliazzo).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/80ca97db-3365-48c7-9ace-b03e7a42c0a0?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000049.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000049)
