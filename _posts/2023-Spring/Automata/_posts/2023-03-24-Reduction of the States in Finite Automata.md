---
layout: post
title: Reduction of States in Finite Automata
tags: [Automata]
permalink: /2023-spring/automata/reduction-of-states
---

# Reduction of the States in Finite Automata

# Reduction of the States

Although any dfa defines a unique language, there are many dfa’s that accept the given language. Each dfa may have different number of states. For practical reasons, we prefer the dfa with minimum number of states.

## Inaccessible States

![Figure 2.17](Reduction%20of%20the%20States%20in%20Finite%20Automata%20fd1edd8ef28344eea1ba87e02eff3f34/Untitled.png)

Figure 2.17

A state is **inaccessible** if it can never be reached from initial state $$q_0$$. Then, a state $$q_0$$ is inaccessible if

$$
\delta^*(q_0, w) \neq q_i\ \forall w \in \Sigma^*
$$

As inaccessible states do not play any role in the automaton, it and its related transitions can be removed. In Figure 2.17, it can be easily seen that $$q_5$$ is inaccessible, so we can remove the state $$q_5$$.

## Indistinguishable States

> **Definition 2.8**

Two states $$p$$ and $$q$$ of a dfa are **indistinguishable** if

$$
\delta^*(p, w) \in F \text{ implies } \delta^*(q, w) \in F
$$

for all$$\ w\in\Sigma^*$$. Also, it is equivalent to for all $$w \in F$$,

$$
\delta^*(p, w) \notin F \text{ implies } \delta^*(q, w) \notin F
$$

Similarly, $$p$$ and $$q$$ are **distinguishable** if **$$\exists w \in \Sigma^*$$** such that

$$
\delta^*(p, w) \in F \text{ and } \delta^*(q, w) \notin F
$$

---

Indistinguishability is an equivalence relation, that is, if $$p$$ and $$q$$ are indishtinguishable and $$q$$ and $$r$$ are indistinguishable, so are $$p$$ and $$r$$, and all three states are indistinguishable.

If two states are indistinguishable, then it can be merged into a single state. Therefore, we will first find pairs of distinguishable states.

### Algorithm

> **Procedure** _mark_

1.  Remove all inaccessible states, by examining all simple paths from the initial state.
2.  Consider all pairs of states $$(p, q)$$. By definition, if $$p \in F$$ and $$q \notin F$$ or vice versa, mark the pair as distinguishable.
    The process is starting from the final state (bottom-up), since those are the base case of distinguishable pairs.
3.  Repeat the following step until no previously unmarked pairs are marked, i.e., no more marked pairs found.

    1. For all $$(p, q)$$ and all $$a\in \Sigma$$, compute $$\delta(p, a)=p_a$$ and $$\delta(q, a) = q_a$$.
    2. If exists some $$a$$ such that the pair $$(p_a, q_a)$$ is already marked then mark $$(p, q)$$ as distinguishable.

    - Detail
      $$(p_a, q_a)$$ is distinguishable means that

      $$
          \delta^*(\delta(p, a), w) \in F \text{ and } \delta^*(\delta(q, a), w) \notin F, \\
          \implies \delta^*(p, v) \in F \text{ and } \delta^*(q, v) \notin F
      $$

    for some string $$v = aw  \in \Sigma^*$$. Therefore, if $$(p_a, q_a)$$ is distinguishable, then $$(p, q)$$ are distinguishable too.

---

> **Theorem 2.3**

The procedure _mark_ terminates and determines all pairs of distinguishable states for any dfa $$M = (Q, \Sigma, \delta, q_0, F )$$

---

### Proof by Correctness

We need to prove two claims, that the _mark_ terminates (1) and that the _mark_ determines all pairs of distiniguishable states(2).

First, it is obvious that the procedure terminates, since there are finite number of states, there fore finite number of pairs to be marked.

Now, we will prove the procedure finds all distinguishable pairs.

Before getting in, note that $$q_i$$ and $$q_j$$ are distinguishable with $$w_n$$ of length $$n$$ if and only if if there exists some $$a \in \Sigma$$ , such that

$$
\begin{equation}
\delta(q_i, a) = q_k \text{ and } \delta(q_j, a) = q_l
\end{equation}


$$

with $$q_k$$ and $$q_l$$ are distinguishable by string $$w_n$$ of length $$n-1$$.

Again, we will prove the claim with induction. Our **basis** is $$n= 0.$$ That is, we will start with the states that can be distinguished with $$\lambda$$ . It is clear that $$\lambda$$ can distinguish non-final states and final states. Now **assume** that our claim is true for $$i = 0, 1, \dots n-1$$.

By the assumption, it is clear that

- At the beginning of $$n$$th pass, pairs that can be distinguished with the string of length $$n-1$$ are all marked.
- With $$(1)$$, at the end of $$n$$th pass, pairs that can be distinguished with the string of length $$n$$ are all marked.

Therefore, after $$n$$th pass, all pairs that can be distinguished with $$w$$ such that $$\|w\|\le n$$ are all marked.

Assume the _mark_ terminates after $$k$$ passes. Then no new state pair was marked during $$k$$th passes, i.e. marked pairs during $$k$$th and $$k+1$$th are the same. Thus, the procedure terminates and all distinguishable pairs are marked. (If $$\|w\|=n$$ cannot distinguish any state, so does $$\|w\|=n+1$$ )
