# path2-two-shadow-recovery

**Path 2 of the shadow-resolution capstone.** Pure Rust, **zero deps**.

Path 1 (the `dbbh-coms-quant-prism` crate) recovers a *retained* object by content address — a
store holds it. **Path 2 retains nothing.** It recovers an object from **two jointly-injective
lossy shadows**: each shadow alone is provably ambiguous (non-injective — many objects cast it),
but the two together cut the fiber `P1⁻¹(s1) ∩ P2⁻¹(s2)` to a singleton and reconstruct the
object **exactly, with no store anywhere.** This is the honest **double binary black hole**: two
poles recover what neither holds.

## Mechanism — CRT over coprime cylinders (the Asolaria CRT-coprime-cylinder lane)

For a block `x < R` and coprime primes `p1, p2`:
- `shadow1 = x mod p1`, `shadow2 = x mod p2` — each **lossy** (`x` and `x+k·p` share a shadow).
- if `p1·p2 ≥ R`: the pair uniquely determines `x` (Chinese Remainder Theorem) → **exact recovery, no store**.
- if `p1·p2 < R`: the two shadows don't jointly carry `log2(R)` bits → **`Held::InsufficientJointCapacity`** (the Shannon wall; add a third cylinder / pole).

## Honest ledger (Shannon intact)

- One shadow: `~log2(p)` bits, non-injective. Two shadows: `~log2(p1)+log2(p2) ≥ log2(R)` bits —
  the excess is the **over-determination margin** that buys *no store*.
- **Path 1 pays** `store(H(X)) + tiny address`. **Path 2 pays** bigger shadows, *no store*. Both
  `≥ H(X)`. No bijection beats Shannon; the entropy is *carried by the two shadows*, not destroyed.

## Federation form (the frontier)

`tests/federation.rs`: party **A** holds *only* `shadow_a` (mod `p1`), party **B** holds *only*
`shadow_b` (mod `p2`); the object is in no store; recovery is the **consent of the two poles** —
and a single pole reconstructs nothing. This is `acer ↔ liris` as two jointly-injective
projections whose consensus reconstructs a truth neither retained — the capstone's
`I(X;S2|S1) ≥ H(X|S1)`, in running code. It is why the bilateral convergence (two seats
independently reaching one theorem) is itself a Path-2 event.

## Status (dual-lens)

- `MEASURED` — the CRT two-shadow recovery, the byte round-trip, the neither-pole-alone property,
  and the Shannon-held boundary are covered by `cargo test` (zero deps).
- `CANON` — CRT / Bézout; the capstone theorem (a second jointly-injective shadow pays
  `I(X;S2|S1) ≥ H(X|S1)` to cut the fiber).
- `UNVERIFIED` — a *live* federated deployment where acer and liris are the two physical poles over
  Hilbra (this crate is the mechanism; the cross-machine live run is the next rung).


## Liris multi-cylinder 3D Q-PRISM slice harness

This branch adds the Liris side of the cross-fabric synthesis: `MultiCylinder` +
`QPrismSlice3d`. It generalizes the two-shadow proof to N coprime cylinders,
then projects a frozen slice into classical representation wavelengths: binary/hex/sha,
BEHCS-64, BEHCS-256, BEHCS-1024, and a digest-derived HyperBEHCS-60D coordinate. The
HBP rows end in `json=0` and carry no payload body.

The key measured property is the calculable slice roof: two ~25-bit cylinders are not
enough for an 8-byte slice, three are enough, and every added cylinder raises the roof.
See [`docs/LIRIS-MULTICYLINDER-QPRISM-SLICE.md`](docs/LIRIS-MULTICYLINDER-QPRISM-SLICE.md).

## Liris PIE world-slice harness

This branch also adds the first falsifiable PIE cell: metatagged particles render into a
pixels-first bounded slice, the slice projects into N coprime cylinder shadows, same-radius
pixels form a frequency-sphere view, and a deterministic LeWorld-style rule computes the
next or previous slice byte-identically only after sufficient cylinder recovery. If two
cylinders do not carry enough capacity, the system returns `Held::InsufficientJointCapacity`
instead of inventing a future. See
[`docs/LIRIS-PIE-WORLD-SLICE.md`](docs/LIRIS-PIE-WORLD-SLICE.md).

The N-Q-prism residual selector lane measures how many bits remain after the shared
Brown-Hilbert/PID/coprime-cylinder context collapses the fiber. `select_for_residual_bits`
keeps adding cylinders until that residual is at or below the target; all extra cylinders
are consistency-checked, and overflow-sized capacity receipts are capped/lower-bounded
instead of silently printing zero.


## Liris watcher gate

The watcher gate wraps the DBBH -> DBWH local throat with black/white round-trip checks:
GNN-forward proposes the emitted slice, reverse-GNN recompresses it, OmniShannon checks the
capacity ledger, and MTP1/2/3 observe pixel, shell, and cylinder consistency. The output is
either a verified classical clone or `Held`. This is a structural universe-analogue, not a
physical-universe claim and not quantum cloning.

## Tests

`cargo test` — unit + federation + Liris multi-cylinder Q-PRISM slice tests. All zero-dep, WSL/rustc.

## License

MIT OR Apache-2.0.
