# Adversarial Defense by Suppressing High Frequencies
We develop a **higt frequency suppression module** based on discrete Fourier transform which is used for adversiaral defense. It is 
efficient, differentiable and controllable. Together with adversiaral training, we won the fifth place of the defense track of the [IJCAI-2019 Alibaba Adversarial AI Challenge](https://security.alibaba.com/alibs2019)(AAAC). This project is a minimum implementation of our solution.

The motivation of our solution is that adversarial perturbations are dominated by high frequencies while information on clean images converges on low frequencies. Thus, if we suppress high frequencies of adversiaral images, the effects of adversarial perturbations will be reduced while the basic information on clean images will be preserved. See details in our paper and presentation.

# Results on AAAC
There are about 11,000 images with 110 categories for electric business. The goal is to give a right classification of an image under adversiaral perturbations which are generated by top-5 **black box attackers**. The score of a defense model for an image is measured as *0* if misclassified else L2 norm of perturbations.

| High frequency suppression | adversiaral training | Model ensemble | Score   |
| no                         | no                   | no             | 2.04    |
| no                         | yes                  | no             | 9.99    |
| yes                        | no                   | no             | 14.97   |
| yes                        | yes                  | no             | 19.05   |
| yes                        | yes                  | yes            | 19.75   |
