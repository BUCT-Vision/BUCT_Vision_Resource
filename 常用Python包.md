# 常用Python包

这里整理了一些深度学习常用的python包，以PyTorch相关工具为主。

## 深度学习框架

### 基础版

- PyTorch [[homepage](https://pytorch.org/)] [[doc](https://pytorch.org/docs/stable/index.html)] [[github](https://github.com/pytorch/pytorch)]
- TensorFlow [[homepage](https://www.pytorchlightning.ai/)] [[doc](https://www.tensorflow.org/tutorials)] [[github](https://github.com/PyTorchLightning/pytorch-lightning)] (我们组内用的不多)

### 进阶版

进阶版通常基于上述基础框架进行二次封装，有针对特定任务更丰富的功能/工具。

- PyTorch Lightning [[homepage](https://www.pytorchlightning.ai/)] [[doc](https://pytorch-lightning.readthedocs.io/en/stable/)] [[github](https://github.com/PyTorchLightning/pytorch-lightning)] (基于PyTorch)

- OpenMMLab系列 [[homepage](https://openmmlab.com/)] (基于PyTorch)

  - MMCV  [[homepage](https://openmmlab.com/)] [[doc](https://mmcv.readthedocs.io/en/latest/)] [[github](https://github.com/open-mmlab/mmcv)] (OpenMM的基础视觉库)
  - MMDetection  [[homepage](https://openmmlab.com/)] [[doc](https://mmdetection.readthedocs.io/en/latest/)] [[github](https://github.com/open-mmlab/mmdetection)] (目标检测)

  - MMSelfSup  [[homepage](https://openmmlab.com/)] [[doc](https://mmselfsup.readthedocs.io/en/latest/)] [[github](https://github.com/open-mmlab/MMSelfSup)] (自监督学习)
  - 更多框架可见[**介绍页**](https://openmmlab.com/codebase): MMRotate, MMDeploy, MMRazor, MMHuman3D, MMFlow, **MMFewShot**, MMAction2, **MMClassification**, **MMSegmentation**, MMDetection3D, MMEditing, MMPose, MMTracking, MMOCR, MMGeneration

- solo-learn [[doc](https://solo-learn.readthedocs.io/en/latest/index.html)] [[github](https://github.com/vturrisi/solo-learn)] (自监督学习, 基于PyTorch Lightning)
- PyG (PyTorch Geometric) [[doc](https://pytorch-geometric.readthedocs.io/en/latest/)] [[github](https://github.com/pyg-team/pytorch_geometric)] (图神经网络)
- DGL (Deep Graph Library) [[doc](https://docs.dgl.ai/index.html)] [[github](https://github.com/dmlc/dgl)] (图神经网络库)

## 训练数据记录

- TensorBoard [[homepage](https://www.tensorflow.org/tensorboard/)] [[doc](https://www.tensorflow.org/tensorboard/get_started)] [[github](https://github.com/tensorflow/tensorboard)]
- wandb [[homepage](https://wandb.ai/site)] [[doc](https://docs.wandb.ai/)] [[github](https://github.com/wandb)] (功能丰富，支持各种可视化及训练管理，但没开源)
- 更多[训练管理工具](https://cloud.tencent.com/developer/article/1935949)

## 模型解释性

- UMAP [[doc](https://umap-learn.readthedocs.io/en/latest/)] [[github](https://github.com/lmcinnes/umap)] (数据降维可视化)
- Captum [[homepage](https://captum.ai/)] [[doc](https://captum.ai/docs/introduction)] [[github](https://github.com/pytorch/captum)]
- MLxtend [[homepage](http://rasbt.github.io/mlxtend/)] [[doc](http://rasbt.github.io/mlxtend/)] [[github](https://github.com/rasbt/mlxtend)]

- SHAP [[homepage](http://rasbt.github.io/mlxtend/)] [[doc](https://shap.readthedocs.io/en/latest/index.html)] [[github](https://github.com/slundberg/shap)]
- grad-cam [[PyPI](https://pypi.org/project/grad-cam/)] [[github](https://github.com/jacobgil/pytorch-grad-cam)] (注意力可视化)
