---
layout: post
image: images/cxr.jpg
title: Detect COVID-19 from Chest X-ray Images using Transfer Learning
sitemap: false
permalink: projects/cxr
# All dates must be YYYY-MM-DD format!
date: 2021-05-01
# labels:
#   - Deep reinforcement learning
#   - OpenAI gym
#   - python
#   - stable baseline
# summary: A draft implementation for a smart pricing agent based on real-world data
---
<p align="center"><img src="../images/cxr.jpg"></p>

#### Tech stack: deep learning, transfer learning, image classification

See manuscript [here](https://github.com/lilsummer/CS598_DL/blob/main/output/manuscript.pdf).

The global pandemic of COVID-19 has lead to more than $137$ million cases and 2.97 million deaths worldwide. The viral RNA RT-PCR used for screening COVID-19 is highly sensitive but requires a short sampling window and the test can be costly and time-consuming. The chest X-ray images (CXR) can provide a faster and more cost-effective way of diagnosis. There has been a considerable number of research in deep learning focusing on building image classifiers to detect COVID-19 and other types of lung diseases. We presented the performance of using several reported transfer learning methods to build a four-class classifier. We provided a comprehensive comparison on data augmentation and learning rate optimization. The performance of models were evaluated using sensitivity, specificity, PR-AUC score, precision-recall curve and training time. We discovered that the model performance was improved due to increased data size compared with the model reported one year ago. The data augmentation technique used in this study was not very effective in increasing sensitivity and might have harmed specificity. The best sensitivity score (0.9784) was through DenseNet121 with cropping augmentation and the best specificity (0.9969) was from baseline DenseNet121. Furthermore, we implemented one cycle learning policy and reduced learning rate policy on ResNet50, resulting in better performance than training with constant learning rate within shorter training time. Overall, this study explored the state-of-the-art transfer learning approaches and investigated a collection of methods to improve model performance.