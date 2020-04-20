# Machine Learning

## terms
- data set
- instance
- sample
- attribute / feature
- attribute value
- attribute space
- sample space
- feature vector
- dimensionality
- learning / training
- training data / training sample
- training set
- hypoyhesis
- ground-truth
- learner
- prediction
- label
- example
- label space
- classification: predict discrete value
  - binary classification
    - positive class
    - negative class
  - multi-class classification
- regression: predict continuous value
- testing: the process of predicting
- testing sample: sample used for testing
- cluster: group of training data
- supervised learning
- unsupervised learning
- generalization
- distribution
  - i.i.d: independent and identical distribution
- induction: generalization
- deduction: specialization
- version space: a set of hypothesis that fits data
- no free launch theorem
  - all algos are equal, assuming problems have the chance of happening and of equal importance

- statistical learning
	- support vector machine
	- kernal method
	- connectionism: deep learning 
- error
	- training error / emperical error: training set
	- generalization error: test set

- overfitting
	- learnt too much from samples
	- bad for generalization
- underfiting
	- learnt too little

- model selection:
	- minimize generalization error




## neural networks vs biological neurons
	data processed in layers
	layers stack on top of each other
	connections only between adjacent ones

## layer vs math function
	layer is stateful
	weight is the state

## measure performance
- confusion matrix
	- true positive
	- true negative
	- false positive
	- false negative
- AUC curve

## how to divide training & test data
- stratified sampling: sample while maintaining the data ratio
- hold-out: divde data with no overlap
  - 4/5 for training or 2/3 for training

- cross validation
	- aka. k-fold cross validation
	- divide data into k subsets
	- for each of the subset
		- use it as test set,
		- use the remaining data as train set
	- result is the average of the k train/test pair
	- special case: LOO (leave one out)

- bootstrap sampling
	- randomly select data from data pool
		- allow sampling data already sampled
		- 0.368 chance of data not selected at all
	- test data = data pool - sampled data
	- test result called out-of-bag estimate
	- applicable only to small data
		- change original data distribution
		- introduct estimation bias

## reinforcement learning
- the input output system
  - input: the state
  - policy: transform state to action
  - output: the action
- the reward
  - can be defined as derivitive of score
- the AI environment
  - state
  - action
  - reward
- the markov decision process (MDP)
  - observe current state
  - perform action
  - receive reward based on state and action
  - enters next state
  - the ultimate goal is to maximize sum of all rewards
- training and inference
  - training
    - choose model
    - init params
    - for each iteration (called episode)
      - give award based on action
      - adjust params using q-learning, stochastic gradient descent, backpropogation
    - repeat the iterations
  - inference
    - don't adjust params
    - act based on trained model

## concepts
- Goal
  The fundamental tension of machine learning is between fitting our data well, but also fitting the data as - simply as possible
- Data types
  - categorical Data
  - numercial data
- Evaluatation
   - MSE vs RMSE
    RMSE can be interpreted on the same scale as the - original targets
- Prevent overfitting
  - divide into training set, validation set and test set
    - train on training set
    - tweak params based on validation set
    - test on test set
  - regularization
    - minimize both loss term and model complexity
    - prefer smaller weights
    - L1 regularization
      - penalizes |weight|
      - effect: drives ineffective weights to 0
    - L2 regularization (ridge)
      - penalizes weight ^ 2
      - effect: drives all weights to be small
      - complexity = sum of square of weights
    - dropout
- Logistic Regression
  - need regularization to prevent overfit
  - result can be used as probability by default
  use threshold to turn probability into binary - classification
  - accuracy has no meaning to class imbalanced data set
  - need to consider both accuracy and recall
    - accuracy = correct ones / all predications
    - recall = predicted ones / all positives
  AUC: meansures how well the examples are ranked in the - predictions
- Non-linear functions
  - RELU (rectified linear unit)
    - f(x) = max(0,x)
  - sigmoid
    - f(x) = 1 / (1 + e ^(-x))
- Neural Nets
  - add non-linearity layer
    - non-linear node: aka activation function
  - back propagation
    - most common training algo for NN
  - forward propagation
- Lasso?
- TensorFlow
  - feature column: store description about feature
- Multilayer Perceptrons
- feedforward neural networks
- convolutional neural network

## software frameworks
- tensorflow: top machine learning platform
  - Keras: Libray or API to tensorflow
- SciPy: scientific computing
- numpy: scientific computing
- scikit-learn:  popular open-source ML library in Python
- pandas: library for handling input data