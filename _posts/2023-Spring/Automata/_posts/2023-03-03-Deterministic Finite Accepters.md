---
layout: post
title: Deterministic Finite Accepters
tags: [Automata]
permalink: /2023-spring/automata/dfa
---

# Deterministic Finite Accepters

# Deterministic Accepters and Transition Graphs

## Deterministic Accepters

> Definition 2.1

A **deterministic finite accepter (dfa)** is defined by the quintuple

$$
M=(Q, \Sigma, \delta, q_0, F)
$$

- $$Q$$: finite set of internal states
- $$\Sigma$$: finite set of symbols called the (input alphabet)
- $$\delta$$: $$Q\times E \mapsto Q$$ is a total function (transition function)
- $$q_0\in Q$$: is the initial state
- $$F\subseteq Q$$: is a set of final states

---

A dfa is assumed to be in the initial state $$q_0$$ at the initial time. It will read input from left to right, one symbol at a time. If it is in one of its final states $$F$$ when the end of input string has reached, then the string is accepted. The transition from one state to another is governed by the transition function $$\delta$$. For example, $$\delta(q_0, a) =q_1$$.

## Transition Graphs

To visuallize and represent finite automata, we use **\*\***\*\*\*\***\*\***\*\***\*\***\*\*\*\***\*\***transition graphs**\*\***\*\*\*\***\*\***\*\***\*\***\*\*\*\***\*\***. The vertices represent states and edges represent transitions. Formally, if $$M=(Q, \Sigma, \delta,q_0, F)$$ is a dfa, then its associated transition graph $$G_M$$ has exactly $$\|Q\|$$ vertices (states). For every transition rule $$\delta(q_i,a)=q_j$$, the graph has an edge $$(q_i, q_j)$$ labeled $$a$$ .

## Extended Transition Function

For convinience, we introduce the **extended transition function**

$$
\delta^*:Q\times \Sigma^*\rightarrow Q
$$

The second arguement of $$\delta^*$$ is a string ($$w\in \Sigma^*$$), not a single symbol. For example,

$$
\text{if}\ \delta(q_0, a)=q_1,\ \delta(q_1,b)=q_2,\\
\text{then}\ \delta^*(q_0, ab)=q_2
$$

Formally, $$\delta^*$$ is recursively defined by

$$
\delta^*(q, \lambda)=q,\\
\delta^*(q,wa) = \delta(\delta^*(q,w),a)
$$

for all $$q\in Q,\ w\in \Sigma^*,\ a \in \Sigma$$.

# Languages and DFA’s

## Language and DFA

> **Definition 2.2**

The language accepted by a dfa $$M=(Q,\Sigma, \delta, q_0, F)$$ is the set of all strings on $$\Sigma$$. That is,

$$
L(M)=\{w\in \Sigma^*: \delta^*(q_0, w) \in F\}
$$

---

At each step, a unique move is defined, therefore the automata is deterministic. A dfa will process every string in $$\Sigma^*$$ and accept it if the dfa stops in a final state. Otherwise, it will reject it, so that

$$
\overline{L(M)} = \{w\in \Sigma^*:\delta^*(q_0, w) \notin F\}
$$

> **Theorem 2.1**

Let $$M=(Q, \Sigma, \delta, q_0, F)$$ be a dfa, and $$G_M$$ bee its associated transition graph. Then for every $$q_i, q_j \in Q,\ w\in \Sigma^*,\ \delta^*(q_i,w)=q_j$$ if and only if there is a walk with label $$w$$ from $$q_i$$ to $$q_j$$ in $$G_M$$.

- Proof
  For the proof, we will use an induction on the length of $$w$$. **Assume** the claim is true for all strings $$v$$ with $$\|v\|\le n$$. And consider any $$w$$ of length $$\|w\|\le n+1$$ and write as $$w = va$$.
  Now, suppose that $$\delta^*(q_i, v) = q_k$$. As $$\|v\|= n$$, there must be a walk in $$G_M$$ labeled $$v$$ from $$q_i$$ to $$q_k$$ (**assumption**). But if $$\delta^*(q_i, w) = q_j$$, then $$M$$ must have a transition $$\delta(q_k, a)=q_j$$. Therefore, $$G_M$$ has an edge $$(q_k, q_j)$$ with label $$a$$ , consequently, exists a walk labeled $$va = w$$ between $$q_i$$ and $$q_j$$ .
  As a **basis**, choose $$n=1$$, and obviously, it is true for $$n=1$$. $$\blacksquare$$

---

Also, we can represent automata with the table, as seen below.

![Untitled](Deterministic%20Finite%20Accepters%20a8a39e56c24f48f2b0409bd0c1d0fa18/Untitled.png)

- Example 2.3
  > Find a dfa that recognizes the set of all strings on $$\Sigma=\{a,b\}$$starting with the prefix $$ab$$.
  > If the first symbol of the string is $$b$$ , then it would go into the trap state. Also, if the second $$a$$ is followed by the first $$a$$, that is, the sting has the prefix of $$aa$$, it will go into the trap state. Otherwise, the string would be accepted. Therefore, our solution is
  > ![Untitled](Deterministic%20Finite%20Accepters%20a8a39e56c24f48f2b0409bd0c1d0fa18/Untitled%201.png)

# Regular Languages

## Regular Languages

The **family** of languages is a set of languages. There is the family of languages that is acepted by deterministic finite automata. We say the languages in this family of language are \***\*regular\*\***.

> Definition 2.3

A language $$L$$ is called **\*\***\*\*\*\***\*\***regular**\*\***\*\*\*\***\*\*** ↔ Exists some dfa $$M$$ such that

$$
L=L(M)
$$

---

To show any language is regular, all we have to do is find a dfa for it. By the definition of regular, if exists any dfa $$M$$ accepts the language $$L$$, then the language is regular.

It is known that the union, intersection, and difference of two regular languages and the complement of the regular language are also regular. Also, reversal, concatenation and closure of regular language are regular.

![Source: [https://www.univ-orleans.fr/lifo/Members/Mirian.Halfeld/Cours/TLComp/TLComp-ProRegLang.pdf](https://www.univ-orleans.fr/lifo/Members/Mirian.Halfeld/Cours/TLComp/TLComp-ProRegLang.pdf)](Deterministic%20Finite%20Accepters%20a8a39e56c24f48f2b0409bd0c1d0fa18/Untitled%202.png)

Source: [https://www.univ-orleans.fr/lifo/Members/Mirian.Halfeld/Cours/TLComp/TLComp-ProRegLang.pdf](https://www.univ-orleans.fr/lifo/Members/Mirian.Halfeld/Cours/TLComp/TLComp-ProRegLang.pdf)

We will learn those closures and operations of regular languages in **Chapter 4**, **Theorem 4.1.**
