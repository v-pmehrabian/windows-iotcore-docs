---
title: Computer Vision
ms.date: 08/28/2017
ms.topic: article
ms.prod: windows-iot
ms.technology: iot
description: Learn how to use Microosft Cognitive Services and OpenCV for your IoT device.
keywords: windows iot, computer vision, Cognitive Services, OpenCV
---

# Computer Vision

Humans perceive our three-dimensional world with relative ease. Starting from an early age, our brains can gather valuable insights including feature identification, obstacle avoidance, coordination, depth perception, and many others from visual stimuli. Computer vision is an attempt to use processors and cameras to do the same thing. It has countless applications for today's devices. A drone can use it to rapidly detect and avoid obstacles during flight; a factory can use it to detect cosmetic defects in the smallest components on the assembly line; and a person can use it to detect his or her heart rate without use of a monitor or doctor's equipment. Our data-focused world has made computer vision an incredibly active research area. Companies are utilizing it in ways considered improbable even ten years ago. As computers, cameras, and data becomes more ingrained in our society, tools to leverage computer vision's most exciting capabilites should be made as easy to access and use as possible. Windows 10 IoT Core attempts to satisfy this need through compatability with two offerings: Microsoft Cognitive Services and OpenCV.

## Services
___

### Cognitive Services

#### Overview
Cognitive Services, originally a Microsoft Research project called Project Oxford, is a collection of APIs which perform high-level "cognitive tasks". These APIs pull insights from your data based on highly-trained machine learning models from years of exploration and development at Microsoft Research.

Cognitive Services is comprised of 5 categories: Vision, Speech, Languages, Knowledge, and Search.

You can find more information about Cognitive Services on the Cognitive Services [website](https://www.microsoft.com/cognitive-services).

The Vision category, the most valuable category for computer vision applications, contains four APIs: Computer Vision, Emotion, Face, and Video. These APIs provide the following functionality:
- Facial recognition
- Motion detection
- Emotion recognition
- Video stabilization
- Image content analysis

Cognitive Services is great for working with large amount of data, accessing Microsoft Azure, and greatly reducing you application's time-to-market, as the Vision APIs often prove to be time-consuming to develop independently. The model used for these APIs is well-trained and extensive thanks to the efforts of Microsoft Research. On the other hand, its cloud connectivity requirement reduces system performance and creates the requirement for an internet connection.

#### Pricing
Each API subscription comes with a set of free transactions every month (300 to 30,000, depending on the API). After exceeding this initial amount, the services come with a reasonable price. For example, the Emotion API provides the first 30,000 transactions for free and requires $0.10 or $0.25 every 1000 transaction after that depending on the subscription type.

More details about Cognitive Services pricing is found on their [website](https://www.microsoft.com/cognitive-services/en-us/pricing).

#### Get Started
To employ Cognitive Services, users must sign up at the Congitive Services website to receive API keys. After providing an API key to Cognitive Services, users can call the APIs within the limitations mentioned in the "Pricing" section.

Documentation for each API can be found on the Cognitive Services [website](https://www.microsoft.com/cognitive-services/en-us/documentation).

All Cognitive Services APIs can be implemented on any hardware platform using C#.

Want to run Cognitive Services on your IoT Device? Visit our [tutorial](/samples/microsoft/windows-iotcore-samples/congitive-services) to get started.

### OpenCV

OpenCV is an open source computer vision and machine learning software library designed for computational efficiency and real-time applications. It is widely popular among developers and in industry due to its unprecedented efficiency, versatile tools, support for a wide range of platforms, and vibrant online community of developers. It is by far the most popular open source computer vision tool. OpenCV libraries are available for C/C++, Java, and C#.

The OpenCV [website](http://opencv.org/) provides additional details.

OpenCV features:
- Local image and video processing and analysis
- Real time object identification, matching, and tracking
- Real time facial recognition
- Distance determination from image and real-time
- 3D mapping/modeling/reconstruction
- Image editing (such as composition and color change)

OpenCV provides a number of advantages. It is very efficient for local data processing because of the optimized C/C++ internals and its access to the GPU using OpenCL (if enabled). It contains most, if not all, computer vision functionality currently available. Its longevity and utility has formed an extensive and experienced online community which can help new users with application or library issues. On the other hand, there is a steep learning curve due to the complex code and library setup as well as inconsistencies in tutorials and sample code.

Currently, OpenCV with IoT Core only works if users build the library from source, which can be time-consuming. Because of this, we are actively working to make OpenCV easier to set up on IoT Core by creating a collection of NuGet packages for it. A NuGet package, which Cognitive Services uses, allows developers to import a prebuilt library into their application, providing full functionality with a few clicks. The application using the NuGet package will continue to receive library updates from a dedicated server; the user does not need to rebuild new source code when there are public changes to the open source software. The package also relieves storage space on devices only using parts of the library.

This is currently a work in progress, so keep checking WindowsOnDevices.com for updates!

In the meantime, to build the library from source for ARM, visit the [GitHub repository](https://github.com/Microsoft/opencv/tree/vs2015-samples-ARM).

Want to run OpenCV on your IoT Core device? Visit our [tutorial](/samples/microsoft/windows-iotcore-samples/opencv) to get started.

## Comparing OpenCV and Cognitive Services

> |Features|Microsoft Cognitive Services|OpenCV|
> |---------------------|--------|------|
> |Easy to use on Windows|Yes|No |
> |Architecture support|ARM, x86, x64 | ARM, x86, x64|
> |Facial recognition and tracking| Yes | Yes|
> |Emotion recognition| Yes | Yes|
> |3D reconstruction and mapping| No | Yes|
> |Content detection| Detects general features rather than specific objects | Yes|
> |Video stabilization| Yes | Yes|
> |Motion detection| Yes | Yes|
> |Community| Cognitive Services has many active users across multiple industries and a few popular websites, including how-old.net and celebslike.me | OpenCV is a very popular Open Source project; thousands of people have contributed to it and maintained it|
> |Documentation| Cognitive Services has overall clear and extensive documentation | There are many samples available online, but each sample is written by a different person and as a result can be inconsistent at times|
> |Free| Yes, to an extent (more details [here](https://azure.microsoft.com/pricing/details/cognitive-services/)) | Yes|
> |Performance| All operations and API calls require accessing data in the cloud | All algorithms are optimized and local, and using C++ rather than Python increases speeds even further|
> |Supported cameras/hardware| Any USB or embedded camera | Any USB or embedded camera|
> |Supported languages/frameworks| C#, UWP | C/C++, Python, Java, C#, UWP|
> |Startup time| Users can use code samples along with intuitive APIs directly from the documentation | OpenCV's power and flexibility means it also requires plenty of configuration and code to perform complex operations|
> |Links| [Sample program](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/CognitiveServicesExample) | [Sample program](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/OpenCVExample) |
> |    |   [Cognitive Services Website](https://azure.microsoft.com/services/cognitive-services/) |  [OpenCV Website](http://opencv.org/)
