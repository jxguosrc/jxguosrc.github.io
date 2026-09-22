# NP and verifiers

A language `A` is in NP if there is a deterministic polynomial-time algorithm `V` and a polynomial `p` such that, for every string `w`,

```text
w ∈ A  ⇔  there exists a string c with |c| ≤ p(|w|) for which V(w, c) accepts.
```

`V` is called a **verifier** for `A`. The string `c` is a **certificate** (or **witness**) that `w` belongs to `A`. Given `c`, the verifier can check membership efficiently; the definition does not require an efficient way to find `c`.
