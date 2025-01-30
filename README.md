### Dataset

This repository includes a **diverse dataset** of images and text, enabling the testing and visualization of **Integrated Gradients** on a variety of input types. The dataset has been expanded with extra images to provide more varied input for testing how the Integrated Gradients method works across different domains. 

---

### Paper-Work2: Integrated Gradients on Text and Image Data

This repository also includes the implementation of **Integrated Gradients** applied to both **text** and **image** data.

- **For Text Data**: We use the **BART model** from Facebook. The BART model is a transformer-based architecture designed for sequence-to-sequence tasks like text generation, summarization, and classification. In this implementation, we apply Integrated Gradients to the text data to determine which words contribute the most to the model's prediction. This helps in understanding how the model makes decisions based on textual inputs.
  
- **For Image Data**: We use the **VGG19 model**, a deep convolutional neural network that has been widely used for image classification tasks. By applying Integrated Gradients to image inputs, we can identify the regions of an image that most influence the model's prediction, providing insight into the decision-making process of the VGG19 model.

By using Integrated Gradients, we aim to gain interpretability and transparency for both types of data (text and image) in deep learning models, helping researchers understand the contributions of individual features to the model’s output which is pretty much the starting step of explainbale AI.

## Axiomatic Attribution for Deep Networks

This paper is an extension to the previous paper for given for the reserach work which marks a starting for the core concept of *Explainable AI* by introducing key concepts such as *Integrated Gradients* and *Axiomatic Attribution*. While the previous work focused on computing gradients and going back and examining their impact on the model’s predictions, this paper dives deeper into the principles that should guide attribution methods.

### Key Axioms:

1. **Sensitivity**:  
   In previous work, we didn’t explicitly consider the scenario where a feature differs between the input and baseline as we jumped straight into the final output(basically input), but the predictions diverge as a result. According to this axiom, any differing feature should receive a non-zero attribution.  
   **Example**: For a function like \( f(x) = 1 - \text{ReLU}(1 - x) \), with a baseline of 0 and an input of 3, the gradient may flatten at 1, but the input still changes from the baseline, which should reflect a non-zero attribution.

2. **Implementation Invariance**:  
   Two networks are considered functionally equivalent if their outputs are the same for all inputs, even if their architectures or implementations differ significantly. Attribution methods should respect this equivalence and provide consistent attributions across different models that produce the same output.

3. **Completence**
   Integrated gradients satisfy an axiom called completeness that the attributions add up to the difference between the output of F at the input x and the baseline x.This axiom ensures that the attributions provided by the method are faithful and accurate in explaining the model's prediction.

4. **Lineraity**
     They also follow the axioms of linearity where it follows a straightline path from the baseline to input.
   
### Architecture/Working:
The Integrated Gradients method is defined as follows:

$$
\text{IntegratedGrads}_i(x) := (x_i - x'_i) \times \int_{\alpha=0}^{1} \frac{\partial F(x' + \alpha \times (x - x'))}{\partial x_i} \, d\alpha
$$

Where:
- $x_i$ is the original input feature.
- $x'_i$ is the baseline or reference value for that feature.
- $F$ is the model function.
- $\alpha$ scales the input from the baseline to the actual input.


In this method we use a straight line path from the baseline to the input, where the basic idea is calculate the gardient of all interporated inputs and take an average of these gradients which is then scaled from 0 to 1 to show the average contribution of each pixels all the way along from the baseline to the input 

### Explanation of Integrated Gradients Equation Components

#### 1. Feature Difference Component:
$$
(x_i - x'_i)
$$

It basically acts as a scaling factor. This factor ensures that the contributions are calculated relative to how much each feature differs from its baseline showing the impact of specific feature on the output.

#### 2. Gradient Integration Component:
$$
\int_{\alpha=0}^{1} \frac{\partial F(x' + \alpha \times (x - x'))}{\partial x_i} \, d\alpha
$$

This integral calculates the gradients of the model output \(F\) with respect to the feature \(x_i\) at all points along the straight-line path from the baseline \(x'\) to the input \(x\) as parameterized by \(\alpha\). Here, \(\alpha\) varies from 0 (the baseline) to 1 (the actual input), allowing us to examine how sensitive the output is to changes in each feature across this path. The integral aggregates these gradients to determine the overall contribution of the feature \(x_i\).In Simple terms we can say that we are calculating the gradient of all the interporation states wrt to input and aaverage it ,to estimate the 
cntribution of all these states form basline to input to achive the input.

