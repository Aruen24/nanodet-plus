# nanodet-plus
```shell
训练如果报错：KeyError: 'Non-existent config key: model.weight_averager'
执行python setup.py develop 然后再训练
```

## train
```shell
CUDA_VISIBLE_DEVICES=0 python tools/train.py config/nanodet-plus-m_416_stop_line.yml
```

## test
```shell
CUDA_VISIBLE_DEVICES=0 python demo/demo.py image --config config/nanodet-plus-m_416_stop_line.yml --model workspace_stop_line/nanodet-plus-m_416/model_last.ckpt --path images.jpg

#/home/wyw/nanodet/nanodet/model/head/nanodet_head.py中注释掉onnx转换部分操作
#去掉fpn中上下采样  修改/home/wyw/nanodet/nanodet/model/fpn/ghost_pan.py 把上下采样都注释掉,训练报错，只能训练原始的网络架构

#為了方便起見我們直接更改 outputs 的位置，我們使用 onnx_edit.py 來更改，--outpus 第一個位置放 output name，[]裡放 output shape，例如 831[1,80,10,10]，點選 node 可以查看資訊。input id

$ wget https://raw.githubusercontent.com/d246810g2000/tensorrt/main/onnx_edit.py
$ python onnx_edit.py output.onnx nanodet.onnx --outputs '787[1,80,40,40], 788[1,32,40,40], 809[1,80,20,20], 810[1,32,20,20], 831[1,80,10,10], 832[1,32,10,10]'
```

## test result
![17_14_19_41_1](https://github.com/Aruen24/nanodet-plus/assets/27750891/93e6aa21-7f16-415c-b125-18e05944f793)
![1639730132_Blur_1](https://github.com/Aruen24/nanodet-plus/assets/27750891/94985637-561d-485d-868a-b8a2154f2b92)
