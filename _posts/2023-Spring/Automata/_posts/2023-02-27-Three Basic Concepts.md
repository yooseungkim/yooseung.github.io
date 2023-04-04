---
layout: post
title: Three Basic Concepts
tags: [Automata]
permalink: /2023-spring/automata/basic-concepts
---

# Three Basic Concepts

# Languages

## Alphabet and String

An **alphabet $$\Sigma$$** is a finite, nonepty set of symbols. A **string $$w$$** is a finite sequence of symbols from alphabet $$\Sigma$$. For example, if $$\Sigma=\{a,b\}$$, then $$aaabb$$ and $$aaba$$ are strings on $$\Sigma$$. We will use $$a, b, c, \dots$$ for symbols, i.e., elements of $$\Sigma$$ and $$u, v, w$$ for strings.

## Concatenation, Reverse and Length

The **concatenation** of two strings $$w$$ and $$v$$ is the string obtained by appending symbols of $$v$$ to the $$w$$ and denoted by

$$
\begin{align*}
&w=a_1a_2a_3\cdots a_n\\
&v = b_1b_2b_3\cdots b_m\\
&wv=a_1a_2\cdots a_nb_1b_2\cdots \cdots b_m
\end{align*}
$$

The **reverse** of a string is obtained by writing the symbols in reverse order. For example, if $$w=a_1a_2\cdots a_n$$, then the reverse of $$w$$ is

$$
w^R = a_n\cdots a_2a_1
$$

The **length** of a string $$w$$ is denoted by $$\|w\|$$ , is the number of symbols in the string. An **empty string $$\lambda$$** is a string with no symbols. Therefore, for all $$w$$,

$$
\begin{align*}
&\|\lambda\|=0,\\
&\lambda w = w\lambda = w
\end{align*}
$$

A **substring** of a string $$w$$ is a string of consecutive symbols in $$w$$. If $$w =vu$$, then $$v$$ and $$u$$ are said to be **prefix** and \*\*suffix\*\* of $$w$$, respectively.

### Example 1.8

In following example, we will show that $$\|uv\|=\|u\|+\|v\|$$. To prove this, we will define a length of string in a recusive way,

$$
\begin{align*}
\|a\|=1,\; \|wa\|=\|w\|+1
\end{align*}
$$

for all $$a\in \Sigma$$ and $$w$$ be any string on $$\Sigma$$. This definition can be understood as following.

- The length of a single symbol is one
- The length of any string is increased by one if another symbol is added to it.

As an inductive assumption, we take that $$\|uv\|=\|u\|+\|v\| \ (\star)$$ holds for $$u$$ of any length and $$v$$ of length $$1,\ 2,\dots,\ n$$.

For an inductive basis, we have $$u$$ of any length and $$v$$ of length 1.

Now we take any $$v$$ of length $$n + 1$$ and $$v = wa$$ . Then,

$$
\begin{align*}
&\|v\|=\|w\|+1\\
&\|uv\|=\|uwa\| = \|uw\|+1
\end{align*}
$$

By the inductive hypothesis $$(\star)$$,

$$
\|uv\|=\|uw\|+1=\|u\|+\|w\|+1=\|u\|+\|v\|
$$

Therefore, $$(\star)$$ holds for all $$u$$ and all $$v$$ of length up to $$n+1$$, so we completed inductive step.

## Language

If $$w$$ is a string, then $$w^n =ww...w$$ , and if $$n=0$$, we define $$w^0=\lambda$$ .

If $$\Sigma$$ is an alphabet, we use $$\Sigma^*$$ to denote the set of strings obtained by concatenating zero or more symbols from $$\Sigma$$. For all $$\Sigma$$, $$\lambda \in \Sigma^*$$. TO exclude the empty string, we define $$\Sigma^+ = \Sigma^*-\{\lambda\}$$.

Note that $$\Sigma^*$$ and $$\Sigma^+$$ are infinte set, although $$\Sigma$$ is a finite.

A **language $$L$$** is a subset of $$\Sigma^*$$. A string $$w\in L$$ is called a **sentence** of $$L$$. Therefore, a sentence is a string.

