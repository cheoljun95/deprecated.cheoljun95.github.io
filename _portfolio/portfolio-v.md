---
title: "NS-VQA: application to real world data and limitation"
excerpt: "Bachelor’s Thesis, SNU<br/><img src='/images/NS-GQA_2.png' align='middle' width='700' height='500'>"
collection: portfolio
---
<br><br>

<img src='/images/NS-GQA_2.png' class="center" width='1000' height='700'> <br>

<font size="2"> This research project was conducted for Bachelor’s Thesis of the department of Computer Science and Engineering at Seoul National University. </font><br> 

<p style="text-align:justify;">
Visual Question Answer (VQA) is an artificial intelligence (AI) task that answers questions based on images. This is a task that can comprehensively evaluate AI's perceptual ability and reasoning ability, where AI should interpret given questions and deduce answers based on the relationship between recognized objects. In other words, the ability to understand the relationship between objects must be good first, and the second must be to understand what the questionnaire requires and what reasoning should be done. Finally, the ability to draw conclusions by aggregating visually recognized information and instructions extracted from natural language is needed. The system proposed in NS-VQA[1] consists of modules responsible for each of these three essential capabilities. <br> <br>

The most efficient form of data in the task of reasoning based on relationship information is a graph [4]. In the field of computer vision, this is a Scene Graph Generation (SGG) task that recognizes not only objects but also relationships between objects [6], [7], [8]. Most existing VQA models utilize the end-to-end model [10] that combines natural language processing modules with object recognition models, and the latest [1],[9], and [11] have the form of a Modular Network model based on SGGG. [1] uses the symbol as it is, while [9], [11] uses the method of learning the embedding of the symbol. <br> <br>

This study uses the NS-VQA approach of [1]. In [1], the applied CLEVR dataset is a dataset with very limited types and properties of objects. Conversely, a GQA dataset is a dataset that is closer to the real-world by encompassing hundreds of types, attributes, and relationships. Also, the dataset provides a label for the Symbolic program. This study aims to apply the NS-VQA system to GQA datasets. The system is composed of the following three modules: a detector module that generates a scene graph from an image, an encoder module that extracts a symbolic program from a natural language question, and an executor module that yields the answer from the scene graph and the symbolic program. In this study, the performance of the system without end-to-end learning is reported, and the limitation of NS-VQA approach for the real-world is analyzed. <br><br>

<p style="text-align:center;"><font size="5">  <br> Method  </font><br> <br> </p>

Detector Module <br><br>

</p>
   
 <p style="text-align:center;"> <img src='/images/2020BT/figure_1.png' align='middle' width='800' height='500'> <br> <font size = "2"> Figure 1. Detector module pipeline.
 </font> <br> <br> </p>

<p style="text-align:justify;">

The detector module is an object detection model that learns end-to-end by adding a relation head to deduce the relationship between objects. First, create a ground truth label for the name, attribute, and relationship of the object within each image in the scene graph provided by the GQA dataset. In this procedure, the top 800, 600, and 200 labels were selected for each label type, and the selected data cover more than 95% of the original dataset. <br><br>

Due to the large number of labels,  the model utilizes the hierarchical Softmax. This method is from [12], in which the label is reconstructed into a tree structure of higher and lower concepts, and then individual Softmax is applied to the lower concepts of the same higher concepts. WordNet [14] is used to obtain a directed graph of the relationship between the parent and the child. By setting the first root as 'physical identity', leaving only the shortest-distance node from each label to the root, a tree-shaped hierarchy can be derived. In this case, 64 newly generated intermediate nodes are added to the label so that Softmax is applied for each level of the hierarchy. Inference consists of multiplying the probability of the higher concept up to the root according to the principle of conditional probability. This allowed performance (mAP) to be improved from 0.17 to 0.19/ <br> <br>

In the case of attributes, it is divided into non-exclusive (e.g., color & shape) and exclusive (e.g., red & blue). The "Query - " in the question data provided from the GQA dataset was used. For example, "Query color ..." The following answers (e.g. "red", "blue") are regarded as lower concepts of the querying attribute (e.g. color). <br><br>

