---
title: "BiLSTM with Attention Pooling for Dialogue Act Recognition"
excerpt: "Brain-Mind-Behavior Independent Research Course, SNU<br/><br/><img src='/images/SAR_2.png' align='middle' width='700' height='500'>"
collection: portfolio
---

<br><br>

<img src='/images/SAR_2.png' class="center" width='1000' height='700'>


<p style="text-align:justify;">
Speech act (or Dialogue act) means a role of each utterance within a dialogue, such as command, question, or acknowledgement. Speech act focuses on “what language does” and analyzing one’s speech act can infer the speaker's intention and status. As understanding speakers’ intention and status is critical for a human-like conversation, the automatic speech act recognition has a great potential to improve automatic dialogue application, such as a chatbot. <br><br> 
 

</p>
   
 <p style="text-align:center;"> <img src='/images/2019BMB/table_1.png' align='middle' width='400' height='400'> <br> <font size = "2"> Table 1. Examples of speech act classification. Retrieved from [2]. </font> <br> <br> </p>

<p style="text-align:justify;">


This study aims to implement automatic speech act classifier by utilizing deep learning model based on the 2-layer RNN structure (Figure.2) used by existing models (Kumar et al [1], Chen et al [2]). In addition, Attention Mechanism [7] is applied to the pooling method, which was not focused in previous studies, and compared with existing methods. <br><br>

Many studies have been done on converting natural words to numerical data. Simply encoding words in one-hot vector is not only inefficient, it cannot represent the relationship between words. To solve this problem, there have been many attempts to find a vector space, so called an embedding space, that well represents the relationship of words. In addition to word2vec [3] and GloVe [4], efforts have been made to obtain good word vectors until BERT [5], which has recently revolutionized the field of natural language processing. However, relatively little research has been done to obtain the vector of sentence units. In many cases, simple methods are used to obtain sentence vectors, such as averaging vectors of words in the sentence, or taking only the last output when gone through an RNN structure. Taking this into account, this study seeks to obtain sentence (or utterance) vectors that better represent the meaning of sentences through a novel pooling method. <br><br>

Building Block<br><br>

 </p>
   
 <p style="text-align:center;"> <img src='/images/2019BMB/figure_1.png' align='middle' width='800' height='500'> <br> <font size = "2"> Figure 1. (a) LSTM unit architecture and formula. (b) Bi-LSTM data flow.
. </font> <br> <br> </p>

<p style="text-align:justify;">
 
 
</p>

 Speech act classification is a type of natural language processing (NLP). Natural language is featured as time-series data, and this study utilizes RNN (Recurrent Neural Network) structures which are suitable for time series data. In particular, LSTM (Long Short-Term Memory) is used as a unit building block in this study and in previous studies ([1], [2]). LSTM is an extension of RNN by incorporating memory units and update/forget gates, which solves the existing problem of vanishing gradient facilitates learning long term dependency. Furthermore, by bi-directionally arranging LSTM (Bi-LSTM, Bidirectional LSTM), the information flows both following and reversing time sequence, achieving better understanding of back and forth contexts. Bi-LSTM is an effective model for speech act classification, as understanding contexts is important to infer speakers’ intention ([1], [2]). <br><br>
 

Layer Architecture <br><br>

<p style="text-align:center;"> <img src='/images/2019BMB/figure_2.png' align='middle' width='800' height='500'> <br> <font size = "2"> Figure 2. Overall architecture of speech act classification. </font> <br> <br> </p>
<p style="text-align:justify;">

A dialogue consists of a dual hierarchical structure; a dialogue is a sequence of utterances, and each utterance is a sequence of words. As there is a high correlation in speech acts of utterances within a dialogue, such as the high probability of “answer” after “question,” the temporal dependency between utterances is also important, not only considering the temporal dependency between words. Taking this into account, the existing models ([1], [2]) and the model suggested in this study have a two-level hierarchical structure (Figure. 2). The first level layer is Utterance feature extractor that extracts an utterance vector from the sequence of words, and the second level layer, Logit, deduces speech act categories from utterance vectors. Both Utterance feature extractor and Logit use Bi-LSTM as the core skeleton. <br><br>