## Operations

Since languages are sets, operations such as the union, intersection, and difference is defined. As $$L \subseteq \Sigma^*$$, the **complement** of a language is defined by

$$
\overline{L} = \Sigma^* - L
$$

Also, the **reverse** of a language is the set of all string reversals, i.e.,

$$
L^R = \{w^R: w\in L\}
$$

The **concatenation** of two langauges $$L_1$$ and $$L_2$$ is the set of all strings obtained by concatenating any element of $$L_1$$ and $$L_2$$.

$$
L_1L_2 = \{xy:x\in L_1,\ y\in L_2\}
$$

We define $$L^n$$ as $$L$$ concatenated with itself $$n$$ times. For all $$L$$ , it holds that

- If $$n=0$$, then $$L^0 \overset{\text{def}}{=} \{\lambda \}$$ (note that $$\{\lambda\}$$ is a set)
- If $$n=1$$, then $$L^1 \overset{\text{def}}{=}L$$

We define the star-closure of a language as

$$
L^* = L^0 \cup L^1\cup L^2\cdots
$$

And the positive-closure is defined as

$$
L^+ = L^1\cup L^2\cdots
$$

# Grammars

## Definition

A **grammar** describes how sentence in languages should be formed.

Formally, a grammar $$G$$ is defined as a quadruple,

$$
G = (V, T, S, P)
$$

- $$V$$ is a finite set of objects called **variables $$(V\neq \emptyset)$$**
- $$T$$ is a finite set of obejcts called **\*\***\*\*\*\***\*\***\*\***\*\***\*\*\*\***\*\***terminal symbols $$(T\neq\emptyset)$$\*\*
- $$S\in V$$ is a special symbol called the **start** variable
- $$P$$ is a finite set of **productions**

## Production

The production rules specify how the grammar transforms one string into another. We assume all production rules are of the form

$$
x \rightarrow y,
$$

where $$x \in (V\cup T)^+$$ and $$y \in (V \cup T)^*$$. This implies that some string can be transformed into $$\lambda$$ , but $$\lambda$$ cannot be transformed into another.

Given a string $$w$$ of the form $$w = uxv$$, the production $$x\rightarrow y$$ is applicable in this string. So we may use the production and replace $$x$$ with $$y$$ and obtain a new string $$z = uyv$$. This process can be written as

$$
w \Rightarrow z
$$

and we say that $$w$$ **derives** $$z$$ . Any successful strings can be derived by applying the productions in arbitrary order. If

$$
w_1 \Rightarrow w_2 \Rightarrow \cdots \Rightarrow w_n,
$$

we say that $$w_1$$ derives $$w_n$$, and write

$$
w_1 \overset{*}{\Rightarrow} w_n
$$

The $$*$$ indicates that unspecified number of steps (including zero) can be taken.

## Derivation and Sentential Forms

Let $$G = (V, T, S, P)$$ be a grammar. Then the set

$$
L(G) = \{w\in T^*: S \overset{*}{\Rightarrow}w_n\}
$$

is the langauge **generated** by $$G$$.

This definition says that if $$w \in L(G)$$, then the sequence

$$
S\Rightarrow w_1 \Rightarrow w_2 \Rightarrow \cdots \Rightarrow w
$$

is a **derivation** of the sentence $$w$$ and $$w$$ is a sequence of terminal symbols ($$T^*)$$. The strings $$S,\ w_1,\ w_2,\ \dots,\ w_n$$ are called **sentential forms** of the derivation

### Example 1.13

Prove $$G =(\{S\}, \{a,b\}, S, P)$$ with the productions

$$
S\rightarrow SS \| \lambda \\
S\rightarrow aSb \| bSa
$$

generates the language $$L = \{w: n_a(w) = n_b(w)\}$$

First, prove every sentence generated by $$G$$ has an equal number of $$a$$’s and $$b$$’s. It is obvious since productions that generate $$a$$ simultaneously generate $$b$$Therefore, every element of $$L(G)$$ is in $$L$$, thus $$**L(G) \subseteq L$$.\*\*

