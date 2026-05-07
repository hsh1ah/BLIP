## This repo is DEPRECATED and no longer supported - We recommend that you do not use the content in this repo for any production or sensitive purpose

## BLIP: Bootstrapping Language-Image Pre-training for Unified Vision-Language Understanding and Generation

## Announcement: BLIP is now officially integrated into [LAVIS](https://github.com/salesforce/LAVIS) - a one-stop library for language-and-vision research and applications!

<img src="BLIP.gif" width="700">

This is the PyTorch code of the <a href="https://arxiv.org/abs/2201.12086">BLIP paper</a> [[blog](https://blog.salesforceairesearch.com/blip-bootstrapping-language-image-pretraining/)]. The code has been tested on PyTorch 1.10.
To install the dependencies, run <pre/>pip install -r requirements.txt</pre> 

Catalog:
- [x] Inference demo
- [x] Pre-trained and finetuned checkpoints
- [x] Finetuning code for Image-Text Retrieval, Image Captioning, VQA, and NLVR2
- [x] Pre-training code
- [x] Zero-shot video-text retrieval
- [x] Download of bootstrapped pre-training datasets 


### Inference demo:
Run our interactive demo using [Colab notebook](https://colab.research.google.com/github/salesforce/BLIP/blob/main/demo.ipynb) (no GPU needed).
The demo includes code for: 
1. Image captioning
2. Open-ended visual question answering
3. Multimodal / unimodal feature extraction
4. Image-text matching

Try out the [Web demo](https://huggingface.co/spaces/Salesforce/BLIP), integrated into [Huggingface Spaces 🤗](https://huggingface.co/spaces) using [Gradio](https://github.com/gradio-app/gradio). 

Replicate web demo and Docker image is also available at [![Replicate](https://replicate.com/salesforce/blip/badge)](https://replicate.com/salesforce/blip)

### Pre-trained checkpoints:
Num. pre-train images | BLIP w/ ViT-B | BLIP w/ ViT-B and CapFilt-L | BLIP w/ ViT-L 
--- | :---: | :---: | :---: 
14M | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_base_14M.pth">Download</a>| - | -
129M | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_base.pth">Download</a>| <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_base_capfilt_large.pth">Download</a> | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_large.pth">Download</a>

### Finetuned checkpoints:
Task | BLIP w/ ViT-B | BLIP w/ ViT-B and CapFilt-L | BLIP w/ ViT-L 
--- | :---: | :---: | :---:
Image-Text Retrieval (COCO) | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_base_retrieval_coco.pth">Download</a>| - | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_large_retrieval_coco.pth">Download</a>
Image-Text Retrieval (Flickr30k) | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_base_retrieval_flickr.pth">Download</a>|  - | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_large_retrieval_flickr.pth">Download</a>
Image Captioning (COCO) | - | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_base_caption_capfilt_large.pth">Download</a>| <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_large_caption.pth">Download</a> | 
VQA | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_vqa.pth">Download</a>| <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_base_vqa_capfilt_large.pth">Download</a> | - 
NLVR2 | <a href="https://storage.googleapis.com/sfr-vision-language-research/BLIP/models/model_base_nlvr.pth">Download</a>| - | - 

### Image-Text Retrieval:
1. Download COCO and Flickr30k datasets from the original websites.
2. Download and preprocess the datasets using `preprocess.py` in the `data` folder.
3. Run `python -m torch.distributed.run --nproc_per_node=8 train_retrieval.py`

### Image Captioning:
1. Download COCO datasets from the original websites.
2. Download bootstrapped pre-training dataset using `download_data.py` in the `data` folder.
3. Run `python -m torch.distributed.run --nproc_per_node=8 train_caption.py`

### VQA:
1. Download VQA v2 dataset from the original website.
2. Run `python -m torch.distributed.run --nproc_per_node=8 train_vqa.py`

### NLVR2:
1. Download NLVR2 dataset from the original website.
2. Run `python -m torch.distributed.run --nproc_per_node=8 train_nlvr.py`

### Pre-training:
1. Prepare training data as json files where each json file contains a list of annotations.
2. Run `python -m torch.distributed.run --nproc_per_node=8 train_pretrain.py`

### Zero-shot video-text retrieval:
1. Download a video dataset, e.g., MSVD, MSRVTT, VATEX, etc.
2. Run `python video_retrieval.py`

## Citation
```
@misc{li2022blip,
      title={BLIP: Bootstrapping Language-Image Pre-training for Unified Vision-Language Understanding and Generation}, 
      author={Junnan Li and Dongxu Li and Caiming Xiong and Steven Hoi},
      year={2022},
      eprint={2201.12086},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```

## Acknowledgement
The implementation of BLIP relies on resources from <a href="https://github.com/salesforce/ALBEF">ALBEF</a>, <a href="https://github.com/huggingface/transformers">Huggingface Transformers</a>, and <a href="https://github.com/rwightman/pytorch-image-models/tree/master/timm">timm</a>. We thank the original authors for their open-sourcing.

Related project: [LAVIS](https://github.com/salesforce/LAVIS)