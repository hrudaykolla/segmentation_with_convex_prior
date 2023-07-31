# Scribble-based Image Segmentation with Convexity Prior

<img align="center" src="result.png" width="750">

## Introduction

simple architecture for segmenting convex objects in images using user-provided scribbles. The proposed approach involves a primary model to segment pixels into foreground and background regions. The primary model’s output is subsequently passed to a Convex network, which refines the foreground pixels to adhere to the convexity prior, assuming smooth and continuous boundaries without concave regions. The architecture achieves memory efficiency and does not require training on a vast number of images, making it suitable for practical applications with limited computational resources.
This has been accomplished using two approaches:
• Approach 1: Generating the convex segmented image using a fully connected network and convex network architecture.
• Approach 2: Generating the convex segmented image using a pre-trained segmentation network and convex network architecture.

## Requirements

See requirements.txt file

## Setup

1.  Install PyTorch and other required Python libraries in a virtual environment with:

    ```
    pip install -r requirements.txt
    ```

2.  Collect Data:

    Foreground and background scribbles are to be made on Images that need to be segmented. Save them in the data folder.

    For example, data floder contains the folder single_apple which contains the input image, scribble_fg and scribble_bg.
    
    All the data to be stored in a similar way.
    

## Usage

`python main.py` executes and runs the code with all the default arguments.

For changing the default arguments follow the below instructions:

1. Input: Folder of the image which needs to be segmented to be proved here.

    `python main.py --inputpath data/single_apple/`

2. Primary model selection: 

    Neural net as a primary model: `python main.py -pm neuralnet`

    Segmentation net as a primary model: `python main.py -pm segmentationnet`

3. Primary model parameters:
    
    Batch size, epochs, learning rate, and hidden units are some of the neural net parameters that can be altered through command line.

    `python main.py -pm neuralnet -nnbs 64 -nne 100 -nnlr 0.00001 -nnhu 256`

    Batch size, epochs, learning rate are some of the segmentation net parameters that can be altered through command line.
    `python main.py -pm segmentationnet -snbs 64 -sne 100 -snlr 0.0001`

4. Convex net parameters:
    
    Batch size, epochs, learning rate, hidden units are some of the convex net parameters that can be altered through command line.
    
    `python main.py -pm neuralnet -nnbs 64 -nne 100 -nnlr 0.00001 -nnhu 256 -cnbs 64 -cne 50 -cnlr 0.00001 -cnhu 256`
    `python main.py -pm segmentationnet -snbs 64 -sne 100 -snlr 0.0001 -cnbs 64 -cne 50 -cnlr 0.00001 -cnhu 256`

## Outputs

The output of the network is saved in repective data folder. Output contains result.png, model configurations, terminal output and logs of tensorboard.
