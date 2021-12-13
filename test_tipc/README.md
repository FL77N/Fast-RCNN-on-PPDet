
# 飞桨训推一体认证

## 1. 简介

飞桨除了基本的模型训练和预测，还提供了支持多端多平台的高性能推理部署工具。
本文档提供了 Fast-RCNN 的飞桨训推一体认证 (Training and Inference Pipeline Certification(TIPC)) 信息和测试工具，
方便用户查阅每种模型的训练推理部署打通情况，并可以进行一键测试。


## 2. 汇总信息

已填写的部分表示可以使用本工具进行一键测试，未填写的表示正在支持中。

**字段说明：**
- 基础训练预测：包括模型训练、Paddle Inference Python预测。
- 更多训练方式：包括多机多卡、混合精度。

| 算法论文 | 模型名称 | 模型类型 | 基础<br>训练预测 | 更多<br>训练方式 | 模型压缩 |  其他预测部署  |
| :--- | :--- | :----: | :--------: | :---- | :---- | :---- |
| [Fast-RCNN](https://arxiv.org/abs/1504.08083) | [fast_rcnn_r50_fpn_1x_coco](../configs/fast_rcnn) | 目标检测  | 支持 | 混合精度 | - | -  |


## 3. 测试工具简介
### 目录介绍

```shell
test_tipc/
├── configs/                              # 配置文件目录
│   ├── fast_rcnn_r50_fpn_1x_coco.txt      
│   ├── ...
├── docs/                                 # 相关说明文档目录
│   ├── install.md                        # 环境准备及 TensorRT 安装
│   ├── test_train_inference_python.md    # 依赖安装以及快速指引
├── output/                               # 训推测中的 log 及模型保存
│   ├── results.log
│   ├── ...
├── weights/                              # 预训练和最优权重
│   ├── xxx.pdparams
│   ├── ...
├── prepare.sh                            # 完成 test_*.sh 运行所需要的数据和模型下载
├── README.md                             # 使用文档
├── test_train_inference_python.sh        # 测试 python 训练预测的主程序
├── compare_results.py                    # 用于对比 log 中的预测结果与 results 中的预存结果精度误差是否在限定范围内

```

### 测试流程概述

1. 运行prepare.sh准备测试所需数据和模型；
2. 运行要测试的功能对应的测试脚本`test_*.sh`，产出 log，由 log 可以看到不同配置是否运行成功；

测试单项功能仅需两行命令，**如需测试不同模型/功能，替换配置文件即可**，命令格式如下：
```shell
# 功能：准备数据
# 格式：bash + 运行脚本 + 参数1: 配置文件选择 + 参数2: 模式选择
bash test_tipc/prepare.sh  configs/[model_name]/[params_file_name]  [Mode]

# 功能：运行测试
# 格式：bash + 运行脚本 + 参数1: 配置文件选择 + 参数2: 模式选择
bash test_tipc/test_train_inference_python.sh configs/[model_name]/[params_file_name]  [Mode]
```

例如，测试基本训练预测功能的`lite_train_infer`模式，运行：
```shell
# 准备数据
bash test_tipc2/prepare.sh ./test_tipc2/configs/fast_rcnn_r50_fpn_1x_coco.txt 'lite_train_infer'
# 运行测试
bash test_tipc2/test_train_inference_python.sh ./test_tipc2/configs/fast_rcnn_r50_fpn_1x_coco.txt 'lite_train_infer'
```
关于本示例命令的更多信息可查看[基础训练预测使用文档](docs/test_train_inference_python.md)。

## 4. 开始测试
各功能测试中涉及混合精度、裁剪、量化等训练相关，及 mkldnn、Tensorrt 等多种预测相关参数配置，请点击下方相应链接了解更多细节和使用教程：  
- [test_train_inference_python 使用](docs/test_train_inference_python.md) ：测试基于 Python 的模型训练、评估、推理等基本功能，包括裁剪、量化、蒸馏。
