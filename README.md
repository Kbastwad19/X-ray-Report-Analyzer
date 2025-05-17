# X-ray Report Analyzer

## Overview
The X-ray Report Analyzer is a Python-based project designed to process and analyze X-ray images to detect potential fractures or anomalies in bone structures. It leverages computer vision techniques using OpenCV and machine learning models to preprocess images, segment them, and identify regions of interest that may indicate fractures. The project also includes visualization tools using Matplotlib to display results, such as histograms and distance plots.

This tool is particularly useful for researchers, medical imaging enthusiasts, or developers exploring automated X-ray analysis. It supports multiple image formats (JPG, PNG) and allows users to switch between different machine learning models for thresholding predictions.

## Features
- **Image Preprocessing**: Loads and preprocesses X-ray images in various formats.
- **Edge Detection and Segmentation**: Applies manual edge detection and thresholding to segment bone structures.
- **Fracture Detection**: Identifies potential fracture points by analyzing distance variations in segmented regions.
- **Visualization**: Displays processed images, distance plots, and histograms for analysis.
- **Model Flexibility**: Supports multiple machine learning models (`ridge_model`, `lr_model`, `rfc_model`) for thresholding.
- **Customizable Inputs**: Allows users to specify input image names and models via configuration in `main.py`.

## Prerequisites
To run the X-ray Report Analyzer, ensure you have the following installed:
- Python 3.8 or higher
- Git
- Virtual environment (optional, but recommended)
- Required Python libraries (listed in `requirements.txt`)

## Setup Instructions
Follow these steps to set up and run the project:

### 1. Clone the Repository
git clone https://github.com/Kbastwad19/X-ray-Report-Analyzer.git


### 2. Create a Virtual Environment (Optional)
python -m venv vem

#### Activate the virtual environment:
vem\Scripts\activate

### 3. Install Dependencies
pip install -r requirements.txt


### 4. Navigate to the Project Directory
cd manual


### 5. Run the Project
python main.py


## Usage
To analyze an X-ray image, follow these steps:

### 1. Prepare the Image
Place the X-ray image in the `images/Fractured Bone/` directory and a resized version in the `images/resized/` directory. Ensure the image is in JPG or PNG format.

### 2. Configure the Input
Edit `main.py` to specify the image name and model:
- **Line 6**: Set `img_name` to the name of your image file (without extension).
  img_name = "new"
 
- **Line 7**: Set `model_name` to one of the available models (`ridge_model`, `lr_model`, or `rfc_model`).
  model_name = "ridge_model"
 

### 3. Run the Script
python main.py

The script will:
- Load the image and its resized version.
- Apply preprocessing and segmentation.
- Detect potential fracture points.
- Display the processed images and visualizations.

### 4. View Results
- OpenCV windows will show the grayscale image and thresholded image.
- Matplotlib will display a plot of distance variations and a histogram of pixel intensities.
- Green rectangles on the original image highlight detected fracture regions.

## Model Selection
The project supports three machine learning models for predicting the thresholding value used in segmentation:

| Model         | Type                   | Use Case                                                                 | When to Use                                                                 |
|---------------|------------------------|--------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| `ridge_model` | Ridge Regression       | Best for general-purpose X-ray analysis with balanced performance.       | Use for standard X-ray images with moderate noise or unsure which to choose.|
| `lr_model`    | Linear Regression      | Suitable for images with clear bone structures and minimal noise.        | Choose for high-quality X-ray images with well-defined edges.              |
| `rfc_model`   | Random Forest Classifier| Ideal for complex images with high variability or non-linear patterns.    | Use for challenging X-ray images with significant noise or irregular bones. |

To change the model, update the `model_name` variable in `main.py`:
model_name = "rfc_model"


## Code Explanation
The `main.py` script is the core of the project. Below is a breakdown of its key components:

### 1. Image Loading
- Loads two versions of the X-ray image:
  - Original image from `images/Fractured Bone/`.
  - Resized image from `images/resized/`.
- Supports JPG and PNG formats (case-insensitive).
- Prints image details (shape, size, data type) for debugging.

### 2. Preprocessing
- Converts the original image to grayscale using `cv2.cvtColor`.
- Applies a median blur (`cv2.medianBlur`) to reduce noise while preserving edges.

### 3. Segmentation
- A machine learning model (loaded via `get_model`) predicts a thresholding value.
- The grayscale image is thresholded using `cv2.threshold` to create a binary image.
- A custom `segment_img` function (commented out) can be used for manual edge detection.

### 4. Fracture Detection
- Identifies transitions in the thresholded image to detect bone edges.
- Calculates the distance between edges for each row (`dist_list`).
- Flags significant distance variations (`err=15`) as potential fracture points (`danger_points`).
- Visualizes fracture points as green rectangles on the original image.

### 5. Visualization
- **OpenCV**: Displays grayscale and thresholded images.
- **Matplotlib**:
  - Plots distance variations (`dist_list`).
  - Displays processed image with fracture regions marked.
  - Generates a histogram of pixel intensities.

### 6. Error Handling
- Handles file loading errors for different image formats.
- Includes try-except blocks for fracture detection and plotting.

## Directory Structure
```
X-ray-Report-Analyzer/
├── images/
│   ├── Fractured Bone/   # Original X-ray images
│   └── resized/          # Resized X-ray images
├── manual/
│   ├── main.py           # Main script
│   ├── pre_process.py    # Preprocessing utilities
│   └── ...               # Supporting scripts
├── requirements.txt      # Dependencies
└── README.md             # Documentation
```

## Dependencies
Key dependencies (see `requirements.txt` for full list):
- `opencv-python`: Image processing and visualization.
- `numpy`: Numerical computations.
- `matplotlib`: Plotting and visualization.
- `scikit-learn` (assumed): Machine learning models.

Install them using:
```bash
pip install -r requirements.txt
```

## Troubleshooting
- **Image Not Found**: Ensure the image exists in both `images/Fractured Bone/` and `images/resized/` with the correct name/format (JPG/PNG).
- **Model Not Found**: Verify the specified model (`ridge_model`, `lr_model`, `rfc_model`) is available in `pre_process.py`.
- **Visualization Issues**: Check Matplotlib/OpenCV installation and console errors.
- **Performance Issues**: Resize large images to reduce processing time.

## Future Improvements
- Support more image formats (e.g., DICOM).
- Add adaptive thresholding for preprocessing.
- Enhance fracture detection with deep learning models.
- Command-line interface for easier configuration.
- Batch processing for multiple images.

## Contributing
1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Commit changes (`git commit -m "Add feature"`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a pull request.

## License
MIT License. See `LICENSE` for details.

## Contact
For questions or feedback, reach out via [GitHub Issues](https://github.com/Kbastwad19/X-ray-Report-Analyzer/issues).
``` 

This markdown file preserves all the key information while organizing it into clear sections with proper formatting for headings, lists, tables, and code blocks. The structure makes it easy to navigate and read.
