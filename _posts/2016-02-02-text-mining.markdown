---
layout: post
title: "Text Mining using Deep Learning"
description: "Word2Vec, Doc2Vec, Gensim, etc"
category: NLP
tags: [NLP, text mining, deep-learning, gensim, python]
---
<div id="toc"><p class="toc_title">목차</p></div>

# Text mining
NLP, Text Mining 에서 사용되는 Deep Learning 및 Topic modelling 관련 기술들을 정리해 봤습니다. 개인적으로 정리 진행중인 문서라 미흡하니 틀린 부분 혹은 추가할 항목 피드백 주시면 감사하겠습니다.

### Word2Vec
- 같은 맥락을 진니 단어끼리 가까운 의미를 지니고 있다는 전제에서 출발
- 한 단어에 대해 주변에 출현하는 다른 단어들을 관련 단어로서 인공 신경망에 학습
- 학습을 반복하는 과정에서 연관된 단어는 점차 가까운 벡터를 지님
- paper : [Efficient Estimation of Word Representations in
Vector Space](http://arxiv.org/pdf/1301.3781.pdf)
- [code](https://code.google.com/p/word2vec/)
- [wiki](https://en.wikipedia.org/wiki/Word2vec)

### Doc2Vec
- Doc2vec modifies the word2vec algorithm to unsupervised learning of continuous representations for larger blocks of text, such as sentences, paragraphs or entire documents.
- The main point is, labels act in the same way as words in Doc2Vec.
- paper : [Distributed Representations of Sentences and Documents](https://cs.stanford.edu/~quocle/paragraph_vector.pdf)
- [code](https://radimrehurek.com/gensim/models/doc2vec.html)

### LDA ( Latent Dirichlet Allocation )
- 주어진 문서들에 대해 각 문서에 어떤 주제들이 존재하는지에 대한 확률 모형
- 미리 학습된 주제별 단어수 분포 정보를 바탕으로, 주어진 문서에 어떤 주제를 다루는지 예측
- paper : [Latent Dirichlet Allocation](https://www.cs.princeton.edu/~blei/papers/BleiNgJordan2003.pdf)
- [wiki](https://en.wikipedia.org/wiki/Latent_Dirichlet_allocation)

### LSI ( Latent Semantic Indexing(Analysis) )
- LSI compares how often words appear together in the same document and compares how often those occurrences happen in ALL of the documents that Google has in its index.
- paper : [Indexing by Latent Semantic Analysis](http://lsa.colorado.edu/papers/JASIS.lsi.90.pdf)
- youtube : [Latent Semantic Indexing](https://www.youtube.com/watch?v=LOPY1hPcZEM)
- [wiki](https://en.wikipedia.org/wiki/Latent_semantic_indexing)

### TF-IDF ( Term Frequency - Inverse Document Frequency )
- 특정 단어가 문서내 얼마나 중요한 것인지 나타내는 통계적 수치
- 문서 내 얼마나 자주 등장하는지에 대한 TF 와 문서군 내에서 자주 등장하는 빈도의 역수인 IDF 를 곱한 값으로, 조사 등 흔하게 등장하는 것은 제외하고 핵심어를 추출 할 수 있다.
- [wiki](https://en.wikipedia.org/wiki/Tf%E2%80%93idf)

### CNN ( Convolutional Neural Network )
- Image Recognition 등 Computer Vision 에 주로 이용
- CNN for Modelling Sentences
    - paper : [A Convolutional Neural Network for Modelling Sentences](http://nal.co/papers/Kalchbrenner_DCNN_ACL14)
- CNN for Sentence Classification
    - paper : [Convolutional Neural Networks for Sentence Classification](http://www.aclweb.org/anthology/D14-1181)
- [wiki](https://en.wikipedia.org/wiki/Convolutional_neural_network)

### RNN ( Recursive Neural Network )
- paper : [Recursive Deep Models for Semantic Compositionality
Over a Sentiment Treebank](http://nlp.stanford.edu/~socherr/EMNLP2013_RNTN.pdf)
- [wiki](https://en.wikipedia.org/wiki/Recursive_neural_network)

### reference
- [(Deep) Neural Networks在 NLP 和 Text Mining 总结](http://www.slideshare.net/ssuser9cc1bd/piji-li-dltm)
- [Deep Learning for NLP: An Introduction to Neural Word Embeddings](http://www.slideshare.net/roelofp/041114-dl-nlpwordembeddings)
- [Deep Learning
and Text Mining](http://will-stanton.com/wp-content/uploads/2015/02/Deep-Learning-with-Text-v4.pdf)
