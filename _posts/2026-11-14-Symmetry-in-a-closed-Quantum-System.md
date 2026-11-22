---
layout: post
title: "Dynamics in a Quantum System"
date: 2026-11-14
---

## § 1. Introduction and Motivation

Quantum mechanics is known for its confusing conclusions and quirky features. Richard Feynman put it best:

<blockquote class="quote">
  <p>I think I can safely say that nobody understands quantum mechanics.</p>
  <footer>— Richard Feynman, <em>The Character of Physical Law</em></footer>
</blockquote>

And yet somehow it is the most successful theory we have: it correctly explains almost every phenomenon observed in experiments.

So how does this theory handle the most important aspect of our world, **dynamics**? Everything we care about changes with time, and a theory that cannot say how things change is not much use. In this piece we ask the following question:

**Given a quantum system undergoing unitary evolution, which properties of its state are invariant under the dynamics?**

To answer it, we first reformulate quantum mechanics using density operators (§ 2). Then we study the structure of the evolution itself (§ 3) and generalise it.

## § 2. From Schrödinger to Von Neumann

To see the simplicity of nature, we shall now step away from the language of the Schrödinger equation and move to a cleaner model.
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

Now, let's relax assumption 4 and introduce a new way of describing a quantum system, in terms of

**The Density Operator** $\rho$.

Why would we ever need to describe a system like this?
<br>
Imagine a machine that prepares quantum systems in certain states. <br>
It could be an oven shooting out spin-1/2 particles, or a quantum-optics setup producing photons. <br>

Now suppose the apparatus is imperfect (perhaps a toaster that always burns your bread), so it does not always produce the same state. That is, it produces the state $\lvert\psi_1\rangle$ with probability $p_1$, the state $\lvert\psi_2\rangle$ with probability $p_2$, and so on. Here we are introducing a *classical* uncertainty: each $\lvert\psi_i\rangle$ is a quantum state, but we simply do not know which one comes out of the machine! We may have as many $p_i$ as we like, provided they satisfy the usual properties of a probability distribution.

Now let $A$ be an observable. If the state is $\lvert\psi_1\rangle$, the expectation value of $A$ is $\langle\psi_1\rvert A\lvert\psi_1\rangle$. If it is $\lvert\psi_2\rangle$, it is $\langle\psi_2\rvert A\lvert\psi_2\rangle$ (I sure hope you paid attention in Linear Algebra![^linear]).
<br>
The actual expectation value must therefore be an average of quantum averages:

$$
\langle A\rangle = \sum_i p_i \,\langle\psi_i\rvert A\lvert\psi_i\rangle .
\tag{2.2}
$$

We simply weight each possible expectation value $\langle\psi_i\rvert A\lvert\psi_i\rangle$ by the probability $p_i$ that it occurs.

Now, we can see that in general this kind of average cannot be written as $\langle\varphi\rvert A\lvert\varphi\rangle$ for some single ket $\lvert\varphi\rangle$ (as can be seen above). If we want to attribute a "state" to our system, we must therefore generalize the idea of a ket. To do so, we write

$$
\langle\psi_i\rvert A\lvert\psi_i\rangle = \operatorname{tr}\!\big(A\,\lvert\psi_i\rangle\langle\psi_i\rvert\big).
\tag{2.3}
$$

Substituting this into Eq. (2.2) and using the linearity of the trace gives

$$
\langle A\rangle
= \sum_i p_i \operatorname{tr}\!\big(A\,\lvert\psi_i\rangle\langle\psi_i\rvert\big)
= \operatorname{tr}\!\Big(A \sum_i p_i \lvert\psi_i\rangle\langle\psi_i\rvert\Big).
\tag{2.4}
$$

This motivates the following definition.

<div class="definition" markdown="1">
The **density operator** (or density matrix) of the system is

$$
\rho = \sum_i p_i \,\lvert\psi_i\rangle\langle\psi_i\rvert ,
\tag{2.5}
$$

</div>

With this definition, the expectation value of any observable takes the compact form $\langle A\rangle = \operatorname{tr}(A\rho)$.

