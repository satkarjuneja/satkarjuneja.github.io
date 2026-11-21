---
layout: post
title: "Draft: Symmetry in a Quantum System"
date: 2026-11-14
---

## § 1. Introduction and Motivation

Quantum mechanics is known for its confusing conclusions. Richard Feynman put it best:

<blockquote class="quote">
  <p>I think I can safely say that nobody understands quantum mechanics.</p>
  <footer>— Richard Feynman, <em>The Character of Physical Law</em></footer>
</blockquote>

And yet it is the most successful theory we have: it correctly explains almost every phenomenon observed in experiments.

So how does this theory handle the most important aspect of our world, **dynamics**? Everything we care about changes with time, and a theory that cannot say how things change is not much use. In this piece we ask the following question:

**Given a quantum system undergoing unitary evolution, which properties of its state are invariant under the dynamics?**

To answer it, we first reformulate quantum mechanics using density operators (§ 2). Then we study the structure of the evolution itself (§ 3).
We will answer that question in this piece.

## § 2. From Schrödinger to Von Neumann

To see the simplicity of nature, we shall now step away from language of the Schrödinger equation, and move to a cleaner model.
<br>
<br>
This requires a bit of setup, but I promise it will be worth it ;)

### § 2.1 What is a density operator?

The Schrödinger equation gives a complete description of an isolated quantum system, under four standard assumptions (collapsed below).

<details class="derivation" markdown="1">
<summary>Show assumptions</summary>

1. The state of the system is described by a unit vector $\lvert\psi\rangle$ in a Hilbert space.
2. Every observable is represented by a Hermitian operator $A$, and its expectation value in the state $\lvert\psi\rangle$ is $\langle\psi\rvert A\lvert\psi\rangle$.
3. The system is isolated, so its time evolution is linear and unitary.
4. We know the state of the system exactly (a *pure state*).

</details>

Under these assumptions, the state evolves according to

$$
i\hbar \frac{d}{dt}\lvert\psi(t)\rangle = H\lvert\psi(t)\rangle ,
\tag{2.1}
$$

where $H$ is the Hamiltonian of the system.

Now,let's relax assumption 4 and introduce a new way of describing a quantum system, in terms of 

**The Density Operator** $\rho$.

Why would we ever need to describe a system like this ?
<br>
 Imagine a machine that prepares quantum systems in certain states. <br>
It could be an oven shooting out spin-1/2 particles, or a quantum-optics setup producing photons. <br>

Now suppose the apparatus is imperfect (perhaps a toaster that always burns your bread), so it does not always produce the same state. That is, it produces the state $\lvert\psi_1\rangle$ with probability $p_1$, the state $\lvert\psi_2\rangle$ with probability $p_2$, and so on. Here we are introducing a *classical* uncertainty: each $\lvert\psi_i\rangle$ is a quantum state, but we simply do not know which one comes out of the machine! We may have as many $p_i$ as we like, provided they satisfy the usual properties of a probability distribution.

Now let $A$ be an observable. If the state is $\lvert\psi_1\rangle$, the expectation value of $A$ is $\langle\psi_1\rvert A\lvert\psi_1\rangle$. If it is $\lvert\psi_2\rangle$, it is $\langle\psi_2\rvert A\lvert\psi_2\rangle$ (I sure hope you paid attention in Linear Algebra![^linear]).
<br>
The actual expectation value must therefore be an average of quantum averages:

$$
\langle A\rangle = \sum_i p_i \,\langle\psi_i\rvert A\lvert\psi_i\rangle .
\tag{2.3}
$$

We simply weight each possible expectation value $\langle\psi_i\rvert A\lvert\psi_i\rangle$ by the probability $p_i$ that it occurs.

It is important to realize that this type of average cannot, in general, be written as $\langle\varphi\rvert A\lvert\varphi\rangle$ for some single ket $\lvert\varphi\rangle$ (as can be seen above). If we want to attribute a "state" to our system, we must therefore generalize the idea of a ket. To do so, we write

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

