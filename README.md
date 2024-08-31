Project 0 Getting Started
====================

**University of Pennsylvania, CIS 5650: GPU Programming and Architecture, Project 0**

* Michael Rabbitz
  * https://www.linkedin.com/in/mike-rabbitz/
* Tested on: Windows 10, i7-9750H @ 2.60GHz 32 GB, RTX 2060 6GB (Personal)

## CUDA Compute Capability
### The CUDA Compute Capability of the RTX 2060 is 7.5 as displayed in the following image
![Cuda_Compute_Capability](images/CudaComputeCapability.PNG)

## Nsight Debugging
### Breakpoint condition set to index == 1025
The block index shows correspondance between variable blockIdx in the Autos window and CTA under the Shader Info column within Warp Info.
The thread index shows correspondance where if you look at Thread under Shader Info within Warp Info, in the highlighted row the value (0, 0, 0) is the first index of the 4 green segments to the right. The 2 green segments on the left hold value 0 for y (x, 0, z), and the right 2 segments hold value 1 for y (x, 1, z). Within each set of 2 segments, there are 16 sub-segments (8 sub-segments in each segment). From left to right, they hold the value 0 to 15, and this value is given to x. This shows why the threadIdx is {x = 1, y = 1, z = 0} for the sub-segment with the yellow arrow and red background.

![Nsight_Debugging](images/NsightDebugging.PNG)

## Nsight Systems
### Analysis Summary
![Nsight_Systems_Analysis_Summary](images/NsightSystems_AnalysisSummary.PNG)
### Timeline View
![Nsight_Systems_Timeline](images/NsightSystems_Timeline.PNG)

## Nsight Compute
### Summary
![Nsight_Compute_Summary](images/NsightCompute_Summary.PNG)
### Details
![Nsight_Compute_Details](images/NsightCompute_Details.PNG)

## WebGL 2 Compatability
### From https://webglreport.com/?v=2
![WebGL_2_Compatibility](images/WebGL_2_Compatibility.PNG)

## WebGPU Compatability
### From https://webgpureport.org
![WebGPU_Compatibility_0](images/WebGPU_Compatibility_0.PNG)
### From https://webgpu.github.io/webgpu-samples/?sample=instancedCube
![WebGPU_Compatibility_1](images/WebGPU_Compatibility_1.PNG)