This has an important caveat: there can be different ensembles representing the same density operator (but let's not think about that right now).

I would like to emphasize what is being done here. We have introduced a classical uncertainty in a quantum system! Even electrons and photons can't save themselves from noisy environments.[^classical]

[^classical]: Usually, when we talk about uncertainty in the quantum world, we are talking about Heisenberg's uncertainty principle, the built-in fuzziness of nature, where a particle simply doesn't have a definite position and momentum at the same time. The uncertainty discussed here is purely classical.

[^linear]: Don't worry, you can still follow along if you didn't.

### § 2.2 Deriving the Von Neumann Equation

After all this setup we can now move on to the actual equation we are after ;)
<br><br>
Differentiating the density operator in time and using the Schrödinger equation gives a closed equation for $\rho$. The full derivation is collapsed below.

<details class="derivation" markdown="1">
<summary>Show derivation</summary>

Each state in the ensemble evolves under Eq. (2.1), and the probabilities $p_i$ are fixed by the preparation, so they do not depend on time. Taking the adjoint of Eq. (2.1), and using $H^\dagger = H$, gives

$$
-i\hbar \frac{d}{dt}\langle\psi_i(t)\rvert = \langle\psi_i(t)\rvert H .
\tag{2.6}
$$

Now differentiate Eq. (2.5) with the product rule and substitute Eqs. (2.1) and (2.6):

$$
i\hbar \frac{d\rho}{dt}
= \sum_i p_i \Big( \big(i\hbar\,\lvert\dot\psi_i\rangle\big)\langle\psi_i\rvert + \lvert\psi_i\rangle\big(i\hbar\,\langle\dot\psi_i\rvert\big) \Big)
= \sum_i p_i \Big( H\lvert\psi_i\rangle\langle\psi_i\rvert - \lvert\psi_i\rangle\langle\psi_i\rvert H \Big).
\tag{2.7}
$$

Since $H$ is the same for every member of the ensemble, it factors out of the sum, and the sum is just $\rho$ again.

</details>

The result is the **Von Neumann equation**:

$$
i\hbar \frac{d\rho}{dt} = H\rho - \rho H = [H,\rho] .
\tag{2.8}
$$

It is the Schrödinger equation rewritten for the density operator, and it holds whether or not the state is pure!

### § 2.3 Properties of the Density Operator

The density operator $\rho=\sum_i p_i\lvert\psi_i\rangle\langle\psi_i\rvert$ of Eq. (2.5) has the following basic properties.

**1. Hermiticity.** $\rho^\dagger=\rho$, since each $\lvert\psi_i\rangle\langle\psi_i\rvert$ is Hermitian and the $p_i$ are real.

**2. Unit trace.** Using $\langle\psi_i\vert\psi_i\rangle=1$ and $\sum_i p_i=1$,

$$
\operatorname{tr}\rho=\sum_i p_i\langle\psi_i\vert\psi_i\rangle=\sum_i p_i=1 .
\tag{2.9}
$$

**3. Positivity.** For any vector $\lvert\phi\rangle$,

$$
\langle\phi\rvert\rho\lvert\phi\rangle=\sum_i p_i\,\big\lvert\langle\phi\vert\psi_i\rangle\big\rvert^2\ \ge\ 0 ,
\tag{2.10}
$$

so $\rho\ge 0$. Together with the first two properties, this characterizes a density operator: any operator that is Hermitian, positive and has unit trace describes a valid state.

**4. Purity.** $\operatorname{tr}\rho^2\le 1$, with equality if and only if $\rho$ is a pure state, $\rho=\lvert\psi\rangle\langle\psi\rvert$.

<details class="derivation" markdown="1">
<summary>Show derivation</summary>

Let $\lambda_k$ be the eigenvalues of $\rho$. By properties 1 to 3 they satisfy $\lambda_k\in[0,1]$ and $\sum_k\lambda_k=1$. Since $\lambda_k^2\le\lambda_k$ on $[0,1]$,

$$
\operatorname{tr}\rho^2=\sum_k\lambda_k^2\ \le\ \sum_k\lambda_k=1 .
\tag{2.11}
$$

