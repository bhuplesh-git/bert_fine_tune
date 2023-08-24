# Fine Tune BERT for Text Classification

<div align="center">
    <img width="512px" src='https://drive.google.com/uc?id=1fnJTeJs5HUpz7nix-F9E6EZdgUflqyEu' />
    <p style="text-align: center;color:gray">Figure 1: BERT Classification Model</p>
</div>

In this notebook, we will fine tune a BERT base model with Quora data

**BERT Model:** https://tfhub.dev/tensorflow/bert_en_uncased_L-12_H-768_A-12/4 <br>
**BERT Data Preprocessor:** https://tfhub.dev/tensorflow/bert_en_uncased_preprocess/3 <br>
**Dataset:** https://archive.org/download/fine-tune-bert-tensorflow-train.csv/train.csv.zip

Here is flow on high level:

- #1 - Install and load necessary packages
- #2 - Read the data into a pandas dataframe
- #3 - Split dataset into train, validation and test data sets
- #4 - Create input pipeline using tf.data.dataset
- #5 - Load the encoder model and preprocessor model. BERT encoder require input data in fixed format, i.e., input_word_ids, input_mask input_type_ids. We can preprocess using tensorflow/keras tokenizer or use preprocessor model. In this notebook, I have used preprocess model. 
- #6 - Create the model with:
    - Input tensor
    - Preprocessor model
    - encoder
    - dropout
    - Final dense with sigmoid activation
- #7 - Compile the model, using BinaryCrossEntropy loss and AdamW optimizer. 
- #8 - Train the model
- #9 - Evaluate model against the test dataset


Fine tuning is a compute intensive work. Ideally it require GPU to take advantage of parallel computation. However, if GPU is not accessible, run it on environment with several CPUs. Best to run in Google colab or AWS SageMaker. I have used colab for this notebook.

<H3>Acnowledgement</h3>

This notebook was created based on guided project on Coursera at https://www.coursera.org/learn/fine-tune-bert-tensorflow/ungradedLti/ack5t/fine-tune-bert-for-text-classification-with-tensorflow. I modified it to take advantage of preprocessor model and latest version of tensorflow.