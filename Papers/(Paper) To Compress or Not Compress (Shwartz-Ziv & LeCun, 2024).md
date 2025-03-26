#paper 

> Deep neural networks excel in supervised learning tasks but are constrained by the need for extensive labeled data. Self-supervised learning emerges as a promising alternative, allowing models to learn without explicit labels. Information theory, and notably the information bottleneck principle, has been pivotal in shaping deep neural networks. This principle focuses on optimizing the trade-off between compression and preserving relevant information, providing a foundation for efficient network design in supervised contexts. However, its precise role and adaptation in self-supervised learning remain unclear. In this work, we scrutinize various self-supervised learning approaches from an informationtheoretic perspective, introducing a unified framework that encapsulates the self-supervised information-theoretic learning problem. We weave together existing research into a cohesive narrative, delve into contemporary self-supervised methodologies, and spotlight potential research avenues and inherent challenges. Additionally, we discuss the empirical evaluation of information-theoretic quantities and their estimation methods. Overall, this paper furnishes an exhaustive review of the intersection of information theory, self-supervised learning, and deep neural networks.

![[Resources/Pasted image 20250325193129.png]]

(Just means $Y|T$ and $X$ are conditionally independent)

![[Resources/Pasted image 20250325193400.png]]

(This means $T$ captures all the sufficient information about $X$)

![[Resources/Pasted image 20250325193431.png]]

(MSS are statistics with the maximum information about $Y$ while retaining the least information about $X$ as possible)

--- 

### Information Bottleneck as a framework

- Majority of distributions lack exact minimal sufficient statistics 
- $X$ is the input, $Y$ is the target, and $T$ is a stochastic representation of $X$ via $P(T \mid X)$.
- $Y - X - T$ forms a Markov chain; mutual information terms of interest are $I(X; T)$ and $I(Y; T)$.
- ==Goal if IB==: to extract relevant info about $Y$ (maximize $I(Y; T)$) while compressing $X$ (minimize $I(X; T)$).
- **BUT!!!** the Data Processing Inequality: $I(Y; T) \leq I(X; Y)$.
- Trade-off between compression and prediction is controlled by optimizing:
   $$\mathcal{L} = \min_{P(t|x), p(y|t)} \; I(X; T) - \beta I(Y; T)$$
- $\beta$ controls how much information about $Y$ is preserved in $T$.
- Mutual information can be rewritten as:
  $$I(T : Y) = I(X : Y) - \mathbb{E}_{x \sim P(X), \; t \sim P(T|x)} \left[ D\left( P(Y \mid x) \; \| \; P(Y \mid t) \right) \right]$$

### Various results from review wroth minding

Note that some are contradictory...

- Chelombiev et al. (2019) discovered a positive correlation between generalization accuracy and the compression level of the network’s final layer.
- Shwartz-Ziv et al. (2018) also examined the relationship between generalization and compression, demonstrating that generalization error exponentially depends on mutual information.
- Achille et al. (2017) established that flat minima, known for their improved generalization properties, constrain the mutual information.
- Saxe et al. (2019) showed that compression was not necessary for generalization in deep linear networks.
- Basirat et al. (2021) revealed that the decrease in mutual information is essentially equivalent to geometrical compression.
- Mutual information between training inputs and inferred parameters provides a concise bound on the generalization gap (Pensia et al., 2018; Xu and Raginsky, 2017).
- Achille and Soatto (2018) explored using an information bottleneck objective on network parameters to prevent overfitting and promote invariant representations.

### Self-Supervised Learning

- One of the earliest approaches by Linsker (1988(, focused on maximizing information transfer from inputs to latent representations, showing this is equivalent to maximizing the determinant of the output covariance under Gaussian assumptions (need to check this out)
    
- Becker & Hinton (1992), introduced a representation learning method that approximates mutual information between alternative latent vectors derived from the same image.
    
- ICA-Infomax algorithm by Bell & Sejnowski (1995) aimed to separate independent sources by maximizing mutual information between mixtures and estimates, while enforcing statistical independence among outputs.
    
- Hjelm et al. (2018) extended the InfoMax principle to deep learning with Deep Infomax, which learns unsupervised features by maximizing mutual information between inputs and learned representations, while matching them to a prior.
    
- Bachman et al. (2019), Henaff (2020), Hjelm et al. (2018), and Tian et al. (2020) applied this principle to a self-supervised multiview setting, maximizing mutual information between different views by predicting one representation from the other.
    
- ==Tschannen et al. (2019) showed that InfoMax-based models often owe their performance more to inductive biases in architecture and estimators than to the InfoMax objective itself, ==which can be trivially optimized using invertible encoders.
    
- To address the limitations of InfoMax, Sridharan and Kakade (2008) proposed the multiview Information Bottleneck framework, which assumes that either view is sufficient for downstream tasks and defines relevant information as the shared content across views, thus encouraging label-preserving augmentations.
![[Resources/Pasted image 20250325201510.png]]

### Implicit Compression in SSL

- Recent studies have shown that contrastive learning creates compressed representations that include only relevant information (Tian et al., 2020b; Wang et al., 2022)

 > In the supervised case, where Z is a learned stochastic representation of the input and Y is the label, we aim to optimize
 
$$I(Y ; Z) ≥ H(Y ) + \mathbb{E} [\log q(Y | Z)]$$
> Since Y is constant, optimizing the information I(Z; Y ) requires only minimizing the prediction term E \[log q(Y |Z)\] by making Z more informative about Y . This term is the cross-entropy loss for classification or the square loss for regressions. Thus, we can minimize the log loss without any other regularization on the representation.

> In contrast, for the self-supervised case, we have a more straightforward option to minimize H(Z 1 |Z 2 ): ==Making Z 1 easier to predict by Z 2 ==, which can be achieved by reducing its variance along specific dimensions. If we do not regularize H (Z 1 ), it will decrease to zero, and we will observe a collapse. This is why, in contrastive methods, the variance of the representation (large entropy) is significant only in the directions with a high variance in the data, which is enforced by data augmentation (Jing et al., 2021). According to this analysis, the network benefits from making the representations ”simple” (easier to predict). Hence, even though our representation does not have explicit information-theoretical constraints, the learning process will compress the representation.

