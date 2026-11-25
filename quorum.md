# How Many Replicas Do You Need?

```
n ≥ f₁ + ⋯ + f_j + t
```

- **j**: quorums that must all overlap
- **f_i**: failures phase i tolerates (quorum size `q_i = n − f_i`)
- **t**: required overlap
  - crash: `1`
  - Byzantine, self-verifying data: `b + 1`
  - Byzantine, replica-attested data: `2b + 1`
- **b**: unidentified liars, normally `f`, or `f − 1` if an equivocating leader is excluded *and replaced*

**Slack:** `D = n − Σf_i − t ≥ 0` is spare fault tolerance you can spend on any phase.

**Why it holds:** j quorums of sizes q_i always share at least `Σq_i − (j−1)n` replicas. Require that to be ≥ t and set `q_i = n − f_i`.

| Protocol | n ≥ |
|---|---|
| Paxos | 2f + 1 |
| Byzantine, self-verifying | 3f + 1 |
| Byzantine, masking | 4f + 1 |
| Fast Paxos | max(2f + 1, f + 2e + 1) |
| FaB | 3f + 2e + 1 |
| KTZ (1 ≤ e ≤ f) | 3f + 2e − 1 |

**One identified liar = two fewer replicas.**

*Applies to threshold-quorum protocols only. t is an input; proving the protocol achieves it is separate.*
