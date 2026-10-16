Logistic Regression Visualizer

An interactive, single-page visualizer for understanding binary Logistic Regression step by step. Explore how a model learns from data using batch gradient descent, calculates probabilities, classifies data points, updates its decision boundary, and minimizes classification loss.

Overview

Logistic Regression is a supervised machine learning algorithm used for binary classification. It predicts the probability that a data point belongs to one of two classes based on its input features.

This visualizer makes the learning process easier to understand by connecting the mathematical calculations with interactive visualizations. Users can create datasets, adjust hyperparameters, train the model step by step, inspect individual predictions, and observe how the model changes during training.

The application uses two input features, $x_1$ and $x_2$, to classify data points into Class 0 or Class 1.

Features

* Interactive Data Canvas — Visualize data points, classification regions, and the model’s decision boundary in a normalized 0–1 coordinate space.
* Dataset Generation — Generate linearly separable or slightly noisy datasets to explore different classification problems.
* Manual Data Editing — Add Class 0 and Class 1 points or delete existing points to experiment with different datasets.
* Batch Gradient Descent — Train the model using actual parameter updates calculated from the current dataset.
* Step-by-Step Training — Perform one training update at a time to observe changes in the model.
* Automatic Training — Train continuously until the convergence condition is met or the maximum number of epochs is reached.
* Adjustable Hyperparameters — Change the learning rate, maximum epochs, and decision threshold.
* Live Model Parameters — Monitor the learned weights $w_1$, $w_2$, and bias $b$ as training progresses.
* Current Prediction Inspector — Select an individual data point to examine its input features, linear score, sigmoid probability, predicted class, and true class.
* Sigmoid Function Reference — Explore how the sigmoid function converts linear scores into probabilities.
* Decision Boundary Visualization — Observe how the classification boundary and predicted regions change as the model learns.
* Loss Graph — Track binary cross-entropy loss across training epochs using an automatically scaled graph with hover information.
* Input Validation — Display clear error messages when training cannot proceed, such as when the dataset is empty, contains only one class, or reaches the maximum epoch limit.

Application Layout

1. Data Canvas

The Data Canvas displays the dataset and the model’s current classification behavior.

Each data point represents one sample with two input features, $x_1$ and $x_2$. Its class determines its label as Class 0 or Class 1.

The canvas supports two dataset generators:

* Linearly Separable — Generates two classes that can be separated by a straight decision boundary.
* Slightly Noisy — Generates a more challenging dataset with some overlap or irregularity between the classes.

Users can also create custom datasets by adding or deleting individual points.

The canvas visualizes the model’s predicted classification regions and decision boundary. Before the first training step, the decision boundary remains hidden because the model has not yet performed a training update.

2. Training Controls

The training controls allow users to experiment with how the model learns.

Control	Description
Add Class 0	Add a Class 0 point by clicking an empty canvas location.
Add Class 1	Add a Class 1 point by clicking an empty canvas location.
Delete Point	Remove an existing point by clicking it.
Learning Rate	Adjust the step size used during parameter updates.
Maximum Epochs	Set the maximum number of training updates.
Decision Threshold	Set the probability threshold used to assign predicted classes.
Step	Perform one batch gradient descent update.
Play Until Convergence	Train automatically until a stopping condition is met.
Reset	Reset the training state for another experiment.

When a user clicks an existing point while in Add Class 0 or Add Class 1 mode, the point is selected for prediction inspection instead of being duplicated.

3. Model State

The Model State panel displays the current state of the Logistic Regression model.

It includes:

* Current training epoch.
* Current binary cross-entropy loss.
* Learned weights $w_1$ and $w_2$.
* Learned bias $b$.
* The selected point’s input features.
* Linear score $z$.
* Sigmoid probability $\sigma(z)$.
* Predicted class and true class.
* The classification rule and sigmoid reference table.

Selecting a point on the canvas updates the Current Prediction panel, allowing users to examine how the model processes a specific sample.

4. Loss Graph

The Loss Graph plots binary cross-entropy loss against the training epoch.

Each training update produces a new loss value, allowing users to observe whether the model is improving over time.

The graph automatically scales to accommodate the loss values and provides a hover tooltip for inspecting individual points on the curve.

A decreasing loss generally indicates that the model’s predicted probabilities are becoming better aligned with the true class labels. However, the loss curve may not always decrease smoothly, particularly when the learning rate is too high or the dataset is difficult to classify.

How Logistic Regression Works

1. Linear Score

The model first calculates a linear score using the two input features, their corresponding weights, and the bias:

$$
z = w_1x_1 + w_2x_2 + b
$$

Where:

* $x_1, x_2$ are the input features.
* $w_1, w_2$ are the learned feature weights.
* $b$ is the bias term.
* $z$ is the linear score.

The weights determine how the input features contribute to the score, while the bias shifts the score.

2. Sigmoid Function

The linear score is converted into a probability using the sigmoid function:

$$
\sigma(z) = \frac{1}{1 + e^{-z}}
$$

The output is always between 0 and 1 and represents the model’s estimated probability of Class 1.

