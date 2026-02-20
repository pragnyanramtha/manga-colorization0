# Tech Stack

This document outlines the core technologies and libraries used in the Manga Colorization project.

## Programming Language

*   **Python**: The entire project is written in Python, leveraging its extensive ecosystem for machine learning and image processing.

## Deep Learning Framework

*   **PyTorch**: The primary deep learning framework. It handles:
    *   **Model Definition**: Using `torch.nn` modules to define the Generator (U-Net with ResNeXt blocks) and Denoiser (FFDNet).
    *   **Autograd**: For computing gradients during training (though this codebase is primarily for inference).
    *   **GPU Acceleration**: Leveraging CUDA (`torch.cuda`) for fast processing of images.

## Computer Vision & Image Processing

*   **OpenCV (`cv2`)**: Used for image resizing, format conversion, and some basic preprocessing steps (like handling BGR/RGB channels).
*   **Matplotlib (`matplotlib.pyplot`)**: Used for reading input images (`imread`) and saving the final colorized results (`imsave`). It also provides visualization capabilities if needed.
*   **NumPy**: The fundamental package for scientific computing in Python. Used extensively for array manipulation, handling image data (height, width, channels), and converting between PyTorch tensors and image formats.

## Neural Network Architectures

*   **Generative Adversarial Network (GAN)**: The core colorization model is a GAN-based architecture.
    *   **ResNeXt**: The generator uses ResNeXt blocks for feature extraction and processing.
    *   **Squeeze-and-Excitation (SE)**: Enhances representational power by explicitly modelling interdependencies between channels.
    *   **Spectral Normalization**: Used to stabilize training of the discriminator (and generator layers here).
*   **FFDNet**: A Fast and Flexible Denoising Convolutional Neural Network used for the denoising step. It's designed to handle various noise levels efficiently.
