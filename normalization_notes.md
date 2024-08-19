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

**Intuition**: In case of image classification tasks, we would want features of a kernel in a CNN to pick signals differently. So we will not do layer normalization. However, we want each of our data points, that is each image, to contribute to the model learning instead of a fewer number of images. Hence, batch normalization decreases the dominance of individual images in learning at each computation step. During training, if a hidden layer gets unnormalized batches then learning could be very unstable and slow. Imagine, we have wide variety of objects at different corners of the images with varying lighting conditions. In this scenario, pixel values for the three channels might see bumps in different images. When we prepare these images as inputs for model training and create batches of images, pixel values could vary a lot within batches and across batches. Batch normalization will result in consistent mean and variance across batches. This allows for faster learning by not pushing the optimization process towards *saturated regime of nonlinearity*. 

On the other hand, in case of language understanding tasks, we would want each feature of a hidden layer to learn different aspect of semantics without making the model too dependent on a particular feature. As any other normalization, layer normalization helps here in reducing the dominance of individual features of a hidden layer. However, when we allow several batches to pass through a layer during training, layer normalization, like batch normalization, helps in keeping the mean and variance of feature outputs consistent through each iteration step of the training process. This helps in stablizing learning process by making each feature participate in the learning process. 

A simpler way to think is when we study for Maths or History exams in high school, we learn the topics by gradually increasing the complexity and we don't change topics too often, for example, from learning linear algebra to learning coordinate geometry. If we would have changed topics frequently, it would have made our learning slower. 

Source:
- Ioffe, S., & Szegedy, C. (2015, June). Batch normalization: Accelerating deep network training by reducing internal covariate shift. In International conference on machine learning (pp. 448-456). pmlr.
