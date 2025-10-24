# The report!


### Name

Nils Broman

### Introduction

### Answers to questions

#### Question 1 
| Run        |   1       |   2      |  3       | 4       | 5      | **Avg**    |
|------------|-----------|----------|----------|---------|--------|------------|
|Accuracy    |   0.8730  |   0.8710 |  0.8690  | 0.8780  | 0.8780 | **0.8738** |
|Sensitivity |   0.9040  |   0.9100 |  0.9060  | 0.9020  | 0.9020 | **0.9048** |
|Specificity |   0.8420  |   0.8320 |  0.8320  | 0.8540  | 0.8540 | **0.8428** |
|Loss        |   0.2942  |   0.2973 |  0.2993  | 0.2926  | 0.2914 | **0.2950** |


#### Question 2
Using 9 hidden nodes the accuracy of the training dataset averaged 96% over five models for the training data, with all having an accuracy >95%. This yielded and average accuracy of roughly 82% for the validation data, see tables below.

Training data

| Run        |   1       |   2      |  3       | 4       | 5      | **Avg**    |
|------------|-----------|----------|----------|---------|--------|------------|
|Accuracy    |   0.9600  |   0.9500 |  0.9600  | 0.9600  | 0.9700 | **0.9600** |
|Sensitivity |   0.9600  |   0.9400 |  0.9600  | 0.9400  | 0.9600 | **0.9520** |
|Specificity |   0.9600  |   0.9600 |  0.9600  | 0.9800  | 0.9800 | **0.9680** |
|Loss        |   0.0739  |   0.0895 |  0.0736  | 0.0698  | 0.0634 | **0.0740** |

Validation data

| Run        |   1       |   2      |  3       | 4       | 5      | **Avg**    |
|------------|-----------|----------|----------|---------|--------|------------|
|Accuracy    |   0.8290  |   0.8340 |  0.8260  | 0.8160  | 0.8230 | **0.8256** |
|Sensitivity |   0.8780  |   0.8620 |  0.8740  | 0.8380  | 0.8480 | **0.8600** |
|Specificity |   0.7800  |   0.8060 |  0.7780  | 0.7940  | 0.7980 | **0.7912** |
|Loss        |   0.9453  |   1.0068 |  0.8629  | 1.0893  | 1.0715 | **0.9952** |


#### Question 3

The optimal number of hidden nodes for the validation set appear to be 1. 

We have fairly limited training data, so larger models increases the risk of overfitting. Since the data is very cluttered and overlapps, there doesn't seem to be any true well defined hard decision border to completely seperate the two classes.

Also, since the data is simply two normal distributions, centered around two points, the best possible decision boundary would likely be a straight line right in the middle of these two points.

#### Question 4

The optimal number of hidden nodes was 5, with models of four hidden nodes being a close runner up. Average MSE for the validation data for these models where 0.485 and 0.467 respectively. This supports the statement from last exerscise about the number of optimal hidden nodes being somewhere inbetween the number of input (6) and output nodes (1).

4 Nodes
| Run        | 1             | 2             | 3             | 4             | 5            | **Avg**          |
| ---------- | ------------- | ------------- | ------------- | ------------- | ------------ | ---------------- |
| MSE        |  0.4460845590 |  0.5619271398 |  0.5321691632 |  0.4516883194 | 0.4352715015 | **0.4854281366** |
| CorrCoeff  |  0.7573914236 |  0.6974164751 |  0.6975115823 |  0.7551949763 | 0.7633638194 | **0.7341756553** |

5 Nodes
| Run        | 1             | 2             | 3             | 4             | 5            | **Avg**          |
| ---------- | ------------- | ------------- | ------------- | ------------- | ------------ | ---------------- |
| MSE        |  0.4508243799 |  0.4954376817 |  0.4211194813 |  0.5297730565 | 0.4360170960 | **0.4666343391** |
| CorrCoeff  |  0.7549106086 |  0.7327863253 |  0.7705920436 |  0.7032118186 | 0.7603448890 | **0.7443691370** |
   

#### Question 5

