
# 📱 Android-Based Teledermatology App for Skin Lesion Classification

This project is a **deep learning-powered Android application** for classifying **dermoscopic skin lesion images**, focused on assisting early detection of skin cancer. The application leverages the power of **Convolutional Neural Networks (CNN)** and is built upon the **Xception** architecture, achieving a peak accuracy of **92.95%** on the HAM10000 dataset.

> ✅ Designed for remote teledermatology  
> ✅ Powered by TensorFlow & Keras  
> ✅ Implements Transfer Learning with fine-tuning  
> ✅ Deployed as a lightweight `.tflite` model in Android  

---

## 🔬 Motivation

Skin cancer ranks as the third most diagnosed cancer in Indonesia. However, limited access to dermatologists—especially in rural areas—makes **early detection** difficult. This project aims to:
- Bring **automated classification** of skin lesions to mobile devices
- Bridge the urban–rural healthcare gap via **teledermatology**
- Experiment and evaluate **CNN pre-trained models** for medical image classification

---

## 📊 Dataset

**HAM10000** – a public dataset containing **10,015 dermoscopic images** spanning **7 classes of skin lesions**:
- Melanocytic nevi (nv)
- Melanoma (mel)
- Benign keratosis (bkl)
- Basal cell carcinoma (bcc)
- Actinic keratoses (akiec)
- Vascular lesions (vasc)
- Dermatofibroma (df)

**Preprocessing & Augmentation**:
- Image size standardized to **224x224**
- Duplicate images removed (resulting in 5,514 clean samples)
- Dataset split: **80/10/10** for train/validation/test
- Augmentation used to handle class imbalance: rotation, scaling, flipping, shifting

---

## 🧠 Models Compared

| Model         | Peak Accuracy | F1 Score |
|---------------|---------------|----------|
| MobileNetV2   | 90.10%        | 0.703    |
| ResNet50V2    | 90.04%        | 0.737    |
| DenseNet121   | 92.33%        | 0.793    |
| InceptionV3   | 91.08%        | 0.757    |
| **Xception**  | **92.95%**    | **0.803**|

Hyperparameters tuned:
- **Learning Rate:** 0.001 vs 0.0001
- **Optimizers:** Adam, RMSprop, Nadam, SGD
- **Batch Sizes:** 16, 32, 64, 128
- **Dropout Rates:** 0.3 to 0.6  
- **Training Types:** Single-phase vs Two-phase (transfer learning + fine-tuning)

---

## 📱 Android Integration

The best-performing model (**Xception**) was converted into a `.tflite` format and deployed into an Android app via **Android Studio**.

App Features:
- Real-time lesion prediction via camera or gallery
- Clean UI with class-wise prediction output
- Lightweight and optimized for mobile usage

> ⚠️ Notable finding: The app maintains high accuracy with gallery images but sees accuracy drops (up to 23%) with live camera captures due to noise, lighting, and resolution variances.

---

## 🏗️ Architecture Overview

1. **Data Cleaning & Augmentation**
2. **Model Selection & Training**
3. **Hyperparameter Tuning**
4. **Conversion to TensorFlow Lite**
5. **Android Application Development**

---

## 🚀 How to Run

1. Clone this repo
2. Use Google Colab or a local Jupyter Notebook to:
   - Load and preprocess the HAM10000 dataset
   - Train and evaluate models
   - Export `.tflite` using `tf.lite.TFLiteConverter`
3. Open Android Studio
   - Import the `.tflite` model
   - Implement preprocessing in Java/Kotlin
   - Run on device/emulator

---

## 📈 Future Work

- Improve performance on real-time camera input via image enhancement
- Add lesion boundary segmentation before classification
- Incorporate newer models like EfficientNetV2 or lightweight MobileNetV3
- Build a REST API version for hospitals or clinics

---

## 📜 License

This project is open-sourced under the [MIT License](LICENSE).

