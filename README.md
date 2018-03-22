# face_detection_sliding_windows
A simple face detection algorithm with sliding window detector

This is a face detection method introduced in [Dalal and Triggs 2005](https://lear.inrialpes.fr/people/triggs/pubs/Dalal-cvpr05.pdf). The method has the following steps:
1. load 36 x 36 images with face as positive training data, and load random images with face as negative training data;
2. normalize them, and produce the histograms of oriented gradient for both images set;
3. build a linear classifier for the positive and negative HoG features using support vector machine, with low true negative rate;
4. for the test set, scale the image to smaller ones and run through the linear classifier. All the combined bounding box and confidence level builds the detector.

The parameters chosen are:
1. cell size: 4 x 4;
    The cell size affects the detection rate and run speed. The smaller size cell will gives a better detection, yet the run time O(N^3) increases. With 6 x 6 cell size Average Precision is 0.733, and with 4 x 4 cells, the AP increases to 0.798.
    
2. lambda for svm: 0.0001;
    The regularization parameter determines the tolerance for miss-classification. It changes the decision boundary for a non-separable dataset, and larger the lambda less smaller the decision boundary. For 6 x 6 cells, the default 0.0001 has the best performance.
    
    | lambda | average percision |
    | ---    |  ---   |
    | 0.00001|  0.715 |
    | 0.0001 |  0.733 |
    | 0.001  |  0.727 |
    | 0.01   |  0.725 |
    | 0.1    |  0.606 |
    


3. score threshold: 0.75;
    The score threshold 

4. scales: 1, 0.9, 0.75, 0.6, 0.5, 0.4, 0.25, 0.1.
