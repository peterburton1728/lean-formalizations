# Finite uniform Bernoulli shifts with unequal base entropy

This development proves that there exist a countable group G and a nontrivial
finite alphabet A for which the ordinary left Bernoulli shifts on A and A×A,
with independent uniform letters at every group site, are measurably conjugate.
The conjugacy preserves probability, is equivariant, and has a measurable inverse
on invariant conull measurable subsets. The two uniform bases have different
cardinalities and therefore different base Shannon entropies.

The algebraic existence input is due to OpenAI's characteristic-two construction
at commit `adc7f1241b42e322a6451854ab7e4b4c146bf78a`. This development uses checked
algebraic proof terms and constructs the dynamical conjugacy from that input.
Peter Burton is the responsible human author and maintainer. Material GPT-6
Astra and Sol contributions are disclosed in `formalization.yaml`.

## Verification status

The local sequential module-port build passed, including the standalone
`Solution` theorem. All 111 component axiom audits and the standalone theorem
use only `propext`, `Classical.choice`, and `Quot.sound`. Fifty unchanged proof
exports were reused from the completed certificate; eight changed or new modules
were checked. See `verification/local-build.json` and the audit logs.

The optional local export-based Comparator diagnostic was stopped during the
large Solution export. It did not establish statement comparison or independent
kernel acceptance. The pinned full Linux mechanical preflight remains required
before registry submission. No Palomar submission or registration has occurred.

## What is certified

`Challenge.lean` is the short mathematical statement: it imports Mathlib only and
spells out the ordinary left shift, uniform product law and full conull-conjugacy
conditions. Its one deliberate `sorry` is the statement hole supplied for
comparison; it is not a completed proof.

`Solution.lean` repeats the same statement and definitions independently, then
supplies the proof from `BernoulliIso.FiniteBaseCertificate`. It does not import
Challenge. The concrete endpoint is
`BernoulliIso.FiniteBaseCertificate.unequal_finite_bernoulli_shifts`, together
with its `conjugacy` object and `group_countable` theorem. `comparator.json`
selects `BernoulliCertificate.unequal_finite_bernoulli_shifts` for comparison.

The certificate concerns a specific finite uniform alphabet and its square.
It does not certify the accompanying note's all-base extension, finitary
continuity, integer coding inputs, finitely presented or graph formulations.
It makes no two-symbol-versus-four-symbol claim. The formal adapter records
cardinal inequality; its interpretation as unequal uniform base entropy does
not constitute a formalization of a general entropy classification theorem.

## Reproduce the source build

Install the pinned Lean toolchain through elan, then run from the project root:

```sh
lake update
lake exe cache get
lake build Solution
lake build Audit
```

`lean-toolchain` selects Lean 4.35.0. Canonical Mathlib is fixed at
`56a005855ea17e0b0958f73ec801ae140b0a1679`; its own toolchain matches.
The committed `lake-manifest.json` fixes the remaining dependencies. Check that
`lake update` has not changed those pins. The cache command retrieves dependency
build output; it is not a proof-verification claim by itself. Build only one
copy of the large upstream bundle at a time on memory-constrained machines.

For statement comparison on a supported sandbox host:

```sh
lake comparator --config comparator.json
```

This uses Lean 4.35's bundled Comparator rather than the archived standalone
Comparator package. The local source build, axiom audit, statement comparison,
and complete Linux Palomar workflow are distinct checks. This README asserts
no result for a check whose report is not supplied. See `PALOMAR.md` for the
full mechanical preflight and its publication boundary.

## Provenance and license

See `provenance/README.md` for upstream source hashes, the recorded Lean API port,
bundle boundaries and release module-visibility changes. Compare source hashes
against an independently trusted copy of the pinned records; hashes alone do
not prove a mathematical theorem or authenticate their own origin.

The Lean code and build/verification materials are licensed under Apache-2.0; see `LICENSE` and `NOTICE`. Retain the upstream
OpenAI notices and attribution when redistributing its adapted proof sources.
The accompanying written note is `bernoulli-iso.pdf`; its TeX sources are not
part of this release. The metadata describes the narrower formalized result.
