# P, NP, and verifiers

## Search from decision: SAT

The **decision** version of SAT asks whether a Boolean formula `F` has a satisfying assignment. The **search** version asks us to find such an assignment.

Suppose we can call an algorithm that decides SAT. First, ask whether `F` is satisfiable; if not, there is no assignment to find. Otherwise, consider its variables one at a time. For each variable `x_i`, temporarily set `x_i = 0` along with the choices already made, and ask whether the resulting formula is satisfiable. If it is, keep `x_i = 0`; if not, set `x_i = 1`. At every step, the chosen partial assignment still has a satisfying completion. After all `n` variables, we have found one.

This uses at most `n + 1` SAT decision queries and polynomial additional work. It is a polynomial-time **Turing reduction** from search SAT to decision SAT: later queries depend on earlier answers. The argument works because restricting a SAT formula gives another SAT instance (**self-reducibility**). For an arbitrary language in NP, a decision procedure for membership alone does not automatically reveal a witness; we may instead need to ask whether a witness extending a given prefix exists.

## P: polynomial-time decision

A decision problem can be represented by a language `A`: on input `w`, the question is whether `w ∈ A`. We say `A ∈ P` if a **deterministic** algorithm decides this question in polynomial time. That is, there is a polynomial `p` such that, on every input `w`, the algorithm halts within `p(|w|)` steps, accepting exactly when `w ∈ A` and rejecting otherwise.

## Verifiers

A language `A` is in NP if there is a deterministic polynomial-time algorithm `V` and a polynomial `p` such that, for every string `w`,

```text
w ∈ A  ⇔  there exists a string c with |c| ≤ p(|w|) for which V(w, c) accepts.
```

`V` is called a **verifier** for `A`. The string `c` is a **certificate** (or **witness**) that `w` belongs to `A`. Given `c`, the verifier can check membership efficiently; the definition does not require an efficient way to find `c`.

## Polynomial-time verifiers

The condition above has two parts. First, every `w ∈ A` has a **short certificate** `c`: its length is bounded by a polynomial `p(|w|)`. Second, the verifier `V` runs in time polynomial in the size of its input, `|w| + |c|`. Because `|c|` is polynomially bounded in `|w|`, checking a proposed certificate takes polynomial time in `|w|`.

We call `A` **polynomial-time verifiable** if such a verifier exists: it accepts some short certificate for each `w ∈ A`, and accepts none for `w ∉ A`. This says that a proposed solution is easy to check, not that one is easy to find.

## NP: two equivalent definitions

Besides the verifier definition, `A ∈ NP` can be defined using a **nondeterministic** algorithm: there is a polynomial `q` such that every computation branch on input `w` halts within `q(|w|)` steps, and `w ∈ A` exactly when at least one branch accepts. These two definitions are equivalent.

### From a verifier to a nondeterministic algorithm

Suppose `A` has a polynomial-time verifier `V` and certificates of length at most `p(|w|)`. On input `w`, a nondeterministic algorithm guesses such a certificate `c`, then runs `V(w, c)`. Each branch takes polynomial time: guessing `c` takes at most `p(|w|)` steps, and verification is polynomial in `|w| + |c|`. An accepting branch exists exactly when an accepted certificate exists, so the algorithm accepts exactly the strings in `A`.

### From a nondeterministic algorithm to a verifier

Suppose a nondeterministic algorithm decides `A` within `q(|w|)` steps on every branch. A certificate `c` records the choices made along one branch. In the standard machine model, each step has only a constant number of possible choices, so `q(|w|)` steps need only `O(q(|w|))` bits to describe. A deterministic verifier follows the recorded choices, simulates that branch, and accepts if it reaches an accepting state. The simulation is polynomial-time, and an accepted certificate exists exactly when the original algorithm has an accepting branch.

In particular, `P ⊆ NP`: a deterministic polynomial-time decider is a nondeterministic one with only one branch (or a verifier that ignores its certificate).
