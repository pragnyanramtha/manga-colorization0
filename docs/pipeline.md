# Pipeline Workflow

This document details the step-by-step process of converting a black-and-white manga image into a colorized version.

## 1. Input Handling
-   The user provides an input path (file or directory) via the command line (`-p` argument).
-   If a directory is provided, the script (`inference.py`) iterates through all images within it.
-   Images are loaded using `matplotlib.pyplot.imread` or `cv2.imread`.

## 2. Preprocessing & Denoising
Before colorization, the image undergoes preprocessing to ensure optimal results. This is handled by the `MangaColorizator` class in `colorizator.py`.

### Denoising (Optional but Recommended)
-   If enabled (default), the image is passed through an FFDNet (Fast and Flexible Denoising Convolutional Neural Network).
-   The `FFDNetDenoiser` handles this:
    -   Inputs are normalized and converted to PyTorch tensors.
    -   Noise level (`sigma`) is provided (default is 25).
    -   The network estimates and subtracts the noise map from the input image.
    -   This step is crucial for scanned manga to remove compression artifacts and grain.

### Resizing and Padding
-   The generator requires input dimensions to be divisible by 32 (due to downsampling/upsampling layers).
-   The `resize_pad` function (in `utils/utils.py`) resizes the image while maintaining aspect ratio and pads it if necessary to meet the divisibility requirement.
-   Padding information is stored to reverse the process later.

## 3. Colorization Inference
-   The preprocessed image (now a tensor on the GPU/CPU) is fed into the `Generator` model (defined in `networks/models.py`).
-   **Model Architecture**:
    -   **Encoder**: Extracts features using a customized ResNeXt-based backbone with Squeeze-and-Excitation blocks.
    -   **Bottleneck**: Processes deep features using multiple ResNeXt blocks.
    -   **Decoder**: Upsamples the features to generate the colorized output (RGB image).
    -   **Spectral Normalization**: Used in convolutional layers for stability during training.
-   The model outputs a 3-channel (RGB) image tensor.

## 4. Post-processing
-   The output tensor is detached from the computation graph and moved to the CPU.
-   Values are rescaled from `[-1, 1]` to `[0, 1]`.
-   **Unpadding**: The padding added in step 2 is removed to restore the original image dimensions.
-   The result is converted to a NumPy array.

## 5. Output
-   The colorized image is saved to disk using `matplotlib.pyplot.imsave`.
-   The filename is typically appended with `_colorized` or saved into a `colorization` subdirectory.
