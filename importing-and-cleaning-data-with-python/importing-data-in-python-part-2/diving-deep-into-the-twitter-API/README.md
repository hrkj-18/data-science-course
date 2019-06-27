# Importing Data in Python (Part 2)

## Chapter 3 : Diving deep into the Twitter API

### The Twitter API and Authentication
```python
import tweepy
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token,access_token_secret)
```