With this definition, the expectation value of any observable takes the compact form $\langle A\rangle = \operatorname{tr}(A\rho)$.

This has a important caveat: There can be different ensembles representing the same density operator. (but let's not think about that right now)

I would like to emphasize what is being done here. We have introduced a classical uncertainty in a quantum system! even electrons and photons can't save themselves from noisy environments.[^classical]

[^classical]: Usually, when we talk about uncertainty in the quantum world, we are talking about Heisenberg’s Uncertainty Principle, built-in fuzziness of nature where a particle simply doesn't have a definite position and momentum at the same time. The uncertainty discussed here is purely classical


[^linear]: Don't worry you can still follow along if you didn't.

### § 2.2 Deriving the Von Neumann Equation
After all this setup we can now move on to the actual equation we are after ;)
<br><br>
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

Since $H$ is the same for every member of the ensemble, it factors out of the sum, and the sum is just $\rho$ again.

</details>

The result is the **Von Neumann equation**:

$$
i\hbar \frac{d\rho}{dt} = H\rho - \rho H = [H,\rho] .
\tag{2.9}
$$

It is the Schrödinger equation rewritten for the density operator, and it holds whether or not the state is pure!!

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

That's a lot of properties, but we still need one more thing to describe the real world

<p class="aside">cue the Star Wars music…<br>a long time ago, in a Hilbert space far, far away…</p>

### § 2.4 The Evolution Operator

The systems we observe are seldom independent of time (That would be a interesting world), to capture the effect of time we define a Evolution Operator.

For a time-independent Hamiltonian $H$, the Schrödinger equation (2.1) is solved by

$$
\lvert\psi(t)\rangle = U(t)\lvert\psi(0)\rangle ,
\qquad U(t)=e^{-iHt/\hbar} ,
\tag{2.13}
$$

where $U(t)$ is the **evolution operator**. It is unitary, $U^\dagger U = UU^\dagger = I$, This guarantees that the norm of a state is preserved in time. (Implications of this is huge, which we will realise later)

Applying Eq. (2.13) to every member of the ensemble in Eq. (2.6), the density operator evolves as

$$
\rho(t) = U(t)\,\rho(0)\,U(t)^\dagger ,
\tag{2.14}
$$

which is the solution of the Von Neumann equation (2.9) for a time-independent $H$. It says that the whole evolution is a unitary conjugation of the initial state.

### § 2.5 The Bloch Sphere

Since the evolution operator preserves the norm of a state, the evolution of a single qubit can be seen as a rotation of a point on a sphere. This sphere is called the **Bloch sphere**, and it lets us see the conjugation in Eq. (2.14) as an arrow turning in 3D space.

