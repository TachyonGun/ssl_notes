Early theoretical analyses (e.g. Arora et al., 2019) modeled contrastive SSL with strong assumptions (like independent views) and latent classes to explain why learned features enable downstream classification​

From [this review](https://www.mdpi.com/2227-7080/9/1/2#:~:text=framework%20results%20in%20huge%20improvement,Position%20and%20Ordering%20with%20Negatives) quoting [Arora et al., (2019)](https://proceedings.mlr.press/v97/saunshi19a)

> Arora et al. proposed a theoretical framework for contrastive learning that learns useful feature representations from unlabeled data and introduced latent classes to formalize the notion of semantic similarity and performs well on classification tasks using the learned representations. Its performance is comparable to the state-of-the-art supervised approach on the Wiki-3029 dataset. Another recent model, CONtrastive Position and Ordering with Negatives Objective(CONPONO), discourses coherence and encodes fine-grained sentence ordering in text and outperforms BERT-Large model despite having the same number of parameters as BERT-Base.

Recent work has stressed that _model architecture and capacity_ impose critical inductive biases on SSL representations. 

- [Saunshi et al. (2022)](https://arxiv.org/abs/2202.14037) showed that analyses ignoring inductive bias can yield vacuous guarantees, and different function classes (e.g. linear vs. nonlinear networks) with the _same_ contrastive loss behave very differently on downstream tasks​

- [Hao Chen and Ma (2023)](https://arxiv.org/abs/2211.14699)  (ICLR) further prove that a limited-capacity encoder in contrastive SSL will recover only certain clustering structures of the data (those aligned with the architecture’s bias) while ignoring others​

> (1) Quantifying how data augmentations implicitly encode downstream class labels. (2) Demonstrating how representations with small contrastive loss can uncover this implicit structure and do well on downstream tasks


> Nevertheless it raises interesting questions: ==Is the contrastive loss indeed a good indicator of downstream performance==? Do augmentations overlap sufficiently enough in practice to explain the success of contrastive learning? Can contrastive learning succeed even when there is little to no overlap? In a nutshell, the current paper suggests via experiments and simple theory that the answers are, respectively: No, No, Yes.


> ==Function class sensitivity. ==Downstream performance of a representation depends not just on its contrastive loss, but it is also sensitive to the function class (architecture) and training procedure used to learn it.  ==Brittleness of transfer.== Minimizing the contrastive loss to optimality can sometimes have a 2 non-monotonic, deleterious effect on downstream performance, despite the augmentations being effective for some function classes. • T==he disjoint augmentations regime==. When augmentation distributions for inputs do not overlap with each other, it can be shown that any function-class-agnostic analysis (including those from prior work) provably leads to vacuous guarantees. That said, non-overlapping augmentations can sometimes still be informative, and contrastive learning with appropriate function classes can succeed, a phenomenon that is not captured by existing theory.


May need to look at:

> Finally, there are theoretical works for other types of self-supervised learning [Bansal et al., 2021], including methods like context reconstruction [Lee et al., 2021] and language model [Saunshi et al., 2021], studying their benefits on downstream tasks


-  [Saunshi et al. (2022)](https://arxiv.org/abs/2202.14037) Find that analysis which ignore inductive biases cannot account for success, sometimes vacuous results (e.g. if using linear models)

> We run contrastive learning with three models on this dataset. The first is a simple Bag-of-Word (BoW) model that learns a single word embedding matrix and returns the average word embedding of tokens in the text. The second model is Gated Recurrent Unit (GRU), which is a recurrent neural network Chung et al. [2014]. The last is a Transformer [Vaswani et al., 2017], which is the base model for many state-of-the-art neural networks in NLP.


![[Pasted image 20250324142603.png]]









