# Emotion-Classification

## Model for text-based classification
### TextCnn https://github.com/delldu/TextCNN

Here is the replication of the model, here are the operations of the model:
* **Embedding**: Embeds a batch of text of shape (N, L) to (N, L, D), where N is batch size, L is maximum length of the batch, D is the embedding dimension. 

* **Convolutions**: Runs parallel convolutions across the embedded words with kernel sizes of 3, 4, 5 to mimic trigrams, four-grams, five-grams. This results in outputs of (N, L - k + 1, D) per convolution, where k is the kernel_size. 

* **Activation**: ReLu activation is applied to each convolution operation.

* **Pooling**: Runs parallel maxpooling operations on the activated convolutions with window sizes of L - k + 1, resulting in 1 value per channel i.e. a shape of (N, 1, D) per pooling. 

* **Concat**: The pooling outputs are concatenated and squeezed to result in a shape of (N, 3D). This is a single embedding for a sentence.

* **Dropout**: Dropout is applied to the embedded sentence. 

* **Fully Connected**: The dropout output is passed through a fully connected layer of shape (3D, 1) to give a single output for each example in the batch. sigmoid is applied to the output of this layer.

* **load_embeddings**: This is a method defined for TextCNN to load embeddings based on user input. There are 3 modes - rand which results in randomly initialized weights, static which results in frozen pretrained weights, nonstatic which results in trainable pretrained weights. 


Let's note that this model works for variable text lengths! The idea to embed the words of a sentence, use convolutions, maxpooling and concantenation to embed the sentence as a single vector! This single vector is passed through a fully connected layer with sigmoid to output a single value. This value can be interpreted as the probability a sentence is positive (closer to 1) or negative (closer to 0).

The minimum length of text expected by the model is the size of the smallest kernel size of the model.

## Pipeline 
1. gathering dataset (IEMOCAP)
2. extracting utterances and labels
    1. filltering utterances with no annotation
3. preprocessing the data (with punctuation)
    1. Tokenize the data (string_to_sequence)
    2. Creating counter type for the tokens for encoding
    3. Creating the Vocab object to use it as map the encodings
    4. padding the sequences after encoding (for max sequence len of the dataset)
    5. creating trian iterator
4. create the TextCnn model
5. create the model object and optimizer
6. train the model with train_iter
7. Test and evaluation

## Step of Implementation
You can download the IEMCAP dataset and run extrac_label to get the label and then start with preproecssing.
1. Download the train.pkl and test.pkl files
2. Run preparing_Data.ipynb to create pickle file
3. Model.ipynb loads the pickel file, preprocess it and train the model

