# X-Decoder: Generalized Decoding for Pixel, Image, and Language

\[[arXiv (comming soon)]()\]    \[[Hugging Face Demo](https://huggingface.co/spaces/xdecoder/Demo)\]    \[[Video](https://youtu.be/wYp6vmyolqE)\]

:sunflower: Try out our Hugging Face Demo!

by [Xueyan Zou*](https://maureenzou.github.io/), [Zi-Yi Dou*](https://zdou0830.github.io/), [Jianwei Yang*](https://jwyang.github.io/),  [Zhe Gan](https://zhegan27.github.io/), [Linjie Li](https://scholar.google.com/citations?user=WR875gYAAAAJ&hl=en), [Chunyuan Li](https://chunyuan.li/), [Xiyang Dai](https://sites.google.com/site/xiyangdai/), [Harkirat Behl](https://harkiratbehl.github.io/), [Jianfeng Wang](https://scholar.google.com/citations?user=vJWEw_8AAAAJ&hl=en), [Lu Yuan](https://scholar.google.com/citations?user=k9TsUVsAAAAJ&hl=en), [Nanyun Peng](https://vnpeng.net/), [Lijuan Wang](https://scholar.google.com/citations?user=cDcWXuIAAAAJ&hl=zh-CN), [Yong Jae Lee^](https://pages.cs.wisc.edu/~yongjaelee/), [Jianfeng Gao^](https://www.microsoft.com/en-us/research/people/jfgao/?from=http%3A%2F%2Fresearch.microsoft.com%2Fen-us%2Fum%2Fpeople%2Fjfgao%2F).

https://user-images.githubusercontent.com/11957155/209029370-c7ed5d08-6d1b-45c6-8433-13e57247be0c.mp4

## :fire: Updates
* **[2022.12.21]** We release inference code of X-Decoder.
* **[2022.12.21]** We release Focal-T pretrained checkpoint.
* **[2022.12.21]** We release open-vocabulary segmentation benchmark.

## :notes: Introduction
X-Decoder is a generalized decoding model that can predict **pixel-level segmentation** and **language tokens** seamlessly. 

**It achieves:**

* SoTA results on open-vocabulary segmentation and referring segmentation on eight datasets; 
* Better or competitive finetuned performance to generalist and specialist models on SEG and VL tasks; 
* Flexibility for efficient finetuning and novel task composition.

**It supports:** 

* Pretrained: Semantic/Instance/Panoptic Segmentation; Referring Segmentation; Image Captioning; Image/Text Retrieval
* Finetuned/Compostion: VQA; Region Retrieval; Referring Captioning; Image Editing


## :snowflake: TODO
- [ ] Release Training and Prompt Tuning code
- [ ] Release Finetuned model
- [ ] Release Base and Large model

## Getting Started

### Installation
```sh
pip3 install torch==1.13.1 torchvision==0.14.1 --extra-index-url https://download.pytorch.org/whl/cu113
python -m pip install 'git+https://github.com/MaureenZOU/detectron2-xyz.git'
pip install git+https://github.com/cocodataset/panopticapi.git
python -m pip install -r requirements.txt
```

To prepare the dataset: [DATASET.md](./DATASET.md)

## Open Vocabulary Segmentation
```sh
mpirun -n 8 python eval.py evaluate --conf_files configs/xdecoder/svlp_focalt_lang.yaml  --overrides WEIGHT /pth/to/ckpt
```
Note: Due to zero-padding, filling a single gpu with multiple images may decrease the performance.

## Inference Demo
```sh
# For Segmentation Tasks
python demo/demo_captioning.py evaluate --conf_files configs/xdecoder/svlp_focalt_lang.yaml  --overrides WEIGHT /pth/to/ckpt
# For VL Tasks
python demo/demo_captioning.py evaluate --conf_files configs/xdecoder/xdecoder_focalt_last_novg.pt  --overrides WEIGHT /pth/to/ckpt
```


## Model Zoo
|           |         | ADE  |      |      | ADE-full | SUN  | SCAN |      | SCAN40 | Cityscape |      |      | BDD  |      |
|-----------|---------|------|------|------|----------|------|------|------|--------|-----------|------|------|------|------|
| model     | ckpt    | PQ   | AP   | mIoU | mIoU     | mIoU | PQ   | mIoU | mIoU   | PQ        | mAP  | mIoU | PQ   | mIoU |
| X-Decoder | [BestSeg Tiny](https://projects4jw.blob.core.windows.net/x-decoder/release/xdecoder_focalt_best_openseg.pt) | 19.1 | 10.1 | 25.1 | 6.2      | 35.7 | 30.3 | 38.4 | 22.4   | 37.7      | 18.5 | 50.2 | 16.9 | 47.6 |
| X-Decoder | [Last Tiny](https://projects4jw.blob.core.windows.net/x-decoder/release/xdecoder_focalt_last.pt) |  |  |  |       |  |  |  |    |       |  |  |  |  |
| X-Decoder | [NoVG Tiny](https://projects4jw.blob.core.windows.net/x-decoder/release/xdecoder_focalt_last_novg.pt) |  |  |  |       |  |  |  |    |       |  |  |  | |


## Acknowledgement
We appreciated the solid codebase of [Mask2Former](https://github.com/facebookresearch/Mask2Former).
