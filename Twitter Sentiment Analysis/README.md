
Link: https://notebooks.azure.com/CharlBest/libraries/learn/html/TwitterSentimentAnalysis.ipynb

Just make sure the dependencies are installed


```python
!pip install tweepy
!pip install textblob
```

Test out the Text Blob library


```python
from textblob import TextBlob

wiki = TextBlob("Charl is very happy that he is searching for a new job")
wiki.tags
wiki.sentiment.polarity
```

    Requirement already satisfied: tweepy in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages
    Requirement already satisfied: requests>=2.4.3 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from tweepy)
    Requirement already satisfied: six>=1.7.3 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from tweepy)
    Requirement already satisfied: requests-oauthlib>=0.4.1 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from tweepy)
    Requirement already satisfied: chardet<3.1.0,>=3.0.2 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from requests>=2.4.3->tweepy)
    Requirement already satisfied: idna<2.7,>=2.5 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from requests>=2.4.3->tweepy)
    Requirement already satisfied: urllib3<1.23,>=1.21.1 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from requests>=2.4.3->tweepy)
    Requirement already satisfied: certifi>=2017.4.17 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from requests>=2.4.3->tweepy)
    Requirement already satisfied: oauthlib>=0.6.2 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from requests-oauthlib>=0.4.1->tweepy)
    Requirement already satisfied: textblob in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages
    Requirement already satisfied: nltk>=3.0 in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from textblob)
    Requirement already satisfied: six in /home/nbcommon/anaconda3_501/lib/python3.6/site-packages (from nltk>=3.0->textblob)





    0.5681818181818181



Understanding and extracting feelings from Twitter data


```python
import tweepy
from textblob import TextBlob

consumer_key = 'pQYdePDc16g0uJWJcjPWTY2km'
consumer_secret = 'Vnr3qXystswaimMBp1SBdklgIEkoCnQxBUuDVyfeJ3NLWAUkn2'

access_token = '2723557496-GUGqpJeN4scsPRzxyUrRGtxAcHnyv81JtgN7l4z'
access_token_secret = 'ZtPq7OcW9TcxeicQpMteX2e8J8p2LFSJ2adJaGJhsbluU'

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.API(auth)

public_tweets = api.search('Trump')
for tweet in public_tweets:
    print(tweet.text)
    analysis = TextBlob(tweet.text)
    print(analysis.sentiment)
```

    RT @keithboykin: Don’t act surprised that Trump is resurrecting his “Pocahontas” attack on Senator Elizabeth Warren today. Remember, this w…
    Sentiment(polarity=0.1, subjectivity=0.9)
    RT @CNN: Sarah Sanders says she doesn't think it's a racial slur for President Trump to refer to Sen. Warren as "Pocahontas" https://t.co/S…
    Sentiment(polarity=0.0, subjectivity=0.0)
    RT @CNN: Bottles from Trump Winery have been on sale at a gift shop in Shenandoah National Park, drawing criticism from ethics watchdogs fo…
    Sentiment(polarity=0.0, subjectivity=0.0)
    RT @amvetsupport: Damn these trump supporters are morons. They truly believe that greedy CEO's and shareholders are going to use their extr…
    Sentiment(polarity=-0.8, subjectivity=1.0)
    RT @C_W_UK: #RoyMoore #Trump #MAGA https://t.co/KMvM77fa4u
    Sentiment(polarity=0.0, subjectivity=0.0)
    RT @SethAbramson: @ScottMStedman 15/ That Aras Agalarov signed a letter-of-intent in November 2013, then waited *well over 3 years* to decl…
    Sentiment(polarity=0.0, subjectivity=0.0)
    @NigarTugsuz Bürokrasinin hükümranlığı veya vesayeti daha doğru bir ifade olur, aynı bürokrasi Trump’tan da kurtulm… https://t.co/rwMFkfhvmY
    Sentiment(polarity=0.0, subjectivity=0.0)
    RT @aparnapkin: i honestly would not be surprised if a bug crawled out of trump’s mouth next
    Sentiment(polarity=0.2333333333333333, subjectivity=0.6)
    RT @RedTRaccoon: To Sarah Huckabee Sanders &amp; Donald Trump,
    
    Just because you don't believe the term Pocahontas is a racial slur, doesn't ch…
    Sentiment(polarity=0.0, subjectivity=0.0)
    RT @DewsNewz: The winners for the #FakeNewsAwards for 2017 are ...
    Fake News Anchor - Joe and Mika
    Entertainer - Colbert
    Publication - NY T…
    Sentiment(polarity=-0.5, subjectivity=1.0)
    RT @SenFeinstein: The president claims he won’t benefit from the #GOPTaxPlan. If that’s true, he can easily prove it by releasing his retur…
    Sentiment(polarity=0.39166666666666666, subjectivity=0.7416666666666667)
    RT @vicenews: Donald Trump was supposed to be honoring Native American code talkers who served in WWII. And then he called Elizabeth Warren…
    Sentiment(polarity=0.0, subjectivity=0.0)
    @jonfavs You heard it, Alabama. Write in Ringo Starr. It's what Brietbart wants. It's what President Trump wants. Write in Ringo Starr.
    Sentiment(polarity=0.2, subjectivity=0.1)
    RT @faesq3639: @imwithher61 @KaivanShroff @vickscan The Franken mania is so hypocritical. Calling for him to resign while Alabama eects a p…
    Sentiment(polarity=0.0, subjectivity=0.0)
    RT @thehill: Morrissey: I would kill Trump "for the safety of humanity" https://t.co/nt78DTNXiT https://t.co/eBDNGbK5OC
    Sentiment(polarity=0.0, subjectivity=0.0)

