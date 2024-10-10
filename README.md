# GAN-model-extraction-attack
This repository contains the source code for the paper “Towards Model Extraction Attacks in GAN-Based Image Translation via Domain Shift Mitigation” accepted by AAAI 2024 conference.


## Environment Configuration
```
!pip install -r requirements.txt
```

## Description
You can collect training data for the attack model by sending queries to the victim model with the attack data as stated in our paper. In training, you need to construct a dataset that includes trainA and trainB. By default trainA is the attack dataset and trainB is the data returned by the victimization model. Similarly, during testing, you need to construct a dataset that includes testA and testB, containing source and target domain data, respectively.


## How to run the program
If your data is
stored under the path ./train_data, then you can use the following command to train your attack model. You can also name the current run using "your_attack_model_name". For example:

### Pix2Pix
```
python train.py --dataroot ./data --model pix2pix --name attack_model_name
```
### CycleGAN
```
python train.py --dataroot ./data --model cycle_gan --name attack_model_name
```

## How to test

### Pix2Pix
```
python test.py --dataroot ./test_data --model pix2pix --name your_attack_model_name
```
### CycleGAN
```
python test.py --dataroot ./test_data/testA --name your_attack_model_name --model test --no_dropout
```
### Fid and kid score
```
pip install torch-fidelity

fidelity --kid --fid --kid-subset-size 100 --gpu 0 --input1 ./fake_images --input2 ./ture_images
```
### Acknowledgement
This code is implemented based on https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix, https://github.com/ArchipLab-LinfengZhang/wkd-datasets, and https://github.com/google-research/sam. For more details, you can check their GitHub project page.
