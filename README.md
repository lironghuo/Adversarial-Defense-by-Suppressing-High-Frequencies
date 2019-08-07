# Adversarial Defense by Suppressing High Frequencies
We develop a **higt frequency suppression module** based on discrete Fourier transform which is used for adversiaral defense. It is 
efficient, differentiable and controllable. Together with adversiaral training, we won the fifth place of the defense track of the [IJCAI-2019 Alibaba Adversarial AI Challenge](https://security.alibaba.com/alibs2019)(AAAC). This project is a minimum implementation of our solution.

The motivation of our solution is that adversarial perturbations are dominated by high frequencies while information on clean images converges on low frequencies. Thus, if we suppress high frequencies of adversiaral images, the effects of adversarial perturbations will be reduced while the basic information on clean images will be preserved. See details in our paper and presentation.

# Results on AAAC
There are about 11,000 images with 110 categories for electric business. The goal is to give a right classification of an image under adversiaral perturbations which are generated by top-5 **black box attackers**. The score of a defense model for an image is measured as *0* if misclassified else L2 norm of perturbations.

| High frequency suppression | adversarial training | Model ensemble | Score   |
| :------:                   | :------:             | :------:       | ------: |
| no                         | no                   | no             | 2.04    |
| no                         | yes                  | no             | 9.99    |
| yes                        | no                   | no             | 14.97   |
| yes                        | yes                  | no             | 19.05   |
| yes                        | yes                  | yes            | 19.75   |

As we can see, our high frequency suppression module works well. It is even better than adversarial training on this challenge. The official leaderboard is [here](https://tianchi.aliyun.com/competition/entrance/231701/rankingList/5).

# How to use our code

### Requirements

Pytorch >= 0.4.0
Python >= 3.5

### Prepare your data

First, modify the meta information in `cfg.py`. `root` means the root path of your data. `croped_size` is the size which images are croped to during training. We suggest you resize your images into a fixed size before training.
Then, generate text files of the training data and validation data. Each line of the file records the relative path and the label of an image. The label is an integer started from 0. Here is an example of a line:
```
image_00000.jpg,0
```
### Run the scripts

Suppose your training data is recorded in `train.txt` and your validation data is recorded in `valid.txt`. Then train the base model (without adversarial training):
```
python train_base.py train.txt valid.txt
```
Then the model file will be saved. Suppose it is `base.pth`. Then train the final model (with adversarial training):
```
python train_adv.py train.txt valid.txt -pth base.pth
```
See the help of `train_base.py` and `train_adv.py` for more details.

