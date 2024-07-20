# 2D Gaussian Splatting with Localized Point Management

> [**Gaussian Splatting with Localized Points Management**](https://surrey-uplab.github.io/research/LPM/)           
> Haosen Yang*, Chenhao Zhang*, Wenqing Wang, Marco Volino, Adrian Hilton, Li Zhang, Xiatian Zhu  
> **Arxiv preprint**

> [**Gaussian Splatting with Localized Points Management**](https://surrey-uplab.github.io/research/LPM/)           
> Binbin Huang, Zehao Yu, Anpei Chen, Andreas Geiger, Shenghua Gao  
> **SIGGRAPH 2024**


## Get started

### Environment

The hardware and software requirements are the same as those of the [2D Gaussian Splatting](https://github.com/hbb1/2d-gaussian-splatting), which this code is built upon. To setup the environment, please run the following command:

```shell
# Install 2DGS enviroment
git clone https://github.com/Surrey-UP-Lab/X-LPM.git ----recursive
cd 2dgs_lpm
conda env create --file environment.yml
conda activate surfel_splatting
# Install LightGlue enviroment
git clone https://github.com/cvg/LightGlue.git && cd LightGlue
python -m pip install -e .
```
### Data preparation
Please refer the [2D Gaussian Splatting](https://github.com/hbb1/2d-gaussian-splatting)
### Running

After installation and data preparation, you can train  and evaluate the model.
**Training**:
```shell
python train.py -s <dataset path> --eval --m <model path>  \
--densify_from_iter 500 --densify_until_iter 15000 \
--reset_from_iter 500 --reset_until_iter 15000 \
--densification_interval 100 --reset_interval 100 \
--angle 45
```
**Note:** For indoor scenes, we suggest using less frequent resets and a larger neighbor angle, hence setting reset_interval to 200 and angle to 90. For outdoor scenes, use the default settings. You can modify these settings to fit your specific scene needs. For indoor scene, only kitchen set angle to 45.
        
**Evaluation and Mesh Extraction**

All the commands are the same as in 2DGS. Please refer to [2D Gaussian Splatting](https://github.com/hbb1/2d-gaussian-splatting) for details.

## Results on MpiNeRF360
**SSIM**:  
| Method        | Bicycle | Flowers | Garden | Stump | Treehill | avg      | Room  | Counter | Kitchen | Bonsai | avg      |
|---------------|---------|---------|--------|-------|----------|----------|-------|---------|---------|--------|----------|
| 2D-GS         | 0.733   | 0.575   | 0.843  | 0.756 | 0.619    | 0.7052   | 0.906 | 0.892   | 0.917   | 0.93   | 0.91125  |
| 2D-GS w/LPM   | 0.761   | 0.592   | 0.856  | 0.771 | 0.601    | 0.7162   | 0.915 | 0.904   | 0.924   | 0.935  | 0.9195   |

**PSNR** :
| Method        | Bicycle | Flowers | Garden | Stump | Treehill | avg      | Room  | Counter | Kitchen | Bonsai | avg      |
|---------------|---------|---------|--------|-------|----------|----------|-------|---------|---------|--------|----------|
| 2D-GS         | 24.743  | 21.131  | 26.708 | 26.15 | 22.347   | 24.2158  | 30.763| 28.114  | 30.316  | 31.229 | 30.1055  |
| 2D-GS w/LPM   | 25.073  | 21.349  | 26.915 | 26.401| 22.397   | 24.427   | 31.093| 28.451  | 30.612  | 31.573 | 30.43225 |

**LPIPS**:

| Method        | Bicycle | Flowers | Garden | Stump | Treehill | avg      | Room  | Counter | Kitchen | Bonsai | avg      |
|---------------|---------|---------|--------|-------|----------|----------|-------|---------|---------|--------|----------|
| 2D-GS         | 0.266   | 0.373   | 0.144  | 0.257 | 0.372    | 0.2824   | 0.243 | 0.229   | 0.146   | 0.227  | 0.21125  |
| 2D-GS w/LPM   | 0.22    | 0.349   | 0.121  | 0.24  | 0.392    | 0.2644   | 0.22  | 0.207   | 0.132   | 0.215  | 0.1935   |

## 📜 Reference
```bibtex
@article{yang2024localized,
  title={Localized Gaussian Point Management},
  author={Yang, Haosen and Zhang, Chenhao and Wang, Wenqing and Volino, Marco and Hilton, Adrian and Zhang, Li and Zhu, Xiatian},
  journal={arXiv preprint arXiv:2406.04251},
  year={2024}
}

@inproceedings{huang20242d,
  title={2d gaussian splatting for geometrically accurate radiance fields},
  author={Huang, Binbin and Yu, Zehao and Chen, Anpei and Geiger, Andreas and Gao, Shenghua},
  booktitle={ACM SIGGRAPH 2024 Conference Papers},
  pages={1--11},
  year={2024}
}
```
