### 数据处理
1. 经过BICUBIC下采样后再BICUBIC上采样，获得lr(低清晰度图像)
2. 裁切3×32×32大小的图片
   1. 上下间隔16裁切（原本样本集）
   2. 随机裁切（增加样本多样性）
   3. 计算方差从大到小后的前6%地方裁切（增加复杂图像样本）
3. 一共95855张训练图像
### 使用模型
1. 原始srcnn 9-5-5模型
   - （描述）由于模型比较简单，由于数据集巨大，拟合能力较为欠缺
2. 原始9-5-5模型+vgg19感知损失+vgg19风格损失，
   - （描述）添加感知损失、风格损失，虽然psnr会升高，但是人眼感官更佳。
3. 将srcnn 9-5-5替换为去掉批次归一化的Unet
   - （描述）模型加强，拟合能力增强
### 训练
1. 每个模型都训练100次，去除最后一个epoch的模型参数
2. 使用adam优化，学习率全都是0.0001
### 测试
1. 使用psnr指标
2. 分为bicubic、和模型的psnr、图像如文件夹内所示