Problem Statement:

The primary objectives of this capstone project are as follows:
 a) Lane Detection: To enable a self-driving vehicle to navigate effectively, we need to implement a lane detection system. This system should take an image from a car dashboard or a video feed as input and produce an output image with the lanes marked. 
b) Steering Angle Calculation: Once the lanes are detected and marked, the next step is to use these lanes as guidance to determine the steering angle for autonomous driving. The steering angle should be calculated based on the relative position of the center of the captured image and the center of the detected lanes. This will enable the self-driving vehicle to stay within the lanes and navigate safely.

Introduction: 
Self-driving vehicles represent a technological revolution in the automotive industry. The ability of a self-driving car to navigate safely and efficiently is heavily dependent on the accurate detection of lanes on the road. This project aims to develop a Lane Detection system for self-driving vehicles that can detect and mark the lanes in real-time, and subsequently use this information to determine the steering angle for autonomous driving.
Humans can easily identify and understand road markings like yellow and white lines, but for a computer, these are just pixels with different color values. Teaching a computer to recognize and interpret these features requires sophisticated image processing and computer vision techniques.


Prerequisite:
Knowledge of python, ML and deep learning. Deep learning involves utilizing multiple-layered neural networks, which use mathematical properties to minimize losses from predictions vs. actuals to converge toward a final model, effectively learning as they train on data

Dataset: 
The dataset provided in the project description (e.g., https://xingangpan.github.io/projects/CULane.html) .

Methods:
Convolutional Neural Networks (CNNs) are typically constructed by layering convolutional operations one after another. While CNNs have demonstrated robustness in extracting meaningful information from raw pixel data, their ability to fully exploit spatial connections between pixels along the rows and columns of an image has not thoroughly investigated. These connections play a crucial role in understanding semantic objects characterized by distinct shapes but inconsistent visual appearances, like traffic lanes. Traffic lanes, for instance, are frequently obscured or may not be clearly marked on the road surface.
Spatial CNN (SCNN), which generalizes traditional deep layer-by-layer convolutions to slice-byslice convolutions within feature maps, thus enabling message passings between pixels across rows and columns in a layer. Such SCNN is particular suitable for long continuous shape structure or large objects, with strong spatial relationship but less appearance clues, such as traffic lanes, poles, and wall.
Spatial CNN (SCNN), a generalization of deep convolutional neural networks to a rich spatial level. In a layer-by-layer CNN, a convolution layer receives input from the former layer, applies convolution operation and nonlinear activation, and sends result to the next layer. This process is done sequentially. Similarly, SCNN views rows or columns of feature maps as layers and applies convolution, nonlinear activation, and sum operations sequentially, which forms a deep neural network. In this way information could be propagated between neurons in the same layer. It is particularly useful for structured object such as lanes, poles, or truck with occlusions, since the spatial information can be reinforced via inter layer propa

Spatial CNN Traditional methods to model spatial relationship are based on Markov Random Fields (MRF) or Conditional Ran- dom Fields (CRF).
It can be seen that in the message-passing process of traditional methods, each pixel receives information from all other pixels, which is very computational expensive and hard to be used in real time tasks as in autonomous driving. For MRF, the large convolution kernel is hard to learn and usually requires careful initialization (Tompson et al. 2014; Liu et al. 2015). Moreover, these methods are applied to the output of CNN, while the top hidden layer, which comprises richer information, might be a better place to model spatial relationship

To address these issues, and to more efficiently learn the spatial relationship and the smooth, continuous prior of lane markings, or another structured object in the driving scenario, we propose Spatial CNN. Note that the ’spatial’ here is not the same with that in ’spatial convolution’, but denotes propagating spatial information via specially designed CNN structure. As shown in the ’SCNN D’ module of Fig. 2 , considering a SCNN applied on a 3-D tensor of size C × H × W, where C, H, and W denote the number of channel, rows, and columns respectively. The tensor would be splited into H slices, and the first slice is then sent into a convolution laye
 
Fig 2: Spatial CNN

As shown in the ’SCNN D’ module of Fig. 3 (b), considering a SCNN applied on a 3-D tensor of size C × H × W, where C, H, and W denote the number of channel, rows, and columns respectively. The tensor would be splited into H slices, and the first slice is then sent into a convolution layer
with C kernels of size C ×w, where w is the kernel width. In a traditional CNN the output of a convolution layer is then fed into the next layer, while here the output is added to the next slice to provide a new slice. The new slice is then sent to the next convolution layer and this process would continue until the last slice is updated. Specifically, assume we have a 3-D kernel tensor K with element Ki,j,k denoting the weight between an element in channel i of the last slice and an element in channel j of the current slice, with an offset of k columes between two elements. Also denote the element of input 3-D tensor X as Xi,j,k, where i, j, and k indicate indexes of channel, row, and column respectively. Then the forward computation of SCNN is:
where f is a nonlinear activation function as ReLU. The X with superscript 0 denotes the element that has been updated. Note that the convolution kernel weights are shared across all slices, thus SCNN is a kind of recurrent neural network. Also note that SCNN has directions. In Fig. 3 (b), the four ’SCNN’ module with suffix ’D’, ’U’, ’R’, ’L’ denotes SCNN that is downward, upward, rightward, and leftward respectively.
Steering Angle Calculation:
The procedure used is divided in multiple stages. The first stage includes determination of the road's midpoint using Robert edge detection and morphological operations. This midpoint is then used to determine the angle by which a vehicle must steer to maintain its position at the center of the road
Table 1:CONDITIONS FOR DIFFERENT ROAD SCENARIOS
 

b1=b2=640/2=320 pixel distance a1= distance of (250, 0) value from edge. a2= distance of (250, 640) value from edge.
𝜃1=𝑎𝑟𝑐tan(𝑎1/𝑏1) 
 𝜃2=𝑎𝑟𝑐tan(𝑎2/𝑏2) 
 Φ = 𝜃1 − 𝜃2 
 𝜇 = 𝑎1 − 𝑎2 (7)
 
	 
                                                             Fig.3 Road lane extracted

CULane is a large scale challenging dataset for academic research on traffic lane detection. It is collected by cameras mounted on six different vehicles driven by different drivers in Beijing.
Data examples are shown below in the figure 1.


