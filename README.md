# interaction-aware_factorization_machine(https://arxiv.org/abs/1902.09757)

This is our implementation for the paper(https://arxiv.org/abs/1902.09757) based on
[Attentional Factorization Machines](https://github.com/hexiangnan/attentional_factorization_machine)

**Please cite our AAAI'19 paper if you use our codes. Thanks!**

The usage of IFM is similar to AFM.

## Environments
* Tensorflow (version: 1.0.1)
* numpy
* sklearn
## Dataset
We use the same input format as the LibFM toolkit (http://www.libfm.org/). In this instruction, we use [MovieLens](grouplens.org/datasets/movielens/latest).
The MovieLens data has been used for personalized tag recommendation, which contains 668,953 tag applications of users on movies. We convert each tag application (user ID, movie ID and tag) to a feature vector using one-hot encoding and obtain 90,445 binary features. The following examples are based on this dataset and it will be referred as ***ml-tag*** wherever in the files' name or inside the code.
When the dataset is ready, the current directory should be like this:
* code
    - IFM.py
    - FM.py
    - LoadData.py
* data
    - ml-tag
        - ml-tag.train.libfm
        - ml-tag.validation.libfm
        - ml-tag.test.libfm

## Quick Example with Optimal parameters
Use the following command to train the model with the optimal parameters:
```
# step into the code folder
cd code
# train FM model and save as pretrain file
python FM.py --dataset ml-tag --epoch 100 --pretrain -1 --batch_size 4096 --hidden_factor 256 --lr 0.01 --keep 0.3
# train IFM model using the pretrained weights from FM
python IFM.py --dataset ml-tag --epoch 100 --pretrain 1 --batch_size 4096 --hidden_factor [8,256] --keep [1.0,0.9] --temp 10 --lr 0.1 --lamda_attention1 0.01
```
The instruction of commands has been clearly stated in the codes (see the parse_args function).

The current implementation supports regression classification, which optimizes RMSE.