Every qubit state corresponds to a point in the unit ball. Pure states sit on the surface, and mixed states sit inside it.
(don't worry about the formulas just look as the visualization)

<details class="derivation" markdown="1">
<summary>Show the math</summary>

The Pauli matrices are

$$
\sigma_x=\begin{pmatrix}0&1\\1&0\end{pmatrix},\quad
\sigma_y=\begin{pmatrix}0&-i\\i&0\end{pmatrix},\quad
\sigma_z=\begin{pmatrix}1&0\\0&-1\end{pmatrix}.
\tag{2.15}
$$

Together with $I$ they form a basis of the $2\times 2$ Hermitian matrices, and fixing the trace to $1$ fixes the coefficient of $I$ to $\tfrac12$. Using Hermiticity and unit trace from § 2.3, every qubit density operator can therefore be written as

$$
\rho = \frac{1}{2}\big(I + \vec n\cdot\vec\sigma\big),
\qquad \vec n = (n_x, n_y, n_z)\in\mathbb R^3 .
\tag{2.16}
$$

Since $$(\vec n\cdot\vec\sigma)^2=\lvert\vec n\rvert^2 I$$, the eigenvalues of $$\vec n\cdot\vec\sigma$$ are $$\pm\lvert\vec n\rvert$$, and the eigenvalues of $$\rho$$ are

$$
\lambda_\pm=\frac{1\pm\lvert\vec n\rvert}{2} .
\tag{2.17}
$$

Positivity of $\rho$ is therefore exactly $\lvert\vec n\rvert\le 1$. Pure states have $\lvert\vec n\rvert=1$, mixed states have $\lvert\vec n\rvert<1$, and the maximally mixed state $I/2$ sits at the center. The purity is $$\operatorname{tr}\rho^2=\tfrac12\big(1+\lvert\vec n\rvert^2\big)$$.

Finally, the components of $$\vec n$$ are the spin expectation values:

$$
\langle\sigma_i\rangle=\operatorname{tr}(\rho\,\sigma_i)=n_i .
\tag{2.18}
$$

</details>

Drag the arrow below, or use the sliders.

{% include bloch.html %}

The components $$n_x, n_y, n_z$$ shown above are exactly the measurable spin expectations $$\langle\sigma_x\rangle, \langle\sigma_y\rangle, \langle\sigma_z\rangle$$.

Now let us see what the Von Neumann equation does to this arrow. For a Hamiltonian $H=\tfrac{\hbar\omega}{2}\,\hat m\cdot\vec\sigma$, where $\hat m$ is a unit vector, Eq. (2.9) becomes a rotation:

$$
\dot{\vec n}=\omega\,\hat m\times\vec n .
\tag{2.19}
$$

<details class="derivation" markdown="1">
<summary>Show derivation</summary>

From $$\sigma_i\sigma_j=\delta_{ij}I+i\epsilon_{ijk}\sigma_k$$ we get $$(\vec a\cdot\vec\sigma)(\vec b\cdot\vec\sigma)=\vec a\cdot\vec b\,I+i(\vec a\times\vec b)\cdot\vec\sigma$$, so

$$
[\vec a\cdot\vec\sigma,\ \vec b\cdot\vec\sigma]=2i\,(\vec a\times\vec b)\cdot\vec\sigma .
\tag{2.20}
$$

The identity part of $\rho$ commutes with everything, so only $\vec n\cdot\vec\sigma$ contributes:

$$
\dot\rho=-\frac{i}{\hbar}[H,\rho]
=-\frac{i}{\hbar}\cdot\frac{\hbar\omega}{4}\,[\hat m\cdot\vec\sigma,\ \vec n\cdot\vec\sigma]
=\frac{\omega}{2}\,(\hat m\times\vec n)\cdot\vec\sigma ,
\tag{2.21}
$$

and comparing with $$\dot\rho=\tfrac12\dot{\vec n}\cdot\vec\sigma$$ gives Eq. (2.19).

</details>

This is a rotation about $\hat m$ at angular speed $\omega$, so the arrow travels along a circle and its length $\lvert\vec n\rvert$ never changes. This matches Eq. (2.17), since the eigenvalues of $\rho$, and with them the purity, are conserved by unitary evolution. In the visualization, moving the arrow around while keeping $r$ fixed therefore corresponds to a possible evolution of the state, while changing $r$ would need something that is not unitary.

## § 3 Symmetry in the Von Neumann Equation

### § 3.1 Properties of the Von Neumann Equation

The Von Neumann equation can be written as $\dot\rho=\mathcal L\rho$, where $\mathcal L=-\tfrac{i}{\hbar}[H,\,\cdot\,]$ is a linear map acting on operators. It has the following properties.

**1. Linearity.** Since $\mathcal L$ is linear, a mixture $$\rho=\sum_i p_i\rho_i$$ evolves as the mixture of the individual evolutions. It makes no difference whether we mix first and then evolve, or evolve first and then mix!
<br>
This is what makes density operators a consistent description of classical ensembles. Linearity is special to this equation, and we will see in § 3.5 that the structure uncovered below survives without it.

**2. Trace is preserved.** By cyclicity of the trace,

$$
\frac{d}{dt}\operatorname{tr}\rho=-\frac{i}{\hbar}\operatorname{tr}[H,\rho]=0 .
\tag{3.1}
$$

This is the first of a family of conserved quantities $\operatorname{tr}(\rho^n)$, which we return to below.

**3. Positivity is preserved.** For a time-independent $H$, the solution of Eq. (2.9) is $\rho(t)=U\rho(0)U^\dagger$ with $U=e^{-iHt/\hbar}$. For any $\lvert\phi\rangle$,

$$
\langle\phi\rvert U\rho U^\dagger\lvert\phi\rangle=\langle\phi'\rvert\rho\lvert\phi'\rangle\ \ge\ 0 ,
\qquad \lvert\phi'\rangle=U^\dagger\lvert\phi\rangle ,
\tag{3.2}
$$

so $\rho(t)\ge0$ for all $t$.

**4. Conserved quantities.** For any time-independent observable $A$,

$$
\frac{d}{dt}\operatorname{tr}(\rho A)=\frac{i}{\hbar}\operatorname{tr}\big(\rho\,[H,A]\big) ,
\tag{3.3}
$$

so every observable commuting with $H$ is conserved. In particular the energy $\operatorname{tr}(\rho H)$ is conserved.

### § 3.2 The Evolution Operators Form a Group

<details class="derivation" markdown="1">
<summary>Show the definition of a group</summary>

A **group** is a set $G$ together with an operation $\cdot$ that satisfies four rules:

1. **Closure:** for all $a,b\in G$, the product $a\cdot b$ is also in $G$.
2. **Associativity:** $(a\cdot b)\cdot c=a\cdot(b\cdot c)$ for all $a,b,c\in G$.
3. **Identity:** there is an element $e\in G$ with $e\cdot a=a\cdot e=a$ for all $a\in G$.
4. **Inverses:** for every $a\in G$ there is an element $a^{-1}\in G$ with $a\cdot a^{-1}=a^{-1}\cdot a=e$.

Below, the set is $\{U_t\}$, the operation is matrix multiplication, the identity is $U_0=I$, and the inverse of $U_t$ is $U_{-t}$.

</details>

Recall that $\rho(t)=U_t\,\rho(0)\,U_t^\dagger$ with $U_t=e^{-iHt/\hbar}$. We shall now see that the family of operators $\{U_t\}$ has more structure than a mere list of operators. The $U_t$ satisfy all the properties of a group:

$$
U_tU_s=U_{t+s},\qquad U_0=I,\qquad U_{-t}=U_t^{-1}=U_t^\dagger .
\tag{3.4}
$$

The first relation holds because $H$ commutes with itself, so the exponents simply add. Evolving for a time $s$ and then for a time $t$ is the same as evolving for a time $t+s$, and every evolution can be undone by running it backwards. This is a **one-parameter group** of unitary operators.

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

### § 3.3 What path can the evolution follow?

<details class="derivation" markdown="1">
<summary>Show the definition of conjugation</summary>

**Conjugating** an operator $A$ by an invertible operator $V$ means forming

$
A \;\longmapsto\; V A V^{-1} .
$

For a unitary $U$ we have $U^{-1}=U^\dagger$, so conjugation reads $A\mapsto UAU^\dagger$, which is exactly the form of the evolution in Eq. (2.14).

If you know linear algebra, this might look familiar. It is a **similarity transformation**, the same operation as a change of basis. Matrices related by conjugation describe the same linear map in different bases, and they always have the same eigenvalues.

</details>

Since the evolution is a conjugation, the conserved quantities are easy to find. For any $n$,

$$
\operatorname{tr}\big(\rho(t)^n\big)=\operatorname{tr}\big[(U\rho U^\dagger)^n\big]=\operatorname{tr}\big[U\rho^nU^\dagger\big]=\operatorname{tr}\big(\rho^n\big),
\tag{3.6}
$$

where we used $U^\dagger U=I$ to collapse the product, and then the cyclicity of the trace. The same fact is visible in the eigenvalues: if $$\rho(0)\lvert v\rangle=\lambda\lvert v\rangle$$, then $$\rho(t)\,U_t\lvert v\rangle=\lambda\,U_t\lvert v\rangle$$. So $\rho(t)$ and $\rho(0)$ have **exactly the same spectrum**.

Two consequences stand out:

- The purity $\operatorname{tr}\rho^2$ is conserved, so a pure state stays pure.
- The von Neumann entropy $S(\rho)=-\operatorname{tr}(\rho\ln\rho)$ is conserved, so a mixed state stays exactly as mixed as it started.

Unitary evolution can never turn our ignorance about the state into knowledge, or the other way around. The spectrum is the part of $\rho$ that the dynamics cannot touch.

That means the classical uncertainty we introduced at the start always remains there throughout the evolution.
### § 3.4 Group Actions and Orbits

Now, we shall formalize what our state can explore, we put the conjugation $\rho\mapsto U\rho U^\dagger$ in the language of group actions.

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
<!-- add footnote of what multiplicity means -->
<details class="derivation" markdown="1">
<summary>Show derivation</summary>

($\Rightarrow$) This is Eq. (3.6) and the eigenvector argument above: conjugation by a unitary preserves the spectrum.

($\Leftarrow$) A Hermitian matrix has an orthonormal basis of eigenvectors. Let $\lvert e_k\rangle$ be such a basis for $\rho$, and $\lvert f_k\rangle$ one for $\sigma$. Since the two spectra agree (with multiplicity), we can number the vectors so that both have the same eigenvalue $\lambda_k$ for the same $k$:

$$
\rho=\sum_k\lambda_k\lvert e_k\rangle\langle e_k\rvert,\qquad
\sigma=\sum_k\lambda_k\lvert f_k\rangle\langle f_k\rvert .
\tag{3.8}
$$

Define the operator that sends the first basis to the second,

$$
U=\sum_k\lvert f_k\rangle\langle e_k\rvert .
\tag{3.9}
$$

It is unitary, since $$U^\dagger U=\sum_{k,l}\lvert e_k\rangle\langle f_k\vert f_l\rangle\langle e_l\rvert=\sum_k\lvert e_k\rangle\langle e_k\rvert=I$$
<br>
And because $U\lvert e_k\rangle=\lvert f_k\rangle$,

$$
U\rho U^\dagger=\sum_k\lambda_k\,U\lvert e_k\rangle\langle e_k\rvert U^\dagger=\sum_k\lambda_k\lvert f_k\rangle\langle f_k\rvert=\sigma ,
\tag{3.10}
$$

so $\sigma\in U(d)\cdot\rho$.

$$
\sigma=WV^\dagger\,\rho\,\big(WV^\dagger\big)^\dagger ,
\tag{3.8}
$$

and $WV^\dagger$ is unitary, so $\sigma\in U(d)\cdot\rho$.

</details>

So the orbits are labelled exactly by spectra: the set of density operators splits into layers, one for each possible spectrum, and unitary dynamics lives inside a single layer.

One caveat though. A *single* Hamiltonian only traces out a curve inside an orbit. The whole orbit is what all Hamiltonians together can reach. By the spectral theorem(which we basically derived above) every unitary can be written as $U=e^{-iK}$ for some Hermitian $K$, so every element of $U(d)$ is the evolution of some Hamiltonian over some time.


### § 3.5 The Lax Form

Eq. (2.9) can be written in a way that hides the quantum mechanics. Define the matrix $M=-\tfrac{i}{\hbar}H$, so that

$$
\dot\rho=[M,\rho] .
\tag{3.11}
$$

An equation of the form

$$
\dot L=[M,L]
\tag{3.12}
$$

for matrices $L(t)$ and $M(t)$ is called a **Lax equation**, after Peter Lax, who introduced it in 1968 to study nonlinear wave equations. The Von Neumann equation is the simplest case: $M$ is a fixed matrix, so the equation is linear in $L=\rho$. In general $M$ may depend on time, and even on $L$ itself, and then the equation is **nonlinear**. The conservation law of § 3.3 survives anyway.

Suppose $L(t)$ solves Eq. (3.12), and let $U(t)$ solve $\dot U=MU$ with $U(0)=I$. Then

$$
L(t)=U(t)\,L(0)\,U(t)^{-1} .
\tag{3.13}
$$

So $L(t)$ is a conjugation of $L(0)$, exactly as in § 3.3, and **the spectrum of $L$ is conserved**. Equivalently, every $\operatorname{tr}L^n$ is conserved. If $M$ is anti-Hermitian, as it is for the Von Neumann equation, then $U(t)$ is unitary and the flow stays inside an orbit of § 3.4.

<details class="derivation" markdown="1">
<summary>Show derivation</summary>

The matrix $U(t)$ is invertible, since it solves a linear differential equation and $\det U=\exp\int_0^t\operatorname{tr}M$. Using $\tfrac{d}{dt}U^{-1}=-U^{-1}\dot U\,U^{-1}=-U^{-1}M$,

$$
\frac{d}{dt}\big(U^{-1}LU\big)=-U^{-1}MLU+U^{-1}(ML-LM)U+U^{-1}LMU=0 .
$$

So $U^{-1}LU$ is constant, and it equals $L(0)$ at $t=0$. This gives Eq. (3.13).

The statement about traces also has a one-line proof that does not use $U$. By cyclicity of the trace,

$$
\frac{d}{dt}\operatorname{tr}L^n=n\operatorname{tr}\big(L^{n-1}[M,L]\big)=n\Big(\operatorname{tr}(L^nM)-\operatorname{tr}(L^nM)\Big)=0 .
$$

</details>

The conservation law of § 3.3 is therefore not special to quantum mechanics. It is a feature of the commutator form itself. Equations of this type are central in the study of integrable systems, a subject we only point to here.


### § 3.6 Symmetries of the Hamiltonian

So far the group $U(d)$ acted on states from outside. The symmetries of the system itself form a smaller group. Suppose a unitary $V$ commutes with $H$. If $\rho(t)$ solves Eq. (2.9), then $\sigma(t)=V\rho(t)V^\dagger$ solves it too:

$$
\dot\sigma=-\frac{i}{\hbar}V[H,\rho]V^\dagger=-\frac{i}{\hbar}[VHV^\dagger,\sigma]=-\frac{i}{\hbar}[H,\sigma] .
\tag{3.17}
$$

So a symmetry sends solutions to solutions: transforming first and evolving second gives the same answer as evolving first and transforming second. The set of all such $V$ is a group, the **symmetry group of $H$**. Its infinitesimal generators are Hermitian operators commuting with $H$, and by Eq. (3.3) these are exactly the conserved quantities.

## § 4 Conclusion

We started by asking whether symmetry can bring some determinism into a quantum world. Both the Schrödinger and the von Neumann equations are already deterministic. What the group structure adds is a precise statement of what the dynamics can never change. The evolution is a conjugation, a group action, and its orbits are labelled by the spectrum of $\rho$. So a state keeps the same purity, the same entropy, the same "amount of ignorance". Symmetries of $H$ add conserved quantities on top.

The Lax form of § 3.5 shows that this is not special to quantum mechanics. Any equation of the form $\dot L=[M,L]$ is a conjugation flow, even a nonlinear one such as the Toda chain, and so conserves the spectrum of $L$.

The picture does have limits. Unitary evolution never leaves its orbit, but a noisy evolution can, for example by turning a pure state into a mixed one and so changing its spectrum. Describing such evolution takes a larger framework, the Lindblad equation. In that setting the group of evolutions loses its inverses, and one is left with a semigroup.

## References

1. P. D. Lax, "Integrals of nonlinear equations of evolution and solitary waves", *Comm. Pure Appl. Math.* 21 (1968).
2. H. Flaschka, "The Toda lattice. I. Existence of integrals", *Phys. Rev. B* 9 (1974).
3. M. Toda, *Theory of Nonlinear Lattices*, Springer.
4. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press (chapter 2).
5. M. A. Armstrong, *Groups and Symmetry*, Springer.