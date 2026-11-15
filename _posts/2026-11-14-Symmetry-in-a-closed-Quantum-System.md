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

### § 2.3 Properties of the Density Operator

The density operator $\rho=\sum_i p_i\lvert\psi_i\rangle\langle\psi_i\rvert$ of Eq. (2.6) has the following basic properties.

**1. Hermiticity.** $\rho^\dagger=\rho$, since each $\lvert\psi_i\rangle\langle\psi_i\rvert$ is Hermitian and the $p_i$ are real.

**2. Unit trace.** Using $\langle\psi_i\vert\psi_i\rangle=1$ and Eq. (2.2),

$$
\operatorname{tr}\rho=\sum_i p_i\langle\psi_i\vert\psi_i\rangle=\sum_i p_i=1 .
\tag{2.10}
$$

**3. Positivity.** For any vector $\lvert\phi\rangle$,

$$
\langle\phi\rvert\rho\lvert\phi\rangle=\sum_i p_i\,\big\lvert\langle\phi\vert\psi_i\rangle\big\rvert^2\ \ge\ 0 ,
\tag{2.11}
$$

so $\rho\ge 0$. Together with the first two properties, this characterizes a density operator: any operator that is Hermitian, positive and has unit trace describes a valid state.

**4. Expectation values.** For any observable $A$, $\langle A\rangle=\operatorname{tr}(A\rho)$, as shown in Eq. (2.5).

**5. Purity.** $\operatorname{tr}\rho^2\le 1$, with equality if and only if $\rho$ is a pure state, $\rho=\lvert\psi\rangle\langle\psi\rvert$.

<details class="derivation" markdown="1">
<summary>Show derivation</summary>

Let $\lambda_k$ be the eigenvalues of $\rho$. By properties 1 to 3 they satisfy $\lambda_k\in[0,1]$ and $\sum_k\lambda_k=1$. Since $$\lambda_k^2\le\lambda_k$$ on $[0,1]$,

$$
\operatorname{tr}\rho^2=\sum_k\lambda_k^2\ \le\ \sum_k\lambda_k=1 .
\tag{2.12}
$$

Equality requires $\lambda_k^2=\lambda_k$ for every $k$, so each $\lambda_k$ is $0$ or $1$. Because they sum to $1$, exactly one eigenvalue equals $1$ and the rest vanish. That means $\rho=\lvert\psi\rangle\langle\psi\rvert$ for the corresponding eigenvector, which is a pure state. Conversely, a pure state has eigenvalues $(1,0,\dots,0)$, so $\operatorname{tr}\rho^2=1$.

</details>

with equality only when a single eigenvalue equals $1$ and the rest vanish.

### § 2.4 The Evolution Operator

For a time-independent Hamiltonian $H$, the Schrödinger equation (2.1) is solved by

$$
\lvert\psi(t)\rangle = U(t)\lvert\psi(0)\rangle ,
\qquad U(t)=e^{-iHt/\hbar} ,
\tag{2.13}
$$

where $U(t)$ is the **evolution operator**. It is unitary, $U^\dagger U = UU^\dagger = I$, because $H$ is Hermitian. This is what guarantees that the norm of a state is preserved in time.

Applying Eq. (2.13) to every member of the ensemble in Eq. (2.6), the density operator evolves as

$$
\rho(t) = U(t)\,\rho(0)\,U(t)^\dagger ,
\tag{2.14}
$$

which is the solution of the Von Neumann equation (2.9) for a time-independent $$H$$. It says that the whole evolution is a unitary conjugation of the initial state.

## § 3 Symmetry in the Von Neumann Equation

### § 3.1 Properties of the Von Neumann Equation

The Von Neumann equation can be written as $\dot\rho=\mathcal L\rho$, where $\mathcal L=-\tfrac{i}{\hbar}[H,\,\cdot\,]$ is a linear map acting on operators. It has the following properties.

**1. Linearity.** Since $\mathcal L$ is linear, a mixture $$\rho=\sum_i p_i\rho_i$$ evolves as the mixture of the individual evolutions. It makes no difference whether we mix first and then evolve, or evolve first and then mix. This is what makes density operators a consistent description of ensembles.

**2. Hermiticity is preserved.** If $\rho$ is Hermitian, then $[H,\rho]^\dagger=[\rho,H]=-[H,\rho]$, so $-\tfrac{i}{\hbar}[H,\rho]$ is Hermitian as well.

