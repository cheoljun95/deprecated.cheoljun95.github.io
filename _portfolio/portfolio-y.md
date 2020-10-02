---
title: "Plant Disease Detecting Web Service"
excerpt: "Creative Integrated Design Course, SNU<br/><br/><img src='/images/Farmhannong.png' align='middle' width='700' height='500'>"
collection: portfolio
---

<br><br>

<img src='/images/Farmhannong.png' align='middle' width='1000' height='700'>

<p style="text-align:justify;">

This project was conducted as a part of 2018 Fall Creative Integrated Design Course in Seoul National University, which aimed to provide opportunities to participate in university-industry projects. <br><br>

I was involved in developing a plant disease detection system & web application as a team of four. Our team collaborated with LG Farm Hannong, the biggest agricultural company in South Korea, under the supervision of Prof. Yeong-Gil Shin, SNU. My role was implementing and testing deeplearning models, and visualizing the model interpretation, and implementing the backend server. <br><br>

The plant disease detection was tackled by solving the image classification problem, which categorizes the pathological degree of each disease (e.g. unaffected/early/terminal marssonia blotch). As the dataset provided from Farm Hannong was limited, we also used public plant disease dataset from PlantVillage [1] to facilitate transfer learning [2]. ResNet [3] with 34 layers showed the best performance (96.89 %) on validation data in the experiment. 

<br><br>

To improve users' confidence in our system, we also implemented a feature visualization. We utilized Guided GRAD-CAM [4] techniques to highlight which parts of the plant image are attributed to the specific classification results. <br><br>

Finally, our team implemented the web application providing plant disease detection & visualization, and relevant product recommendation. <br><br>


</p>


Reference <br><br>

[1] Hughes, D., & Salathé, M. (2015). An open access repository of images on plant health to enable the development of mobile disease diagnostics. arXiv preprint arXiv:1511.08060. <br>

[2] Yosinski, J., Clune, J., Bengio, Y., & Lipson, H. (2014). How transferable are features in deep neural networks?. In Advances in neural information processing systems (pp. 3320-3328).<br>

[3] He, K., Zhang, X., Ren, S., & Sun, J. (2016). Deep residual learning for image recognition. In Proceedings of the IEEE conference on computer vision and pattern recognition (pp. 770-778). <br>

[4] Selvaraju, R. R., Cogswell, M., Das, A., Vedantam, R., Parikh, D., & Batra, D. (2017). Grad-cam: Visual explanations from deep networks via gradient-based localization. In Proceedings of the IEEE international conference on computer vision (pp. 618-626).
