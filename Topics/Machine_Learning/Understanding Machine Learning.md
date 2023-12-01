## Machine Learning Basics

### Understanding Machine Learning:
Machine Learning is about developing customized algorithms that may be used for various purposes which may include predictions, and identifying patterns such that a machine can perform [tasks](#Task) that humans are able to conduct. While a model that could explain the provided dataset effectively gets customized by fine-tuning the [parameters](#Parameter) and [hyperparameters](#Hyperparameter), it is important that the [model](#Model) can generalize the provided dataset in such a way that a model shall be able to explain if new data were to be added on top.

The parameters of these algorithms heavily depend on the provided dataset. This means it is possible that while the algorithm explains the current dataset fairly well, such an algorithm may not work well for the other dataset with the relevant context. This ["over-fitting"](#Overfitting) can be prevented by splitting the dataset into three categories that may serve different purposes during the learning process.

The first set of data is called the training dataset. As the name suggests, this dataset is used to "train" the algorithm. When we say training, we mean tuning the parameters of the algorithm to the given dataset. As this will determine the "optimal" algorithm that would solve the provided tasks, it is typical to have over 50% of the dataset as a training dataset. We may set hyperparameters to decide how the algorithm will learn.
The second set of data serves as a verifier thus called the validation dataset. In order to avoid over-fitting, this set of data will serve as an unknown yet reusable data to verify the generalization of the fitted model. Each time a model gets trained, it will try to explain the task on the validation dataset to let the Machine Learning practitioner know its performance. While the accuracy measurement metrics may vary (i.e. one example would be a simple proportion of correct predictions), it is important to have a metric that is appropriate for the given task. Ideally, we would want to make sure the model has the minimum error on the validation set while having a relatively low error on the training set.

![Image Credit: The Elements of Statistical Learning](example_machine_learning.png?raw=true "Training and Validation")

The last set of data can be used for the testing purpose. It is important to note that while this dataset is similar to validation dataset such that it serves as an unknown data to be tested on, it cannot be reused for more testing purpose. The purpose of this dataset remains as demonstrating the performance of the algorithm in general.

It can be easily seen that the existence of a large set of data is essential to develop Machine Learning algorithms for a given problem. Where the definition of "large" may depend on the context and the algorithms that are trying to be implemented, more data would usually result in a better fitted and generalized model. Fundamentally, since the algorithm goes through this provided "large" dataset to be trained on, Machine Learning algorithms go through computationally heavy training process which may not be feasible for certain situations. As a Machine Learning practioner and a Software developer, it is important to idenfity when to use these expensive processes and when to not. This primarily depends on which task an application needs to resolve.

There are three large branches of Machine Learning which may defer by the nature of the task:

#### Supervised Learning

Supervised Learning involves a prediction or classification of a label using provided information. An easy example would be to idenfity whether a provided object is an orange or apple based on qualitative/quantitative information such as dimensions, shape, colour, etc or predicting a person's height based on other personal traits. It is important to note that the dataset contains the [target variable](#Target) to the tasks such that the machine can learn the relationship between the predictors (variables used for prediction/classification purposes) and the targets (labels/outcomes) that need to get predicted.

Algorithms may include: k-Nearest Neighbours, Decision Tree, Logistic Regression, Neural Network, etc.

#### Unsupervised Learning

If the nature of tasks involves a dataset which does not contain the target variables (that is, we do not know what the data is supposed to represent beforehand), it is impossible to "supervise" the machine's training process. However, a machine may be able to develop an algorithm such that patterns that may exist in the dataset can be indentified. For example, considering if we want to determine preferences on movies for the user. Given a dataset which contains the user's netflix history, an algorithm may be able to determine the categories of the movies that the user may prefer. 

Algorithms may include: k-means, Principal Component Analysis

#### Reinforcement Learning

Reinforement Learning involves tasks such that past actions may affect the future actions. Unlike supervised learning, it does not require predictor-target paired dataset, but rather it requires a defined reward signal such that how performing a certain action could be beneficial over the others. An example would be predicting the best move for the given chess board. 

Algorithms may include: Q-learning, Actor-Critic methods


### Implementation in Software Engineering

The biggest draw backs of implementing Machine Learning algorithms are the requirements of large dataset and expensive computation time. Implementations may not be feasible if the none of the mentioned two can be achieved as the accuracy may be poor and the correct representation of the dataset may not be possible. As a developer, one should consider collecting data upon the user's consent if the quality and volume of the data become a problem. 

Another major issue of implementing Machine Learning algorithms may lie in ethics. Due to the bias that may exist in the provided dataset, there have been numerous incidents where the algorithm resulted in discriminative behaviour. A developer should always know how the fitted model behaves to prevent this issue and make sure that the quality of the data provided is adequate. The process of data collection along with how those data get used is another ethical concern that a developer should have in mind. It is important to note that having the users' consents are a must and not an option when using their data.

However, if the task involves resolving tasks which may involve non-deterministic behaviours, these algorithms can be extremely powerful. That is, if there does not exist a feasible rule-based alrogithms to correctly resolve the task, it is worth considering implementation of the algorithms as none of the deterministic algorithm would do a better job.

If implemented correctly, a Machine Learning algorithm could yield effecitve results in both generalization and specification which may be necessary to make a better software.

### Appendix:
* **<span id="Model">Model</span>**: A model in Machine Learning refers to an established statistical algorithm that can "explain" the provided dataset and task effectively with optimized parameters.
* **<span id="Task">Task</span>**: A task in Machine Learning refers to a goal of the algorithm (i.e. predict certairn variable using the others). Tasks are usually generalized problems that an algorithm attempts to explain.
* **<span id="Hyperparameter">Hyperparameter</span>**: A parameter that can be tuned which would dictate how the model gets trained. This needs to get manually set up by a Machine Learning practioner BEFORE the training process starts.
* **<span id="Parameter">Parameter</span>**: A parameter that can be determined by the provided dataset. The values of parameters are assigned during the learning process and not by the Machine Learning practioner. The parameters are set by the data and algorithm AFTER the training process.
* **<span id="Overfitting">Over-fitting</span>**: Understanding over-fitting is important in Machine Learning. Over-fitting refers to a situation where the model successfully explains the training dataset well (i.e. high accuracy in prediction), but fails to explain external dataset (i.e. new set of data with the same context). The primary goal of Machine Learning algorithm is to produce a model that can generalize resolving a given task.
* **Under-fitting**: Under-fitting is the opposite of over-fitting. If the fitted model fails to explain the training-set well, it is considered under-fitted.
* **<span id="Target">Target Variable</span>**: A target variable is a variable present in the dataset that the model is trying to predict/categorize on. For example, if we want to fit a model to categorize an object as a human or not by using various traits such as height, weight, shape, etc. A target variable would be a binary indicator indicating whether the object represented by the data is human or not.



### References

* Krishnan, Rahul G. Interview. Conducted by Seo Won Yi. 29 Nov 2023.
