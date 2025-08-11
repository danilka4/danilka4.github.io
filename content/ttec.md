---
title: "TTEC"
date: 2025-05-07T02:05:52-05:00
---

This page will give a rundown of the theoretical background and methodology of Temporal Topic Embeddings with a Compass.
I will assume that the reader has a working knowledge of Word2vec/Doc2vec and topic modeling.
Going off that, here are the concepts I have divided this space into, along with a short description of each:
* Temporal Word2vec - See how words change over time
* Dynamic topic modeling - See how topics change over time
* Compass-Aligned Distributional Embeddings - A temporal embedding model paradigm that achieves alignment through freezing the output layer
* Temporal Word Embeddings with a Compass - CADE applied to Word2vec
* Temporal Document Embeddings with a Compass - CADE applied to Doc2vec
* Temporal Topic Embeddings with a Compass - CADE expanded to dynamic topic modeling

# Temporal Word2vec

Word2vec is based off the "distributional hypothesis."
This means that words are defined in terms of their environment (surrounding words).
Temporal Word2vec notices that the environment a word is used in changes over time.
Similar words across different slices should have similar vectors.
So, if a different person occupies a position across time slices, the model should capture it.
For example, "Obama" in 2009 has a vector similar to "Bush" in 2008.
If a word's context changes between slices, the vector also changes.
This allows for the tracking of a word over time as new contexts develop where it is used.
For example, Blackberry and Apple both "turn" from food into IT words.

# Dynamic Topic Modelling

Work in Progress

# Compass-Aligned Distributional Embeddings (CADE)

CADE is a family of temporal algorithms that aligns with a compass.
The base of the compass is a shallow neural network word/doc2vec model trained on all the text data.
Afterward, each time slice can be trained using the hidden layer of the compass.
Since the hidden layer is the same for all time slices, obtaining similar outcomes per slice requires similar inputs.
Thus, this method achieves temporal embedding stability.
It was initially proposed by Bianchi et al. (2020) with TWEC, which uses Word2vec.
Palamarchuk (2024, 19–24) later expands the method to documents and topics in TDEC and TTEC.

# Temporal Word Embeddings with a Compass (TWEC)

TWEC is a CADE algorithm for temporal word2vec from Di Carlo, Bianchi, and Palmonari (2019). It starts off by training a compass, which is a word2vec model trained off an entire text corpus. The compass’ hidden/output layer is frozen and used as the hidden layer of each local time slice. A local time slice is initiated as a word2vec model with the hidden layer of the compass. It is then trained on the data in the local time slice and creates local word vectors. The compass layer ensures similar words between slices have similar slices, despite being different models.

# Temporal Document Embeddings with a Compass (TDEC)

TDEC is a CADE algorithm for temporal doc2vec from Palamarchuk (2024, 16–19) (Palamarchuk et al. 2025, 274–75). It starts off by training a compass, which is a doc2vec model trained off an entire text corpus. The hidden layer of that doc2vec model is frozen and used as the hidden layer of each time slice. Functionally, it is the same as TWEC except with its Word2vec models replaced by Doc2vec.

# Temporal Topic Embeddings with a Compass (TTEC)

TTEC is a CADE algorithm for dynamic topics from Palamarchuk (2024, 19–24).
 It starts off by training a compass, which is a TDEC compass with a UMAP and HDBSCAN topic space.
 The global topic space is created using the compass document vectors.
 The global topic descriptors are the closest word vectors to the document vectors per topic.
 Time slices start off as TDEC slices trained from the global TDEC compass.
 Local topic spaces are created by placing local document vectors in the global topic space.
 Finally, local topic descriptors are made using local word vectors.

# Bibliography

Bianchi, Federico, Valerio Di Carlo, Paolo Nicoli, and Matteo Palmonari. 2020. “Compass-Aligned Distributional Embeddings for Studying Semantic Differences Across Corpora.” *arXiv Preprint arXiv:2004.06519*.

Di Carlo, Valerio, Federico Bianchi, and Matteo Palmonari. 2019. “Training Temporal Word Embeddings with a Compass.” In *Proceedings of the AAAI Conference on Artificial Intelligence*, 33:6326–34. <https://aaai.org/papers/06326-training-temporal-word-embeddings-with-a-compass/>.

Palamarchuk, Daniel. 2024. “Temporal Topic Embeddings with a Compass.” Master’s thesis, Virginia Tech. <https://hdl.handle.net/10919/119057>.

Palamarchuk, Daniel, Lemara Williams, Brian Mayer, Thomas Danielson, Rebecca Faust, Larry Deschaine, and Chris North. 2025. “Visualizing Temporal Topic Embeddings with a Compass.” *IEEE Transactions on Visualization and Computer Graphics* 31 (1): 272–82. <https://doi.org/10.1109/TVCG.2024.3456143>.

# Citation Information

Work in Progress