For the object detection model, ResNet was used as the backbone of the Faster-RCNN [13] model. In addition to the object detection head, the attribute head is introduced to infer not only the class of the object but also its properties. <br><br>

For inferring relations in the form of a graph, the Neural Motif [7] method was introduced. In the method, the relationships of objects are inferred considering the given context. In this study, Transformer [15] was used as a module to calculate the context of the image. Due to the fact that the number of labels is 200, which is four times higher than [7], but has less data, this study adopted the predicate classification paradigm where the model learns to infer relations (predicates) from the ground truth boxes and labels. <br><br>

Encoder Module <br><br>

Encoder module functions to convert a given natural language question into a symbolic program. Before entering, I would like to explain the Symbolic program approach introduced in this study. <br><br>

Neural State Machine (NSM) is an automata that yields answers with scene graphs and instructions, proposed in [9]. In this method, the activation value is endowed in each node and edge in the scene graph, and each instruction sequentially changes the activation states of the graph to produce the final answer. The instruction activates the node or edge that best matches the instruction. In the NSM, the degree of matching is calculated by the distance in the embedding space, so called a conceptual embedding. The conceptual embedding also distinguishes whether the construction is applied to nodes or to edges. In this study, the concept of the state machine is introduced, but the activation is determined based on symbol matching without the use of embedding. <br><br>

So, it is necessary to convert the symbolic program label of existing datasets into NSM format. The existing construction consists of "Select," "Relate," "Query," "Exist," "Verify," "Choose," "Choose relation," "And," "Or," "Different," "Common," all of which, except "Select" and "Relate," indicate the requirements and types of questions in order to produce the final answer. Except for "Different," and "Common," NSM and NS-VQA are equivalent. A new simpler format is defined to make instructions more machine-interpretable ( "instruction = [n,r,o]").

All values for "n,r,o" are binary, i.e. 0 or 1. "n" indicates when the construction wants to find an object that does not correspond to the concept (e.g. "Select (not) black"). "r" indicates whether the instruction is applied to the edge. "o" indicates whether the direction of the edge meant by "r" instruction. And to make the system simple, it does not cover "Different" and "Common" queries. The dataset for the encoder module could eventually include approximately 94% of existing questions. <br><br>

</p>
   
 <p style="text-align:center;"> <img src='/images/2020BT/figure_2.png' align='middle' width='800' height='500'> <br> <font size = "2"> Figure 2. Encoder module pipeline.
 </font> <br> <br> </p>

<p style="text-align:justify;">
   
The architecture of the encoder model is a Seq2seq model, as both input and output data are sequences. The model utilizes biLSTM combined with attention mechanism, followed by the method of [17]. The word embedding was initialized with GloVe [18]. The input consists of words from a natural language question and yields a sequence of symbols, instructions, and their types. <br><br>

Executer Module <br><br>

</p>
   
 <p style="text-align:center;"> <img src='/images/2020BT/figure_3.png' align='middle' width='800' height='500'> <br> <font size = "2"> Figure 3. An example of executer module process.
 </font> <br> <br> </p>

<p style="text-align:justify;">

The executer module is a module that executes the aforementioned state machine. Initially, all the activations of nodes and edges are initialized to 1 and are filtered out by solving instructions. Here, the value of the state was defined conclusively ( state(i) {0,1} ). For this purpose, a threshold was set for each concept to activate or filter out nodes or edges ( match(i), symbol), match(i,j), symbol {0,1} in Algorithm 1 ). The threshold value was set as the minimum value allowing 90 % recall for each concept, which can be derived from the statistics of the detector module. If any matching label is present, the state must be activated, which is simple to implement using the max function (Algorithm 1). <br><br>


</p>
   
 <p style="text-align:center;"> <img src='/images/2020BT/algorithm_1.png' align='middle' width='800' height='500'> <br> <font size = "2"> Algorithm 1. Executer Algorithm.
 </font> <br> <br> </p>

<p style="text-align:justify;">
  