Equality requires $\lambda_k^2=\lambda_k$ for every $k$, so each $\lambda_k$ is $0$ or $1$. Because they sum to $1$, exactly one eigenvalue equals $1$ and the rest vanish. That means $\rho=\lvert\psi\rangle\langle\psi\rvert$ for the corresponding eigenvector, which is a pure state. Conversely, a pure state has eigenvalues $(1,0,\dots,0)$, so $\operatorname{tr}\rho^2=1$.

</details>
<br>
That's a lot of properties, but we still need one more thing to describe the real world.

<p class="aside">cue the Star Wars music…<br>a long time ago, in a Hilbert space far, far away…</p>

### § 2.4 Introducing the Evolution Operator

The systems we observe are seldom independent of time (that would be an interesting world). To capture the effect of time, we define an evolution operator.

For a time-independent Hamiltonian $H$, the Schrödinger equation (2.1) is solved by

$$
\lvert\psi(t)\rangle = U(t)\lvert\psi(0)\rangle ,
\qquad U(t)=e^{-iHt/\hbar} ,
\tag{2.12}
$$

where $U(t)$ is the **evolution operator**. It is unitary, $U^\dagger U = UU^\dagger = I$. This guarantees that the norm of a state is preserved in time. (The implications of this are huge, as we will realise later.)

Applying Eq. (2.12) to every member of the ensemble in Eq. (2.5), the density operator evolves as

$$
\rho(t) = U(t)\,\rho(0)\,U(t)^\dagger ,
\tag{2.13}
$$

which is the solution of the Von Neumann equation (2.8) for a time-independent $H$. It says that the whole evolution is a unitary **conjugation** of the initial state. If that word is new to you, the definition is collapsed below.

<details class="derivation" markdown="1">
<summary>Show the definition of conjugation</summary>

**Conjugating** an operator $A$ by an invertible operator $V$ means forming

$$
A \;\longmapsto\; V A V^{-1} .
$$

For a unitary $U$ we have $U^{-1}=U^\dagger$, so conjugation reads $A\mapsto UAU^\dagger$, which is exactly the form of the evolution in Eq. (2.13).

If you know linear algebra, this might look familiar. It is a **similarity transformation**, the same operation as a change of basis. Matrices related by conjugation describe the same linear map in different bases, and they always have the same eigenvalues.

</details>

### § 2.5 The Bloch Sphere

Since the evolution operator preserves the norm of a state, the evolution of a single qubit can be seen as a rotation of a point on a sphere. This sphere is called the **Bloch sphere**, and it lets us see the conjugation in Eq. (2.13) as an arrow turning in 3D space.[^trust]

[^trust]: I haven't told you why this is true yet, but you'll have to trust me for now. The collapsed math below and the rotation equation (2.18) give the details.

