## Original results

### On original pre-trained model, no modifications:
The MIA has an accuracy of 0.579 on forgotten vs unseen images
Train set accuracy: 99.5%
Test set accuracy: 88.3%

### On forget-by-finetuning model, epoch=5, lr=0.1, momentum=0.9, wd=5e-4, SGD
The MIA has an accuracy of 0.512 on forgotten vs unseen images
Retain set accuracy: 98.3%
Test set accuracy: 84.0%

### On re-trained model:
The MIA has an accuracy of 0.502 on forgotten vs unseen images
Retain set accuracy: 99.5%
Forget set accuracy: 88.2%

## Forget by Neutralizing Forget Labels

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