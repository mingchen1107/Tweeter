# Tweeter

Tweeter is a Character Language Model which takes in a user's Twitter Handle (gathers tweets using the [tweepy](https://www.tweepy.org/) API) and generates tweets that sound like them. 

I chose to use a Character Model over a Language Model for a few reasons:
- Character Models take up considerablly less space. For any decent word model to work, it would need to have a large vocabulary and would have to have a size in the order of thousands. For Character Models, there are < 100 characters that are feasibilly considered. This makes our vocabulary much smaller and lets us consider more samples
- Character Models allowed me to consider non english words or words that were not previously encountered. With Word Models, I would be limitted to only words that I had seen in my training data. It would be possible to come up with an "Unknown" token but this would mean that all words that are unknown would have the same meaning and weight by the models definition.

You have a few options when running the notebook:

- Train a new base model: A base model is just a model trained on generic tweets that are not from a specific user. Training over a large corpus an iterating over it multiple times will allow us to have a general model that can be fine-tuned on a per user basis. This can be modified by making
    - `TRAIN_BASE_MODEL = True`
- Iterate on the base model: You can load the base model, iterate on it and save it back thus making the generic model better. This can be modified by making
    - `TRAIN_BASE_MODEL=True`
    - `USE_OLD_MODEL=True`
- Create a new user-specific model: Input a user’s Twitter handle. By default, it will just create a new model from scratch
    - Everything can remain False
- Create a user model from the base model: You can load the base model and train the user model on top of it. This is particularly useful for users who have few tweets. It also allows you to do far fewer epochs than a new model from scratch.
    - `USE_BASE_MODEL = True`
- Train on an existing model: You can train on an existing user model and iterate on it just like iterating on the base model
    - `USE_OLD_MODEL = True`