<p style="text-align:center;"><font size="5">  <br> Results  </font><br> <br> </p>

The experiment was conducted upon the balanced version of GQA dataset, which eliminated biases in the distribution of answers. The dataset consists of about 940 K training data and 130 K validation data for questions, and the number of photos corresponding to each division is about 74,000 and 10,000. The model was implemented with PyTorch running on a single NVIDIA Titan X GPU.<br><br>

First, the results of the Detector module are as follows.  The mAP metric is calculated based on IoU > 0.5. Graph recall averages the proportion of correct answers in the top 20. The performance of the attribute head is not reported as it is hard to validate because attribute categories are not exclusive and labeling is not complete.  The performance of the detector module is not very good as shown in Table 1.<br><br>

</p>
   
 <p style="text-align:center;"> <img src='/images/2020BT/table_1.png' align='middle' width='300'> <br> <font size = "2"> Table 1. Detector module fitting results. 
 </font> <br> <br> </p>

<p style="text-align:justify;">
   
The results of fitting the encoder module are as follows. In contrast to the detector module, the performance is fine enough. This seems to be due to the fact that the question data is more than the photo data and that the question structure has a relatively simple pattern. The performance degradation factor of the Encoder module is mainly inferring symbol.<br><br>


</p>
   
 <p style="text-align:center;"> <img src='/images/2020BT/table_2.png' align='middle' width='300'> <br> <font size = "2"> Table 2. Encoder module fitting results. 
 </font> <br> <br> </p>

<p style="text-align:justify;">
 
Finally, the results are as in Table 3. The results of this study were marked NS-VQA and NS-VQA (oracle) was the result of the use of the correct scan graph. 

</p>
   
 <p style="text-align:center;"> <img src='/images/2020BT/table_3.png' align='middle' width='300'> <br> <font size = "2"> Table 3. Performance of the proposed system and models from previous studies.
 </font> <br> <br> </p>

<p style="text-align:justify;">
   
The final results in Table 3 show that NS-VQA's performance is significantly lower than that of previous studies. I would like to discuss the cause of this. The biggest cause is the degradation of performance due to the limits of the detector module. The results from Table 1 earlier show that the performance learned is not so good, as shown by the performance differences between NS-VQA and NS-VQA (oracle) in Table 3. <br><br>

The low performance of the Detector module is due to the fact that the types of labels assumed by the GQA are very numerous and complex. Compared to MS COCO, which is a performance indicator of existing object recognition models, the number of labels is also significantly insufficient. In addition, labels are not meaningfully independent, and interrelated labels interact as distractors, significantly reducing model performance [12]. The scene graph label of the dataset is only partially labeled and the distribution is also highly biased [7], [8]. Incomplete labeling also resulted in poor performance of NS-VQA (oracle). In [1], the reason why NS-VQA could be successful with respect to CLEVR is also because CLEVR has a very limited label structure. <br><br>

The preceding analysis suggests that the NS-VQA system is not scalable for the label structure. Embedding can be introduced as a solution to mitigate this non-scalability. It is calculated from the distance between the embedding by projecting whether or not the Symbol matches into the embedding space.[9],[11]. In addition, the application of end-to-end or joint training methods is indispensable to introduce such embedding. In this study, a fundamental number is needed to apply the end-to-end or point-training learning structure because it is designed for the purpose of viewing the performance limits when each is learned in the absence of an end-to-end. In [1], [9], which is applied with a deuterical exit, reinforcement learning method was used for point training. In [11], encoder module and exit module are taught end-to-end. <br><br>

Finally, the introduction of advanced embedding also mitigates the degradation of the detector module and is not a fundamental solution. This is a more fundamental problem because it is difficult to implement a complete cognitive model with simple visual or natural language data alone. The vision model, such as object recognition or SGG, is simply a statistical model of the distribution of given visual data and the extracted visual representation, not a model of the world that is actually formed within a human brain. These problems mean that there is a performance cap for VQA tasks. <br><br>
    
   
Reference <br><br>