Now, we need to prove all elements in $$L$$ can be generated by $$G$$, i.e., $$L \subseteq L(G)$$. We will consider various forms of $$w\in L$$ can have.

Begin by the case with $$w$$ that starts with $$a$$ and ends with $$b$$, i.e., $$w = aw_1 b$$. Intuitively, we can see that starting with the production $$S\rightarrow aSb$$ derives any of this case. Similar argument for the case when $$w$$ starts with $$b$$ and ends with $$a$$.

To be more rigorous, use mathematical induction for the proof. **Assume** all
$$w\in L$$ with $$\|w\|\le 2n$$ can be derived with $$G$$. Take any $$w \in L$$ of $$\|w\|=2n+2$$. If $$w= aw_1b$$ , then $$w_1\in L$$ and $$\|w_1\|=2n$$. Thus by assumption,

$$
S\overset{*}{\Rightarrow}w_1
\\\therefore S \Rightarrow aSb \overset{*}{\Rightarrow}aw_1b = w
$$

Therefore, we proved that $$w$$ can be derived with $$G$$. Similar argument can be made for $$w=bw_1a$$.

Also, we need to investigate the case with $$w = aw_1a$$ or $$w = bw_1b$$. Starting at the left end, we will count +1 for $$a$$ and -1 for $$b$$ . By assumption, final count must be $$0$$ since $$n_a(w) = n_b(w)$$. In the case of $$w=aw_1a$$, the count must be +1 after the first $$a$$, and -1 before the last $$a$$. This implies that there exists some point in the middle that the count is $$0$$. Therefore, $$w$$ can be splitted into two sentences, that is, $$w= w_1w_2$$ , where $$w_1, w_2 \in L$$ and $$\|w_1\|\le 2n$$ and $$\|w_2\|\le 2n$$. Applying production rules, we can see that

$$
S\Rightarrow SS \overset{*}{\Rightarrow}w_1S \overset{*}{\Rightarrow}w_1w_b = w
$$

is possible derivation. Therefore, $$w$$ can be generated by $$G$$.

We choose **basis** as $$n=1$$, and it is clear that inductive assumption is satisfied. Thus, the claim is true for all $$n$$.

We have $$L(G)\subseteq L$$ and $$L\subseteq L(G)$$, therefore $$L(G)=L$$.

## Equivalent Grammars

Normally, a language has many grammars that generate it. Two grammars $$G_1$$ and $$G_2$$ are said to be \***\*\*\*\*\***\*\*\***\*\*\*\*\***equivalent\***\*\*\*\*\***\*\*\***\*\*\*\*\*** if they generate the same language, i.e.,

$$
L(G_1) = L(G_2)
$$

# Automata

## Terminology

An automaton is an abstract model of a digital computer. It has a mechanism for reading input. The input is a string over a given alphabet, written on an **input file**. Also, an automaton can have a **storage.** Both input file and storage is divided into cells, and each cell can hold one symbol from an alphabet. (But two alphabet may not equal.) Finally, an automaon has a control unit, which can be in any one of a finite number of **internal state**, and change its state in some defined manner. The internel state of the next time step is determined by **next-state** and **transition function**. The particular state, input file and storage is called a \***\*\*\*\*\*\*\***\*\*\***\*\*\*\*\*\*\***configuration\***\*\*\*\*\*\*\***\*\*\***\*\*\*\*\*\*\***. A transition from one configuration to the next is called a \***\*\*\*\*\***move\***\*\*\*\*\***.

## Types of Automata

Automata can be distinguished into **deterministic automata** and **nondeterministic automata**. In a deterministic automata, each move is uniquely determined by the current configuration. However, in nondeterministic automata, several move is possible at each point. Thus we can only predict a set of possible actions.

Also, automata can be distinguished into **\*\*\*\***\*\***\*\*\*\***accepter**\*\*\*\***\*\***\*\*\*\*** and \***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***transducer\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***. An accepter can only response “yes”(accepted) or “no”(rejected) for each input string. A transducer is a more general automaton, which can produce strings of symbols as an output.
