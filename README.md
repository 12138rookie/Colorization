#  Colorization


---

## Installation
### Core dependencies
* CUDA >= 10.0 (test on 10.0, 10.2, and 11.1)
* gcc >= 7.3
* pytorch >= 1.6 (test on 1.6, 1.7.1, and 1.9.0)
* python3 (test on 3.8)
* yacs

### Install DCN package (only required by torchvision < 0.9.0)
```shell
# you can skip this step if you are using torchvision >= 0.9.0
cd ops
python setup.py develop
```

## Inference
### Test in the wild images
1. Predict ImageNet label (0-999) for these images
   1. install awesome timm, `pip install timm`
   2. use a SOTA classification model from timm to predict the labels
      ```shell
      python predict_imagenet_label.py test --model beit_large_patch16_512 --pretrained
      ```
      here `testcase_in_the_wild` folder has the images you want to test
   3. you will get the label map in `assets/predicted_label_for_user_image.txt`

2. Inference colorization
    ```shell
    python main.py --expname inference_test --test_folder test DATA.FULL_RES_OUTPUT True
    ```
    ```Console
    options:
        --expname: the results will be saved in results/{expname}-{time} folder
        --inference_in_the_wild: contains the images you want to test
        --bs: batch size
        DATA.FULL_RES_OUTPUT: True or False. If set to True
                              the full resolution results will be saved in results/{expname}-{time}/full_resolution_results
                              batch size should be 1 if this flag is set to True
        DATA.CENTER_CROP: whether to center crop the input images.
                          This flag and DATA.FULL_RES_OUTPUT flag can not be both set to True
    ```
