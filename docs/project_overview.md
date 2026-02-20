# Project Overview: Manga Colorization

This project, also known as "Manga Colorization v2.5", is designed to automatically colorize black and white manga images. It leverages deep learning models, specifically Generative Adversarial Networks (GANs), to predict color information from grayscale inputs.

## Key Features

-   **Automatic Colorization**: Transforms black and white manga pages into colorized versions without manual intervention.
-   **Denoising**: Includes a denoising step using FFDNet (Fast and Flexible Denoising Convolutional Neural Network) to clean up input images before colorization, which is particularly useful for scanned manga.
-   **Batch Processing**: Supports processing entire folders of images at once, making it suitable for colorizing whole chapters or volumes.
-   **Customizable Pipeline**: Users can toggle denoising, adjust the denoising strength (`sigma`), and specify the target image size.
-   **GPU Support**: Designed to run efficiently on GPUs (CUDA) for faster inference, but also supports CPU execution.

## How It Works

The core of the project relies on two main neural network models:

1.  **The Generator**: A deep neural network (based on U-Net architecture with ResNeXt blocks) that takes a grayscale image as input and outputs a colorized version. It is trained to understand the structures and textures in manga to apply appropriate colors.
2.  **The Denoiser**: An FFDNet model that removes noise and artifacts from the input images. This step is crucial for maintaining high-quality output, as noise can often be misinterpreted by the colorization model.

## Usage

The project is primarily used via the command line interface (`inference.py`). Users provide paths to input images or directories, and the script handles the loading, processing, and saving of the results.

Example command:
```bash
python inference.py -p "path/to/image_or_folder"
```

The output images are saved in a `colorization` subdirectory within the input folder or alongside the input image.
