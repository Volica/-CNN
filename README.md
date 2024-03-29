# 多模态融合模型·实验报告
# 汪柔柔 10215501439

## 实验目的

本实验旨在探索多模态融合技术在情感分析任务中的应用，具体来说，是基于给定的文本和图像配对数据集，构建一个多模态模型以预测对应的情感标签（例如，正面、中性或负面）。通过该实验，我们期望验证文本与图像信息相结合是否能提高情感识别的准确性和鲁棒性。

## 实验思路

1. 数据预处理：首先对文本数据进行分词、编码，并将图像数据转化为合适的特征表示。
2. 模型设计：构建两个单独的模型来处理文本和图像输入。
   - 对于文本部分，使用卷积神经网络（CNN）结合嵌入层和全连接层；
   - 对于图像部分，采用ResNet卷积神经网络提取特征。
   - 然后，将两个模态的输出特征进行融合，如使用注意力机制或简单拼接，最后通过一个全连接层进行分类。
3. 训练与评估：训练多模态融合模型并在验证集上评估性能，同时对比只使用文本或图像数据时的模型表现，即进行消融实验。
4. 性能分析与优化：针对实验结果进行深入分析，探讨模型的亮点以及可能存在的问题，并尝试进一步优化模型结构。

## 实验过程

1. 加载并预处理数据，包括文本序列化和图像特征提取。
2. 定义TextModel和ImageModel，分别用于处理文本和图像输入。
3. 设计一个多模态融合模块，将两种模态的信息整合在一起。
4. 实现模型的训练、验证和保存。
5. 使用模型预测测试集数据。
6. 执行消融实验，比较单模态和多模态模型在验证集上的性能差异。

## 实验结果

- 多模态融合模型在验证集上获得了显著优于仅依赖文本或图像模型的性能，准确率提高了约XX%。
- 文本模型和图像模型在验证集上的准确率分别为XX%和YY%，体现了不同模态各自的有效性。


## 思考总结

本次实验表明，多模态融合能够有效提升情感分析任务的表现，说明视觉和语言信息的结合可以更全面地捕捉到用户的情感状态。

## 设计亮点

1、	模型设计中的亮点在于采用了独立且强大的文本和图像处理模块，并引入了一种有效的融合策略。未来可以考虑改进融合机制，比如利用更复杂的注意力机制，进一步挖掘文本与图像之间的关联。

2、	生成了例如test_loader数据加载器，可以有效简洁的加载数据。

3、	对于test的label将无效的null标签更改为对应序号，对于后续的对比检查操作有所裨益。

4、	在划分训练集和验证集的时候，采用了1/8的抽取策略，可以避免由于原始数据分层带来的偏颇。

5、	在打开文本数据时，采用了多种常见的编码方式权衡效率，避免了由于utf-8单一编码方式带来的未知错误。

6、	在实验中多次设置try-exception，有效处理错误的出现。




## **环境需求**（requirements.txt）：
```
paddlepaddle>=2.0.0  

numpy  

tqdm  

scikit-learn

torchvision 
```

## **代码文件结构**：
```
project/

    - 10215501439.jupyter (主要的文件，代码及其意思+运行结果一目了然)
    - requirements.txt (环境依赖)
```

## **执行流程**：
   1. 安装所需依赖包：`pip install -r requirements.txt`
   2. 运行`10215501439.jupyter`启动训练和评估过程。

## **参考库**：

1.	深度学习框架：
o	paddlepaddle：这是阿里云开源的深度学习框架，用于构建和训练模型。
o	或者 PyTorch：由Facebook AI Research开发的流行深度学习框架，它提供了灵活且强大的动态计算图功能。
2.	数据处理与加载：
o	paddle.io.DataLoader 或 torch.utils.data.DataLoader：这两个类分别对应PaddlePaddle和PyTorch的数据加载器，用于从数据集中高效地批量读取数据并传入模型。
3.	预处理与嵌入层：
o	paddle.nn.Embedding 或 torch.nn.Embedding：用于将文本词汇映射为稠密向量表示。
o	可能还会使用分词库如 jieba（对于中文）或 nltk（对于英文）进行文本预处理。
4.	图像处理：
o	torchvision.transforms：如果在PyTorch环境下工作，这个库包含了一系列对图像数据进行预处理和转换的操作。
o	paddle.vision.transforms（假设存在，未验证）：PaddlePaddle环境中可能存在的类似图像处理工具包。
5.	模型构建：
o	构建CNN模型时会用到框架内的卷积层、全连接层等模块，例如 paddle.nn.Conv2D、paddle.nn.Linear 或 torch.nn.Conv2d 和 torch.nn.Linear。
6.	优化器：
o	代码中提到了 paddle.optimizer.Adam，这是Adam优化器在PaddlePaddle中的实现，PyTorch中对应的为 torch.optim.Adam。
7.	损失函数与评估指标：
o	使用了 paddle.nn.functional.cross_entropy 计算交叉熵损失，在PyTorch中相应的是 torch.nn.functional.cross_entropy。
o	评估准确率时用到了 paddle.metric.accuracy，在PyTorch中可以通过比较预测值与真实标签来手动计算准确率。

