# How to prepare data

Create a directory to store reid datasets under this repo via
```bash
cd deep-person-reid/
mkdir data/
```

Note that
- if you wanna store datasets in another directory, you need to specify `--root path_to_your/data` when running the training code.
- please follow the instructions below to prepare each dataset. After that, you can simply give the corresponding keys to the training scripts to use the datasets, e.g. `-s market1501` (use Market1501 as the training dataset).

- please use the suggested names for the dataset folders, otherwise you have to modify the `dataset_dir` attribute in the specific `dataset.py` file in `torchreid/datasets/` accordingly.
- if you find any errors/bugs, please report in the Issues section.
- in the following, we assume that the path to the dataset directory is `data/`.

## Image ReID

**Market1501**:
1. Download the dataset to `data/` from http://www.liangzheng.org/Project/project_reid.html.
2. Extract the file and rename it to `market1501`. The data structure should look like:
```
market1501/
    bounding_box_test/
    bounding_box_train/
    ...
```
3. Use `market1501` as the key to load Market1501.

**CUHK03**:
1. Create a folder named `cuhk03/` under `data/`.
2. Download the dataset to `data/cuhk03/` from http://www.ee.cuhk.edu.hk/~xgwang/CUHK_identification.html and extract `cuhk03_release.zip`, so you will have `data/cuhk03/cuhk03_release`.
3. Download the new split (767/700) from [person-re-ranking](https://github.com/zhunzhong07/person-re-ranking/tree/master/evaluation/data/CUHK03). What you need are `cuhk03_new_protocol_config_detected.mat` and `cuhk03_new_protocol_config_labeled.mat`; put these two mat files under `data/cuhk03`. Finally, the data structure should look like
```
cuhk03/
    cuhk03_release/
    cuhk03_new_protocol_config_detected.mat
    cuhk03_new_protocol_config_labeled.mat
    ...
```
4. Use `cuhk03` as the dataset key. In the default mode, we load data using the new split (767/700). If you wanna use the original (20) splits (1367/100), please specify with `--cuhk03-classic-split`. As the CMC is computed differently from Market1501 for the 1367/100 split (see [here](http://www.ee.cuhk.edu.hk/~xgwang/CUHK_identification.html)), you need to specify `--use-metric-cuhk03` to activate the corresponding metric for fair comparison with some methods that adopt the original splits. In addition, we support both `labeled` and `detected` modes. The default mode loads `detected` images. Specify `--cuhk03-labeled` if you wanna train and test on `labeled` images.


**DukeMTMC-reID**:
1. The process is automated so you can simply do `-s dukemtmcreid -t dukemtmcreid`. The final folder structure looks like
```
dukemtmc-reid/
    DukeMTMC-reid.zip # (you can delete this zip file, it is ok)
    DukeMTMC-reid/
```


**MSMT17**:
1. Create a directory named `msmt17/` under `data/`.
2. Download the dataset `MSMT17_V1.tar.gz` from http://www.pkuvmc.com/publications/msmt17.html to `data/msmt17/`. Extract the file under the same folder, so you will have
```
msmt17/
    MSMT17_V1.tar.gz # (do whatever you want with this .tar file)
    MSMT17_V1/
        train/
        test/
        list_train.txt
        ... (totally six .txt files)
```
3. Use `msmt17` as the key for this dataset.

**VIPeR**:
1. The code supports automatic download and formatting. Just use `-s viper -t viper`. The final data structure would look like:
```
viper/
    VIPeR/
    VIPeR.v1.0.zip # useless
    splits.json
```

**GRID**:
1. The code supports automatic download and formatting. Just use `-s grid -t grid`. The final data structure would look like:
```
grid/
    underground_reid/
    underground_reid.zip # useless
    splits.json
```

**CUHK01**:
1. Create `cuhk01/` under `data/`.
2. Download `CUHK01.zip` from http://www.ee.cuhk.edu.hk/~xgwang/CUHK_identification.html and place it in `cuhk01/`.
3. Do `-s cuhk01 -t cuhk01` to use the data.


**PRID450S**:
1. The code supports automatic download and formatting. Just use `-s prid450s -t prid450s`. The final data structure would look like:
```
prid450s/
    cam_a/
    cam_b/
    readme.txt
    splits.json
```


**SenseReID**:
1. Create `sensereid/` under `data/`.
2. Download the dataset from this [link](https://drive.google.com/file/d/0B56OfSrVI8hubVJLTzkwV2VaOWM/view) and extract to `sensereid/`. The final folder structure should look like
```
sensereid/
    SenseReID/
        test_probe/
        test_gallery/
```
3. The command for using SenseReID is `-t sensereid`. Note that SenseReID is for test purpose only so training images are unavailable. Please use `--evaluate` along with `-t sensereid`.


## Video ReID

**MARS**:
1. Create a directory named `mars/` under `data/`.
2. Download the dataset to `data/mars/` from http://www.liangzheng.com.cn/Project/project_mars.html.
3. Extract `bbox_train.zip` and `bbox_test.zip`.
4. Download the split metadata from https://github.com/liangzheng06/MARS-evaluation/tree/master/info and put `info/` in `data/mars` (we want to follow the standard split). The data structure should look like:
```
mars/
    bbox_test/
    bbox_train/
    info/
```
5. Use `mars` as the dataset key.

**iLIDS-VID**:
1. The code supports automatic download and formatting. Simple use `-s ilidsvid -t ilidsvid`. The data structure would look like:
```
ilids-vid/
    i-LIDS-VID/
    train-test people splits/
    splits.json
```

**PRID**:
1. Under `data/`, do `mkdir prid2011` to create a directory.
2. Download the dataset from https://www.tugraz.at/institute/icg/research/team-bischof/lrs/downloads/PRID11/ and extract it under `data/prid2011`.
3. Download the split created by [iLIDS-VID](http://www.eecs.qmul.ac.uk/~xiatian/downloads_qmul_iLIDS-VID_ReID_dataset.html) from [here](http://www.eecs.qmul.ac.uk/~kz303/deep-person-reid/datasets/prid2011/splits_prid2011.json), and put it under `data/prid2011/`. Note that only 178 persons whose sequences are more than a threshold are used so that results on this dataset can be fairly compared with other approaches. The data structure would look like:
```
prid2011/
    splits_prid2011.json
    prid_2011/
        multi_shot/
        single_shot/
        readme.txt
```
4. Use `-s prid2011 -t prid2011` when running the training code.

**DukeMTMC-VideoReID**:
1. Use `-s dukemtmcvidreid -t dukemtmcvidreid` directly.
2. If you wanna download the dataset manually, get `DukeMTMC-VideoReID.zip` from https://github.com/Yu-Wu/DukeMTMC-VideoReID. Unzip the file to `data/dukemtmc-vidreid`. Ultimately, you need to have
```
dukemtmc-vidreid/
    DukeMTMC-VideoReID/
        train/ # essential
        query/ # essential
        gallery/ # essential
        ... (and license files)
```


# Dataset loaders
These are implemented in `dataset_loader.py` where we have two main classes that subclass [torch.utils.data.Dataset](http://pytorch.org/docs/master/_modules/torch/utils/data/dataset.html#Dataset):
* [ImageDataset](https://github.com/KaiyangZhou/deep-person-reid/blob/master/dataset_loader.py#L22): processes image-based person reid datasets.
* [VideoDataset](https://github.com/KaiyangZhou/deep-person-reid/blob/master/dataset_loader.py#L38): processes video-based person reid datasets.

These two classes are used for [torch.utils.data.DataLoader](http://pytorch.org/docs/master/_modules/torch/utils/data/dataloader.html#DataLoader) that can provide batched data. The data loader wich `ImageDataset` will output batch data of size `(batch, channel, height, width)`, while the data loader with `VideoDataset` will output batch data of size `(batch, sequence, channel, height, width)`.


# Evaluation
## Image ReID
- **Market1501**, **DukeMTMC-reID**, **CUHK03 (767/700 split)** and **MSMT17** have fixed split so keeping `split_id=0` is fine.
- **CUHK03 (classic split)** has 20 fixed splits, so do `split_id=0~19`.
- **VIPeR** contains 632 identities each with 2 images under two camera views. Evaluation should be done for 10 random splits. Each split randomly divides 632 identities to 316 train ids (632 images) and the other 316 test ids (632 images). Note that, in each random split, there are two sub-splits, one using camera-A as query and camera-B as gallery while the other one using camera-B as query and camera-A as gallery. Thus, there are totally 20 splits generated with `split_id` starting from 0 to 19. Models can be trained on `split_id=[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]` (because `split_id=0` and `split_id=1` share the same train set, and so on and so forth.). At test time, models trained on `split_id=0` can be directly evaluated on `split_id=1`, models trained on `split_id=2` can be directly evaluated on `split_id=3`, and so on and so forth.
- **CUHK01** is similar to VIPeR in the split generation.
- **GRID** and **PRID450S** have 10 random splits, so evaluation should be done by varying `split_id` from 0 to 9.
- **SenseReID** has no training images and is used for evaluation only.

## Video ReID
- **MARS** and **DukeMTMC-VideoReID** have fixed single split so using `-s dataset_name -t dataset_name` and `split_id=0` is ok.
- **iLIDS-VID** and **PRID2011** have 10 predefined splits so evaluation should be done by varying `split_id` from 0 to 9.