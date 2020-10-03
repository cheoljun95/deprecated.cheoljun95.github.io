---
title: "BiLSTM with Attention Pooling for Dialogue Act Recognition"
excerpt: "Brain-Mind-Behavior Independent Research Course, SNU<br/><br/><img src='/images/SAR_2.png' align='middle' width='700' height='500'>"
collection: portfolio
---

<br><br>

<img src='/images/SAR_2.png' class="center" width='1000' height='700'>


<p style="text-align:justify;">
Speech act (or Dialogue act) means a role of each utterance within a dialogue, such as command, question, or acknowledgement. Speech act focuses on “what language does” and analyzing one’s speech act can infer the speaker's intention and status. As understanding speakers’ intention and status is critical for a human-like conversation, the automatic speech act recognition has a great potential to improve automatic dialogue application, such as a chatbot. <br><br> </p>
 

   
 <p style="text-align:center;"> <img src='/images/2019BMB/table_1.png' align='middle' width='400' height='400'> <br> <font size = "2"> Table 1. Examples of speech act classification. Retrieved from [2]. </font> <br> <br> </p>
 
 
<p style="text-align:justify;">
This study aims to implement automatic speech act classifier by utilizing deep learning model based on the 2-layer RNN structure (Figure.2) used by existing models (Kumar et al [1], Chen et al [2]). In addition, Attention Mechanism [7] is applied to the pooling method, which was not focused in previous studies, and compared with existing methods. <br><br>

Many studies have been done on converting natural words to numerical data. Simply encoding words in one-hot vector is not only inefficient, it cannot represent the relationship between words. To solve this problem, there have been many attempts to find a vector space, so called an embedding space, that well represents the relationship of words. In addition to word2vec [3] and GloVe [4], efforts have been made to obtain good word vectors until BERT [5], which has recently revolutionized the field of natural language processing. However, relatively little research has been done to obtain the vector of sentence units. In many cases, simple methods are used to obtain sentence vectors, such as averaging vectors of words in the sentence, or taking only the last output when gone through an RNN structure. Taking this into account, this study seeks to obtain sentence (or utterance) vectors that better represent the meaning of sentences through a novel pooling method. <br><br>

</p>

Reference <br><br>

[1] Kumar, H., Agarwal, A., Dasgupta, R., Joshi, S., & Kumar, A. (2017). Dialogue Act Sequence Labeling using Hierarchical encoder with CRF. Retrieved from http://arxiv.org/abs/1709.04250 <br>

[2] Chen, Z., Yang, R., Zhao, Z., Cai, D., & He, X. (2018). Dialogue Act Recognition via CRF-Attentive Structured Network. The 41st International ACM SIGIR Conference on Research & Development in Information Retrieval  - SIGIR ’18, 225–234. <br>

[3] Mikolov, T., Sutskever, I., Chen, K., Corrado, G. S., & Dean, J. (2013). Distributed representations of words and phrases and their compositionality. In Advances in neural information processing systems (pp. 3111-3119) <br>

[4] Mackay, C. (1875). “Glove.” Notes and Queries, s5-IV(96), 346. https://doi.org/10.1093/nq/s5-IV.96.346-c <br>

[5] ﻿Devlin, J., Chang, M.-W., Lee, K., & Toutanova, K. (2018). BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding. (Mlm). Retrieved from http://arxiv.org/abs/1810.04805 <br>

[6] Core, M. G., & Allen, J. (1997, November). Coding dialogs with the DAMSL annotation scheme. In AAAI fall symposium on communicative action in humans and machines (Vol. 56).
[7] Luong, M. T., Pham, H., & Manning, C. D. (2015). Effective approaches to attention-based neural machine translation. arXiv preprint arXiv:1508.04025. <br>

