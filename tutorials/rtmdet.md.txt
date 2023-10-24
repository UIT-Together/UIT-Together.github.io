Hồ Chí Minh, 16-08-2023
[Trần Nguyễn Chí Huy], [Võ Duy Nguyên](https://nguyenvd-uit.github.io/), [UIT-Together Research Group](https://uit-together.github.io/) 
# RTMDet
## Mục Lục
[TOC]

## Step 1. Cài đặt môi trường 
### Step 1.1. Tạo môi trường anaconda
 
 Đặt tên theo cú pháp: Ten_viet tat cua ho va chu lot

VD: Tran Nguyen Chi Huy -> Huytnc
```gherkin=
conda create --name Huytnc python=3.8 -y
```

![](https://hackmd.io/_uploads/r1kjnf5n3.png)


### Step 1.2. Kích hoạt môi trường vừa tạo
```gherkin=
conda activate Huytnc
```
![](https://hackmd.io/_uploads/HyD1aM5hh.png)

### Step 1.3. Cài đặt PyTorch trên GPU platforms
```gherkin=
conda install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cudatoolkit=11.3 -c pytorch
```
![](https://hackmd.io/_uploads/BJvghC_jh.png)

## Step 2. Cài đặt MMEngine và MMCV sử dụng MIM
```gherkin=
pip install -U openmim
mim install mmengine
mim install "mmcv>=2.0.0,<2.1.0"
```
Hình ảnh cài đặt thành công openmim
![](https://hackmd.io/_uploads/BJKJAC_i3.png)

Hình ảnh cài đặt thành công MMEngine
![](https://hackmd.io/_uploads/B1_Q0COin.png)

Hình ảnh cài đặt thành công MMCV
![](https://hackmd.io/_uploads/ryT40Cujh.png)


## Step 3. Thao tác với MMDetection
Truy cập vào thư mục luutru 
VD: /home/u2301/luutru/
```gherkin=
cd luutru/
```
Tạo thư mục tương ứng với tên môi trường bên trên
![](https://hackmd.io/_uploads/SkGITz533.png)

```gherkin=
cd Huytnc/
```

### Step 3.1. Cài đặt MMDetection
Tại thư mục này thực hiện clone và cài đặt mmdetection
```gherkin=
git clone https://github.com/open-mmlab/mmdetection.git
cd mmdetection
pip install -v -e .
```
Hình ảnh clone thành công
![](https://hackmd.io/_uploads/rJHLxeKjn.png)
![](https://hackmd.io/_uploads/H1o5aMq22.png)



### Step 3.2. Tạo thư mục checkpoints và tải file config  
Tạo thư mục checkpoints
```gherkin=
mkdir ./checkpoints
```
![](https://hackmd.io/_uploads/ryuC0zqnn.png)

Tải checkpoints của file config rtmdet_tiny_8xb32-300e_coco
```gherkin=
mim download mmdet --config rtmdet_tiny_8xb32-300e_coco --dest ./checkpoints
```
Hình ảnh tải thành công file config và checkpoints
![](https://hackmd.io/_uploads/B1aviz93h.png)
![](https://hackmd.io/_uploads/SyM6JXc32.png)


## Verify the installation
**Chọn GPU**
Chọn GPU bằng lệnh:
```gherkin=
CUDA_VISIBLE_DEVICES=0
```
**Verify the inference demo**

```gherkin=
python demo/image_demo.py demo/demo.jpg checkpoints/rtmdet_tiny_8xb32-300e_coco.py --weights checkpoints/rtmdet_tiny_8xb32-300e_coco_20220902_112414-78e30dcc.pth --device cuda:0
```

Kết quả được lưu trong thư mục outputs/vis
Vd: /home/u2301/luutru/Huytnc/mmdetection/outputs/vis/

![](https://hackmd.io/_uploads/Hydk7S932.png)



Tạo thư mục data trong thư mục mmdetection để chứa shortcut dẫn tới thư mục MS-COCO

![](https://hackmd.io/_uploads/H1CD4gFj3.png)


Sử dụng chung thư mục MS-COCO nên chúng ta sẽ tạo 1 shortcut dẫn tới thư mục MS-COCO dùng chung bằng lệnh:
ln -s /duong dan toi thu muc goc /duong dan toi thu muc luu shortcut

```gherkin=
ln -s /home/u2301/luutru/coco/ /home/u2301/luutru/Huytnc/mmdetection/data/
```

![](https://hackmd.io/_uploads/SyQwaH93h.png)


**Test với dữ liệu MS-COCO**
```gherkin=
python tools/test.py \
    configs/rtmdet/rtmdet_tiny_8xb32-300e_coco.py \
    checkpoints/rtmdet_tiny_8xb32-300e_coco_20220902_112414-78e30dcc.pth \
    --show
```
Nhấn tổ hợp Ctrl+C để dừng visualized. Màn hình hiện như bên dưới thì dừng thành công:
![](https://hackmd.io/_uploads/HJok6bon2.png)

```gherkin=
python tools/test.py \
    configs/rtmdet/rtmdet_tiny_8xb32-300e_coco.py \
    checkpoints/rtmdet_tiny_8xb32-300e_coco_20220902_112414-78e30dcc.pth \
    --show-dir faster_rcnn_r50_fpn_1x_results
```
## Train with customized dataset
### Chuẩn bị dataset
Ở đây mình dùng dataset visDrone đã được cài đặt sẵn, nên chỉ cần tạo 1 shortcut dẫn tới thư mục visDrone dùng chung bằng lệnh:
```gherkin=
ln -s /home/cvpr2023/LuuTru/dataset/VisDrone/cocoVisdrone/ /home/u2301/luutru/Huytnc/mmdetection/data/
```
### Convert sang COCO format
Vì visDrone đã có COCO format nên không cần convert.

### Prepare a config
Tạo 1 file tên Prepare_Config.py
![](https://hackmd.io/_uploads/r1ZbXO932.png)
với nội dung như bên dưới:
```gherkin=
config_drone = """
# Inherit and overwrite part of the config based on this config
_base_ = './rtmdet_tiny_8xb32-300e_coco.py'

data_root = '/home/cvpr2023/LuuTru/dataset/VisDrone/cocoVisdrone/' # dataset root

train_batch_size_per_gpu = 4
train_num_workers = 2

max_epochs = 1 # so luong epoch can train
stage2_num_epochs = 1
base_lr = 0.00008


metainfo = {
    'classes': ( 'pedestrian','people','bicycle','car','van','truck','tricycle','awning-tricycle','bus','motor'), # so classes cua dataset
    'palette': [
        (220, 20, 60),
        (220, 0, 60),
        (220, 20, 0),
        (220, 20, 60),
        (220, 20, 60),
        (220, 20, 60),
        (220, 0, 60),
        (220, 20, 0),
        (220, 20, 60),
        (220, 20, 60),
    ]
}

train_dataloader = dict(
    batch_size=train_batch_size_per_gpu,
    num_workers=train_num_workers,
    dataset=dict(
        data_root=data_root,
        metainfo=metainfo,
        data_prefix=dict(img='train/'),
        ann_file='annotations/train.json'))

val_dataloader = dict(
    dataset=dict(
        data_root=data_root,
        metainfo=metainfo,
        data_prefix=dict(img='test/'),
        ann_file='annotations/test.json'))

test_dataloader = val_dataloader

val_evaluator = dict(ann_file=data_root + 'annotations/test.json')

test_evaluator = val_evaluator

model = dict(bbox_head=dict(num_classes=10)) # thay doi so classes phu hop

# learning rate
param_scheduler = [
    dict(
        type='LinearLR',
        start_factor=1.0e-5,
        by_epoch=False,
        begin=0,
        end=10),
    dict(
        # use cosine lr from 10 to 20 epoch
        type='CosineAnnealingLR',
        eta_min=base_lr * 0.05,
        begin=max_epochs // 2,
        end=max_epochs,
        T_max=max_epochs // 2,
        by_epoch=True,
        convert_to_iter_based=True),
]

train_pipeline_stage2 = [
    dict(type='LoadImageFromFile', backend_args=None),
    dict(type='LoadAnnotations', with_bbox=True),
    dict(
        type='RandomResize',
        scale=(640, 640),
        ratio_range=(0.1, 2.0),
        keep_ratio=True),
    dict(type='RandomCrop', crop_size=(640, 640)),
    dict(type='YOLOXHSVRandomAug'),
    dict(type='RandomFlip', prob=0.5),
    dict(type='Pad', size=(640, 640), pad_val=dict(img=(114, 114, 114))),
    dict(type='PackDetInputs')
]

# optimizer
optim_wrapper = dict(
    _delete_=True,
    type='OptimWrapper',
    optimizer=dict(type='AdamW', lr=base_lr, weight_decay=0.05),
    paramwise_cfg=dict(
        norm_decay_mult=0, bias_decay_mult=0, bypass_duplicate=True))

default_hooks = dict(
    checkpoint=dict(
        interval=5,
        max_keep_ckpts=2,  # only keep latest 2 checkpoints
        save_best='auto'
    ),
    logger=dict(type='LoggerHook', interval=5))

custom_hooks = [
    dict(
        type='PipelineSwitchHook',
        switch_epoch=max_epochs - stage2_num_epochs,
        switch_pipeline=train_pipeline_stage2)
]

# load COCO pre-trained weight
load_from = './checkpoints/rtmdet_tiny_8xb32-300e_coco_20220902_112414-78e30dcc.pth'

train_cfg = dict(type='EpochBasedTrainLoop', max_epochs=max_epochs, val_interval=1)

"""

with open('./configs/rtmdet/rtmdet_tiny_1xb4-1e_drone.py', 'w') as f:
    f.write(config_drone)
```
Sau đó chạy lệnh:
```gherkin=
python "/home/u2301/luutru/Huytnc/mmdetection/Prepare_Config.py"
```
Bắt đầu train với lệnh:
```gherkin=
python tools/train.py configs/rtmdet/rtmdet_tiny_1xb4-1e_drone.py
```
Sau khi train xong, chúng ta có thể tính toán điểm mAP từng class bằng cách chạy câu lệnh:
```gherkin=
./tools/dist_test.sh \
    configs/rtmdet/rtmdet_tiny_1xb4-1e_drone.py\
    work_dirs/rtmdet_tiny_1xb4-1e_drone/best_coco_bbox_mAP_epoch_1.pth \
    1 \
    --out results.pkl \
    --cfg-options test_evaluator.classwise=True
```
Bên dưới là điểm mAP từng class.
![](https://hackmd.io/_uploads/SkMdy3j2n.png)

Tiếp theo sẽ đến với phần visualize kết quả.

### Visualize kết quả sau khi train
#### Visualize nhiều ảnh:
Chạy câu lệnh:
```gherkin=
python tools/test.py \
    configs/rtmdet/rtmdet_tiny_1xb4-1e_drone.py \
    work_dirs/rtmdet_tiny_1xb4-1e_drone/best_coco_bbox_mAP_epoch_1.pth \
    --show-dir rtmdet_tiny_1xb4-1e_drone_results
```
Sau khi chạy, thư mục các ảnh kết quả sẽ nằm trong thư mục work_dirs.
#### Visualize 1 ảnh:
Tạo file Demo_Detec.py 
![](https://hackmd.io/_uploads/BkdLSO922.png)

với nội dung:
```gherkin=
from mmdet.apis import DetInferencer
import glob

# Change to use a config
config = '/home/u2301/luutru/Huytnc/mmdetection/configs/rtmdet/rtmdet_tiny_1xb4-1e_drone.py'

# Setup a checkpoint file to load
checkpoint = glob.glob('/home/u2301/luutru/Huytnc/mmdetection/work_dirs/rtmdet_tiny_1xb4-1e_drone/best_coco_bbox_mAP_epoch_1.pth')[0]

# Set the device to be used for evaluation
device = 'cuda:0'

# Initialize the DetInferencer
inferencer = DetInferencer(config, checkpoint, device)

# Co the dung img khac trong thu muc test
img = '/home/cvpr2023/LuuTru/dataset/VisDrone/cocoVisdrone/test/0000074_08202_d_0000016.jpg'
result = inferencer(img, out_dir='./outputs')
```
Chạy lệnh dưới để visualize:
```gherkin=
python "/home/u2301/luutru/Huytnc/mmdetection/Demo_Detec.py"
```
Kết quả sau khi chạy sẽ được lưu trong thư mục outputs.
![](https://hackmd.io/_uploads/HyLBjZjh3.png)


 Tài liệu hướng dẫn dùng cho nhóm [UIT-Together Research Group](https://uit-together.github.io/) 
 