Utterance feature extractor consists of Embedding layer, Bi-LSTM and Pooling layer (Fig. 3-(a). Embedding layer is a layer with pretrained word embedding model, which converts words to embedding vectors. Word2vec [3] and GloVe [4] are tested and GloVe with 300 dimensions is adopted. As an augmentation of the word vectors, morpheme vectors extracted by Natural Language Tool Kit (NLTK) are concatenated to the word vectors. Pooling layer serves to obtain an embedding vector of the utterance unit by aggregating the hidden state obtained by Bi-LSTM. This will be discussed in more detail later in the subsequent section. <br><br>

Logit (Fig.3-(a)) has a relatively simple structure. The utterance vectors are processed through Bi-LSTM, and the probability of each speech act category is obtained by applying Softmax to the output hidden states of Bi-LSTM. Before the utterance vectors entering Bi-LSTM, the additional informative data are augmented: a flag identifying speakers, and a flag for indicating whether the utterance ends with a question mark. <br><br>

<p style="text-align:center;"> <img src='/images/2019BMB/figure_3.png' align='middle' width='800' height=' 1600'> <br> <font size = "2"> Figure 3. Architecture of utterance feature extractor (b) and logit (a).</font> <br> <br> </p>
<p style="text-align:justify;">
 
Pooling method <br> <br>

<p style="text-align:center;"> <img src='/images/2019BMB/figure_4.png' align='middle' width='800' height='700'> <br> <font size = "2"> Figure 4. Diagram of each pooling method. (a) attention pooling, (b) average pooling, (c) last pooling. </font> <br> <br> </p>
<p style="text-align:justify;">
 

This study proposes Attention pooling, as a novel pooling method utilizing Attention Mechanism, and compares with the existing method, Average pooling [1]. Pooling is the aggregation of a column of hidden state vectors produced by Bi-LSTM to obtain a single unit of utterance vector. Average pooling (Fig.4-(b)) is the method of averaging the hidden state vectors, and Last pooling (Fig.4-(c) is the method of using the last hidden state. Attention pooling (Fig.4-(a) proposed in this study is a method of weighting the hidden state vectors by calculating the attention weight through the Attention module. As a result, the Attention module is trained to yield attention weights in accordance with relevant significance of the given pieces. FC (Fullly Connected) network and Bi-LSTM are tested as candidate structures for the Attention Module. <br> <br>

Dataset & Experimental setting <br> <br>

SwDA (Switch Board Dialogue Act Corpus, 2000) dataset is used to test the performance of the suggested models. The SwDA consists of 1,115 call chat data and a total of about 210,000 utterances. Each utterance is labeled into 42 speech act categories according to the taxonomy from DAMSL (Dialog Act Markup in Several Layers) [6]. The policy for splitting dataset is same as existing studies (Training:1003, Validation:112, Test:19). <br> <br>

Adam optimizer is used and the initial learning rate is set to 0.01. After 100 epochs, the learning rate is lowered to 0.0001 for fine tuning. The dimension size for hidden states in all Bi-LSTM is 128, the batch size is 128, and the dropout rate is 0.2. The dimension of Attention Module is 16. Embedding layer utilizes the pretrained model (Glove [4]) without extra learning. The word length for each utterance is fixed to 36 with zero-padding. For training, 8 pieces of consecutive utterance are used as input, and the entire conversation for evaluation to calculate the accuracy. It was implemented in Python 3.6 using Pytorch 1.10 and trained using NVIDIA Titan X GPU (12GB). <br> <br>

Results <br> <br>

Comparison of Pooling Methods <br> <br>

</p>
   
 <p style="text-align:center;"> <img src='/images/2019BMB/table_3.png' align='middle' width='400' height='400'> <br> <font size = "2"> Table 2. Accuracy(precision) of each method and previous study. </font> <br> <br> </p>

<p style="text-align:justify;">

Table 2 is the result of training models with different pooling methods. Attention Pooling shows the highest performance with 80.7 percent of validation accuracy, which is higher than the existing pooling methods, the last pooling and the average pooling. Also, the performance of the proposed model is comparable with the state-of-the-art model by Chen et al[2], indicating the validity of the model. <br> <br>

The effect of the different structures of Attention Module, FC or Bi-LSTM, is not significant. This is because the hidden states from Bi-LSTM of Utterance feature extractor, which are input data of Attention Model, already have information about the context. Therefore, even in FC structure, the contexts are embedded in the attention weights. <br><br>

Qualitative Analysis of Attention <br> <br>

<p style="text-align:center;"> <img src='/images/2019BMB/figure_6.png' align='middle' width='800' height='700'> <br> <font size = "2"> Figure 5. Qualitative analysis of attention weights. </font> <br> <br> </p>
<p style="text-align:justify;">

One of the benefits of using Attention Mechanism is that it is easy to intuitively show how the model works. In this study, attention weights are extracted from Attention Module for qualitative analysis. The attention weights near the subject words in utterance tend to have higher values, meaning that the information of those parts significantly affects the classification.<br> <br>

From this result, we can infer that subjects and predicates might be critical for recognizing speech acts. As those parts are adjacent in sentence structure of English, the attention weights near the subject words are required to have high values.<br> <br>

Conclusion<br> <br>


Finally, the model proposed in this study achieved 80.73% validation accuracy. This is quite competitive considering the existing SOTA model (chen et al, CRF-ASN[2] : 80.8%) and the actual human accuracy (84%). It is less accurate than CRF-ASN, but while the CRF-ASN model applies a very complex methodology, this model has a relatively simple structure.<br> <br>

The pooling method using Attention Mechanism allow us to intuitively interpret the model's process as well as improve the performance. This certainly contributes to the field of interpretable artificial intelligence. CRF-ASN also applies the Attention Mechanism, but not to the pooling method, but to the CRF (Conditional Random Field) structure. In other words, the model in this study has the advantage of being able to interpret the operation of the model in the word level, showing which parts of utterances are critical for recognizing speech acts.<br> <br> </p>






Reference <br><br>

[1] Kumar, H., Agarwal, A., Dasgupta, R., Joshi, S., & Kumar, A. (2017). Dialogue Act Sequence Labeling using Hierarchical encoder with CRF. Retrieved from http://arxiv.org/abs/1709.04250 <br><br>

[2] Chen, Z., Yang, R., Zhao, Z., Cai, D., & He, X. (2018). Dialogue Act Recognition via CRF-Attentive Structured Network. The 41st International ACM SIGIR Conference on Research & Development in Information Retrieval  - SIGIR ’18, 225–234. <br><br>

[3] Mikolov, T., Sutskever, I., Chen, K., Corrado, G. S., & Dean, J. (2013). Distributed representations of words and phrases and their compositionality. In Advances in neural information processing systems (pp. 3111-3119) <br><br>

[4] Mackay, C. (1875). “Glove.” Notes and Queries, s5-IV(96), 346. https://doi.org/10.1093/nq/s5-IV.96.346-c <br><br>

[5] Devlin, J., Chang, M.-W., Lee, K., & Toutanova, K. (2018). BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding. (Mlm). Retrieved from http://arxiv.org/abs/1810.04805 <br><br>

[6] Core, M. G., & Allen, J. (1997, November). Coding dialogs with the DAMSL annotation scheme. In AAAI fall symposium on communicative action in humans and machines (Vol. 56).
[7] Luong, M. T., Pham, H., & Manning, C. D. (2015). Effective approaches to attention-based neural machine translation. arXiv preprint arXiv:1508.04025. <br><br>