1 Hidden layer with 15 nodes and L2 regularization paramater 0.01 got an average MSE of 0.365.
| Run       | 1            |   2          |  3           | 4            | 5            | **Avg**          |
|-----------|--------------|--------------|--------------|--------------|--------------|------------------|
| MSE       | 0.3583167791 | 0.3607652783 | 0.3683314621 | 0.3524079919 | 0.3871167898 | **0.3653876602** |
| CorrCoeff | 0.8344250477 | 0.8388091459 | 0.8295898273 | 0.8430562209 | 0.8182193817 | **0.8328199247** |

Clear improvement compared to no regularization. 

#### Question 6

I stuggled to find a design that gave consistant models with good performance and ended up writing several loops that tested nodes in the range of 15-50 and dropout 0.05-0.5, generating hundreds of models trying to find one with better performance than in Q5, I realized that I had misread the question. Wanting to keep the network small the design I found performed the best was

30 nodes, 10% dropout, 500 epochs, batch size 50, lr 0.025
Avg MSE: ~0.5

#### Question 7

After (again) having tried litteraly hundreds of models, trying to keep the number of nodes low, I came to the rather sad conclusion that of "bigger is better" even though I've been tought otherwise. The smaller models averaged around 90% accuracy on both validation and test set, whereas the presented model averaged 93.8%. The model structure is shown in table below. 

| Nodes | Dropout | l2   | lr    | Epochs | Batch Size |
| ----- | ------- | ---- | ----- | ------ | ---------- |
| 200   | 50%     | 0.05 | 0.005 | 1000   | 512        |

I found that using only dropout led to high loss, especially when trained longer (I tested up to 5000 epochs), and by also including l2 regulurization it learned to reduce loss during training. Since the accuracy didn't increase dramatically during longer training, I settled for 1000 epochs. I believe even 300 would be more than enough though. For almost all models, a rather low learning rate and large batch size was needed for a stable learning process. Complete performance scores over five runs is shown in table below.

| Run        | 1      | 2      | 3      | 4      | 5      | **Avg**     |
| ---------- | ------ | ------ | ------ | ------ | ------ | ----------  |
| Train Loss | 0.0694 | 0.0705 | 0.0703 | 0.0691 | 0.0634 | **0.06854** |
| Train Acc  | 0.9874 | 0.9803 | 0.9801 | 0.9801 | 0.9843 | **0.98244** |
| Val Loss   | 0.2148 | 0.1766 | 0.2024 | 0.2147 | 0.1947 | **0.20064** |
| Val Acc    | 0.9393 | 0.9420 | 0.9376 | 0.9262 | 0.9367 | **0.93636** |
| Test Loss  | 0.2227 | 0.1798 | 0.1955 | 0.1997 | 0.1862 | **0.19678** |
| Test Acc   | 0.9361 | 0.9414 | 0.9379 | 0.9327 | 0.9417 | **0.93796** |

I also played around with wider models, that performed similarly. However, they all suffered from much higher loss, which is why I picked this single layer model as my final one. 

#### Question 8
Since the targets are hard labled categoricals while the loss function is continious, we can still end up with the same lableing and accuracy even though the loss is different. The categorical crossentropy loss function used for multi-class classification is defined as 

$$L(\hat{y}, y) = -\sum_i^M \log \hat{y_i} \cdot y_i $$

where $M$ is the number of output nodes, $\hat{y_i}$ the model outputs and $y_i$ the targets. In our case there's only one correct answer, so the loss is only the negative logarithm of our predicted likelihood of the target. This metric shows how certain the model is of it's prediction. High loss could therefor cause for some alarm, since this could indicate that the model haven't found very distinct differences between the different classes, which would increase the risk of incorrectly classifying some similar future input. 

I's also worth noting that the loss can be a bit missleading. We could have a situation where the model predicts e.g. 50% for the target, 43% for some other class and 1% for other 7 classes, and another model with 44% for the target and 7% for the other 8 classes. I would argue that the latter is a better prediction in most cases, since the model is much more certain of the target in relation to the other classes, whereas with the first there's more uncertainty around the prediction. With the curent loss function however, the second model would be more punished due to it only taking the target likelihood in consideration.   

