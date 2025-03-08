README

# Recommender System for Leroy Merlin Products Using Machine Learning

## Overview
This project aims to enhance the online shopping experience at Leroy Merlin by developing a content-based recommender system. Given a product reference, the system returns 5 similar products based on their various attributes. The approach leverages machine learning, specifically a k-Nearest Neighbors (KNN) model with cosine similarity, to compare products in a unified feature space.

## Project Description
- **Purpose:**  
  Improve product discovery by suggesting similar items, thereby enhancing the overall user experience.
  
- **Objective:**  
  Build a system that, for any given product reference, returns five similar products based on content and category.

- **Approach:**  
  The project involves rigorous data preprocessing, feature engineering, and the application of a KNN model. A simple web interface built with Flask allows users to input a product reference and receive recommendations.

## Dataset
- **Source:**  
  The dataset contains over 300,000 product entries from Leroy Merlin.
  
- **Key Attributes:**  
  - **LM Internal Reference:** Unique product identifier  
  - **Section & Type:** Product categories  
  - **Dimensions & Weight:** Physical characteristics  
  - **Designación Administrativa:** Detailed product description  
  - **Letra de Gama:** Sales probability ranking

- **Data Filtering:**  
  - Exclude products with references starting with "48" or "49".
  - Remove entries with missing or undesired 'Letra de Gama' values (empty or values such as "E", "L", "S").

## Data Preprocessing & Feature Engineering
- **Missing Value Imputation:**  
  - Categorical data (e.g., 'Section' and 'Type') are filled with a placeholder (e.g., "Unknown").  
  - Numerical data (e.g., dimensions and weight) are filled using the column mean.

- **Feature Transformation:**  
  - **Categorical Data:** One-Hot Encoding is applied to 'Section' and 'Type'.  
  - **Numerical Data:** Standard Scaling is used for dimensions and weight.  
  - **Text Data:** The 'Designación Administrativa' field is converted to embeddings using SentenceTransformer, capturing semantic information.  
  - **Ranking Data:** 'Letra de Gama' is encoded with One-Hot Encoding.

- **Feature Combination:**  
  All transformed features are concatenated into a single vector per product.

## Machine Learning Model
- **Algorithm:**  
  We use the k-Nearest Neighbors (KNN) algorithm to find the most similar products.
  
- **Distance Metric:**  
  Cosine similarity is used to measure the angle between product vectors, ensuring that products with similar feature patterns are identified regardless of scale.

- **Sectorization:**  
  Through the encoding of categorical features (Section and Type), products are effectively grouped into sectors. This ensures that similar products—within the same or related categories—are more likely to be recommended.

## Web Application
- **Framework:**  
  A simple web interface is built using Flask.
  
- **Functionality:**  
  Users can enter a product reference into a form. The backend uses the KNN model to retrieve 5 similar products, which are then displayed with their "LM Internal Reference", "Section", and "Designación Administrativa".

## Installation & Usage

### Prerequisites
- Python 3.7 or above
- Required libraries:
  - pandas
  - numpy
  - scikit-learn
  - sentence-transformers
  - flask

### Installation
1. Clone the repository or download the project files.
2. Install the required libraries using pip:

   ```bash
   pip install pandas numpy scikit-learn sentence-transformers flask
