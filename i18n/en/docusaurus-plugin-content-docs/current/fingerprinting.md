---
title: Fingerprinting
sidebar_position: 3
---

# Fingerprinting Technology

DigiCAP's Fingerprinting technology uses a CNN (Convolutional Neural Network)-based deep learning algorithm to extract unique features from images and videos, thereby verifying the content's authenticity.
:::info Core Technology
The core of fingerprinting technology lies in its **robustness**, which allows it to track the original content without losing its uniqueness, even if the content is partially edited (e.g., cropped, resized, color-corrected) or reprocessed into another form.
:::

## Technology Overview

### Key Technologies

Instead of relying on a single technology, this system adopts a **Hybrid Model** that combines two powerful approaches to maximize accuracy and efficiency.

**CNN (Convolutional Neural Network) Feature Extraction**

- Quantifies the unique visual characteristics of images/videos.
- Extracts robust feature points that are resistant to compression, resizing, and format changes.
- Enables real-time similarity matching and tampering detection.
- Utilizes Deep Learning-based feature extraction.

**Perceptual Hash (PHash) Generation**

- Generates a unique hash value based on the overall structure and shape of image frames.
- Effectively finds similar candidates in large-scale databases.
- Reduces the load of CNN analysis.

### Fingerprint Extraction Pipeline

Video fingerprints are generated through the following systematic steps.

**Frame-level Feature Extraction (extract frame feature)**

- First, the video is separated into individual image frames.
- Each frame is fed into a Deep Learning-based MultiTaskModel to be converted into a 1280-dimensional CNN feature vector (fingerprint).
- This vector compresses the core visual information of the corresponding frame.

**Segment-level Feature Aggregation (extract segment feature)**

- Since frame-level features can be unstable, they are grouped into 'segments' of a certain duration (e.g., 5 seconds) and averaged (Average Pooling).
- This creates a noise-resistant and stable representative fingerprint for the segment.

**Hybrid Fingerprint Generation and Storage**

- The hybrid fingerprint is completed by combining the segment's CNN fingerprint with a 144-bit Perceptual Hash value.
- This information is stored in a .pth file format and kept in a database.

### Excellent Robustness and Accuracy

Thanks to the abstract features learned by the AI, this system's fingerprints can accurately identify the original content despite various modifications such as:

- **Re-encoding and Compression**: Robust against quality degradation and compression that occurs when uploading to various platforms.
- **Resolution and Aspect Ratio Changes**: Detection is possible even if the video size is adjusted or parts of the screen are cropped.
- **Corrections and Filter Applications**: Maintains the uniqueness of the original even when visual effects like brightness, contrast, and color filters are added.

For technical inquiries, please contact [info.bornid@digicaps.com](mailto:info.bornid@digicaps.com).
