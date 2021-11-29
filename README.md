## Introduction
Fast-RCNN implemented on PPDet

## Results
Method|Environment|mAP|Epoch|Dataset
:--:|:--:|:--:|:--:|:--:
r50_fpn_1x_ms_training|**Tesla V-100 x 4**|**37.7**|12|COCO

[The Results of TIPC](https://github.com/FL77N/Fast-RCNN-on-PPDet/tree/main/test_tipc/output)

## Model and Pretrain Model
* The multi scale training best model and train-log are saved to: [Baidu Aistudio](https://aistudio.baidu.com/aistudio/datasetdetail/118142)
* The PrecomputedProposals is saved to: [Baidu Aistudio](https://aistudio.baidu.com/aistudio/datasetdetail/117919)

## Train
* <font color=pink>single gpu</font> 
    
    ```python PaddleDetection/tools/train.py -c PaddleDetection/configs/fast_rcnn/fast_rcnn_r50_fpn_1x_coco.yml --eval```
* <font color=red>mutil gpu</font>
   
   ```python -m paddle.distributed.launch --gpus 0,1,2,3 PaddleDetection/tools/train.py -c PaddleDetection/configs/fast_rcnn/fast_rcnn_r50_fpn_1x_coco.yml --eval```

## Eval

```python tools/eval.py -c PaddleDetection/tools/train.py -c PaddleDetection/configs/fast_rcnn/fast_rcnn_r50_fpn_1x_coco.yml```


## GETTING_STARTED
[The tutorials of TIPC](https://github.com/FL77N/Fast-RCNN-on-PPDet/tree/main/test_tipc/docs)
[More detail about PPDet](https://github.com/PaddlePaddle/PaddleDetection/tree/develop/docs/tutorials)
