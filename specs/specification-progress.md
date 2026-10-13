# Rifle specification progress

Goal: implement the pure program validator/evaluator from the agreed v1 contract.
Repository bootstrap baseline: 4f5798f. New source is pinned by file hashes in
[initial validation](validation/initial-20261014/README.md); no extraction from
Hunter/BuildHunter runtime occurs. The schema originates from BuildHunter
79fa49303e73a595330fcb7441d5f8c2f430098d, copied byte-for-byte.

| Role | Contract / evidence | State |
|---|---|---|
| ProgramLoading.StrictJson | rifle.program/validation; src/json.rs; parser tests | Implemented, local tests; CI pending |
| ProgramLoading.SemanticValidation | rifle.program/validation,limits; src/validate.rs | Implemented, local tests; CI pending |
| ValidatedPlan | rifle.program/input_contract; private indexed expressions | Immutable public API; host order obligation explicit |
| Evaluation | rifle.program/pure,three_valued; src/lib.rs; truth tables | Implemented, local tests; no benchmark claim |
| ContractTests | tests/contract.rs | Significant semantic/negative/concurrency scenarios; not exhaustive input proof |
| Host adapters, catalog loader/JCS, target resolution, SDK/FFI | Excluded from this initial slice | Separate next work, not implied implemented |

One implementation boundary is sufficient: parsing/plan/evaluation share a pure
consumer contract. HC nesting is composition only. Root AGENTS.md requires maps
and contracts to follow future source changes. Preserve prior validation records.

Accepted: owner-approved plugin contract direction. New Rust API and BoundarySpec
remain reviewable drafts. Fresh validation distinguishes local debug/Release,
structural checks and actual GitHub CI. Next boundary: catalog/identity validation
and conformance before host integration; performance optimization needs baseline
measurement, not only a successful build.
