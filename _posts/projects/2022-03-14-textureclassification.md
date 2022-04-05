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

This project introduces a novel sensor and corresponding method to classify tactile textural data, using an analog piezoelectric record cartridge. Two distinct manners of data preprocessing were developed and investigated, using principal component analysis (PCA) on frequency-spectrum data and manual feature selection using methods inspired from audio and music classification. <br><br>

![Record Needle](/assets/images/projects/texture/record_needle.png)
<center><h2>A record cartridge, similar to what was used for classification </h2></center>


Additionally, a textural dataset was developed, consisting of eleven classes of both similar and varying textures. Multiple classifiers were used to compare with the existing literature. The best performing were found using PCA, with 99.8% test accuracy for Support Vector Machines, and 99.7% for Extra Trees and Random Forest Classifiers. Additionally, an Extra Trees Classifier using manual feature selection achieves 76.6% accuracy on only 10 milliseconds of sampling time. <br><br>

![Textures Used](/assets/images/projects/texture/texture_dataset.png)
<center><h2>The textures in the dataset. See report for full list of materials</h2></center>


These results match and exceed the current state-of-art performances while using a third or less training data on a similar set of classes, while using an inexpensive COTS sensor with two channels, as opposed to similar works which almost universally use sensors that are either 1. Custom, without instructions, 2. Expensive, or 3. Have many more input channels. <br><br>

### More Information

A recording of the corresponding presentation is shown below. For even more information, <a href="https://drive.google.com/file/d/1u7AozTrO2Hw2sq41u9TIP8lyHH0yUuEb/view?usp=sharing" target="_blank"><u>this report</u></a> provides more detail on the implementation, novelty, and more. <br><br>

{% include youtubePlayer.html id=page.youtubeId %}

<br><br>

