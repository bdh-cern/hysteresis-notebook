[[Hysteresis in Functional Materials, Kaltenbacher & Pechstein, 2026]] (HiFM) describes the play operator $P_r$ in its opening pages.

Imagine a paper coffee cup and a stirrer, perhaps similar to those dispensed by the coffee machine on the first floor of building 865 of the Prevessin site of CERN. The cup can be moved by placing the stirrer inside the cup and moving it left and right. The cup will only move when the stirrer pressed against the walls.

This cup-stirrer system is hysteretic, because its position of the cup at any time (the output) is not just dependent on the present position of the stirrer (the input), but its past positions (the history). As an example, if the stirrer is moved 10cm to the right, the cup position afterwards will be dependent on the position of the stirrer inside the cup before.

![[Pasted image 20260427164126.png]]

Denote the radius of the cup as $r$. The position of the centre of the cup at time $t$ is denoted $\xi^r$ and the position of the stirrer is at time $t$ is $u(t)$. The displacement of the stirrer from the centre of the cup is $x = u - \xi^r$. We can easily imagine that over a time interval $t \in [a,b]$:

$$\xi^r(t)=max(\xi^r(a), u(t)\mp r)$$where the $\mp$ is resolved to $-$ or $+$ for $u(t)$ being non-decreasing or non-increasing.

From this, we can construct a play operator $P_r$ which gives the evolution of the hysteretic quantity from the evolution of the input and the starting displacement, and unique to this radius of cup:

$$P_r : [-r,r] \times W^{1,1}(0,T) \rightarrow W^{1,1}(0,T) : (x^r_0,u) \mapsto \xi^r $$
where $W^{1,1}(0,T)$ is a space of functions which are integrable and have at least weak derivatives. The space is 'whole' in that it has no boundary conditions and all functions satisfying the conditions are included. 

In our case, $P_r$ gives us the position of the cup based on the history of the position of the stirrer; it gives us the hysteresis loop.

There is also the 'stop' operator:

$$S_r = u - P^r \equiv u - \xi^r$$ The stop operator gives us the deplacement of the stirrer from the centre of the cup from the position of the stirrer: $$S_r : (x^r_0, u) \mapsto x^r $$
Both $S_r$ and $P_r$ are Lipschitz continuous. If $\xi$ and $\eta$ represent two different branches after inputs $u$ and $v$, then:

$$|\xi^r - \eta^r| \leq max(|\xi^r - \eta^r|, |u-v|_{[0,T]})$$
