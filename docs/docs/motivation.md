# Motivation

## Why we need Learning to Optimize?
Optimization provides a mathematical foundation for solving quantitative problems in many fields,
along with numerical challenges. The no free lunch theorem indicates the non-existence of a universally best optimization algorithm for all objectives. To manually design an effective optimization
algorithm for a given problem, many efforts have been spent on tuning and validating pipelines,
architectures, and hyperparameters.

To overcome the laborious manual design, an emerging approach of meta-learning (learning to learn)
takes advantage of the knowledge learned from related tasks. In meta-learning, the goal is to learn
a meta-learner that could solve a set of problems, where each sample in the training or test set is a
particular problem. As in classical machine learning, the fundamental assumption of meta-learning
is the generalizability from solving the training problems to solving the test ones. For optimization
problems, a key to meta-learning is how to efficiently utilize the information in the objective function
and explore the space of optimization algorithms.

## What are the remaining gaps?
The target applications of previous methods are mainly focused on training deep neural networks,
except [1] focusing on optimizing black-box functions. There are three limitations of these methods.

* First, they learn in a limited algorithmic space, namely point-based optimization algorithms that use
gradients or not (including SGD and Adam). So far there is no method in learning to learn that reflects
population-based algorithms (such as evolutionary and swarm algorithms) proven powerful in many
optimization tasks. 
* Second, their learning is guided by a limited meta loss, often the cumulative regret
in sampling history that primarily drives exploitation. One exception is the expected improvement
(EI) used by [1] under Gaussian processes. 
* Last but not the least, these methods do not interpret the
process of learning update formula, despite the previous usage of attention mechanisms in [2].

## Why LOIS?
To overcome aforementioned limitations of current learning-to-optimize methods, we present a new
meta-optimizer with the following contributions:

* (**Where to learn**): We learn in an extended space of both point-based and population-based
optimization algorithms.

* (**How to learn**): We incorporate the posterior into meta-loss to guide the search in the
algorithmic space and balance the exploitation-exploration trade-off.

* (**What more to learn**): We design a novel architecture where a population of LSTMs jointly
learn iterative update formula for a population of samples and embedded sample- and
feature-level attentions to explain the formula


## References

[1] Yutian Chen, Matthew W Hoffman, Sergio Gómez Colmenarejo, Misha Denil, Timothy P
Lillicrap, Matt Botvinick, and Nando de Freitas. Learning to learn without gradient descent by
gradient descent. In *Proceedings of the 34th International Conference on Machine Learning Volume 70*, pages 748–756. JMLR. org, 2017.

[2] Olga Wichrowska, Niru Maheswaranathan, Matthew W Hoffman, Sergio Gomez Colmenarejo,
Misha Denil, Nando de Freitas, and Jascha Sohl-Dickstein. Learned optimizers that scale and
generalize. In *Proceedings of the 34th International Conference on Machine Learning Volume 70*, pages 3751–3760. JMLR. org, 2017.