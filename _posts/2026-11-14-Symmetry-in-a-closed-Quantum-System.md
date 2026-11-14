---
layout: post
title: "Draft: Symmetry in a Quantum System"
date: 2026-11-14
---


## &sect; 1. Introduction and Motivation

When quantum mechanics was first established, it shook the worldview of many physicists. Our classical model of the world had no room for non-deterministic models.
 Even Einstein is quoted as saying:

<blockquote class="quote">
  <p>God does not play dice with the universe.</p>
  <footer>— Albert Einstein</footer>
</blockquote>

In such a non-deterministic model of the universe, can symmetry, or the ideas of group theory, introduce some determinism?

We will answer that question in this blog.

## &sect; 2. From Schrödinger to Von Neumann

The Schrödinger equation gives a complete description of an isolated quantum system, under the following assumptions:

1. The state of the system is described by a unit vector $\lvert\psi\rangle$ in a Hilbert space.
2. Every observable is represented by a Hermitian operator $A$, and its expectation value in the state $\lvert\psi\rangle$ is $\langle\psi\rvert A\lvert\psi\rangle$.
3. The system is isolated, so its time evolution is linear and unitary.
4. We know the state of the system exactly (a *pure state*).

Under these assumptions, the state evolves according to

$$
i\hbar \frac{d}{dt}\lvert\psi(t)\rangle = H\lvert\psi(t)\rangle ,
\tag{2.1}
$$

where $H$ is the Hamiltonian of the system.

 Assumption 4 is the one we now relax. To do so, we introduce a new way of describing a quantum system, in terms of the **density operator** $\rho$.

To motivate the idea, imagine a machine that prepares quantum systems in certain states. For instance, it could be an oven producing spin-1/2 particles, or a quantum-optics setup producing photons. Suppose the apparatus is imperfect, so it does not always produce the same state. That is, it produces the state $\lvert\psi_1\rangle$ with probability $p_1$, the state $\lvert\psi_2\rangle$ with probability $p_2$, and so on. Here we are introducing a *classical* uncertainty: each $\lvert\psi_i\rangle$ is a quantum state, but we simply do not know which one comes out of the machine. We may have as many $p_i$ as we like, provided they satisfy the usual properties of a probability distribution:

$$
p_i \in [0,1], \qquad \sum_i p_i = 1 .
\tag{2.2}
$$

Now let $A$ be an observable. If the state is $\lvert\psi_1\rangle$, the expectation value of $A$ is $\langle\psi_1\rvert A\lvert\psi_1\rangle$. If it is $\lvert\psi_2\rangle$, it is $\langle\psi_2\rvert A\lvert\psi_2\rangle$. The actual expectation value must therefore be an average of quantum averages:

$$
\langle A\rangle = \sum_i p_i \,\langle\psi_i\rvert A\lvert\psi_i\rangle .
\tag{2.3}
$$

We simply weight each possible expectation value $\langle\psi_i\rvert A\lvert\psi_i\rangle$ by the probability $p_i$ that it occurs.

It is important to realize that this type of average cannot, in general, be written as $\langle\varphi\rvert A\lvert\varphi\rangle$ for some single ket $\lvert\varphi\rangle$. If we want to attribute a "state" to our system, we must therefore generalize the idea of a ket. To do so, we write

$$
\langle\psi_i\rvert A\lvert\psi_i\rangle = \operatorname{tr}\!\big(A\,\lvert\psi_i\rangle\langle\psi_i\rvert\big).
\tag{2.4}
$$

Substituting this into Eq. (2.3) and using the linearity of the trace gives

$$
\langle A\rangle
= \sum_i p_i \operatorname{tr}\!\big(A\,\lvert\psi_i\rangle\langle\psi_i\rvert\big)
= \operatorname{tr}\!\Big(A \sum_i p_i \lvert\psi_i\rangle\langle\psi_i\rvert\Big).
\tag{2.5}
$$

This motivates the following definition.

<div class="definition" markdown="1">
The **density operator** (or density matrix) of the system is
</div>

$$
\rho = \sum_i p_i \,\lvert\psi_i\rangle\langle\psi_i\rvert ,
\tag{2.6}
$$

so that the expectation value of any observable takes the compact form $$\langle A\rangle = \operatorname{tr}(A\rho)$$.
