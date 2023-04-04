---
layout: post
title: Introduction (ii)
tags: [MLDL]
permalink: /2023-spring/mldl/intro-2
---

# Introduction (ii)

# Formal version of ML categorization

- Supervised Learning
  - Given $$D=\{X_i, Y_i\}$$, learn a model or a function $$F: X_k \rightarrow Y_k$$
- Unsupervised Learning
  - Given $$D = \{X_i\}$$, group the data into $$Y$$ classes using a model $$F : X_i \rightarrow Y_j$$
- Self-supervised Learning
  - Given $$D=\{X_i\}$$, group the data into $$Y$$ classes, pretrain a model $$F: X_i \rightarrow Y_j$$
  - Then, fine-tune the pretrained model for supervised task
- Semi-supervised Learning
  - Given $$D=\{\{X_i, Y_i\}, \{X_j\}\}$$, learn a model or a function $$F: X_k \rightarrow Y_k$$
  - Some data has its label, but others don’t
- Active Learning
  - Given $$D = \{\{X_i, Y_i\}, \{X_j\}\}$$, learn a function $$F_1 : \{X_j\} \rightarrow x_k$$ to maximize the success of the supervised learning function $$F_2 : \{X_i, x_k\} \rightarrow Y$$
  - $$x_k$$ : psuedo-labeled sample
- Reinforcement Learning
  - Reasoning under uncertainty
  - Learn actions in order to maximize cumulative reward
  - Given $$D = \{environment,\, action,\, reward\}$$, learn a policy and value functions
    - Policy: $$F_1 : \{e, r\} \rightarrow a$$
    - Value: $$F_2: \{a, e\} \rightarrow r$$

# Cost and accuracy of learning paradigms

- Depends on how much supervision is required
- Supervised > Active Learning > Semi-superised > Self-supervised
