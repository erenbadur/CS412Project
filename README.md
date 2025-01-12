# CS412Project

Dataset Overview

This project utilized two primary datasets to support the classification and regression tasks. The first dataset, “Training Dataset (training-dataset.jsonl.gz),” contained comprehensive profile information of Instagram accounts, such as username, biography, category name, follower counts, and engagement metrics. A sample entry from this dataset highlights the detailed structure:
{
  "profile": {
    "username": "deparmedya",
    "id": "3170700063",
    "full_name": "Depar Medya",
    "biography": "#mediaplanning #mediabuying #sosyalmedya",
    "category_name": "Local business",
    ...
  },
  ...
}

The second dataset consisted of annotated labels provided in files such as “annotated_users_CS412-2fa73b22df12.csv” and “train-classification.csv.” These files mapped Instagram account URLs and usernames to their respective influencer categories, influencer mentions, and account types. For instance:
url,influencerCategory,influencerMention,accountType
enveraputkan,"https://instagram.com/enveraputkan",Health and Lifestyle,No,Influencer
kurulusdizisi,"https://instagram.com/kurulusdizisi",Entertainment,No,Company
...

,label
taskirancemal,Mom and Children
tam_kararinda,Food
...

The accounts were categorized into various influencer types such as “Food,” “Fashion,” “Health and Lifestyle,” “Entertainment,” “Mom and Children,” “Gaming,” “Tech,” and “Travel.” The dataset exhibited an imbalance, with some categories, like “Food” and “Health and Lifestyle,” having a significantly larger number of samples compared to less frequent categories such as “Gaming” or “Art.” The textual data provided by user biographies and post captions offered rich context for classification but also posed challenges due to its language, predominantly Turkish, which necessitated the use of language-specific models such as “dbmdz/bert-base-turkish-uncased.”

Methodology
This project involved two distinct tasks: multi-class classification of influencer categories and regression for content popularity prediction. The classification task aimed to predict one of ten (later nine) categories, using accuracy as the evaluation metric. The regression task focused on predicting the log10-transformed “like_count” variable, with mean squared error (MSE) serving as the evaluation metric.

In Round 1, TF-IDF was used for feature extraction in both tasks. Several machine learning models, including Naïve Bayes, Logistic Regression, XGBoost, and LightGBM, were tested, with hyperparameter tuning performed using Optuna. LightGBM emerged as the best-performing algorithm for its robustness with structured data and strong predictive capabilities. However, dataset imbalance posed challenges. Early attempts to address this issue, such as employing SMOTE, yielded unsatisfactory results. For regression, LightGBM demonstrated reliable performance with TF-IDF features, and the log10 transformation of the “like_count” variable improved prediction consistency.

Round 2 introduced refinements to the classification task, including the consolidation of “Gaming” and “Tech” categories to reduce the total from ten to nine. Class weights were incorporated into the LightGBM model to handle imbalances more effectively, and early stopping was applied to enhance model efficiency and generalization. For regression, the focus remained on optimizing LightGBM through enhanced hyperparameter tuning and improving input feature quality.

In Round 3, a pre-trained BERT model was fine-tuned to generate contextual embeddings, significantly enhancing the classification task’s feature quality. PCA was used for dimensionality reduction before feeding data into LightGBM, resulting in improved computational efficiency without compromising performance. Class weights were retained to address imbalance, but time constraints limited the implementation of additional improvements, such as early stopping and feature importance analysis. For the regression task, additional feature engineering was undertaken, while LightGBM continued to be used for its consistency.

Results and Findings

The classification task showed clear progression across the rounds. In Round 1, LightGBM outperformed other models but faced challenges with imbalanced data. Round 2’s use of class weights and category consolidation led to improved accuracy and reduced training time. Round 3’s adoption of BERT fine-tuning significantly enhanced feature representation, capturing the contextual nuances of Instagram posts more effectively. PCA further optimized computational efficiency, although minor overfitting issues persisted.
For the regression task, LightGBM consistently delivered reliable results. The introduction of log10 transformation for the “like_count” variable improved prediction stability, while iterative refinements in feature engineering and hyperparameter tuning contributed to better model performance. Despite the effectiveness of TF-IDF, embedding-based approaches like BERT were identified as potential avenues for future improvement.

Limitations and Future Improvements

Despite the advancements achieved, several limitations were noted. For the classification task, challenges related to dataset imbalance persisted. Although merging categories and applying class weights provided partial solutions, a more comprehensive strategy, such as advanced resampling techniques or cost-sensitive learning, remains an area for exploration. Time constraints also prevented the integration of early stopping and feature importance methods into the BERT framework.

For the regression task, while LightGBM consistently performed well, the reliance on TF-IDF for feature extraction limited the model’s ability to fully keep the contextual richness of the textual data. Incorporating embedding-based approaches like BERT or exploring other deep learning models could further enhance predictive accuracy. Additionally, expanding feature engineering efforts to include temporal patterns and engagement dynamics may provide deeper insights.

In conclusion, this project demonstrated significant progress in methodology and outcomes across three rounds. The classification task benefited from the transition to BERT fine-tuning and the application of PCA, while the regression task achieved steady improvements through iterative refinements. Future work should focus on addressing the noted limitations and exploring advanced techniques to further enhance both tasks.