In general, I'd say accuracy is the more important metric for picking a model since in the end, this is typically the type of result we're after. It all depends on what we're going to use it for, and sometimes it might be better to prioritize something else, e.g. recall when working with diseases.

#### Question 9

For this task, I experimented with a few ways of combating the issue of imbalanced data, namely adding class weights to the loss function and a few different types of resampling (SMOTE, ROS, RUS, SMOTETomek and SMOTEENN). I found that random under/oversampling worked quite poorly while SMOTE did a decent job at improving the performance, though somewhat inconsistantly. Unfortunately I did a poor job documenting the results during my experimentation, but I ended up favouring the use of a weighted loss function as my method of choice, since it proved more reliable. As for performance measures, it depends on the intent of the model, but for this exercise I'll assume we want a balanced performance across all three classes. Accuraacy is generally a poor measure for imbalanced data, since it gives very little information of the performance on the minority class. The f1 score, i.e. the harmonic mean of precision and recall, is generally a better measurement, especially since you can use a weighted average to combat imbalances in multiclass classification. Even better is simply observing the confusion matrices to get an idea of the model performance across all three classes, though more difficult to use when comparing performance of different models. 

Best model: 

| Nodes         | Parameters | lr     | Dropout | Batch size    | Epochs |
| ------------- | ---------- | ------ | ------- | ------------- | ------ |
| 64, 32        | 2819       | 0.005  | 0.5, 0  | 128           | 500    |

Stats: 

| Metric | Train | Val  | Test |
| ------ | ----- | ---- | ---- |
| wF1    |  0.89 | 0.67 | 0.63 |

#### Question 10
I found that this dataset was much more sensitive to learning rate than the ones in previous exercises, needing it to be low, where 0.001 produced good results for batch size 100. Initially I hade trouble finding a design that was capable of solving the problem, but once I started to scale in both width and depth I started to consistently find well performing models. The first design in the table below generated models with perfect accuracy nearly every time, with a clean decision boundary, which worked just as well on a second generated "test" set. However, it was a pretty large model with a total of 835 parameters. The second design that worked quite consistently had less than half the parameters, but resulted in a more messy desicion boundary, that crossed the spiral at some small gaps, which resulted in worse performance on the second set. This "test" set was not part of the exercise, but shows if the model actually finds the spiral pattern or just fits the generated data set. 

However, since the task was to find a model as small as possible to only fit the training set, I figured I could probably go smaller if I increased the batch size such that the gradient updates always considered the entire set, and increase the number of epochs to intentionally overfit the models. This allowed me to find an even smaller design with only 129 parameters, that aditionally could be trained much quicker due to higher learning rate and fewer updates per epoch. Ignoring the urge of fast training by reducing the elarning rate and training for even more epochs allowed for an even smaller design of 105 parameters. These models resulted in quite messu desicion boundaries however, and performed worse on the "test" set.  


| Nodes         | Parameters | lr     | Batch size    | Epochs (tot/peak) | Training time |
| ------------- | ---------- | ------ | ------------- | ----------------- | ------------- |
| 24, 18, 12, 6 | 835        | 0.001  | 100           | 1000/500          | ~3 min        |
| 12, 12, 12    | 361        | 0.001  | 100           | 1000/700          | ~2 min        |
| 10, 6, 4      | 129        | 0.005  | 3000          | 5000/2000         | ~30 s         |
| 8, 8          | 105        | 0.0005 | 3000          | 50000/30000       | ~5 min        |


### Summary

Through this lab, one thing that I've learnt time and time again, is the danger of getting data bias. I couldn't seem to stop myself from tweaking the parameters to the point that I pretty much had to start from scratch and redesign the entire model, only to do it all over again. One day I also hope to learn to keep record of my actions such that it allows me to take a few steps back to a more stable ground, instead of having to start over. I've also learnt the value of trying large variations of models rather than fixating on small tweaks too early. 

