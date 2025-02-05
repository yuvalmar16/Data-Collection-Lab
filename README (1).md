# Data Collection Lab Project: LinkedIn Profile Picture Evaluator

<h1 align='center'>LinkedIn Profile Picture Evaluator</h1>

<p align='center'>
    <a href="https://github.com/yuvalmar16">Yuval Margolin</a> | 
    <a href="#">Ravid Gersh</a> | 
    <a href="https://github.com/danielmaor0808">Daniel Maor</a>
    <br/> 
    Technion - Israel Institute of Technology
    <br/> Data and Decision Science Faculty 
</p>

<p align='center'>
    <a href="https://youtu.be/Wn_zD-uUX1E">User Journey Video</a> |
    <a href="https://www.youtube.com/watch?v=Trc2p41LRhM">Technical Overview Video</a>
</p>

<p align='center'>
  <img src="https://finlink.co.uk/wp-content/uploads/2023/11/LinkedIn-page.jpg" alt="Logo" width="300" height="200">
</p>

---

## Contents
- [Overview](#overview)
- [Scraping Pictures](#scraping-pictures)
- [Preprocessing Images](#preprocessing-images)
- [Running the Train and Test Code](#running-the-train-and-test-code)
- [Download Model Weights](#download-linkedin-score-predictor-weights)
- [Running The App](#running-the-app)

---

## Overview

In today's professional world, first impressions matter—and a LinkedIn profile picture plays a key role! As part of the **Data Collection Lab** at the Technion, we built a **LinkedIn Profile Image Evaluator** 🏆

### 🔹 What does it do?

Our app analyzes a profile image and provides:

✅ A rating (1-100) based on key visual and professional factors  
✅ Three personalized suggestions to enhance the picture  

The goal? Helping users make **data-driven choices** about their professional presence on LinkedIn!

### 🔍 Technologies Used:

🖥️ **MediaPipe & dlib** – Face detection & analysis  
🤖 **OpenAI CLIP** – AI-powered image understanding  
🔥 **PyTorch TabNet** – Machine learning model training  
⚡ **PySpark** – Efficient large-scale data processing  
📷 **OpenCV** – Image preprocessing  

---

## Scraping Pictures

The **scraping notebook** uses the **Google Search API (SerpAPI)** to extract profile images from corporate websites. It automates retrieving image URLs by searching for professional profile pictures from company "Our Team" pages.

---

## Preprocessing Images

The image analysis pipeline was executed on **Azure Databricks**, using a notebook named **"PreProcess images and features"**, with data stored in `dbfs/FileStore`. 

### **Preprocessing Steps:**
- Unzipped multiple image archives and merged them into a single directory (`/dbfs/FileStore/all_images_combined`).
- Ensured no duplicates by renaming files with identical names.
- Labeled images with a **score (1-100)** and extracted **29 features** using CLIP.
- Saved the extracted features into a CSV file (`Profile_Pictures_extracted.csv`).

### **Feature Extraction Techniques:**
- **CLIP**: Analyzed images for professional attributes like smile, attire, background clarity, and trustworthiness.
- **MediaPipe**: Detected facial landmarks and body proportions, ensuring proper face positioning.
- **Dlib**: Analyzed nose and eye alignment for direct eye contact assessment.
- **OpenCV**: Evaluated **image resolution, lighting quality, and clarity**.

---

## Running the Train and Test Code

The **[Train and Test Notebook](https://github.com/yuvalmar16/Data-Collection-Lab/blob/main/Train%20and%20test%20(3).ipynb)** loads the extracted dataset (`Profile_pictures_extracted.csv`) and performs:

- **Exploratory Data Analysis (EDA)**: Correlation matrix to identify key feature relationships.
- **Model Training**: A machine learning model predicts LinkedIn scores from extracted image attributes.
- **Model Evaluation**: Performance assessed using **MSE, R², and feature importance analysis**.

This transforms raw image data into actionable insights and predictive analytics for profile evaluation.

---

## Download LinkedIn Score Predictor Weights

You can download the **pre-trained model weights** from:

📥 [linkedin_score_predictor.pth](https://github.com/yuvalmar16/Data-Collection-Lab/blob/main/linkedin_score_predictor.pth)

To use it in your notebook, save it in the **models** folder in `dbfs`, ensuring:
```python
input_dim = 28
```
✅ Model loading is already included in the **train & test** notebook and the **app notebook**.

---

## Running The App

The **[LinkedIn Image Evaluator App](https://github.com/yuvalmar16/Data-Collection-Lab/blob/main/Linkedin_image_evaluator_App.ipynb)** allows real-time evaluation of LinkedIn profile pictures. You can run the evaluation using urls as input, or Alternatively add your own ngrok Authentication in the marked place to run the site.

### **App Features:**
- Users can **input image URLs** or **upload images** for scoring.
- The trained model **assesses key professional attributes** like expression, attire, background, and overall appeal.
- Offers a **web-based interactive experience** for improving profile images.

🚀 Run the app and optimize your LinkedIn presence today! 🔥
