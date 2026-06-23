# Interactive INT8 Quantization Visualizer

An interactive, local-first web dashboard designed to visualize how high-precision neural network weights and activations (`FP32`) are mapped into hardware-efficient 8-bit integers (`INT8`). 

**[👉 Live Interactive Dashboard](https://manthasaigopal/quantization-visualization-tool/)**


## 🚀 Overview

In production deep learning deployment (using frameworks like NVIDIA TensorRT or ONNX Runtime), **Quantization** is essential for reducing VRAM footprints and maximizing hardware throughput. This tool serves as a visual playground to understand the mathematical mechanics, dynamic boundaries, and trade-offs involved in lower-precision signal processing.

### Key Visualizations
* **FP32 Space vs. Information Loss:** Observe how continuous distributions map to discrete bins and how a poorly calibrated **Scale ($S$)** or **Zero-point ($Z$)** introduces quantization noise, measured via Mean Squared Error (MSE).
* **Hardware Register Space:** View the actual distribution inside the 256 physical integer slots (`-128` to `127`) and see exactly where overexposure/clipping occurs when outliers escape the quantization boundaries.


## 🧮 The Mathematics Behind the Visualizer

The dashboard runs uniform affine quantization locally in the browser using the standard linear mapping equation:

$$q = \text{clip}\left( \text{round}\left(\frac{x}{S}\right) + Z, \,\, -128, \,\, 127 \right)$$

And approximates the original value during de-quantization via:
$$\hat{x} = S \cdot (q - Z)$$

### Supported Modes
* **Asymmetric Quantization:** Maps the tight minimum/maximum boundaries of the tensor to the full range of the integer register, explicitly calculating $Z$ to align real-world `0.0`.
* **Symmetric Quantization:** Centers the boundaries strictly around zero ($\max(|x_{min}|, |x_{max}|)$), forcing $Z = 0$ for optimized hardware execution pipelines.

## 📄 License
MIT License
