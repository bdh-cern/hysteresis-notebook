# Phase Space

A space $(x, x')$ where:

- $x$ (mm) is the x-position of the particle
- $x'$ (mrad) is the angle of the particle's motion off the x-axis.

The coordinate $x'$ is useful as it describes the momentum of the particle: $$x' = \frac{p_s}{p_x}$$
Particles orbit in ellipses in phase space. Phase space can also be presented in a normalised form, in which case particles orbit in circles.

The area of an ellipse is given by $A=\pi a b$ where $a$ and $b$ are the semi-major and semi-minor axes. We call $ab$ the **emittance** of the beam, $\epsilon$. Both $A$ and $\epsilon$ are conserved quantities as it corresponds to the action of the system (see below: Lagrangian mechanics).

The aspect ratio of the ellipse is $\beta$, aka the **betatron function**. This is a function of the focusing and gives the extents of the ellipse via $\hat{x} = \sqrt{\epsilon\beta}$ and $\hat{x'} = \sqrt{\frac{\epsilon}{\beta}}$ . The $\beta$ varies around the ring.

The normalised **betatron amplitude** of a particle is given by $A_x = \sqrt{\frac{E_x}{\pi}}$  where $E_x$ is the particle's 'single-particle emittance'.

![[Pasted image 20260811110357.png]]


# Lagrangian/Hamiltonian Mechanics

Some concepts:

- **Lagrangian mechanics**: the treatment of the system in terms of action (as opposed to e.g. a Newtonian treatment in terms of forces)
	![[Pasted image 20260811113653.png]]
	
- **The Lagrangian**: any function $L$ which, under the Lagrangian treatment, gives the correct equations of motion for the system in question. Formulated in terms of position and velocity ($r$ and $v$). Often $L= T-V$, where $T$ is kinetic energy and $V$ is 'potential' energy.
- **Hamiltonian mechanics**: Equivalent to Lagrangian mechanics, but formulated in terms of position and momentum (q and p).
- **Canonical coordinates**: a coordinate system which results in Hamilton's equations taking a standard form: $$\dot{q} = \frac{\delta H}{\delta p_i} \qquad \dot{p_i} = \frac{-\delta H}{\delta q_i}$$ These are typically denoted $q$ and $p$. Note that $p$ is not (necessarily) the 'physical' momentum; rather, it is a 'generalised momentum'. In all cases, generalised momentum is to $q$ as physical momentum is to $r$. For example, if $q$ is an angle, $p$ will be an angular momentum, or if $q$ is a charge, $p$ will be a magnetic flux. Likewise $q$ is the 'generalised coordinate'. The product $pq$ must have dimensions of energy.
- **Action-angle coordinates**: a specific choice of canonical coordinates for periodic systems which causes the equations of motion to become trivial. When the system orbits on an unchanging loop in phase space, $H$ is constant and depends only the area of the loop (which corresponds to the energy or action of the system). Thus we choose canonical coordinates $\theta$ (angle, the generalised coordinate) and $I$ (action, the generalised momentum) so that we can defined each phase loop purely by its action $I$.                                                                                                                            
# Beam Optics

In a synchrotron, we have a balance between the centrifugal force and the Lorentz force: 

$$
\begin{align}
-evB &= \frac{mv^2}{R}\\ 
\frac{e}{p}B_z(x,z,s) &= \frac{1}{R(x,z,s)}
\end{align}
$$

We presume that any velocity not in the beam direction is negligible ($v=v_s$) and that the magnetic field only has transverse components ($\vec{B}=\vec{B}(B_x,B_z,0)$ ). We then MacLaurin-expand the field in the region of the nominal trajectory:

$$
\begin{align}
\frac{e}{p}B_z(x) &= \frac{e}{p}B_{z0} + \frac{e}{p}\frac{\delta B_{z}}{\delta x}x + \frac{e}{2!\cdot p}\frac{\delta^2 B_{z}}{\delta x^2}x^2+ \frac{e}{3! \cdot p}\frac{\delta^3 B_{z}}{\delta x^3}x^2 + \dots \\
&= \frac{1}{R} + kx + \frac{1}{2!}mx^2 + \frac{1}{3!}ox^3 + \dots
\end{align}
$$

Each term of the expansion gives us the effect of some class of magnet: dipoles setting the radius, quadrupoles setting the restoring (focusing), sextupoles setting the chromaticity, etc. The expressions are the **strengths** of those magnets:

| Magnet Type | Symbol for strength | Symbol for field quality | Definition                                     |
| ----------- | ------------------- | ------------------------ | ---------------------------------------------- |
| Dipole      | $k_0$               | $b_1$                    | $\frac{e}{p}B_{z0}$                            |
| Quadrupole  | $k_1$               | $b_2$                    | $\frac{e}{p}\frac{\delta B_{z}}{\delta x}$     |
| Sextupole   | $k_2$               | $b_3$                    | $\frac{e}{p}\frac{\delta^2 B_{z}}{\delta x^2}$ |
| Octupole    | $k_3$               | $b_4$                    | $\frac{e}{p}\frac{\delta^3 B_{z}}{\delta x^3}$ |
Dipolar and quadrupolar fields produce **linear** optics. Sextupoles and above give **non-linear** optics.

# Weak Focusing

Weak focusing a natural focusing effect arising from circular motion (or, as some would say, arising only from the dipoles). Particles with some deviation from the reference orbit, but nonetheless moving in a perfect circle, will oscillate around either side, resulting in a low tune.

![[Pasted image 20260811173206.png]]