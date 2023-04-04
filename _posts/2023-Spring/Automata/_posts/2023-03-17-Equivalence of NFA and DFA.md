---
layout: post
title: Equivalence of DFA and NFA
tags: [Automata]
permalink: /2023-spring/automata/equivalence-of-dfa-and-nfa
---

# Equivalence of NFA and DFA

# Equivalence between Automata

To inspect the difference between nfa and dfa, we need to introduce the equivalence between automata.

> ****\*\*\*\*****\*\*\*\*****\*\*\*\*****Definition 2.7****\*\*\*\*****\*\*\*\*****\*\*\*\*****

Two finite accepters $$M_1$$ and $$M_2$$ are said to be **equivalent** if they both accept the same language,

$$
L(M_1)=L(M_2)
$$

---

In general, there are many accepters for a given language, therefore any dfa or nfa has many equivalent accepters.

Since a dfa is a restricted kind of nfa, it is clear that any language that is accepted by dfa is also accepted by some nfa. The converse is not so obvious, but it is also true. In the next section, the method of converting nfa to dfa will be demonstrated.

# Converting NFA into DFA

The key point in converting nfa to dfa is that we don’t know what state the nfa would be in after reading a string $$w$$, but we can say that it must be in one of a set of possible states, namely $$\{q_i, q_j, \dots, q_k\}$$. Then, we will label the states of dfa with set of states. As $$Q$$ is a finite set and there are exactly $$2^{\|Q\|}$$ subsets, the corresponding dfa will have finite number of states.

Therefore, the states in dfa will be labeled as sets, such as $$\{q_0\}, \{q_0,q_1\}$$. A state labeled $$\empty$$ refers to an impossible mobe for nfa, thus it must be a nonfinal trap state in dfa.

## Algorithm

> **Theorem 2.2**

Let $$L$$ be the language accepted by a nfa $$M_N=(Q_N, \Sigma, \delta_N,q_0, F_N)$$ . THen there exists a dfa $$M_D=(Q_D, \Sigma, \delta_D, \{q_0\}, F_D)$$, such that

$$
L=L(M_D)
$$

---

We will prove the theorem by \***\*\*\*\*\*\***nfa-to-dfa\***\*\*\*\*\*\*** procedure. Before going on, remember that the every vertex in $$G_D$$ must have $$\|\Sigma\|$$ outgoing edges.

> **Procedure** \***\*\*\*\*\***nfa-to-dfa\***\*\*\*\*\***

1. Create a graph $$G_D$$ with vertex $$\{q_0\}$$ as the initial vertex.
   ※ Note that the label is a set of states.
2. Repeat the following steps until no more edges are missing (= every edge has $$\|\Sigma\|$$ outgoing edges)
   1. Take any vertex $$\{q_i,\dots q_k\}$$ of $$G_D$$ that has no outgoing edge for some $$a \in \Sigma$$.
   2. Compute $$\delta^*(q_i, a)\cup \dots \cup \delta^*(q_k,a) = \{q_l, \dots q_n\}$$.
   3. If vertex labeled $$\{q_l, \dots, q_n\}$$ does not exist in $$G_D$$, create a vertex.
   4. Add an edge from $$\{q_i,\dots q_k\}$$ to $$\{q_l, \dots, q_n\}$$, with label $$a$$.
3. Every state of $$G_D$$ whose label contains any $$q_f \in F_N$$ is a final vertex.
4. If $$M_N$$ accepts $$\lambda$$ , then the initial vertex $$\{q_0\}$$ is also a final vertex.

We are now arguing that any nfa can be converted into dfa. But we need to prove that this procedure gives the correct answer. Therefore, we will prove the **correctness** of the procedure by induction on the length of the input string.

By \***\*\*\*\*\*\***nfa-to-dfa\***\*\*\*\*\*\*** procedure, any nfa can be converted into the equivalent dfa.

- **Proof**
  **Assume** that $$\forall v$$ s.t. $$\|v\|\le n$$, the existence of a walk labeled $$v$$ from $$q_0$$ to $$q_i$$ in $$G_N$$ implies that there is a walk labeled $$v$$ from $$\{q_0\}$$ to state $$Q_i=\{\dots,\ q_i,\ \dots \}$$ in $$G_D$$.
  For any $$w=va$$ (**Inductive step**), if there is a walk labeled $$w$$ from $$q_0$$ to $$q_l$$ in $$G_N$$, there must be a walk labeled $$v$$ from $$q_0$$ to $$q_i$$ and a walk labeled $$a$$ from $$q_i$$ to $$q_l$$.
  By the inductive assumption, there is a walk labeled $$v$$ from $$\{q_0\}$$ to $$Q_i$$ in $$G_D$$. By construction, there will be an edge from $$Q_i$$ to some $$Q_l$$ such that $$q_l \in Q_l$$.
  Therefore, the inductive assumption holds for all strings of length $$n+1$$. Also, it is obviously true for $$n=1$$, so it is true for all $$n$$.
  Therefore, the result is that whenever $$q_f\in\delta^*_N(q_0, w)$$, the label of $$\delta^*_D(\{q_0\},w)$$ also contains $$q_f$$.