[1] Yi, K., Torralba, A., Wu, J., Kohli, P., Gan, C., and Tenenbaum, J. B. (2018). Neural-symbolic VQA: Disentangling reasoning from vision and language understanding. Advances in Neural Information Processing Systems (NeurIPS), 1031–1042, 2018.<br><br>

[2] J. Johnson, B. Hariharan, L. Maaten, J. Hoffman, L. Fei-Fei, L. Zitnick, and R. Girshick (2018). Inferring and executing programs for visual reasoning. In IEEE international conference on computer vision (ICCV), 2017b.<br><br>
[3] D. Hudson and C. D Manning (2019). GQA: A new dataset for real-world visual reasoning and compositional question answering. In Conference on Computer Vision and Pattern Recognition (CVPR), 2019.<br><br>

[4] Battaglia, P. W., Hamrick, J. B., Bapst, V., Sanchez-Gonzalez, A., Zambaldi, V., Malinowski, M., … Pascanu, R. (2018). Relational inductive biases, deep learning, and graph networks. 1–40. <br><br>

[5] K. He, G. Gkioxari, P. Dollár, and R. Girshick (2017). Mask R-CNN. In Proceedings of the IEEE international conference on computer vision (ICCV), pp. 2961–2969, 2017.<br><br>

[6] D. Xu, Y. Zhu, C. B Choy, and L. Fei-Fei (2017). Scene graph generation by iterative message passing. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), volume 2, 2017.<br><br>

[7] R. Zellers, M. Yatskar, S. Thomson, and Y. Choi (2018). Neural motifs: Scene graph parsing with global context. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), pp. 5831–5840, 2018.<br><br>

[8] J. Yang, J. Lu, S. Lee, D. Batra, and D. Parikh (2018). Graph r-cnn for scene graph generation. arXiv preprint arXiv:1808.00191, 2018.<br><br>

[9] D. A. Hudson and C. D. Manning (2019). Learning by Abstraction: The Neural State Machine. Advances in Neural Information Processing Systems (NeurIPS), 1–17. <br><br>

[10] D. Teney, P. Anderson, X. He, and A. Hengel (2018). Tips and Tricks for Visual Question Answering: Learnings from the 2017 Challenge. Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), pp. 4223–4232. <br><br>

[11] J. Mao, J, C. Gan, P. Kohli, J. B. Tenenbaum, and J. Wu (2019). The neuro-symbolic concept learner: Interpreting scenes, words, and sentences from natural supervision. 7th International Conference on Learning Representations (ICLR) 2019, 1–28.<br><br>

[12] J. Redmon and A.Farhadi (2017). Yolo9000: better, faster, stronger. In Proceedings ofthe IEEE conference on computer vision and pattern recognition (CVPR), pp. 7263–7271, 2017.<br><br>

[13] S. Ren, K. He, R. Girshick, and J. Sun (2015). Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks. Advances in Neural Information Processing Systems (NeurIPS), 2015.<br><br>

[14] G. A. Miller, R. Beckwith, C. Fellbaum, D. Gross, and K. J. Miller (1990). Introduction to wordnet: An on-line lexical database. International journal of lexicography, 3(4):235–244, 1990.<br><br>

[15] A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L. Jones, A. N. Gomez, Ł. Kaiser, and I. Polosukhin (2018). Attention is all you need. Advances in Neural Information Processing Systems (NeurIPS), 2017.<br><br>

[16] R. Krishna, Y. Zhu, O. Groth, J. Johnson, K. Hata, J. Kravitz, S. Chen, Y. Kalantidis, L.-J. Li, D. A. Shamma, et al (2017). Visual genome: Connecting language and vision using crowdsourced dense image annotations. International Journal of Computer Vision, 123(1):32–73, 2017.<br><br>

[17] M. Luong, H. Pham, and C. Manning (2015). Effective approaches to attention-based neural machine translation. In Conference on Empirical Methods in Natural Language Processing (EMNLP), 2015.<br><br>

[18] J. Pennington, R. Socher, and C. Manning. Glove: Global vectors for word representation. In Conference on Empirical Methods in Natural Language Processing (EMNLP), 2014.<br><br>

