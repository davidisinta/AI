# Project Report

## Project Overview
Part 1 was quite straightforward as the most involving step involved converting the audio file into the right format. I then tried different approaches and when transcribing and eventually got an accurate transcription. The results of my transcription were written into transcription.txt . The script for part 1 is speech_to_text.ipynb. I then generated 2 files, one for defamation sentences and another for non defamation sentences. I read them into my sentiment analysis file, used them to train the model. I made use of wandb so an API key is required. After this I trained my model and classified the sentences as defamation or not.

## Design Decisions and Outcome

- HPC: I used default settings on the HPC and they seemed to work okay for my setup.

- For training my model, I went with 3 epochs after trying different ranges and realized the model performed worse with more epochs which might be due to the fact that we have a small dataset so overtraining does not produce great results. The model largely predicted some sentences as defamatory but failed on others which were not necessarily defamatory. This might be due to the few examples we had, therefore the model generally learnt to associate negative sentiments as defamatory even though they might necessarily not be. A good example is [Defamatory] This has moved away from a news story or a lawsuit. Overall the model still performed well especially in the sentences it deemed as non-defamatory. We have almost no false negatives but a few false positives. [Non-Defamatory] I don't know who to believe.
