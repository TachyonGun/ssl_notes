
- [ Wang and Isola (2020)](https://proceedings.mlr.press/v119/wang20k.html) (PMLR) identified two key properties that contrastive losses promote: ==**alignment**== (making features of positive pairs close) and ==**uniformity**== (spread-out feature distribution on the unit hypersphere)​ They proved that asymptotically the contrastive loss optimizes these properties and empirically showed that better alignment & uniformity correlate with better downstream performance​

> We propose quantifiable metrics for ==alignment and uniformity as two measures of representation quality==, with theoretical motivations.


Interesting bit:

> Necessity of normalization. Without the norm constraint, the softmax distribution can be made arbitrarily sharp by simply scaling all the features. Wang et al. (2017) provided an analysis on this effect and argued for the necessity of normalization when using feature vector dot products in a cross entropy loss, as is in Eqn. (1).

![[Pasted image 20250324154121.png]]

Interesting note on common practices,

> We analyze the asymptotics with infinite negative samples. Existing empirical work has established that larger number of negative samples consistently leads to better downstream task performances (Wu et al., 2018; Tian et al., 2019; He et al., 2019; Chen et al., 2020), and often uses very large values (e.g., M = 65536 in He et al. (2019))

Also,

> Many empirical works are motivated by the InfoMax principle, i.e., maximizing I(f(x); f(y)) for (x, y) ∼ ppos. However, the interpretation of Lcontrastive as a lower bound of I(f(x); f(y)) is known to be inconsistent with its actual behavior in practice (Tschannen et al., 2019).

![[Pasted image 20250324155203.png]]

 - [Tian et al. (2021) ](https://arxiv.org/abs/2102.06810)carry out learning dynamics analysis of ==non-contrastive== CL to show that the representations can avoid collapse if data augmentation is sufficiently stronger than regularization.
 
 - Bao (2023) howed that using cosine similarity (i.e. normalized features) changes the dynamics, yielding a stable equilibrium that prevents collapse even when a naive L2-loss analysis predicted collapse​. Also for ==non-contrastive==