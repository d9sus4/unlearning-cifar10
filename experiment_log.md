## Original results

### On original pre-trained model, no modifications:
Train set accuracy: 99.5%
Test set accuracy: 88.3%
The MIA has an accuracy of 0.579 on forgotten vs unseen images

### On forget-by-finetuning model, epoch=5, lr=0.1, momentum=0.9, wd=5e-4, SGD
Retain set accuracy: 98.3%
Test set accuracy: 84.0%
The MIA has an accuracy of 0.512 on forgotten vs unseen images

### On re-trained model:
Retain set accuracy: 99.5%
Forget set accuracy: 88.2%
The MIA has an accuracy of 0.502 on forgotten vs unseen images

## Forget by Neutralizing Forget Labels

Core idea:
For samples in forget set, make the model predictions (raw logits should be processed with softmax to get probabilities) close to uniform distribution. Use MSE loss to optimize for this objective.
For samples in retain set, keep finetuning.

### Exp 1
Settings (for both retain and forget objectives):
- lr=0.1
- momentum=0.9
- wd=5e-4
- epoch=5 (within each epoch, there're 2 objectives: finetuning on whole retain set, and after that, finetuning with modified weights on forget set)
- SGD

Retain set accuracy: 14.2%
Test set accuracy: 15.0%
The MIA has an accuracy of 0.507 on forgotten vs unseen images

### Exp 2
Settings:
- Adam
- lr=0.01
- wd=5e-4
- forget only once (1 epoch) on forget set, then 5 epochs on retain set, same as before

Retain set accuracy: 83.8%
Test set accuracy: 75.1%
The MIA has an accuracy of 0.490 on forgotten vs unseen images

### Exp 3
Settings:
- Adam
- lr=0.001
- wd=5e-4
- Compared to exp 2, only adjust learning rate to 1/10

Retain set accuracy: 99.3%
Test set accuracy: 84.9%
The MIA has an accuracy of 0.507 on forgotten vs unseen images

## Forget by Augmentation Supervision

Core idea:
For samples in forget set, make the model predictions (raw logits should be processed with softmax to get probabilities) close to model predictions of the same images, but augmented. Use MSE loss to optimize for this objective.
Augmentation used: Gaussian blur first to erase some high frequency info, and restore these frequencies with Gaussian noise.
For samples in retain set, keep finetuning.

### Exp 1
Settings:
- Gaussian blur kernel size = 5, sigma = 0.1
- Gaussian noise mean = 0, std = 0.1
- Adam
- lr = 0.001
- wd = 5e-4
- Forget for 1 epoch, finetune for 5 epochs

Retain set accuracy: 98.6%
Test set accuracy: 83.8%
The MIA has an accuracy of 0.506 on forgotten vs unseen images

### Exp 2
Settings:
- Gaussian blur kernel size = 5, sigma = 0.5
- Gaussian noise mean = 0, std = 0.05
- Adam
- lr = 5e-4
- wd = 5e-4
- Just some hyperparam tweaking

Retain set accuracy: 99.5%
Test set accuracy: 85.2%
The MIA has an accuracy of 0.507 on forgotten vs unseen images

This one is good enough on both retain set accuracy and MIA score (overpassing baseline in every way). Generalizability is hurt a little bit. For finetuning maybe introducing data augmentation will help improving generalizability.