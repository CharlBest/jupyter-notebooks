
Link: https://notebooks.azure.com/CharlBest/libraries/learn/html/RecommendationSystems.ipynb


```python
!pip install lightfm
```

    Collecting lightfm
      Downloading lightfm-1.14.tar.gz (250kB)
    [K    100% |################################| 256kB 2.0MB/s ta 0:00:01
    [?25hRequirement already satisfied: numpy in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from lightfm)
    Requirement already satisfied: scipy>=0.17.0 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from lightfm)
    Requirement already satisfied: requests in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from lightfm)
    Requirement already satisfied: chardet<3.1.0,>=3.0.2 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from requests->lightfm)
    Requirement already satisfied: idna<2.7,>=2.5 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from requests->lightfm)
    Requirement already satisfied: urllib3<1.23,>=1.21.1 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from requests->lightfm)
    Requirement already satisfied: certifi>=2017.4.17 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from requests->lightfm)
    Building wheels for collected packages: lightfm
      Running setup.py bdist_wheel for lightfm ... [?25ldone
    [?25h  Stored in directory: /home/nbuser/.cache/pip/wheels/15/05/79/ef0517380683841ac13a08cbb8c90f052f954b91b486cc7e68
    Successfully built lightfm
    Installing collected packages: lightfm
    Successfully installed lightfm-1.14



```python
import numpy as np
from lightfm.datasets import fetch_movielens
from lightfm import LightFM

#fetch data and format it
data = fetch_movielens(min_rating=4.0)

#print training and testing data
#print(repr(data['train']))
#print(repr(data['test']))

#create model (Weighted Approximate-Rank Pairwise)
model = LightFM(loss='warp')
#train model
model.fit(data['train'], epochs=30, num_threads=2)

def sample_recommendation(model, data, user_ids):
    
    #number of users and movies in training data
    n_users, n_items = data['train'].shape
    
    #generate recommendations for each user we input
    for user_id in user_ids:
        
        #movies they already like
        known_positives = data['item_labels'][data['train'].tocsr()[user_id].indices]
        
        #movies our model predicts they will like
        scores = model.predict(user_id, np.arange(n_items))
        #rank them in order of most liked to least
        top_items = data['item_labels'][np.argsort(-scores)]
        
        #print our results
        print("User {}".format(user_id))
        print("   Known positives:")
        
        for x in known_positives[:3]:
            print("      {}".format(x))
            
        print("   Recommended:")
        
        for x in top_items[:3]:
            print("      {}".format(x))
            
sample_recommendation(model, data, [3, 25, 450])
```

    User 3
       Known positives:
          Seven (Se7en) (1995)
          Contact (1997)
          Starship Troopers (1997)
       Recommended:
          Scream (1996)
          L.A. Confidential (1997)
          Apt Pupil (1998)
    User 25
       Known positives:
          Dead Man Walking (1995)
          Star Wars (1977)
          Fargo (1996)
       Recommended:
          L.A. Confidential (1997)
          English Patient, The (1996)
          Titanic (1997)
    User 450
       Known positives:
          Contact (1997)
          George of the Jungle (1997)
          Event Horizon (1997)
       Recommended:
          G.I. Jane (1997)
          Conspiracy Theory (1997)
          Kiss the Girls (1997)

