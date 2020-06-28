# Urban Drone Dataset(UDD)

## 0.Dataset
### 0.1 Dataset Overview
This is a collection of drone image Dataset collected at Peking University, Huludao city, Henan University and Cangzhou city.

*example of UDD：*
![visual_color](img/DJI_0627_visual_color.png)
![visual_mask](img/DJI_0627_visual_mask.png)

**Class Definitions**

- UDD5

|   Class  |Gt Label|   RGB   |Suffix|
|----------|--------|---------|------|
|Vegetation|   0    |(107,142,35)|_t.png|
| Building |   1    |(102,102,156)|_b.png|
|  Road    |   2    |(128,64,128)|_r.png|
|  Vehicle |   3    |(0,0,142)|_v.png|
|  Other   |   4    |(0,0,0) | N/A |

- UDD6 (Released on 28 Jun 2020)

|   Class  |Gt Label|   RGB   |Suffix|
|----------|--------|---------|------|
|  Other   |   0    |(0,0,0) | N/A |
| Building |   1    |(102,102,156)|_b.png|
|  Road    |   2    |(128,64,128)|_r.png|
|Vegetation|   3    |(107,142,35)|_t.png|
|  Vehicle |   4    |(0,0,142)|_v.png|
| **Roof** |   5    |(70,70,70) |_roof.png|


### 0.2 CHANGE LOG

|   Date   |  log   |
|----------|--------|
|2018.03.15| repo init |
|2018.03.23| UDD-3 released |
|2019.11.04| UDD-5 released |
|2020.06.28| UDD-6 released. Beware of the changing Gt Label!! |

now UDD-6 is on air (*Vegetation, Building, Road, Vehicle, Roof and Other*)! See Download Link below.

### 0.3 Download Link

This Dataset is only for non-commercial use. 

- [UDD-6(train, val) + UDD-5(train, val) + UDD-5_tf_Model + PKU-M1(train+val+test)](https://drive.google.com/drive/folders/1x172jM6iF6SZjMB4jH8FVRgiuGcJDtIe?usp=sharing)


## Citation

If you benefit from UDD, please cite our paper:

```
@inproceedings{chen2018large,
  title={Large-scale structure from motion with semantic constraints of aerial images},
  author={Chen, Yu and Wang, Yao and Lu, Peng and Chen, Yisong and Wang, Guoping},
  booktitle={Chinese Conference on Pattern Recognition and Computer Vision (PRCV)},
  pages={347--359},
  year={2018},
  organization={Springer}
}
```


## 1.Labeling Policy (instruction included)
### 1.0 Vegetation
- 1. enter photo shop，press alt+F9 to open Action menu，load action script "ps-annotation.atn"
![selection](img/action.png)
- 2. open the src url, and press CTRL+F2，a raw mask of vegetation would be generated
![selection](img/selection.png)

- 3. adjust the selected area by hand(lasso is recommended, just press shift/alt and drag the mouse)
- 4. then press CTRL+F3 to generate bitmap, save it by "_t.png" suffix，"DJI_0285_t.png",e.g.

*Annotation example*
![vegetation](img/DJI_0285_t.png)

**[Chinese version of annotation instruction](ps-annotation.pdf)**

### 1.1 Building
- 1. new a black layer, using polygon lasso to select building and fill it with black
- 2. press CTRL+F3 to generate bitmap, save it by "_b.png" suffix，"DJI_0285_b.png",e.g.

*example of annotated result*
![Building](img/DJI_0285_b.png)

### 1.2 Other classes
- 1. After filled ROI with black, press CTRL+F3 to generate bitmap. Remember to save it by suffix(see **Class Definitions** above)


## 2. Directory Naming Policy

**/src**  ```origin source image```

**/gt**  ```ground truth```

**/gt_class** ```groundtruth split by classes```

**/ori**  ```annotation raw result(subfolders containing annotated '_t.png', '_b.png', etc. are all here)```

**/visualization** ```visualization result```
```
you can name your directories arbitrarily. Just keep them corresponding to envs in main.m
```


## 3. Scripts

- ### [script/main.m](script/main.m)
Processing with raw annotated result. You can DIY your ground truth label here.

*parameters*：
```
visual_mode = 0; % 1 to run gtVisual.m
visual_resizerate=0.25; % downsample rate to accelerate
split_mode = 1; % 1 to run gtSplit.m
split_visualmode = 0;  % 1 to run visualization.m
```

- ### [script/gtVisual.m (function, called by main.m)](script/gtVisual.m)

To visualize the ground truth map.

- ### [script/gtSplit.m (function, called by main.m)](script/gtSplit.m)

To generate some split map

- ### [script/visualization.m](script/visualization.m)

After running main.m, you can see the visualization result in**/visualization** by running this script.

*parameters*：
```
view_mode = 1; % 0 for automatic, 1 for manual
```

- ### [script/tools/writeTxt.py](script/tools/writeTxt.py)

run this to prepare ```train.txt，val.txt``` for training in [tensorpack](https://github.com/MarcWong/tensorpack).


- ### [script/tools/jpg2png.m](script/tools/jpg2png.m)

Convert JPG to PNG.


## 4. **Acknowledgements**

Sincerely tribute to all companions who contributed to this Dataset: *Xiao Deng(邓枭)*、*Youpeng Gu(顾友鹏)*、*Jianyuan Guo(郭健元)*、*Chen Hou(侯忱)*、*Zhao Jin(金朝)*、*Boning Song(宋博宁)*、*You'er Wen(文佑尔)*、*Yang Yao(姚洋)*、*Kangrui Yi(易康睿)*、*Haotian Zhou(周昊天)*、*Youkun Wu(吴有堃)*、*Xupu Wang(王旭普)*、*Tongwei Zhu(朱彤葳)*、*Zebin Wang(王泽斌)*。
