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

Detector Module <br><br>

The detector module is an object detection model that learns end-to-end by adding a relation head to deduce the relationship between objects. First, create a ground truth label for the name, attribute, and relationship of the object within each image in the scene graph provided by the GQA dataset. In this procedure, the top 800, 600, and 200 labels were selected for each label type, and the selected data cover more than 95% of the original dataset. <br><br>


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

