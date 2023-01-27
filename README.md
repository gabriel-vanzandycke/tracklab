# PbTrack

Work in progress

## Installation guide[^1]

[^1]: Tested on `conda 22.11.1`, `Python 3.10.8`, `pip 22.3.1`, `g++ 11.3.0` and `gcc 11.3.0`

### Clone the repository

```bash
git clone https://github.com/PbTrack/pb-track.git --recurse-submodules
cd pb-track
```

If you cloned the repo without using the `--recurse-submodules` option, you can still download the submodules with :

```bash
git submodule update --init --recursive
```

### Manage the environment

#### Create and activate a new environment

```bash
conda create -y --name "pbtrack" python pip numpy
conda activate pbtrack
```

#### Install the dependencies
Get into your repo and install the requirements with :

```bash
pip install -r requirements.txt
```

#### Setup reid

```bash
cd plugins/reid/bpbreid/
python setup.py develop
```

### External dependencies

- Get the **PoseTrack21** dataset [here](https://github.com/anDoer/PoseTrack21/tree/35bd7033ec4e1a352ae39b9522df5a683f83781b#how-to-get-the-dataset).
- Get the pretrained weights of **BPBReID** [here](https://github.com/VlSomers/bpbreid#download-the-pre-trained-models).


### Quick (dirty?) install guide for inference
1. Follow above instruction for setting up the environment
2. Download the pretrained weights of OpenPifPaf and BPBreID on [Google Drive](https://drive.google.com/drive/folders/1ZLKYpWIFPOw0-op0dNVP1Csw3CjKr-1B?usp=share_link)
3. Update configs to point to the downloaded weights:
4. 'configs/reid/bpbreid.yaml' -> load_weights: "/path/to/job-35493841_85mAP_95r1_ta_model.pth.tar"
4. 'configs/reid/bpbreid.yaml' -> hrnet_pretrained_path: "/path/to/weights/folder" # /!\ just put the folder name in which the weights 'hrnetv2_w32_imagenet_pretrained.pth' are stored, not the filename
5. 'configs/detect/openpifpaf.yaml' -> checkpoint: "/path/to/shufflenetv2k30_dense_default_wo_augm.f07de325"
6. Update config to point to your inference video: in 'configs/config.yaml', remplace '  - dataset: posetrack21'  (line 8) with '  - dataset: external_video'
7. In 'configs/dataset/external_video.yaml', update the path to your video file (under 'video_path')
8. Finally, execute 'python main.py' to run the inference on the video file 'test.mp4'