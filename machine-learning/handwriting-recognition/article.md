---
title: Handwriting recognition
created: 2016-01-01
taxonomy:
  category: [Machine Learning]
  status: in progress
---

## Context
Handwriting recognition has been one of the first task to interest machine learning and AI researchers. The initial goal was to rapidly process IRS forms and convert them into their digital equivalent. This meant that a large amount of handwritten content was available, all that was missing was to label it and then develop tools to convert the characters image into their ASCII equivalent.

## Learned in this study

## Things to explore

# Overview

# Challenges
* How to detect characters?
  * How to support multi-scale characters recognition?
* How to group characters together to form words/large numbers?
* How do you group together words in order to form lines?
* How to improve word recognition accuracy using a vocabulary?

# Assumptions
* Content is written on white sheets of papers
* Paper might have lines (loose leaf sheet)
* Paper may have various formats (generally 8.5"x11")
* Glyphs are generally written using a color that has a large contrast with the sheet/background color
* Text may be blurry due to the capture device
* Image size is expected to vary (due to the capture device)
* PPI may vary
* Language may vary and many languages may be used within the same page
* Page may contain one or many images/drawing

# Naive approach
* Preprocess image
	* RGB to gray (0-255) or black and white (0-1)
	* Canny edge detection
	* Noise removal (Gaussian, salt and pepper)
* Line extraction
	* Cropping of the text region
	* Vertical scan to find blank rows => line separator
* Letter extraction
	* Horizontal scan to find blank columns => character separator

# Method
DNN: 2 layers of dense 512 units with relu activation, with a dropout layer of ratio 0.2, softmax activation on the output layer, optimizing categorical cross-entropy

Based off https://github.com/fchollet/keras/blob/master/examples/mnist_mlp.py.

CNN: 2 convolutional layers of kernel size (3, 3) with relu activation, then max pooling (2, 2), 0.25 dropout, flatten, dense 128 with relu activation, 0.5 dropout and finally a softmax output layer, optimizing categorical cross-entropy

Based off https://github.com/fchollet/keras/blob/master/examples/mnist_cnn.py.


Test set size is 25% of the training set size (thus 20% of the total data set size). The training and test sets are fixed.

# Results

<table>
  <tr>
    <th style="text-align: center;">Network</th>
    <th>Character classes</th>
    <th>Training set size</th>
    <th>Training duration per epoch (s)</th>
    <th>Test loss</th>
    <th>Test accuracy</th>
  </tr>
  <tr>
    <th rowspan="5" style="text-align: center;">DNN</th>
    <th>Digits</th>
    <td>39990</td>
    <td>3</td>
    <td>0.103</td>
    <td>0.973</td>
  </tr>
  <tr>
    <th>Lowercase letters</th>
    <td>103974</td>
    <td>8</td>
    <td>0.295</td>
    <td>0.905</td>
  </tr>
  <tr>
    <th>Uppercase letters</th>
    <td>103974</td>
    <td>9</td>
    <td>0.238</td>
    <td>0.936</td>
  </tr>
  <tr>
    <th>Letters</th>
    <td>207948</td>
    <td>24</td>
    <td>0.700</td>
    <td>0.712</td>
  </tr>
  <tr>
    <th>All</th>
    <td>247938</td>
    <td>32</td>
    <td>0.794</td>
    <td>0.688</td>
  </tr>
  <tr>
    <th rowspan="5" style="text-align: center;">CNN</th>
    <th>Digits</th>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <th>Lowercase letters</th>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <th>Uppercase letters</th>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <th>Letters</th>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <th>All</th>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>

# Improvement of results
* To evaluate what should be improved/worked on, note that a sequential pipeline is the most affected by its earlier components, and thus the accumulation of errors early on will propagate to the further layers

# Papers summaries
## End-to-end scene text recognition
### Character detection
* Multi-scale character detection via sliding window classification
* Use of Random Ferns due to the large number of categories (62 => 26 upper/lower + 10 digits)
  * Naturally multi-class and efficient both to train and test
* The features consist of applying randomly chosen thresholds on randomly chosen entries in a HOG descriptor computed at the window location
* Application of non-maximal suppression

# See also

# References
* Ba, Jimmy, Volodymyr Mnih, and Koray Kavukcuoglu. "Multiple object recognition with visual attention." arXiv preprint arXiv:1412.7755 (2014).
* Ciregan, Dan, Ueli Meier, and Jürgen Schmidhuber. "Multi-column deep neural networks for image classification." Computer Vision and Pattern Recognition (CVPR), 2012 IEEE Conference on. IEEE, 2012.
* Goodfellow, Ian J., et al. "Multi-digit number recognition from street view imagery using deep convolutional neural networks." arXiv preprint arXiv:1312.6082 (2013).
* Graves, Alex, et al. "A novel connectionist system for unconstrained handwriting recognition." IEEE transactions on pattern analysis and machine intelligence 31.5 (2009): 855-868.
* Graves, Alex, and Jürgen Schmidhuber. "Offline handwriting recognition with multidimensional recurrent neural networks." Advances in neural information processing systems. 2009.
* Larochelle, Hugo, and Geoffrey E. Hinton. "Learning to combine foveal glimpses with a third-order Boltzmann machine." Advances in neural information processing systems. 2010.
* Neumann, Lukáš, and Jiří Matas. "Real-time scene text localization and recognition." Computer Vision and Pattern Recognition (CVPR), 2012 IEEE Conference on. IEEE, 2012.
* Wang, Kai, Boris Babenko, and Serge Belongie. "End-to-end scene text recognition." Computer Vision (ICCV), 2011 IEEE International Conference on. IEEE, 2011.
* https://en.wikipedia.org/wiki/Handwriting_recognition
* https://en.wikipedia.org/wiki/Handwriting_movement_analysis
* https://en.wikipedia.org/wiki/Intelligent_character_recognition
* http://arxiv.org/abs/1507.05244
* https://people.eecs.berkeley.edu/~fateman/kathey/char_recognition.html
* http://www.neuroscript.net/movalyzer.php
* http://u-pat.org/ICDAR2017/program_competitions.html
* http://rrc.cvc.uab.es/?ch=10&com=introduction
* Non-maximum suppression - http://www.pyimagesearch.com/2015/02/16/faster-non-maximum-suppression-python/
* https://www.youtube.com/watch?v=nlMjSWnvglU
* http://blog.leanote.com/post/wjgaas@126.com/OCR-List

## Data sets
* http://www.fki.inf.unibe.ch/databases/iam-handwriting-database