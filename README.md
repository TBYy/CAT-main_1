# CAT: Cross Attention in Vision Transformer

This is official implement of ["CAT: Cross Attention in Vision Transformer"](https://arxiv.org/abs/2106.05786).

## Abstract

Since Transformer has found widespread use in NLP, the potential of Transformer in CV has been realized and has inspired many new approaches. However, the computation required for replacing word tokens with image patches for Transformer after the tokenization of the image is vast(e.g., ViT), which bottlenecks model training and inference. In this paper, we propose a new attention mechanism in Transformer termed Cross Attention, which alternates attention inner the image patch instead of the whole image to capture local information and apply attention between image patches which are divided from single-channel feature maps to capture global information. Both operations have less computation than standard self-attention in Transformer. By alternately applying attention inner patch and between patches, we implement cross attention to maintain the performance with lower computational cost and build a hierarchical network called Cross Attention Transformer(CAT) for other vision tasks. Our base model achieves state-of-the-arts on ImageNet-1K, and improves the performance of other methods on COCO and ADE20K, illustrating that our network has the potential to serve as general backbones.

CAT achieves strong performance on COCO object detection(implemented with [mmdectection](https://github.com/open-mmlab/mmdetection)) and ADE20K semantic segmentation(implemented with [mmsegmantation](https://github.com/open-mmlab/mmsegmentation)).

![architecture](figures/architecture.jpg)

**NOTE**: All pretrained-models and logs are released at [releases](https://github.com/linhezheng19/CAT/releases/tag/v1.0).

## Pretrained Models and Results on ImageNet-1K

| name  | resolution |acc@1 | acc@5 | #params | FLOPs | Throughput | model | log |
| :---: | :---: | :---: | :---: | :---: | :---: |:---: |:---: | :---: |
| CAT-T<sup>\*</sup> | 224x224 | 80.3 | 95.0 | 17M | 2.8G | 857 imgs/s | - | - |
| CAT-S<sup>\*</sup> | 224x224 | 81.8 | 95.6 | 37M | 5.9G | 525 imgs/s | - | - |
| CAT-B<sup>\*</sup> | 224x224 | 82.8 | 96.1 | 52M | 8.9G | 384 imgs/s | - | - |
| CAT-T-v2 | 224x224 | 81.7 | 95.5 | 36M | 3.9G | Coming | Coming | Coming|

**Note**: <sup>\*</sup> indicates new version of model and log. Throughput is evaluated on a V100 GPU.

## Models and Results on Object Detection (COCO 2017 val)

| Backbone | Method | pretrain | Lr Schd | box mAP | mask mAP | #params | FLOPs | model | log |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| CAT-S | Mask R-CNN<sup>+</sup> | ImageNet-1K | 1x | 41.6 | 38.6 | 57M | 295G | - | - |
| CAT-B | Mask R-CNN<sup>+</sup> | ImageNet-1K | 1x | 41.8 | 38.7 | 71M | 356G | - | - |
| CAT-S | FCOS | ImageNet-1K | 1x | 40.0 | - | 45M | 245G | - | - |
| CAT-B | FCOS | ImageNet-1K | 1x | 41.0 | - | 59M | 303G | - | - |
| CAT-S | ATSS | ImageNet-1K | 1x | 42.0 | - | 45M | 243G | - | - |
| CAT-B | ATSS | ImageNet-1K | 1x | 42.5 | - | 59M | 303G | - | - |
| CAT-S | RetinaNet | ImageNet-1K | 1x | 40.1 | - | 47M | 276G | - | - |
| CAT-B | RetinaNet | ImageNet-1K | 1x | 41.4 | - | 62M | 337G | - | - |
| CAT-S | Cascade R-CNN | ImageNet-1K | 1x | 44.1 | - | 82M | 270G | - | - |
| CAT-B | Cascade R-CNN | ImageNet-1K | 1x | 44.8 | - | 96M | 330G | - | - |
| CAT-S | Cascade R-CNN<sup>+</sup> | ImageNet-1K | 1x | 45.2 | - | 82M | 270G | - | - |
| CAT-B | Cascade R-CNN<sup>+</sup> | ImageNet-1K | 1x | 46.3 | - | 96M | 330G | - | - |

**Note**: <sup>+</sup> indicates multi-scale training.

## Models and Results on Semantic Segmentation (ADE20K val)

| Backbone | Method | pretrain | Crop Size | Lr Schd | mIoU | mIoU (ms+flip) | #params | FLOPs | model | log |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | 
| CAT-S | Semantic FPN | ImageNet-1K | 512x512 | 80K | 40.6 | 42.1 | 41M | 214G | - | - |
| CAT-B | Semantic FPN | ImageNet-1K | 512x512 | 80K | 42.2 | 43.6 | 55M | 276G | - | - |
| CAT-S | Semantic FPN | ImageNet-1K | 512x512 | 160K | 42.2 | 42.8 | 41M | 214G | - | - |
| CAT-B | Semantic FPN | ImageNet-1K | 512x512 | 160K | 43.2 | 44.9 | 55M | 276G | - | - |

## Citing CAT

You can cite the paper as:
```
@article{lin2021cat,
  title={CAT: Cross Attention in Vision Transformer},
  author={Hezheng Lin and Xing Cheng and Xiangyu Wu and Fan Yang and Dong Shen and Zhongyuan Wang and Qing Song and Wei Yuan},
  journal={arXiv preprint arXiv:2106.05786},
  year={2021}
}
```

## Started

Please refer to [get_started](get_started.md).

## Acknowledgement

Our implementation is mainly based on [Swin](https://github.com/microsoft/Swin-Transformer).
