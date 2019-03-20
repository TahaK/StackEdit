
Name: Large scale distributed neural network training through online distillation
Lab: Google
Reference: Anil, R., Pereyra, G., Passos, A., Ormandi, R., Dahl, G. E., & Hinton, G. E. (2018). Large scale distributed neural network training through online distillation. arXiv preprint arXiv:1804.03235.
[link](https://arxiv.org/pdf/1804.03235.pdf)
[github](https://github.com/google-research/google-research/tree/master/codistillation)

### Purpose

Aims at making distributed training on thousands of GPUs feasible. Builds better alternative during inference than ensemble methods due to lower cost and improve reproducibility

### Method

This method can be summarized as simultaneous distillation. n groups of model each training using M instances with data parallelism try to match their predictions with each other. Every 50 training steps each group saves a checkpoint to a shared disk. In each step models calculate the predictions of other groups using their stale weights and try to match them.

### Contributions

Enables training using many units which weak network connections between them. Where they need to synchronize on a loose schedule. They also reduce the variability among retrained models using a novel distillation mechanism.

### Experiments and Results

Synchronized training doesn't  scale beyond a certain point.

2(a) Codistillation is better than baselines and this is not due to label smoothing.

2(b) Partitioned data is better than same data. This shows that soft labels carry information about data and cause supervision.

3(a) Codistillation also works in ImageNet

3(b) Synchronization of the checkpoints can be done in 50 steps

Codistillation helps reduce the random variability in the training procedure

### Comments

I think this method has important implications for federated training. We need to find a framework which explains both gradient backpropagation and soft labels supervision.

### Extensions

I believe exploring Codistillation method in the model compression framework might be fruitful. Imagine compressing intermediate layers of a model by compressing both the depth and width of layers.

Imagine a layer branching of to 10 branches of depth 2 and gathering the branches back together. Each branch will be evaluated separately but they will try to match their activations of their gathering layer with each other. There is no rule that the depth and width of those branches need to be the same. 

This is of course not relevant if you cannot match the activation maps of one network to the activation maps of another network. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgxMTc1ODM1Nl19
-->