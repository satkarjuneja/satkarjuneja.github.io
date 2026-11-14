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

## &sect; 2 From Schrödinger to Von Neumann

### &sect; 2.1 What is a density operator?
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

$$
\rho = \sum_i p_i \,\lvert\psi_i\rangle\langle\psi_i\rvert ,
\tag{2.6}
$$

</div>

so that the expectation value of any observable takes the compact form $$\langle A\rangle = \operatorname{tr}(A\rho)$$.

### § 2.1 Deriving the Von Neumann Equation

Differentiating the density operator in time and using the Schrödinger equation gives a closed equation for $\rho$. The full derivation is collapsed below.

<details class="derivation" markdown="1">
<summary>Show derivation</summary>

Each state in the ensemble evolves under Eq. (2.1), and the probabilities $p_i$ are fixed by the preparation, so they do not depend on time. Taking the adjoint of Eq. (2.1), and using $$H^\dagger = H$$, gives

$$
-i\hbar \frac{d}{dt}\langle\psi_i(t)\rvert = \langle\psi_i(t)\rvert H .
\tag{2.7}
$$

Now differentiate Eq. (2.6) with the product rule and substitute Eqs. (2.1) and (2.7):

$$
i\hbar \frac{d\rho}{dt}
= \sum_i p_i \Big( \big(i\hbar\,\lvert\dot\psi_i\rangle\big)\langle\psi_i\rvert + \lvert\psi_i\rangle\big(i\hbar\,\langle\dot\psi_i\rvert\big) \Big)
= \sum_i p_i \Big( H\lvert\psi_i\rangle\langle\psi_i\rvert - \lvert\psi_i\rangle\langle\psi_i\rvert H \Big).
\tag{2.8}
$$

Since $$H$$ is the same for every member of the ensemble, it factors out of the sum, and the sum is just $$\rho$$ again.

</details>

The result is the **Von Neumann equation**:

$$
i\hbar \frac{d\rho}{dt} = H\rho - \rho H = [H,\rho] .
\tag{2.9}
$$

It is the Schrödinger equation rewritten for the density operator, and it holds whether or not the state is pure.