**3. Trace is preserved.** By cyclicity of the trace,

$$
\frac{d}{dt}\operatorname{tr}\rho=-\frac{i}{\hbar}\operatorname{tr}[H,\rho]=0 .
\tag{3.1}
$$

This is the first of a family of conserved quantities $\operatorname{tr}(\rho^n)$, which we return to below.

**4. Positivity is preserved.** For a time-independent $H$, the solution of Eq. (2.9) is $\rho(t)=U\rho(0)U^\dagger$ with $U=e^{-iHt/\hbar}$. For any $\lvert\phi\rangle$,

$$
\langle\phi\rvert U\rho U^\dagger\lvert\phi\rangle=\langle\phi'\rvert\rho\lvert\phi'\rangle\ \ge\ 0 ,
\qquad \lvert\phi'\rangle=U^\dagger\lvert\phi\rangle ,
\tag{3.2}
$$

so $\rho(t)\ge0$ for all $t$.

**5. Stationary states commute with $H$.** $\dot\rho=0$ if and only if $[H,\rho]=0$. For example, any function of $H$ is stationary, such as the thermal state $e^{-\beta H}/Z$ with $Z=\operatorname{tr}e^{-\beta H}$.

**6. Conserved quantities.** For any time-independent observable $A$,

$$
\frac{d}{dt}\operatorname{tr}(\rho A)=\frac{i}{\hbar}\operatorname{tr}\big(\rho\,[H,A]\big) ,
\tag{3.3}
$$

so every observable commuting with $H$ is conserved. In particular the energy $\operatorname{tr}(\rho H)$ is conserved.

### § 3.2 The Solution Is a Group

Recall that $\rho(t)=U_t\,\rho(0)\,U_t^\dagger$ with $U_t=e^{-iHt/\hbar}$. The family of operators $\{U_t\}$ has more structure than a list of operators. Recall that a **group** is a set with an associative operation, an identity element, and an inverse for every element. The $U_t$ satisfy all of this:

$$
U_tU_s=U_{t+s},\qquad U_0=I,\qquad U_{-t}=U_t^{-1}=U_t^\dagger .
\tag{3.4}
$$

The first relation holds because $H$ commutes with itself, so the exponents simply add. Evolving for a time $s$ and then for a time $t$ is the same as evolving for $t+s$, and every evolution can be undone by running it backwards. This is a **one-parameter group** of unitary operators.

<details class="derivation" markdown="1">
<summary>Show derivation</summary>

To check that $\rho(t)=U_t\rho(0)U_t^\dagger$ solves Eq. (2.9), differentiate. Since $H$ commutes with $U_t$,

$$
\frac{d\rho}{dt}
=-\frac{i}{\hbar}H\,U_t\rho(0)U_t^\dagger+U_t\rho(0)U_t^\dagger\,\frac{i}{\hbar}H
=-\frac{i}{\hbar}\,[H,\rho(t)] .
\tag{3.5}
$$

</details>

### § 3.3 What Does the Evolution Conserve?

Since the evolution is a conjugation, the conserved quantities are easy to find. For any $n$,

$$
\operatorname{tr}\big(\rho(t)^n\big)=\operatorname{tr}\big[(U\rho U^\dagger)^n\big]=\operatorname{tr}\big[U\rho^nU^\dagger\big]=\operatorname{tr}\big(\rho^n\big),
\tag{3.6}
$$

where we used $U^\dagger U=I$ to collapse the product, and then cyclicity of the trace. The same fact is visible in the eigenvalues: if $\rho(0)\lvert v\rangle=\lambda\lvert v\rangle$, then $\rho(t)\,U_t\lvert v\rangle=\lambda\,U_t\lvert v\rangle$. So $\rho(t)$ and $\rho(0)$ have **exactly the same spectrum**.

Two consequences stand out:

- the purity $\operatorname{tr}\rho^2$ is conserved, so a pure state stays pure
- the von Neumann entropy $S(\rho)=-\operatorname{tr}(\rho\ln\rho)$ is conserved, so a mixed state stays exactly as mixed as it started

Unitary evolution can never turn our ignorance about the state into knowledge, or the other way around. The spectrum is the part of $\rho$ that the dynamics cannot touch.

### § 3.4 Group Actions and Orbits

To see why this is a statement about *groups*, we put the conjugation $\rho\mapsto U\rho U^\dagger$ in the language of group actions.

