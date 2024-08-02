# Segmentation of Multiple Sclerosis Disease Plaques from MRI Images Using 3D Attention U-Net

## Overview
This repository contains the implementation of a 3D Attention U-Net model for segmenting Multiple Sclerosis (MS) disease plaques from MRI images. The model is designed to accurately segment lesions and track their evolution over time, addressing the unique challenges presented by MS lesion segmentation in longitudinal MRI datasets.

## Dataset
The model was trained and tested on the dataset from the *Longitudinal MS Lesion Segmentation Challenge*, conducted at the 2015 International Symposium on Biomedical Imaging in New York, NY. The challenge involved applying automatic lesion segmentation algorithms to MR neuroimaging data acquired at multiple time points from MS patients.

### Reference
- Carass A, et al. Longitudinal multiple sclerosis lesion segmentation: Resource and challenge. Neuroimage. 2017;148:77-102. [Paper Link](https://doi.org/10.1016/j.neuroimage.2016.12.064)

### Challenge Details
- The challenge focused on evaluating the segmentation accuracy of algorithms against manual segmentations and their ability to track lesion evolution.
- Data included MR neuroimaging from multiple time points, providing a dynamic view of lesion development in MS patients.

## Model Performance
The model achieved a performance metric of 92.871 on the test set, demonstrating its effectiveness in segmenting MS lesions with high accuracy.

## Model Overview
The `attn_unet_3D` function defines an Attention U-Net model for 3D image data, particularly suited for tasks like volumetric image segmentation. This architecture is a variant of the standard U-Net model, augmented with attention gates to focus on salient features, enhancing the model's performance in applications like medical image analysis.

## Architecture Details

### Input Layer
- **Input**: The model starts with an input layer that accepts 3D data.

### Downsampling Path (Encoder)
- **Convolutional Blocks**: Each block in this path consists of two 3D convolutional layers with ReLU activation, followed by batch normalization.
- **Number of Filters**: The number of filters doubles at each level (32, 64, 128, 256), allowing the network to capture more complex features.
- **Pooling**: Each convolutional block is followed by a 3D Max Pooling layer to reduce the spatial dimensions.

### Center Block
- **Convolution**: A central convolutional block with 512 filters processes the data at the lowest resolution.

### Attention Gates
- **Function**: Attention gates are applied before each upsampling step. They aim to enhance relevant features and suppress irrelevant ones for better segmentation accuracy.
- **Components**: These gates involve operations like convolutions, activations, and upsampling to generate a gating signal.

### Upsampling Path (Decoder)
- **Transposed Convolutions**: The model uses 3D transposed convolutions to increase the spatial resolution of feature maps.
- **Concatenation**: The transposed feature maps are concatenated with corresponding cropped feature maps from the downsampling path.
- **Filters**: The number of filter halves with each upsampling step (256, 128, 64, 32).

### Output Layer
- **Final Convolution**: A 3D convolutional layer with a single filter and a sigmoid activation function generates the final output, typically a segmented 3D image.
![image](https://github.com/user-attachments/assets/81436efc-f122-4f89-887d-52712f982802)

## Compilation Details

### Loss Function
- **Focal Tversky Loss**: A custom loss function that is a variant of the Tversky loss, adapted to focus more on learning from difficult examples. It's particularly useful for dealing with class imbalance, which is common in medical image segmentation.

### Metric
- **Dice Coefficient Correct**: This metric is likely a variant of the Dice coefficient, a common metric in image segmentation tasks, especially for evaluating performance in medical imaging.
- 
## Comparative Visualization of MRI Slice and Corresponding Segmentation Outputs
![image](https://github.com/AliAmini93/MRI-MS-Plaques-Segmentation/assets/96921261/a9607f7a-4ee6-4173-90d7-9bfefb0ae7c7)

## License
This project is licensed under the MIT License - see the LICENSE.md file for details.

