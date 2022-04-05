---
layout: project
permalink: /:title/
category: projects

meta:
  keywords: "Tactile, Texture, Machine Learning"

project:
  title: "Tactile Texture Classification"
  type: "Jekyll"
  logo: "/assets/images/projects/texture/setup.png"
  tech: "Tactile Sensing, Machine Learning, Research"

youtubeID: TPY07R9Mu50
---

### Abstract

This project introduces a novel sensor and corresponding method to classify textural data, using an analog piezoelectric record cartridge. Two distinct manners of data preprocessing were developed and investigated, using principal component analysis (PCA) on frequency-spectrum data and manual feature selection using methods inspired from audio and music classification. <br><br>

Additionally, a textural dataset was developed, consisting of eleven classes of both similar and varying textures. Multiple classifiers were used to compare with the existing literature. The best performing were found using PCA, with 99.8% test accuracy for Support Vector Machines, and 99.7% for Extra Trees and Random Forest Classifiers. Additionally, an Extra Trees Classifier using manual feature selection achieves 76.6% accuracy on only 10 milliseconds of sampling time. <br><br>

These results match and exceed the current state-of-art performances while using less training data on a similar number of classes, while using only two sensing modalities. <br><br>

### More Information

A recording of the corresponding presentation is shown below. For even more information, <a href="https://drive.google.com/file/d/1u7AozTrO2Hw2sq41u9TIP8lyHH0yUuEb/view?usp=sharing" target="_blank"><u>this report</u></a> provides more detail on the implementation, novelty, and more. <br><br>

{% include youtubePlayer.html id=page.youtubeId %}

