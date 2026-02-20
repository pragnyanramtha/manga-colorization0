# Future Improvements

This document lists potential enhancements and areas for improvement in the Manga Colorization project. These suggestions range from code quality updates to feature additions.

## Code Quality & Maintainability

1.  **Refactoring**: Break down large functions in `inference.py` and `colorizator.py` into smaller, more testable components.
2.  **Type Hinting**: Add type hints to function signatures and variables for better readability and IDE support.
3.  **Logging**: Replace `print` statements with a proper logging framework (`logging` module) to control verbosity and log levels (INFO, DEBUG, ERROR).
4.  **Testing**: Implement unit tests (using `pytest` or `unittest`) for core logic in `colorizator.py` and `utils/utils.py` to ensure reliability during refactoring.

## Feature Enhancements

1.  **Support for More Formats**: Extend support beyond `.png` and `.jpg` to include formats like `.webp`, `.tiff`, and `.heic`.
2.  **Progress Indicators**: Integrate a progress bar library like `tqdm` to show processing status when handling large folders.
3.  **Config Files**: Allow users to specify configuration options (model paths, output directories, denoising settings) in a YAML or JSON file instead of solely relying on command-line arguments.
4.  **Web Interface**: Develop a simple web UI (using Flask, FastAPI, or Streamlit) to allow users to upload images and view results directly in the browser.
5.  **Dockerization**: Create a `Dockerfile` to containerize the application, ensuring consistent environments and easier deployment.

## Model Improvements

1.  **Model Optimization**: Explore quantization or pruning techniques to reduce model size and improve inference speed on CPU/Edge devices.
2.  **Updated Architectures**: Experiment with newer GAN architectures (e.g., StyleGAN2, BigGAN) or Transformer-based models for potentially better colorization quality.
3.  **Training Script**: Provide scripts and instructions for users to fine-tune the model on their own datasets.

## Documentation

1.  **API Documentation**: Generate API documentation (using Sphinx or similar) for the Python modules.
2.  **Troubleshooting Guide**: Add a section for common issues and solutions (e.g., CUDA out of memory, missing dependencies).
