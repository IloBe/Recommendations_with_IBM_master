[//]: # (Image References)

[image1]: ./images/IBM_Watson_articles_appPageFeb2020_small.png "IBM Watson Cloud Articles:"
[image2]: ./images/Title-User-InteractionDistribution.PNG "Interactions Distribution:"
[image3]: ./images/Accuracy-LatentFeatures_LearningCurve.PNG "Learning Curves:"

# Recommendations with IBM Watson

## Project Overview
Welcome to this Udacity Data Science project **Recommender Systems**: We analyse the interactions that users have with articles on the IBM Watson Studio platform, and make recommendation proposals to them about new articles they will like.

On [IBM Watson studio](https://www.ibm.com/cloud/watson-studio) an important component is the community of datasets, articles, notebooks and other assets for domains AI, data science and machine learning. Platform users interact with all this components. 

![IBM Watson Cloud Articles:][image1] 

This project deals with user article interactions and a more personalised recommendation system (RS) shall be implemented, not only getting the newest articles. Build are a number of different methods for making recommendations that can be used for different situations. The used datasets, stored in this repository data subdirectory, are delivered by Udacity. They include article identifier numbers, titles, textual document information and cryptic email strings. 

Note: Not having specific user information, it is unclear, if each email can be mapped to a different user and to exclude the use case that some emails are from the same user. As simplification, we assume that each different email string value is mapped to a different user. Additionally, as interaction with an article we count each email independent if it is from a different or the same user as before.

The project structure is:
1. Exploratory Data Analysis
2. Rank Based Recommendations
3. User-User Based Collaborative Filtering
4. Matrix Factorisation

The following statistical information is explored:
- The number of unique articles that have at least one interaction: 714
- The number of unique articles on the IBM platform: 1051
- The number of unique users: 5148
- The number of user-article interactions: 45993
- The maximum number of user-article interactions by any 1 user is: 364
- The median number of articles users interact with: 3

![Interactions Distribution:][image2]

**Cold-Start Problem**:<br>
This recommendation project implementation does not include ratings from users to the article items. By now, only user-article interaction information is given. So, no predicted rating can be used to recommend articles to a _new user_. Additionally, this new user does not have any own article interactions, therefore no user-user similarity recommendation from the platform is possible as well. This shortcoming of a new user is called cold-start problem. The other option for this issue would be a new article item.

Therefore, as recommendation proposal a new user can only get _best ranked article interactions_ from the whole dataset. This can be classified as a kind of collaborative filtering, because we work with the collaboration of users. If there are many users who interacted with an article then that item can be recommended to the new user who hasn’t seen that article yet. But we shall have in mind, that this is an implicit assumption that simplifies the situation very much.

This kind of interaction ranked recommendation for a new user includes the higher risk, that this recommendation may not fit to the new users interests or taste or article usage goals. We cannot be sure that the existing interaction ranking means that the articles are liked by the interacting users. The real popularity of an article is unclear. In other words, the delivered recommendation could be completely wrong regarding a new user.

**Matrix Factorisation:**<br>
In this project case, we are dealing with user-article interactions and its boolean result (0 = no interaction, 1 = interaction). In other words, our user-item matrix is not empty (no NaN values are available) and we can use a simple SVD approach (no FunkSVD necessary). This gradient descent concept approximates the interaction value cases, so, the system is able to approximate the non-interaction matrix cells as well. Afterwards, both cells are very close. With this optimisation process squared loss error values will be minimised. With the given datasets 'all data', 'training data' and 'testing data' the following learning curves depending on the number of latent features appeared:

![Learning Curves:][image3] 


## Project Instructions
The notebook file can run on a PC, regarding the computational time a specific cloud service is not necessary.

1. **On your local machine** create and activate a new environment. First, move to directory `path/to/RS-project`.
  - __Windows__
  ```
	conda create --name RS-IBM-project python=3.7
	activate RS-IBM-project
	pip install -r requirements/requirements.txt
  ```
  
2. Create an [IPython kernel](http://ipython.readthedocs.io/en/stable/install/kernel_install.html) for the `RS-IBM-project` environment. 
```
python -m ipykernel install --user --name RS-IBM-project --display-name "RS-IBM-project"
```

3. Open the notebook.
```
jupyter notebook Recommendations_with_IBM.ipynb
```

4. Before running code, change the kernel to match the RS-IBM-project environment by using the drop-down menu (**Kernel > Change kernel > RS-IBM-project**).


## License
This project coding is released under the [MIT](https://github.com/IloBe/Recommendations_with_IBM_master/blob/master/LICENSE) license.
