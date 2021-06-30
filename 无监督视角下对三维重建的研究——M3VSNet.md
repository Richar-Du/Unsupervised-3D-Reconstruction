# M3VSNet

## 模型架构

M3VSNet的基本架构由三部分组成——金字塔特征聚合、基于方差的体素生成和三维U-Net正则化。金字塔特征聚合从低层次到高层次依次提取特征，从而能够包含更多的上下文信息。然后使用与MVSNet相同的基于方差的代价体素生成和3D U-Net正则化来生成初始深度图。

除此之外，M3VSNet还使用VGG16进行特征提取，构造了feature-wise的损失函数。

## 训练过程

- 首先下载预处理好的DTU数据集：https://drive.google.com/file/d/1eDjh-_bxKKnEuz5h-HXS7EDJn59clx6V/view
- python train.py --dataset=dtu_yao --batch_size=4 --trainpath=\$MVS_TRAINING --trainlist lists/dtu/train.txt --testlist lists/dtu/test.txt --numdepth=192 --logdir ./checkpoints/d192 $@

## 测试过程

- 首先下载测试集：https://drive.google.com/open?id=135oKPefcPTsdtLRzoDAQtPpHuoIrpRI，放在dtu_test文件夹下面。注意如果需要在自采数据集上进行测试，则需要首先用colmap进行稀疏重建，得到cams文件夹，images文件夹，和一个pair.txt文件，保证和测试集中的数据格式是完全一致的。
- python eval.py --dataset=dtu_yao_eval --batch_size=1 --testpath=dtu_test --testlist lists/dtu/test.txt --loadckpt ./checkpoint/22.ckpt --numdepth=192 --interval_scale=1.06 --display $@

