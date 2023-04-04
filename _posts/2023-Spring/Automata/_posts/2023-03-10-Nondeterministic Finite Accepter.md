---
layout: post
title: Nondeterministic Finite Accepter
tags: [Automata]
permalink: /2023-spring/automata/nfa
---

# Nondeterministic Finite Accepter

# Definition of a Nondeterministic Accepter

## Nondeterminism

**Nondeterminism** means a choice of moves for an automata. Instead of unique move in each situation, we allow a set of possible moves by defining the transition function whose range is a set of possible states.

> **Definition 2.4**

A **\*\*\*\***nondeterministic finite accepter**\*\*\*\*** is defined by the quintuple

$$
M=(Q,\Sigma, \delta, q_0, F),
$$

where $$Q,\Sigma, q_0, F$$ are defined as for nfa, but

$$
\delta: Q\times (\Sigma\cup\{\lambda\})\rightarrow 2^Q
$$

---

There are three major difference between nfa and dfa. First, the range of $$\delta$$ is in the powerset $$2^Q$$, a subset of $$Q$$. This subset is a set of all possible states that can be reached by transition. For example,

$$
\delta(q_0, a)=\{q_0, q_2\} \in 2^Q
$$

Also, we allow $$\lambda$$ as the second argument (string) of $$\delta.$$ It means that the nfa can make a transition without consuming an input symbol. Finally, the set $$\delta(q_i, a)$$ may be empty set, meaning that there is no transition defined for this specific stiuation, $$q_i$$ and $$a$$. We call such situation a **dead configuration**.

A string is accepted by an nfa if there is some sequence of possible moves that puts the machine in a final state at the end of the string.

## Extended Transition for NFA

> ************\*\*\*\*************Definition 2.5************\*\*\*\*************

For an nfa, the **extended transition function** is defined so that $$\delta^*(q_i, w)$$ contains $$q_j$$, if and only if there is a walk in the transition graph from $$q_i$$ to $$q_j$$ labeled $$w$$. (Similar to **\*\***Theorem 2.1**\*\***)

---

- **Example 2.9**
  ![Untitled](Nondeterministic%20Finite%20Accepter%2083a7c32fbaa847b9ba085e1a29a8eb53/Untitled.png)
  - $$\delta^*(q_1, a) = \{q_0, q_1, q_2\}$$ By using $$\lambda$$ -edge 0 or more times.
  - $$\delta^*(q_2, \lambda) = \{q_0, q_2\}$$ $$\lambda$$-edge may or may not be used.

> \***\*Definition 2.6\*\***

The language $$L$$ accepted by an nfa $$M=(Q,\Sigma, \delta, q_0, F)$$ is defined as the set of all strings accepted, formally

$$
L(M) = \{w\in\Sigma^*: \delta^*(q_0, w) \cap F \neq \emptyset\}
$$

$$\delta^*(q_0, w) \cap F \neq \empty$$ means that some sequence of $$\delta^*(q_0, w)$$ ends with the final state in $$F$$. Therefore, in words, the language consists of all strings $$w$$ , for which there is a walk labeled $$w$$ from initial vertex to some final vertex.

---

# Why Nondeterminism?

Although every digital computers are completely deterministic, nondeterminism is very important concept.

First, nondeterministic machines can serve as models of search and backtrack algorithms, since it can follow several alternatives simultaneously.

Also, nondeterminism is sometimes helpful in solving problems easily. In some cases, nondeterministic solutions are natural but deterministic solutions are not as obviously related to the definition of the language.

Moreover, nondeterminsm is an effective mechanism for describing complicated language concisely.

Finally, as there is no essential difference between nfa and dfa (**Section 2.3**), allowing nondeterminism often simplifies the situation, without affecting the generality of the conclusion.
