Over 100 million people visit Quora every month, so it's no surprise that many people ask similarly worded questions. Multiple questions with the same intent can cause seekers to spend more time finding the best answer to their question, and make writers feel they need to answer multiple versions of the same question. Quora values canonical questions because they provide a better experience to active seekers and writers, and offer more value to both of these groups in the long term.

In this project, I tried to tackle this natural language processing problem by applying long short term memory (LSTM) , which is a variance of Recurrent neural network (RNN) to classify whether question pairs are duplicates or not.

In this work, I have used Siamese deep network. Here, loss function is a similarity function which is Manhattan distance [1].	

what is a “Siamese network”?

Siamese networks are networks which consist two or more identical sub-networks in them.
Siamese network perform good with similarity problems. It has been used for the tasks like sentence semantic similarity, recognizing forged signatures etc.

Steps by step guide for the project:

1.	Firstly, word2vec embedding is done with google news as corpus. word embedding is the process of converting word into some numeric form.
word2vec captures relationship between words very nicely in the form of vectors. It consist of 300 dimensions of each word. It means a word in word2vec representation can project in 300 dimensions. word2vec uses shallow neural network to train.

2.	There is need to get rid of stop words, punctuations, special characters etc... so in this step I cleaned the text using  clean_text function which is defined in the implementation  and append 'question1', 'question2' and 'is_duplicate' from our training set csv file to the lists 'train_texts_1', 'train_text_2' and labels respectively.
Likewise,  test csv file treated in the same way.

3.	Inputs to the network are zero-padded sequences of word indices. These inputs are vectors of fixed length, where the first zeros are being ignored and the nonzeros are indices that uniquely identify words.
4.	Those vectors are then fed into the embedding layer. This layer looks up the corresponding embedding for each word and encapsulates all them into a matrix. This matrix represents the given text as a series of embeddings.

5.	 We have two embedded matrices that represent a candidate of two similar questions. Then we feed them into the LSTM  and the final state of the LSTM for each question is a 30-dimensional vector.  It is trained to capture semantic meaning of the question.

6.	By now we have the two vectors that hold the semantic meaning of each question. We put them through the defined similarity function and since we have an exponent of a negative the output (the prediction in our case) will be between 0 and 1.
