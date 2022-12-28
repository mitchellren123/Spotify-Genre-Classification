# Spotify - Genre Classification Analysis

### Overview

My project submission seeks to classify Spotify songs into genres using song features sourced from Spotify's API. In order to successfully do so I will build and iterate on Decision Tree Classifiers and Random Forest Classifiers.

### Business And Data Understanding

My stakeholder for this project is Spotify - an experiential music and audio content streaming service. The dataset I will be using for this analysis contains song data sourced directly from Spotify's API. It contains a mix of both categorical and numerical features. My goal is to build models that Spotify can use to categorize new songs into genres to then provide song recommendations to users building genre-based playlists.

### Modeling Approach

I started my data exploration by looking at all of the dataset's variables. I decided to drop a few features that I felt would not be helpful to the analysis (Album_cover_link for example). A majority of the dataset's features are numerical, however I decided to treat a few of them as categorical given their lack of scale and order (time_signature for example). 

I split the data into train and test sets and then performed the necessary transformations. I OneHotEncoded categorical variables, and used SMOTE to address class imbalance. For both of these transformations I fit only the training data so as to avoid data leakage. I then fit a baseline Decision Tree model and tested performance on both training and test data. In hopes of improving performance I investigated optimal hyper parameter values and used GridSearchCV to test a variety of combinations.

I then iterated to a Random Forest Classifier model. I followed the same steps that I did for the Decision Tree Classifier in terms of hyper parameter tuning and got model performance to improve slightly compared to the Decision tree.

Still not satisfied with the results, I thought about pivoting my approach. I had initially thought of this as a multi-class predictive problem. However, upon further consideration I realized that simplifying the problem into binary classification would still satisfy the business use case and at the same time almost certainly improve model performance. Therefore I created Random Forest Classifiers for each genre to make binary predictions. This approach improved predictive performance significantly.

### Modeling Results

* Baseline DTC: Train Accuracy = 0.90 | Test Accuracy = 0.42
* Tuned DTC: Train Accuracy = 0.58 | Test Accuracy = 0.49
* Baseline RFC: Train Accuracy = 0.91 | Test Accuracy = 0.57   
* Tuned RFC: Train Accuracy = 0.74 | Test Accuracy = 0.59

* Tuned EDM vs. Not EDM RFC: Train Accuracy = 97% | Test Accuracy = 93%
* Tuned Pop vs. Not Pop RFC: Train Accuracy = 93% | Test Accuracy = 82%
* Tuned Latin vs. Not Latin RFC: Train Accuracy = 94% | Test Accuracy = 86%
* Tuned HipHop vs. Not HipHop RFC: Train Accuracy = 93% | Test Accuracy = 85%
* Tuned Rap vs. Not Rap RFC: Train Accuracy = 93% | Test Accuracy = 83%
* Tuned R&B vs. Not R&B RFC: Train Accuracy = 96% | Test Accuracy = 89%
* Tuned Rock vs. Not Rock RFC: Train Accuracy = 97% | Test Accuracy = 91%

Although Accuracy scores improved significantly, these results are a bit misleading given the high class imbalance in test datasets. Taking a closer look at Precision, Recall, and F-1 scores gives us a clearer picture of model performance:

* EDM: (True) Test Precision = 81% | (True) Test Recall = 77% | (True) Test F-1 = 79%
* Pop: (True) Test Precision = 45% | (True) Test Recall = 47% | (True) Test F-1 = 46%
* Latin: (True) Test Precision = 53% | (True) Test Recall = 63% | (True) Test F-1 = 58%
* HipHop: (True) Test Precision = 41% | (True) Test Recall = 58% | (True) Test F-1 = 48%
* Rap: (True) Test Precision = 40% | (True) Test Recall = 61% | (True) Test F-1 = 49%
* R&B: (True) Test Precision = 48% | (True) Test Recall = 26% | (True) Test F-1 = 33%
* Rock: (True) Test Precision = 73% | (True) Test Recall = 75% | (True) Test F-1 = 74%

For each genre, the False cases heavily outweighed the True cases, and this had a siginficant impact on test set model performance. Despite very high accuracy scores, the models did not do a good job predicting the True cases comparitively speaking.

### Conclusion

The top-performing models were for EDM vs. Not EDM, Rock vs. Not Rock, and Latin vs. Not Latin. These results may suggest that those 3 genres are more distinct from the others - and Pop, R&B, HipHop, and Rap may share more similarities.

For the purposes of suggesting songs for genre-based radio or playlists, model performance for Rock and EDM suggest an adequate ability to classify between songs within those genres and songs outside of those genres. Test F-1 scores of around 75% show a good balance between Recall and Precision, combined with 90%+ Accuracy scores - even on heavily class-imbalanced test datasets. Model performance for all other genres would need to be improved. In order to do so, I would suggest analyzing a much larger dataset with additional, distinguishing features included such as record label, album, artist, producer, etc. Another interesting next step would be to analyze the overlap in genres - in other words take a look at songs that were classified into multiple genres using these separate models.

## Repository Structure
```
├── README.md                           <- The top-level README for reviewers of this project
├── Spotify_Genre_Analysis.ipynb        <- Narrative documentation of analysis in Jupyter notebook
├── Presentation.pdf                    <- PDF version of project presentation
├── spotify_genre_final.xlsx            <- King County Housing dataset
```
