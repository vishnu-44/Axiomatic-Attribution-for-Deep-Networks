### Dataset

This repository includes a **diverse dataset** of images and text, enabling the testing and visualization of **Integrated Gradients** on a variety of input types. The dataset has been expanded with extra images to provide more varied input for testing how the Integrated Gradients method works across different domains. 

---

### Paper-Work2: Axiomatic Attribution for Deep Networks

This repository also includes the implementation of **Integrated Gradients** applied to both **text** and **image** data.

- **For Text Data**: We use the **BART model** from Facebook. The BART model is a transformer-based architecture designed for sequence-to-sequence tasks like text generation, summarization, and classification. In this implementation, we apply Integrated Gradients to the text data to determine which words contribute the most to the model's prediction. This helps in understanding how the model makes decisions based on textual inputs.
  
- **For Image Data**: We use the **VGG19 model**, a deep convolutional neural network that has been widely used for image classification tasks. By applying Integrated Gradients to image inputs, we can identify the regions of an image that most influence the model's prediction, providing insight into the decision-making process of the VGG19 model.

By using Integrated Gradients, we aim to gain interpretability and transparency for both types of data (text and image) in deep learning models, helping researchers understand the contributions of individual features to the model’s output which is pretty much the starting step of explainbale AI.


### Key Axioms:

1. **Sensitivity**:
   In the previous work, we didn't explicitly account for the case where a feature differs between the input and baseline, which could affect the model's predictions. According to the **Sensitivity** axiom, any feature that differs between the input and baseline should receive a non-zero attribution.  
   **Example**:  
   Consider the function \( f(x) = 1 - \text{ReLU}(1 - x) \), where the baseline is 0 and the input is 3. While the gradient may flatten at 1, the input still changes from the baseline, which should reflect a non-zero attribution.

2. **Implementation Invariance**:  
   Two models are considered functionally equivalent if their outputs are identical for all inputs, even if their architectures or implementations differ. Attribution methods should respect this equivalence and provide consistent attributions across different models that yield the same output. This ensures fairness and uniformity in the attribution process.

3. **Completeness**:  
   Integrated Gradients satisfies the **Completeness** axiom, meaning the attributions sum up to the total difference between the model's output at the input \(x\) and the baseline \(x'\). This ensures that the attributions provided by the method faithfully explain the model's prediction, and no information is lost in the process.

4. **Linearity**:  
   The method follows the **Linearity** axiom, meaning that the attribution is linear along the straight-line path from the baseline to the input. This property ensures that the contributions from different features are additive and follow a proportional relationship.

---

### Architecture/Working of Integrated Gradients:

The **Integrated Gradients** method is mathematically defined as:

The Integrated Gradients method is mathematically defined as:
$$
\text{IntegratedGrads}_i(x) := (x_i - x'_i) \times \int_{\alpha=0}^{1} \frac{\partial F(x' + \alpha \times (x - x'))}{\partial x_i} \, d\alpha
$$
![{4C641701-2E56-4F9A-AC0B-AF43A81FD09B}](https://github.com/user-attachments/assets/2d3a0f2e-835f-43af-917e-5bf43318d243)

Where:
- \( x_i \) is the original input feature.
- \( x'_i \) is the baseline or reference value for that feature.
- \( F \) is the model function.
- \( \alpha \) scales the input from the baseline to the actual input.



The method uses a **straight-line path** from the baseline to the input. The core idea is to compute the gradient for all interpolated inputs and average them. This average gradient is then scaled from 0 to 1, showing the average contribution of each pixel or feature along the path from baseline to input.

---

### Explanation of Integrated Gradients Equation Components:

#### 1. **Feature Difference Component**:

$$
(x_i - x'_i)
$$

This component acts as a **scaling factor**. It determines how much a particular feature differs from its baseline, thus influencing the contribution of that feature to the model's output.

#### 2. **Gradient Integration Component**:

$$
\int_{\alpha=0}^{1} \frac{\partial F(x' + \alpha \times (x - x'))}{\partial x_i} \, d\alpha
$$

This integral computes the gradients of the model's output \( F \) with respect to the feature \( x_i \) at all points along the straight-line path from the baseline \( x' \) to the input \( x \), as parameterized by \( \alpha \). The variable \( \alpha \) ranges from 0 (baseline) to 1 (input). This allows us to analyze how sensitive the output is to changes in each feature across the path.

In simple terms, we compute the gradient for all interpolation states relative to the input and average them. This gives us an estimate of the contribution of each state along the path from the baseline to the input.

---

### Summary of the Method:

- **Sensitivity** ensures that any change from the baseline to the input is accounted for in the attribution.
- **Implementation Invariance** guarantees that attribution is consistent across different model architectures with the same output.
- **Completeness** assures that the total attribution adds up to the difference between the output at the input and the baseline.
- **Linearity** implies that contributions from features are additive and proportional across the interpolation path.

The Integrated Gradients method provides a transparent and mathematically grounded way to attribute model predictions, making it a valuable tool for interpretable machine learning.

---

By including these clarifications and formatting, the explanations will be clearer to a broader audience. The breakdown of the components will help readers, even those unfamiliar with the method, understand the underlying logic.

