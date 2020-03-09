# Machine Learning

## terms
- data set:
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




## software frameworks
- tensorflow: top machine learning platform
  - Keras: Libray or API to tensorflow
- SciPy: scientific computing
- numpy: scientific computing
- scikit-learn:  popular open-source ML library in Python
- pandas: library for handling input data

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
