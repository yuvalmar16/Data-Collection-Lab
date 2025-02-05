
<h1 align='center' style="text-align:center; font-weight:bold; font-size:2.5em"> Data Collection Lab Project: LinkedIn  Profile Picture Evaluator
 </h1>

<p align='center' style="text-align:center;font-size:1em;">
    <a href="https://github.com/yuvalmar16">Yuval Margolin</a>&nbsp;,&nbsp;
    <a>Ravid Gersh</a>&nbsp;,&nbsp;
    <a href="https://github.com/danielmaor0808">Daniel Maor</a>&nbsp;&nbsp;
    <br/> 
    Technion - Israel Institute of Technology
<br/> 
<br>
    <a href="https://youtu.be/Wn_zD-uUX1E">Users journey Video</a> |<a href="https://www.youtube.com/watch?v=Trc2p41LRhM">Technical Overview Video</a>
    

</p>


<br>
<br>

<p align="center">
  <img src="https://finlink.co.uk/wp-content/uploads/2023/11/LinkedIn-page.jpg" alt="Logo" width="300" height="200">



# Contents
- [Overview](#Overview)
- [Scraping pictures](#Scraping-pictures)
- [PreProccess images](#PreProccess-images)

- [Running the code]
        - [Running the Train and Test code](#Running-the-Train-and-Test-code)
        - [Download linkedin_score_predictor weights](#Download-linkedin_score_predictor-weights)
        - [Running The App](#Runing-the-Image-evaluator-App)

  
# Overview

In today's professional world, first impressions matter—and a LinkedIn profile picture plays a key role! That’s why as part of Data Collection Lab at the Technion We built a LinkedIn Profile Image Evaluator 🏆

🔹 What does it do?

Our app analyzes a profile image and provides:

✅ A rating (1-100) based on key visual and professional factors

✅ Three personalized suggestions to enhance the picture

The goal? Helping users make data-driven choices about their professional presence on LinkedIn!


🔍 Technologies we used:

🖥️ MediaPipe & dlib – Face detection & analysis

🤖 OpenAI CLIP – AI-powered image understanding

🔥 PyTorch TabNet – Machine learning model training

⚡ PySpark – Efficient large-scale data processing

📷 OpenCV – Image preprocessing




# PreProccess images
The image analysis pipeline was executed on Azure Databricks Notebook Which is named "PreProcess images and features", with data stored in dbfs/FileStore. The process began with unzipping multiple image archives and consolidating all images into a single directory (/dbfs/FileStore/all_images_combined). To ensure no duplicates, a renaming strategy was implemented for files with identical names.The name of the csv in the notebook which was saved in the dbfs is Data_NotNorm__1_.
In this folder, the images we collected were labeled with a score ranging from 1 to 100, and approximately 30 features were extracted using CLIP.The csv in this github folder is named Profile_Pictures_extracted.csv
 The feature extraction process involved multiple techniques to assess different aspects of the images. CLIP was used to analyze the similarity between images and predefined textual descriptions, evaluating attributes such as smile, professional attire, clean background, serious expression, confidence, and trustworthiness. Additionally, MediaPipe was utilized to detect facial landmarks and body proportions, determining the percentage of the image occupied by the face and upper body, as well as assessing horizontal and vertical face centering. Nose and eye alignment were analyzed using Dlib and MediaPipe to ensure proper positioning and direct eye contact with the camera. Head tilt was calculated based on the angle between the eyes, while the looking direction score measured the alignment of the nose tip with the eye center to estimate whether the subject was looking straight at the camera. Image quality metrics, including resolution (DPI score) and lighting quality, were also assessed to ensure clarity and brightness. The extracted features were then compiled into a final scoring system, combining CLIP-based similarity scores with numerical attributes, providing a comprehensive evaluation of each image.





# Running the Train and Test code

The [Train and test (1).ipynb](https://github.com/yuvalmar16/Data-Collection-Lab/blob/main/Train%20and%20test%20(1).ipynb) loads the CSV dataset generated from the image analysis pipeline( in this dir named "Profile_pictures_extracted.csv) and performs data analysis, model training, and evaluation. It begins by loading the extracted features and LinkedIn scores into a Pandas DataFrame, followed by exploratory data analysis, including a correlation matrix to identify key feature relationships. The dataset is then split into training and testing sets, and a machine learning model is trained to predict LinkedIn scores based on image attributes. The model's performance is assessed using metrics such as Mean Squared Error (MSE) and R², while feature importance analysis reveals the most influential factors. This notebook serves as the final step in the pipeline, transforming raw image data into actionable insights and a predictive model for professional profile picture evaluation



# Download linkedin_score_predictor weights

You can download the model checkpoints from the [linkedin_score_predictor](https://github.com/yuvalmar16/Data-Collection-Lab/blob/main/linkedin_score_predictor.pth) and save them to the "models" folder in the dbfs and load it to your notebook, notice that you need to define the input_dim=28.(This code section which load the weights is already in the train and test notebook and also in the app notebook.


# Running The App

The [Linkedin_image_evaluator_App.ipynb](#https://github.com/yuvalmar16/Data-Collection-Lab/blob/main/Linkedin_image_evaluator_App.ipynb) notebook is designed to evaluate LinkedIn profile pictures in real-time. It allows users to input image URLs for automatic scoring using the trained model, assessing attributes such as facial expression, attire, background, and overall professionalism. Additionally, the notebook includes functionality to launch a web-based interface where users can upload images directly for evaluation. This provides an interactive way to test the model’s performance on new images, ensuring a seamless user experience for analyzing and improving professional profile pictures.




