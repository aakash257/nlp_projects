Batch normalization:
- **what?** -> each batch of input data is normalized using z-score transformation.
- **how?**  X-> $\large{\frac{X-\mu_{b}}{\sigma_{b}}}$ where X represents a data point with n features in a batch $b$ and $\mu_{b}$ and $\sigma_{b}$ are mean and standard deviation of the batch
- **why?** It facilitates faster training by controlling for the distribution of the inputs across batches which otherwise would make training slower. It helps in regularization and therefore prevents overfitting and it reduces the dependency on dropout.
- **when?** It is applied to the batch of data before it passes through a neural network layer, such as a CNN layer.

Layer normalization
- **what?** A layer's output for each data point is normalized using z-score transformation
- **how?** Y-> $\large{\frac{Y_{l}-\mu_{l}}{\sigma_{l}}}$ where $Y_l$ represents layer $l$'s predictions for an input data point with $\mu_{l}$ and $\sigma_{l}$ are mean and standard deviation of the layer's predictions.
- **why?** It normalizes the hidden layer features to ensure consistent feature distributions across data points. If we don't do layer normalization, then a few of the feature values could be larger. These large values would make the model dependent on these features. In order to make each feature of a layer contribute similarly to the model's predictions, layer normalization is helpful.
- **when?** It is applied to the layer's output right after a hidden layer such as a RNN layer.

While researching about batch normalization, I found out about *internal covariate shift*, which is shift in variance of model's hidden layers' predictions due to shift in input distributions during training.

**Intuition**: In case of image classification tasks, we would want features of a kernel in a CNN to pick signals differently. So we will not do layer normalization. However, we want each of our data point, each image, to contribute to the model learning. Hence, batch normalization decreases the dominance of individual images in learning and allows for faster learning by not pushing the optimization process towards *saturated regime of nonlinearity*. On the other hand, in case of language understanding tasks, we would want each feature of a hidden layer to learn different aspect of semantics without making the model too dependent on a particular feature. Hence, layer normalization helps here in reducing the dominance of individual features of a hidden layer.