Every qubit state corresponds to a point in the unit ball. Pure states sit on the surface, and mixed states sit inside it.
(Don't worry about the formulas, just look at the visualization.)

<details class="derivation" markdown="1">
<summary>Show the math</summary>

The Pauli matrices are

$$
\sigma_x=\begin{pmatrix}0&1\\1&0\end{pmatrix},\quad
\sigma_y=\begin{pmatrix}0&-i\\i&0\end{pmatrix},\quad
\sigma_z=\begin{pmatrix}1&0\\0&-1\end{pmatrix}.
\tag{2.14}
$$

Together with $I$ they form a basis of the $2\times 2$ Hermitian matrices, and fixing the trace to $1$ fixes the coefficient of $I$ to $\tfrac12$. Using Hermiticity and unit trace from § 2.3, every qubit density operator can therefore be written as

$$
\rho = \frac{1}{2}\big(I + \vec n\cdot\vec\sigma\big),
\qquad \vec n = (n_x, n_y, n_z)\in\mathbb R^3 .
\tag{2.15}
$$

Since $(\vec n\cdot\vec\sigma)^2=\lvert\vec n\rvert^2 I$, the eigenvalues of $\vec n\cdot\vec\sigma$ are $\pm\lvert\vec n\rvert$, and the eigenvalues of $\rho$ are

$$
\lambda_\pm=\frac{1\pm\lvert\vec n\rvert}{2} .
\tag{2.16}
$$

Positivity of $\rho$ is therefore exactly $\lvert\vec n\rvert\le 1$. Pure states have $\lvert\vec n\rvert=1$, mixed states have $\lvert\vec n\rvert<1$, and the maximally mixed state $I/2$ sits at the center. The purity is $\operatorname{tr}\rho^2=\tfrac12\big(1+\lvert\vec n\rvert^2\big)$.

Finally, the components of $\vec n$ are the spin expectation values:

$$
\langle\sigma_i\rangle=\operatorname{tr}(\rho\,\sigma_i)=n_i .
\tag{2.17}
$$

</details>

Drag the arrow below, or use the sliders.

{% include bloch.html %}

Every time you click and drag the arrow around, that is a unitary operation on the qubit.

The components $n_x, n_y, n_z$ shown above are exactly the measurable spin expectations $\langle\sigma_x\rangle, \langle\sigma_y\rangle, \langle\sigma_z\rangle$.

Now let's see what the Von Neumann equation does to this arrow. For a Hamiltonian $H=\tfrac{\hbar\omega}{2}\,\hat m\cdot\vec\sigma$, where $\hat m$ is a unit vector, Eq. (2.8) becomes a rotation:

$$
\dot{\vec n}=\omega\,\hat m\times\vec n .
\tag{2.18}
$$

<details class="derivation" markdown="1">
<summary>Show derivation</summary>

From $\sigma_i\sigma_j=\delta_{ij}I+i\epsilon_{ijk}\sigma_k$ we get $(\vec a\cdot\vec\sigma)(\vec b\cdot\vec\sigma)=\vec a\cdot\vec b\,I+i(\vec a\times\vec b)\cdot\vec\sigma$, so

$$
[\vec a\cdot\vec\sigma,\ \vec b\cdot\vec\sigma]=2i\,(\vec a\times\vec b)\cdot\vec\sigma .
\tag{2.19}
$$

The identity part of $\rho$ commutes with everything, so only $\vec n\cdot\vec\sigma$ contributes:

$$
\dot\rho=-\frac{i}{\hbar}[H,\rho]
=-\frac{i}{\hbar}\cdot\frac{\hbar\omega}{4}\,[\hat m\cdot\vec\sigma,\ \vec n\cdot\vec\sigma]
=\frac{\omega}{2}\,(\hat m\times\vec n)\cdot\vec\sigma ,
\tag{2.20}
$$

and comparing with $\dot\rho=\tfrac12\dot{\vec n}\cdot\vec\sigma$ gives Eq. (2.18).

</details>

This is a rotation about $\hat m$ at angular speed $\omega$, so the arrow travels along a circle and its length $\lvert\vec n\rvert$ never changes. This matches Eq. (2.16), since the eigenvalues of $\rho$, and with them the purity, are conserved by unitary evolution. In the visualization, moving the arrow around while keeping $r=\lvert\vec n\rvert$ fixed therefore corresponds to a possible evolution of the state, while changing $r$ would need something that is not unitary.## § 3. Symmetry in the Von Neumann Equation

### § 3.1 Properties of the Von Neumann Equation[^props]

[^props]: Yes, properties again. We just did this for $\rho$ in § 2.3, and now it is the turn of the equation that governs it.

The Von Neumann equation can be written as $\dot\rho=\mathcal L\rho$, where $\mathcal L=-\tfrac{i}{\hbar}[H,\,\cdot\,]$ is a linear map acting on operators. It has the following properties.

**1. Linearity.** Since $\mathcal L$ is linear, a mixture $$\rho=\sum_i p_i\rho_i$$ evolves as the mixture of the individual evolutions. It makes no difference whether we mix first and then evolve, or evolve first and then mix!
<br>
This is what makes density operators a consistent description of classical ensembles. Linearity is special to this equation (we will see in § 3.5 that we might not require it after all).

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

### § 3.2 What's so special about Evolution Operators?

Let's step back for a second and recall that, for a time-independent $H$, $\rho(t)=U_t\,\rho(0)\,U_t^\dagger$ with $U_t=e^{-iHt/\hbar}$. The family of operators $\{U_t\}$ has three simple properties:

$$
U_tU_s=U_{t+s},\qquad U_0=I,\qquad U_{-t}=U_t^{-1}=U_t^\dagger .
\tag{3.4}
$$

In words:

- **Evolutions compose.** Evolving for a time $s$ and then for a time $t$ is the same as evolving for a time $t+s$. This holds because $H$ commutes with itself, so the exponents simply add.
- **Doing nothing is an evolution.** At $t=0$ nothing happens, and $U_0=I$.
- **Every evolution can be undone.** Running the evolution backwards, with $U_{-t}$, returns the state to where it started.

Now, if this sounds familiar, you are on the right track. Combining two evolutions gives another evolution, there is an evolution that does nothing, and every evolution has an undo. These are exactly the rules of a **group**!

<details class="derivation" markdown="1">
<summary>Show the definition of a group</summary>

A **group** is a set $G$ together with an operation $\cdot$ that satisfies four rules:

1. **Closure:** for all $a,b\in G$, the product $a\cdot b$ is also in $G$.
2. **Associativity:** $(a\cdot b)\cdot c=a\cdot(b\cdot c)$ for all $a,b,c\in G$.
3. **Identity:** there is an element $e\in G$ with $e\cdot a=a\cdot e=a$ for all $a\in G$.
4. **Inverses:** for every $a\in G$ there is an element $a^{-1}\in G$ with $a\cdot a^{-1}=a^{-1}\cdot a=e$.

Here the set is $\{U_t\}$ and the operation is matrix multiplication, which is automatically associative. Closure is the relation $U_tU_s=U_{t+s}$, the identity is $U_0=I$, and the inverse of $U_t$ is $U_{-t}$.

</details>

So $\{U_t\}$ is a group, and since it is labelled by the single number $t$, it is called a **one-parameter group** of unitary operators.

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
<br>
<br>

### § 3.3 What path can the evolution follow?

Since the evolution is a conjugation (see § 2.4), the conserved quantities are easy to find. For any $n$,

$$
\operatorname{tr}\big(\rho(t)^n\big)=\operatorname{tr}\big[(U\rho U^\dagger)^n\big]=\operatorname{tr}\big[U\rho^nU^\dagger\big]=\operatorname{tr}\big(\rho^n\big),
\tag{3.6}
$$

where we used $U^\dagger U=I$ to collapse the product, and then the cyclicity of the trace.[^cyclic] The same fact is visible in the eigenvalues: if $$\rho(0)\lvert v\rangle=\lambda\lvert v\rangle$$, then $$\rho(t)\,U_t\lvert v\rangle=\lambda\,U_t\lvert v\rangle$$. So $\rho(t)$ and $\rho(0)$ have **exactly the same spectrum**.

[^cyclic]: Remember that the trace is cyclic: $\operatorname{tr}(XY)=\operatorname{tr}(YX)$ for any two matrices, so we may move a matrix from the front of a product to the back. Here that gives $\operatorname{tr}(U\rho^nU^\dagger)=\operatorname{tr}(U^\dagger U\rho^n)=\operatorname{tr}(\rho^n)$.

Two consequences stand out:

- The purity $\operatorname{tr}\rho^2$ is conserved, so a pure state stays pure.
- The von Neumann entropy $S(\rho)=-\operatorname{tr}(\rho\ln\rho)$ is conserved, so a mixed state stays exactly as mixed as it started. (Now this is huge.)[^entropy]

[^entropy]: The entropy depends only on the eigenvalues of $\rho$, $S(\rho)=-\sum_k\lambda_k\ln\lambda_k$, and unitary evolution cannot change the spectrum. So no evolution operator, however cleverly chosen, can turn a mixed state into a pure one, or the other way around. Lowering the entropy of a system (cooling it, resetting a qubit) needs something that is not unitary, such as a measurement or a coupling to a larger system that carries the entropy away. It also means that when the entropy of a subsystem does change, the subsystem is not isolated: it is entangled with something else.

Unitary evolution can never turn our ignorance about the state into knowledge, or the other way around. The spectrum is the part of $\rho$ that the dynamics cannot touch.

That means the classical uncertainty we introduced at the start always remains there throughout the evolution.

### § 3.4 Group Actions and Orbits

Now we shall formalize what our state can explore: we put the conjugation $\rho\mapsto U\rho U^\dagger$ in the language of group actions.

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
**Theorem.** Two density operators $\rho$ and $\sigma$ lie in the same orbit of $U(d)$ if and only if they have the same eigenvalues, counted with multiplicity.[^mult]
</div>

[^mult]: The multiplicity of an eigenvalue is the number of linearly independent eigenvectors that share it. For example, the maximally mixed qubit state $I/2$ has the eigenvalue $\tfrac12$ with multiplicity $2$, so its spectrum is $\{\tfrac12,\tfrac12\}$ and not just $\{\tfrac12\}$.

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

It is unitary, since

$$
U^\dagger U=\sum_{k,l}\lvert e_k\rangle\langle f_k\vert f_l\rangle\langle e_l\rvert=\sum_k\lvert e_k\rangle\langle e_k\rvert=I .
$$

<br>
And because $U\lvert e_k\rangle=\lvert f_k\rangle$,

$$
U\rho U^\dagger=\sum_k\lambda_k\,U\lvert e_k\rangle\langle e_k\rvert U^\dagger=\sum_k\lambda_k\lvert f_k\rangle\langle f_k\rvert=\sigma ,
\tag{3.10}
$$

so $\sigma\in U(d)\cdot\rho$.

</details>

So the orbits are labelled exactly by spectra: the set of density operators splits into layers, one for each possible spectrum, and unitary dynamics lives inside a single layer.

One caveat though. A *single* Hamiltonian only traces out a curve inside an orbit. The whole orbit is what all Hamiltonians together can reach. By the spectral theorem (don't worry about it if you are not familiar with it), every unitary can be written as $U=e^{-iK}$ for some Hermitian $K$, so every element of $U(d)$ is the evolution of some Hamiltonian over some time.

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

for matrices $L(t)$ and $M(t)$ is called a **Lax equation**, after Peter Lax, who introduced it in 1968 to study nonlinear wave equations.
<br>
The Von Neumann equation is the simplest case of this: $M$ is a fixed matrix, so the equation is linear in $L=\rho$.
<br>
In general, life is not so simple: $M$ may depend on time, and even on $L$ itself! Then the equation is **nonlinear**. The conservation law of § 3.3 survives anyway.

Suppose $L(t)$ solves Eq. (3.12), and let $U(t)$ solve $\dot U=MU$ with $U(0)=I$. Then

$$
L(t)=U(t)\,L(0)\,U(t)^{-1} .
\tag{3.13}
$$

So $L(t)$ is a conjugation of $L(0)$, exactly as in § 2.4, and **the spectrum of $L$ is conserved**. Equivalently, every $\operatorname{tr}L^n$ is conserved. If $M$ is anti-Hermitian, as it is for the Von Neumann equation, then $U(t)$ is unitary and the flow stays inside an orbit of § 3.4.

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
<br>
The conservation law of § 3.3 is therefore not special to quantum mechanics! It is a feature of the commutator form itself. Equations of this type are central in the study of [integrable systems](https://en.wikipedia.org/wiki/Integrable_system).

To see this in action, take a $2\times 2$ example where $M$ is built out of $L$ itself:

$$
L=\begin{pmatrix}b_1&a\\a&b_2\end{pmatrix},\qquad
M=\begin{pmatrix}0&a\\-a&0\end{pmatrix}.
$$

The entry $a$ of $M$ is an entry of $L$, so this equation is **nonlinear**. The commutator $[M,L]$ gives

$$
\dot b_1=2a^2,\qquad \dot b_2=-2a^2,\qquad \dot a=a\,(b_2-b_1),
$$

so the entries of $L$ clearly change in time. Yet the eigenvalues, $\lambda_\pm=s\pm\sqrt{d^2+a^2}$ with $s=\tfrac{b_1+b_2}{2}$ and $d=\tfrac{b_1-b_2}{2}$, do not. Pick a starting matrix below and press restart.

{% include lax.html %}

The coloured curves are the entries of $L$, and the dashed lines are $\lambda_\pm$ recomputed from the current matrix at every instant. The entries move, the dashed lines do not.

<details class="derivation" markdown="1">
<summary>Show why</summary>

Adding the first two equations gives $\dot s=0$. For $d$ we get $\dot d=2a^2$, so

$$
\frac{d}{dt}\big(d^2+a^2\big)=2d\cdot 2a^2+2a\cdot a(b_2-b_1)=4a^2d-4a^2d=0 .
$$

Both $s$ and $d^2+a^2$ are constant, and so are $\lambda_\pm$.

</details>

In this example the flow also does something extra: unless $a=0$, the off-diagonal entry decays to zero and $L$ settles into a diagonal matrix with the eigenvalues on the diagonal, $b_1\to\lambda_+$ and $b_2\to\lambda_-$. The spectrum never changed.
<br>
This is the isospectrality of the Lax equation!
<br>
Now why should we care about this example, or even about the Lax equation?
Writing a nonlinear equation as $\dot L=[M,L]$ handed us conserved quantities for free, namely every $\operatorname{tr}L^n$, with no need to look for symmetries. Lax introduced it for the Korteweg-de Vries equation, where $L$ is a Schrödinger operator and its conserved eigenvalues are the speeds of the solitons. The example above is the two-particle Toda lattice, and its flow towards a diagonal matrix is a continuous cousin of the QR algorithm used to compute eigenvalues. Having a Lax pair does not by itself guarantee that a system is solvable, but it is the standard first sign that one is dealing with an integrable system.

### § 3.6 Symmetries of the Hamiltonian

So far the group $U(d)$ acted on states from outside. The symmetries of the system itself form a smaller group. Suppose a unitary $V$ commutes with $H$. If $\rho(t)$ solves Eq. (2.9), then $\sigma(t)=V\rho(t)V^\dagger$ solves it too:

$$
\dot\sigma=-\frac{i}{\hbar}V[H,\rho]V^\dagger=-\frac{i}{\hbar}[VHV^\dagger,\sigma]=-\frac{i}{\hbar}[H,\sigma] .
\tag{3.14}
$$

So a symmetry sends solutions to solutions: transforming first and evolving second gives the same answer as evolving first and transforming second. The set of all such $V$ is a group, the **symmetry group of $H$**. Its infinitesimal generators are Hermitian operators commuting with $H$, and by Eq. (3.3) these are exactly the conserved quantities.

## § 4. Conclusion

We started by asking which properties of a quantum state are invariant under unitary evolution. We got an interesting answer: **the spectrum of $\rho$ never changes**.
<br>
Every $\operatorname{tr}(\rho^n)$ is conserved, and with them the purity and the entropy: a pure state stays pure, and a mixed state stays exactly as mixed as it began. Unitary evolution can never turn our ignorance about the state into knowledge, or the other way around. On top of this, the expectation value of every observable that commutes with $H$ is conserved too, and the symmetries of $H$ are the source of such observables.

The reason was group structure. The evolution operators form a group, and acting on states by conjugation, $\rho\mapsto U\rho U^\dagger$, this group moves a state only within its own orbit. Two density operators lie in the same orbit exactly when they have the same eigenvalues, so the spectrum is precisely the label of the orbit.

Finally, the Lax form of § 3.5 shows that this is not special to quantum mechanics. Any equation of the form $\dot L=[M,L]$ is a conjugation flow, even a nonlinear one, and so conserves the spectrum of $L$. The conservation law is a feature of the commutator itself.

The picture does have limits. Unitary evolution never leaves its orbit, but a noisy evolution can, for example by turning a pure state into a mixed one and so changing its spectrum. Describing such evolution takes a larger framework, the Lindblad equation.[^topic] In that setting the group of evolutions loses its inverses, and one is left with a semigroup.

[^topic]: A topic for another day.

## References

1. P. D. Lax, "Integrals of nonlinear equations of evolution and solitary waves", *Comm. Pure Appl. Math.* 21 (1968).
2. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press (chapter 2).
3. M. A. Armstrong, *Groups and Symmetry*, Springer.