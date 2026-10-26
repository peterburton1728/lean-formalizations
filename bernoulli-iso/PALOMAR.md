# Statement comparison and Palomar preparation

The intended registry statement is the finite-uniform measurable conjugacy in
`Challenge.lean`, not every theorem claimed by the accompanying PDF.
`Solution.lean` provides the proof. Its repeated definitions deliberately have
the same qualified names and mathematical bodies in a separate module; the
modules must not import each other. Comparator compares the selected theorem's
type and the constants its statement depends on.

The Challenge uses a theorem with a deliberate `by sorry` statement hole.
Do not replace it with an axiom: Lean 4.35 Comparator requires matching
constant kinds, and the Solution endpoint is a theorem. No proof-development
placeholder or additional axiom is permitted in the Solution closure. The
only permitted axioms are `propext`, `Classical.choice`, and `Quot.sound`.

## Recorded local status

The source build and all axiom audits passed. The optional macOS export-based
diagnostic was stopped during the large Solution export; no Comparator or NanoDa
acceptance is claimed. `verification/local-comparator.json` records that boundary.
The full protected Linux preflight below remains required before submission.

## Local checks

```sh
python3 check_package.py .
lake update
lake exe cache get
lake build Solution
lake build Audit
lake comparator --config comparator.json
```

The package scanner checks source formatting and obvious placeholders;
it does not parse Lean or inspect proof terms. The axiom audit and Comparator
are necessary complementary checks. Keep complete logs, exact source hashes,
toolchain/dependency pins and outcomes for every claim made about verification.
A source-only review is not an executed build; a build is not Comparator; a
local Comparator run is not the complete registry workflow. Sandbox commands
may require Linux tooling and privileges unavailable on macOS. Do not relabel
an unsandboxed local diagnostic as a protected mechanical check.

## Full Linux mechanical preflight

Use Palomar's reusable workflow at the exact pinned pipeline revision below,
with the actual public GitHub repository and immutable release commit. No
repository identity has been fabricated in these instructions.

```yaml
jobs:
  palomar-preflight:
    uses: PalomarRegistry/PalomarSubmission/.github/workflows/submission.yml@c02bbeaed888df45c4e28c4e99dba540ad21552a
    with:
      repository: ${{ github.repository }}
      commit: ${{ github.sha }}
      pipeline_commit: c02bbeaed888df45c4e28c4e99dba540ad21552a
      request_id: preflight001
      mode: full
      execution_profile: palomar-standard-v1
      options: '{"comparator_config_path":"comparator.json","authorization_relationship":"I am a responsible author or maintainer"}'
```

The relationship declaration is a permanent claim about the human submitter;
use it only when truthful and authorized. Both pipeline SHA fields must match.
Paths are repository-relative; add project_path or formalization_metadata_path
only if the default root layout changes. This workflow must run on the exact
commit intended for submission and return a passing full mechanical report.
Source changes require checking the new commit.

The pinned verifier accepts Lean releases at least v4.35.0-rc2. This project
uses v4.35.0 and its bundled `lake comparator`, exporter, Lean kernel and NanoDa.
The pipeline selects its own protected configuration, sandbox and checker
revisions; user configuration cannot weaken these. For this toolchain the pinned
pipeline selects con-ron from Lean v4.36.0-rc1 and attempts replay after the
mandatory Lean/NanoDa checks. Record the actual reports and binary digests;
do not infer successful kernel checks from the configuration alone.

Palomar's CONTRIBUTING prose and some older Comparator instructions describe an
older standalone tool arrangement. The exact pipeline implementation and report
must be retained when documenting which checks actually ran. A full preflight
is predictive mechanical evidence, not editorial review or registration.

## Before public submission

Ensure every committed Lean source uses the module system and is at most
10,000 physical lines, including unused sources and contained packages. Challenge
has the tighter 1,000-line/100-KiB cap. Commit only the final source and metadata,
not compiled proof artifacts outside `.lake`; the service discards supplied
`.lake` state. Keep the checkout at most 500 MiB, avoid submodules/LFS pointers,
and retain canonical pinned Git dependencies, the root SPDX license and upstream
provenance. `formalization.yaml` must accurately describe scope, sources,
human authorship, AI contributions and the review actually completed.

Read the current official [policy](https://github.com/PalomarRegistry/PalomarPolicy/blob/main/CONTRIBUTING.md)
and [submission-service contract](https://submit.palomar-registry.org/llms.txt)
before intake. Agent-driven submission requires prior agreement on the actual
repository, exact source commit, Comparator path and relationship claim. Agents
must not perform browser sign-in for the user. Registration is a separate
publication decision tied to the exact review digest, and creates durable public
records. These instructions perform neither submission nor registration.
