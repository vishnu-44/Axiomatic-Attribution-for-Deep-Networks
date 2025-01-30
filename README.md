### Dataset

This repository includes a **diverse dataset** of images and text, enabling the testing and visualization of **Integrated Gradients** on a variety of input types. The dataset has been expanded with extra images to provide more varied input for testing how the Integrated Gradients method works across different domains. 

---

### Paper-Work2: Integrated Gradients on Text and Image Data

This repository also includes the implementation of **Integrated Gradients** applied to both **text** and **image** data.

- **For Text Data**: We use the **BART model** from Facebook. The BART model is a transformer-based architecture designed for sequence-to-sequence tasks like text generation, summarization, and classification. In this implementation, we apply Integrated Gradients to the text data to determine which words contribute the most to the model's prediction. This helps in understanding how the model makes decisions based on textual inputs.
  
- **For Image Data**: We use the **VGG19 model**, a deep convolutional neural network that has been widely used for image classification tasks. By applying Integrated Gradients to image inputs, we can identify the regions of an image that most influence the model's prediction, providing insight into the decision-making process of the VGG19 model.

By using Integrated Gradients, we aim to gain interpretability and transparency for both types of data (text and image) in deep learning models, helping researchers understand the contributions of individual features to the model’s output which is pretty much the starting step of explainbale AI.
