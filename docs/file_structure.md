# File Structure and Purpose

This document explains the organization and purpose of the main files and directories in the Manga Colorization project.

## Root Directory

*   **`inference.py`**: The main entry point for running the colorization pipeline.
    *   Parses command-line arguments (e.g., input path, model paths, options).
    *   Initializes the `MangaColorizator`.
    *   Iterates through input images/directories.
    *   Handles saving the colorized output.

*   **`colorizator.py`**: Encapsulates the core colorization logic.
    *   Defines the `MangaColorizator` class.
    *   Manages the loading of the Generator and Denoiser models.
    *   Orchestrates the preprocessing (denoising, resizing/padding), inference, and post-processing steps.
    *   Interacts with the `networks.models.Colorizer` and `denoising.denoiser.FFDNetDenoiser`.

*   **`requirements.txt`**: Lists the Python dependencies required to run the project.

*   **`readme.md`**: Provides general instructions on installation, model download, and usage.

## Directories

### `networks/`
Contains the definition of the colorization generator model.

*   **`models.py`**:
    *   Defines the `Generator` class, which is the main neural network architecture (based on U-Net with ResNeXt blocks and Spectral Normalization).
    *   Defines the `Colorizer` wrapper class.
    *   Includes custom layers like `Selayer` (Squeeze-and-Excitation), `SpectralNorm`, and `ResNeXtBottleneck`.
*   **`extractor.py`**: Likely used for feature extraction or as part of the discriminator/perceptual loss during training (though primarily used here for loading the generator if needed).

### `denoising/`
Contains the implementation of the denoising functionality.

*   **`denoiser.py`**:
    *   Defines the `FFDNetDenoiser` class.
    *   Handles loading of FFDNet weights (RGB or grayscale).
    *   Provides the `get_denoised_image` method which processes the input image to remove noise.
*   **`models.py`**:
    *   Implements the `FFDNet` architecture (a DnCNN-based model with downsampling and upsampling).
*   **`functions.py`**: Helper functions for FFDNet (e.g., pixel shuffling/unshuffling for downsampling).
*   **`utils.py`**: Utility functions specific to denoising (e.g., normalization, conversion between variable and cv2 image).

### `utils/`
General utility functions.

*   **`utils.py`**: Contains helper functions like `resize_pad`, which ensures input images are divisible by 32 (required by the network architecture).

### `figures/`
*   Contains example images (original and colorized) used in the README to demonstrate the results.