- **Example 2.13**
  Convert following NFA into DFA
  ![Figure 2.14, NFA](Equivalence%20of%20NFA%20and%20DFA%2065426e56028f48daa47bc36b22c407a8/Untitled.png)
  Figure 2.14, NFA
  The NFA accepts $$L =\{0^n:n\ge1\}\cup\{0^n1:n\ge0\}$$
  Step 1:
  Make a vertex labeled $$\{q_0\}$$ and identify as an initial vertex.
  Step 2:
  First, start with $$q_0$$
  - $$\delta_N(q_0, 0) = \{q_0, q_1\}$$ (As $$\{q_0, q_1\}$$ does not exists in $$G_D$$, add $$\{q_0, q_1\}$$)
  - $$\delta_N(q_0, 1)= \{q_1\}$$
    Now we have two new vertices, $$\{q_0, q_1\}$$ and $$\{q_1\}$$. Proceed with $$\{q_1\}$$. ($$\neq$$q_1$$)
  - $$\delta^*_N(q_1,0)=\{q_2\}$$ (Note that $$\delta^*$$ has been used)
  - $$\delta^*_N(q_1, 1)=\{q_2\}$$
    For $$q_2$$, be careful that label $$0$$ is not defined.
  - $$\delta^*_N(q_2, 0) = \empty$$ (Label of empty set $$\empty$$ can also be a state)
  - $$\delta_N^*(q_2, 1) = \{q_2\}$$\delta(q_2, 1) = \{q_2\}$$
  Then move on to $$\{q_0, q_1\}$$
  - $$\delta^*_N(q_0, 0) \cup \delta^*_N(q_1, 0) = \{q_0, q_1\} \cup \{q_2\} = \{q_0, q_1,q_2\}$$
  - $$\delta^*_N(q_0, 1)\cup \delta^*_N(q_1, 1) = \{q_1\}\cup\{q_2\} = \{q_1, q_2\}$$
    Do the same for $$\{q_0, q_1, q_2\}$$ and $$\{q_1, q_2\}$$
  - $$\delta^*_N(q_1, 0) \cup \delta^*_N(q_2, 0) = \{q_2\}  \cup \empty = \{q_2\}$$
  - $$\delta^*_N(q_1,1)\cup\delta^*_N(q_2, 1) = \{q_2\}$$ (As $$\{q_2 \}$$ already exists, don’t add $$\{q_2\}$$)’
  - $$\delta^*_N(q_0, 0) \cup \delta^*_N(q_1, 0) \cup \delta^*_N(q_2,0) = \{q_0, q_1, q_2\}$$
  - $$\delta^*_N(q_0, 1)\cup \delta^*_N(q_1, 1)\cup \delta^*_N(q_2, 1) = \{q_1, q_2\}$$
    Don’t forget to apply the procedure for $$\empty$$
  - $$\delta^*_N(\empty, 0)= \delta^*_N(\empty, 1) = \empty$$
    We added all the vertices and every vertice has edges of label $$0$$ and $$1$$.
    Step 3:
    We need to identify the final states $$Q_f \in F_D$$ for DFA.
    As $$q_1$$ is the only final state in NFA ($$F_N = \{q_1\})$$, every vertices with label containing $$q_1$$ is the final state for the DFA. Therefore, the final state for DFA is $$\{q_1\},\ \{q_0, q_1\},\ \{q_0, q_1, q_2\}$$.
    Step 4:
    As $$M_N$$ does not accept $$\lambda$$ , $$\{q_0\}$$ is not identified as final vertex.
    As a result, we get a transition graph $$G_D$$ for DFA as following:
    ![Figure 2.16, Equivalent DFA for Figure 2.14](Equivalence%20of%20NFA%20and%20DFA%2065426e56028f48daa47bc36b22c407a8/Untitled%201.png)
    Figure 2.16, Equivalent DFA for Figure 2.14
