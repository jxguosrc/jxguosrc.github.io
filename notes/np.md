# NP and verifiers

## Search from decision: SAT

The **decision** version of SAT asks whether a Boolean formula `F` has a satisfying assignment. The **search** version asks us to find such an assignment.

Suppose we can call an algorithm that decides SAT. First, ask whether `F` is satisfiable; if not, there is no assignment to find. Otherwise, consider its variables one at a time. For each variable `x_i`, temporarily set `x_i = 0` along with the choices already made, and ask whether the resulting formula is satisfiable. If it is, keep `x_i = 0`; if not, set `x_i = 1`. At every step, the chosen partial assignment still has a satisfying completion. After all `n` variables, we have found one.

This uses at most `n + 1` SAT decision queries and polynomial additional work. It is a polynomial-time **Turing reduction** from search SAT to decision SAT: later queries depend on earlier answers. The argument works because restricting a SAT formula gives another SAT instance (**self-reducibility**). For an arbitrary language in NP, a decision procedure for membership alone does not automatically reveal a witness; we may instead need to ask whether a witness extending a given prefix exists.

## Verifiers

A language `A` is in NP if there is a deterministic polynomial-time algorithm `V` and a polynomial `p` such that, for every string `w`,

```text
w ∈ A  ⇔  there exists a string c with |c| ≤ p(|w|) for which V(w, c) accepts.
```

`V` is called a **verifier** for `A`. The string `c` is a **certificate** (or **witness**) that `w` belongs to `A`. Given `c`, the verifier can check membership efficiently; the definition does not require an efficient way to find `c`.
