# 📱 Android-Based Teledermatology App for Skin Lesion Classification

This project presents an **Android mobile application** for classifying **skin lesions** using **deep learning and dermoscopic images**. Built upon **pre-trained CNN models**, the app provides an accessible teledermatology solution, especially beneficial in areas with limited dermatological services. The core model achieves a top accuracy of **92.95%** using the **Xception** architecture.

---

## 🔍 Overview

Skin cancer remains one of the most prevalent types of cancer globally and ranks third in Indonesia after cervical and breast cancers. Despite its high curability at early stages, lack of dermatologists in rural areas causes delayed diagnosis. This project seeks to mitigate that gap by developing:

- A **CNN-based classification system** using dermoscopic imagery
- An **Android app** that enables real-time lesion classification using gallery or camera input
- A **training pipeline** for evaluating CNN architectures using transfer learning and hyperparameter optimization

---

## 📦 Dataset: HAM10000

The **HAM10000 ("Human Against Machine with 10000 training images")** dataset consists of 10,015 dermoscopic images across 7 skin lesion categories. It includes both benign and malignant lesion types:

| Class ID | Full Name                   | Description                           |
|----------|-----------------------------|---------------------------------------|
| nv       | Melanocytic nevi            | Common moles                          |
| mel      | Melanoma                    | Malignant tumor of melanocytes        |
| bkl      | Benign keratosis-like       | Includes seborrheic keratoses         |
| bcc      | Basal cell carcinoma        | Common, slow-growing skin cancer      |
| akiec    | Actinic keratoses           | Precancerous areas                    |
| vasc     | Vascular lesions            | Includes angiomas                     |
| df       | Dermatofibroma              | Benign skin growth                    |

---

## 🧹 Data Preprocessing Steps

1. **Cleaning**: Removed 4,501 duplicated images to ensure clean dataset of 5,514 samples.
2. **Splitting**: Used an 80:10:10 split (train:val:test) with care to avoid duplicates in val/test.
3. **Augmentation**: Balanced the dataset via:
   - Rotation (±180°)
   - Shifting (±10%)
   - Flipping (H/V)
   - Zooming (±10%)
   - Nearest fill method
4. **Resizing**: All images resized to **224x224** and normalized according to each model’s input requirements.

---

## 🧠 Deep Learning Models

We evaluated 5 popular CNN architectures, all sourced from Keras Applications:

- `MobileNetV2`
- `ResNet50V2`
- `DenseNet121`
- `InceptionV3`
- `Xception`

Each model underwent:
- Base layer freezing (transfer learning)
- Fine-tuning with additional layers: GlobalAveragePooling2D, BatchNormalization, Dropout, Dense (Softmax)
- Conversion to `.tflite` format for Android compatibility

---

## ⚙️ Hyperparameter Tuning

We tested each model with combinations of:

| Hyperparameter | Tested Values                           |
|----------------|------------------------------------------|
| Learning Rate  | 0.001, 0.0001                            |
| Optimizers     | Adam, RMSprop, Nadam, SGD                |
| Batch Size     | 16, 32, 64, 128                          |
| Dropout Rate   | 0.3, 0.4, 0.5, 0.6                       |
| Training Type  | Single-step (unfreeze all), Two-step     |

Best performance came from:

- **Xception**
- Learning Rate = 0.001 / 0.0001 (two-phase)
- Optimizer = Adam
- Batch Size = 64
- Dropout = 0.5

---

## 📈 Results Summary

| Model         | Accuracy | F1 Score |
|---------------|----------|----------|
| MobileNetV2   | 90.10%   | 0.703    |
| ResNet50V2    | 90.04%   | 0.737    |
| DenseNet121   | 92.33%   | 0.793    |
| InceptionV3   | 91.08%   | 0.757    |
| **Xception**  | **92.95%** | **0.803**  |

Notably, performance on classes like 'mel' (melanoma) lagged due to complexity despite data size. 'df' and 'vasc' classes—though smaller—showed higher F1-scores thanks to simpler image structures.

---

## 📱 Android Integration

The best-performing model (**Xception**) was converted into a `.tflite` format and deployed into an Android app via **Android Studio**.

- Developed with **Android Studio**
- Imports `.tflite` model via **TensorFlow Lite**
- Supports:
  - Real-time camera predictions
  - Static image upload via gallery
- Implements same preprocessing pipeline as training
  
App Features:
- Real-time lesion prediction via camera or gallery
- Clean UI with class-wise prediction output
- Lightweight and optimized for mobile usage

Notable finding: The app maintains high accuracy with gallery images but sees accuracy drops (up to 23%) with live camera captures due to noise, lighting, and resolution variances.

---

## 🏗️ Architecture Overview

1. **Data Cleaning & Augmentation**
2. **Model Selection & Training**
3. **Hyperparameter Tuning**
4. **Conversion to TensorFlow Lite**
5. **Android Application Development**

---

## 🚀 How to Run

1. **Clone the repository**
2. **Train model in Colab**:
   - Preprocess data
   - Tune hyperparameters
   - Save `.tflite` model
3. **Open Android Studio**:
   - Load project under `android_app/`
   - Add `.tflite` to `assets/`
   - Implement preprocessing & inference logic
4. **Run on emulator or physical device**

---

## 🧩 Future Work

- Add **segmentation model** for lesion localization
- Improve **real-time camera robustness** (auto-enhance)
- Add **REST API** for remote diagnosis
- Extend model with **EfficientNetV2** or **ConvNeXt**

---

## 👥 Authors

- **Faris Gymnastiar** – Developer & Researcher  
- **Yoyok Prasetyo**, **Ahmad Yulianto** – Academic Supervisors  
Digital Telecommunication Network, Electronic Engineering Dept, Politeknik Negeri Malang, Indonesia

---

## 📄 License

This project is open-sourced under the [MIT License](https://github.com/fagym/MNIST_HAM1000_Skin_Lession_Classification/blob/main/LICENSE.md).

---

## 💬 Acknowledgments

Special thanks to:
- Keras & TensorFlow communities
- HAM10000 dataset creators
