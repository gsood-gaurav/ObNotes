Highly imbalanced data poses added difficulty, as most learners will exhibit bias towards the majority class and in extreme cases may ignore the minority class altogether.

When class imbalance exists with in training data, learners will typically over-classify the majority group due to its increased prior probability. As a result, the instances belonging to the minority group are misclassified more often than those belonging to the majority group. Furthermore some evaluation metrics such as accuracy may mislead the analyst with high scores that incorrectly indicate good performance. Given a binary data set with a positive class distribution of $1\%$ a naive learner that always outputs the negative class labels for all inputs will achieve 99$\%$ accuracy.

Method for handling class imbalance in machine learning can be grouped into three catagories: data-level techniques, algorithm-level methods and hybird approaches. Data-level techniques attempt to reduce the level of imbalance through various data sampling methods. Algorithm-level methods for handling class imbalance, commonly implemented with a weight or cost schema, incldue modifying the underlying learner or its output in order to reduce bias towards majority group.

The results shows that senstivity to imbalance increases as problem complexity increases, and that non-complex linearly separable problems are unaffected by all levels of class imbalance.