* When $z = 0$, the probability is 0.5.
* When $z$ is positive, the probability is greater than 0.5.
* When $z$ is negative, the probability is less than 0.5.

The sigmoid reference table in the application helps users understand the relationship between the linear score and the resulting probability.

3. Binary Classification

The predicted probability is compared with the selected decision threshold $t$.

$$
\hat{y} =
\begin{cases}
1 & \text{if } \sigma(z) \geq t \\
0 & \text{if } \sigma(z) < t
\end{cases}
$$

Where:

* $\hat{y}$ is the predicted class.
* $t$ is the decision threshold.

With a threshold of 0.5, probabilities greater than or equal to 0.5 are classified as Class 1, while lower probabilities are classified as Class 0.

Changing the threshold changes the classification rule without directly changing the learned weights or bias.

4. Binary Cross-Entropy Loss

The model’s predictions are evaluated using binary cross-entropy loss:

$$
L = -\frac{1}{N}\sum_{i=1}^{N}
\left[
y_i\log(p_i) +
(1-y_i)\log(1-p_i)
\right]
$$

Where:

* $N$ is the number of data points.
* $y_i$ is the true label of data point $i$.
* $p_i$ is the predicted probability of Class 1 for data point $i$.
* $L$ is the average loss across the dataset.

The loss penalizes incorrect probability estimates. Confident predictions that disagree with the true labels receive a larger penalty.

The goal of training is to reduce this loss by adjusting the model parameters.

5. Batch Gradient Descent

The model learns by using batch gradient descent. During each training update, it calculates the gradients using the entire dataset and updates the weights and bias.

For binary Logistic Regression, the gradients are:

$$
\frac{\partial L}{\partial w_1}
= \frac{1}{N}\sum_{i=1}^{N}(p_i-y_i)x_{i1}
$$

$$
\frac{\partial L}{\partial w_2}
= \frac{1}{N}\sum_{i=1}^{N}(p_i-y_i)x_{i2}
$$

$$
\frac{\partial L}{\partial b}
= \frac{1}{N}\sum_{i=1}^{N}(p_i-y_i)
$$

The parameters are then updated using the learning rate $\alpha$:

$$
w_1 \leftarrow w_1 -
\alpha\frac{\partial L}{\partial w_1}
$$

$$
w_2 \leftarrow w_2 -
\alpha\frac{\partial L}{\partial w_2}
$$

$$
b \leftarrow b -
\alpha\frac{\partial L}{\partial b}
$$

These updates move the parameters in the direction that reduces the loss locally.

After each training update, the visualizer refreshes the model parameters, predictions, classification regions, decision boundary, and loss graph.

6. Decision Boundary

The decision boundary represents the locations where the model’s predicted probability equals the selected decision threshold.

For a threshold of 0.5, the sigmoid probability equals 0.5 when $z = 0$. Therefore, the decision boundary is:

$$
w_1x_1 + w_2x_2 + b = 0
$$

For other thresholds $t$, the boundary is defined by:

$$
w_1x_1 + w_2x_2 + b
= \log\left(\frac{t}{1-t}\right)
$$

This means that changing the decision threshold can shift the boundary even when the learned model parameters remain unchanged.

The boundary and classification regions update as training progresses, making it possible to see how the model separates the two classes.

Training Behavior and Stopping Conditions

The visualizer provides both manual and automatic training.

Step-by-step training performs one batch update each time the Step button is pressed. This is useful for examining individual changes in the weights, bias, loss, and decision boundary.

Automatic training repeatedly performs updates until one of the following conditions occurs:

* The maximum number of epochs is reached.
* The absolute loss improvement remains below $0.00001$ for three consecutive epochs.
* The user stops training manually.

The convergence condition helps prevent unnecessary updates when the loss has stopped changing significantly. It is a practical stopping rule rather than a guarantee that the model has reached the global minimum.

The application also validates the dataset before training. An empty dataset or a dataset containing only one class cannot support the intended binary classification training process, so the visualizer reports an appropriate error instead of proceeding.

Learning Objectives

By interacting with the visualizer, users can:

1. Understand how two input features contribute to a Logistic Regression prediction.
2. Explain the roles of weights and bias.
3. Understand how the sigmoid function converts a linear score into a probability.
4. Distinguish predicted probabilities from predicted class labels.
5. Explore how the decision threshold affects classification.
6. Understand binary cross-entropy as a measure of prediction error.
7. Observe how batch gradient descent updates model parameters.
8. Investigate how the learning rate affects training behavior.
9. Compare linearly separable and noisy datasets.
10. Interpret a loss curve and understand the model’s stopping conditions.

Technologies and Design

* HTML, CSS, and JavaScript.
* Single-page, single-file application.
* No external libraries or build dependencies.
* Interactive canvas-based visualizations.
* Dark-themed interface with independently scrollable columns.
* Responsive layout for different screen sizes.
* High-resolution canvas rendering for crisp visualizations.

Project Information

Project: Logistic Regression Visualizer

Course: Introduction to Data Analytics

Institution: CEi, King Mongkut’s Institute of Technology Ladkrabang (KMITL)

Project Type: Interactive machine learning education tool