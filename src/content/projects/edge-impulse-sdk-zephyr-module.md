---
title: Edge Impulse SDK Zephyr Module
summary: A portable C++ library for digital signal processing and machine learning
  inferencing integrated as a native Zephyr RTOS module. It enables the deployment
  of optimized ML models across hundreds of hardware targets using the West build
  system and custom extension commands for automated model management.
slug: edge-impulse-sdk-zephyr-module
codeUrl: https://github.com/edgeimpulse/edge-impulse-sdk-zephyr
siteUrl: https://www.edgeimpulse.com
version: v1.93.31
lastUpdated: '2026-07-24'
licenses:
- BSD-3-Clause-Clear
rtos: zephyr
libraries:
- tensorflow-micro
topics:
- edge-ai
- zephyr
isShow: false
createdAt: '2026-07-29T04:14:37+00:00'
updatedAt: '2026-07-29T04:14:37+00:00'
---

The integration of machine learning into embedded systems often requires navigating complex build environments and managing large sets of dependencies. The Edge Impulse SDK Zephyr module simplifies this process by bringing high-performance digital signal processing (DSP) and machine learning (ML) inferencing directly into the Zephyr RTOS ecosystem. By packaging the SDK as a native Zephyr module, developers can manage ML blocks and learning models with the same tools they use for their firmware, ensuring consistent builds across a wide variety of microcontrollers.

### Seamless Integration with West

One of the defining features of this repository is its deep integration with `west`, Zephyr's meta-tool. Rather than manually copying source files or headers into a project, developers can include the SDK by updating their `west.yml` manifest. This approach ensures that the SDK version remains synchronized with the specific model deployed from Edge Impulse Studio, reducing the risk of compilation errors due to API mismatches.

Beyond basic dependency management, the module introduces custom West extension commands that streamline the development workflow. The `west ei-build` command allows developers to trigger remote model compilation in the cloud, supporting various engines like standard TensorFlow Lite or the memory-optimized EON compiler. Once the model is ready, `west ei-deploy` automates the retrieval and extraction of the deployment artifacts into the local project structure. This automation removes the friction typically associated with updating models during the iterative phase of development.

### Optimized for Resource-Constrained Hardware

The SDK is designed to be highly portable and efficient. It provides the underlying C++ implementation for both processing blocks—handling tasks like spectral analysis or image preprocessing—and learning blocks for actual inference. To maximize performance on Arm-based hardware, the module supports hardware acceleration via CMSIS-NN and loop unrolling. These optimizations are crucial for achieving real-time performance in power-sensitive applications.

Memory management is another area where the module offers flexibility. Through the Zephyr Kconfig system, developers can choose how the SDK handles dynamic memory. It can be configured to use standard `malloc/free` or the Zephyr-native `k_malloc/k_free` functions, allowing the SDK to play nicely with the system's overall heap management strategy.

### Building and Deploying Models

Deploying an inference engine involves more than just adding a library; it requires a structured project layout. The repository includes standalone inferencing examples that demonstrate how to set up a Zephyr application to process raw features. These examples show how to include the model as a sub-module and configure the necessary C++ standards (C++11 or higher) required by the SDK.

Because Zephyr supports over 850 hardware targets, this module acts as a bridge that makes advanced ML capabilities accessible to a vast array of boards, from Nordic Semiconductor's nRF series to various STM32 and NXP platforms. Whether the target is a simple vibration sensor or a complex audio processing node, the module provides a standardized interface for edge intelligence.