<div class="definition" markdown="1">
A group $G$ **acts** on a set $X$ if every $g\in G$ gives a map $x\mapsto g\cdot x$ such that $e\cdot x=x$ and $g\cdot(h\cdot x)=(gh)\cdot x$. The **orbit** of $x$ is the set $G\cdot x=\{g\cdot x: g\in G\}$ of everything that $x$ can be moved to.
</div>

Let $G=U(d)$ be the group of all $d\times d$ unitary matrices, where $d$ is the dimension of the Hilbert space, and let $X$ be the set of density operators. Define

$$
U\cdot\rho=U\rho U^\dagger .
\tag{3.7}
$$

This is an action: $U\cdot(V\cdot\rho)=UV\rho V^\dagger U^\dagger=(UV)\cdot\rho$. It also sends density operators to density operators, by the argument of Eq. (3.2) together with the fact that trace and Hermiticity are preserved. Time evolution is then a curve $t\mapsto U_t\cdot\rho$ that stays inside a single orbit. The key fact is the following.

<div class="definition" markdown="1">
**Theorem.** Two density operators $\rho$ and $\sigma$ lie in the same orbit of $U(d)$ if and only if they have the same eigenvalues, counted with multiplicity.
</div>

<details class="derivation" markdown="1">
<summary>Show derivation</summary>

($\Rightarrow$) This is Eq. (3.6) and the eigenvector argument above: conjugation by a unitary preserves the spectrum.

($\Leftarrow$) By the spectral theorem, $\rho=VDV^\dagger$ and $\sigma=WDW^\dagger$ for unitaries $V,W$ and the *same* diagonal matrix $D$ of eigenvalues, since the spectra agree. Then

$$
\sigma=WV^\dagger\,\rho\,\big(WV^\dagger\big)^\dagger ,
\tag{3.8}
$$

and $WV^\dagger$ is unitary, so $\sigma\in U(d)\cdot\rho$.

</details>

So the orbits are labelled exactly by spectra: the set of density operators splits into layers, one for each possible spectrum, and unitary dynamics lives inside a single layer.

One subtlety is worth stating clearly. A *single* Hamiltonian only traces out a curve inside an orbit. The whole orbit is what all Hamiltonians together can reach. By the spectral theorem every unitary can be written as $U=e^{-iK}$ for some Hermitian $K$, so every element of $U(d)$ is the evolution of some Hamiltonian over some time.

### § 3.5 The Qubit: Orbits Are Spheres

For a single qubit, $d=2$ and the picture is concrete. Use the Pauli matrices

$$
\sigma_x=\begin{pmatrix}0&1\\1&0\end{pmatrix},\quad
\sigma_y=\begin{pmatrix}0&-i\\i&0\end{pmatrix},\quad
\sigma_z=\begin{pmatrix}1&0\\0&-1\end{pmatrix}.
\tag{3.9}
$$

Together with $I$ they form a basis of the $2\times2$ Hermitian matrices, and fixing the trace to $1$ fixes the coefficient of $I$ to $\tfrac12$. So every qubit density operator can be written as

$$
\rho=\tfrac12\big(I+\vec r\cdot\vec\sigma\big),\qquad \vec r\in\mathbb R^3 .
\tag{3.10}
$$

Since $(\vec r\cdot\vec\sigma)^2=\lvert\vec r\rvert^2 I$, the eigenvalues of $\vec r\cdot\vec\sigma$ are $\pm\lvert\vec r\rvert$, and the eigenvalues of $\rho$ are

$$
\lambda_\pm=\frac{1\pm\lvert\vec r\rvert}{2} .
\tag{3.11}
$$

Positivity of $\rho$ is exactly $\lvert\vec r\rvert\le1$. This gives the **Bloch ball**: pure states have $\lvert\vec r\rvert=1$ and sit on the surface, mixed states are inside, and the maximally mixed state $I/2$ is the center. Also $\operatorname{tr}\rho^2=\tfrac12(1+\lvert\vec r\rvert^2)$.

By Eq. (3.11) the spectrum is determined by $\lvert\vec r\rvert$ alone, so the theorem of § 3.4 says that the orbits are the **concentric spheres** $\lvert\vec r\rvert=\text{const}$, and the center is an orbit by itself.

<!-- INTERACTIVE: Bloch ball with a slider for |r| and a trajectory that stays on its sphere for any H. -->

For a fixed Hamiltonian $H=\tfrac{\hbar\omega}{2}\,\hat n\cdot\vec\sigma$, the von Neumann equation becomes a