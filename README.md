# 遥感识图小助手

遥感识图小助手是一款基于internLM大语言模型技术的智能应用，旨在提升遥感图像分析的效率和精度。通过利用先进的自然语言处理和计算机视觉算法，该项目能够对卫星图像进行自动化识别和分类。最终目标是建立一个视觉语言模型（VLM），为问答系统（VQA）提供服务，并利用RAG（Retrieval-Augmented Generation）系统来增强问答的准确性。RAG系统基于空间矢量坐标生成知识图谱，从而更准确地描述图片中的空间关系。

## 系统架构

### 1. 数据预处理

- **图像采集**：从不同的遥感卫星和平台获取高分辨率图像。
- **图像预处理**：包括图像校正、增强和裁剪，以提高图像质量和分析准确性。
- **数据标注**：通过手动或半自动的方式标注图像中的地物、变化和土地利用类型，生成训练数据。

### 2. 模型训练

- **大语言模型（internLM）**：利用预训练的internLM模型，通过转移学习进一步训练，使其适应遥感图像的特定任务。
- **计算机视觉模型（CLIP）**：使用CLIP模型进行图像特征提取和分类，通过结合图像和文本信息实现多模态理解。
- **多任务学习**：结合地物检测、变化监测和土地利用分类任务，进行联合训练，提高模型的泛化能力。

### 3. 视觉语言模型（VLM）

- **模型架构**：结合CLIP模型的图像特征和internLM的语言模型，构建一个多模态模型，用于处理视觉问答任务。
- **训练方法**：使用RSVQA数据集的图像-文本对进行训练，使模型能够理解并生成与图像相关的自然语言描述。

### 4. RAG系统

- **知识图谱生成**：基于OpenStreetMap的空间矢量坐标，通过图像中的地物和空间关系生成知识图谱。
- **检索增强生成**：在回答用户问题时，首先从知识图谱中检索相关信息，然后结合生成模型生成准确的答案。


## 功能模块

### 1. 地物检测

- **功能描述**：自动检测遥感图像中的各种地物，包括建筑物、道路、水体、植被等。
- **实现方法**：使用预处理后的图像数据，通过训练好的计算机视觉模型（如CLIP）进行地物检测。
- **输出**：包含各类地物的边界和类别标签的图像。

### 2. 变化监测

- **功能描述**：识别并标记不同时期遥感图像中的地表变化，如城市扩张、森林砍伐、自然灾害影响等。
- **实现方法**：比较不同时期的遥感图像，利用深度学习算法（如Change Detection Network）检测变化区域。
- **输出**：变化区域的标注和变化类型的分类结果。

### 3. 土地利用分类

- **功能描述**：根据遥感图像中的特征对土地利用类型进行分类，如农业用地、工业用地、居住用地等。
- **实现方法**：使用训练好的卷积神经网络（CNN）模型进行分类。
- **输出**：分类后的土地利用类型图。

### 4. 视觉问答系统（VQA）

- **功能描述**：通过视觉语言模型（VLM）处理用户的图像相关问题，并生成自然语言回答。
- **实现方法**：结合CLIP和internLM模型，使用RSVQA数据集进行训练，回答与图像内容相关的问题。
- **输出**：针对输入问题的自然语言回答。

### 5. 检索增强生成系统（RAG）

- **功能描述**：通过知识图谱增强视觉问答系统的问答准确性。
- **实现方法**：基于OpenStreetMap数据生成空间知识图谱，结合检索增强生成（RAG）技术，在回答用户问题时检索相关信息并生成答案。
- **输出**：增强准确性的自然语言回答。

### 6. 分析报告生成

- **功能描述**：自动生成包含地物检测、变化监测和土地利用分类结果的详细分析报告，并提供专业建议。
- **实现方法**：汇总各功能模块的分析结果，生成易于理解的报告文档。
- **输出**：详细的分析报告，包括图像标注和分类结果。
  


## 部署与使用

### 部署

1. **环境准备**：安装所需的Python库和深度学习框架。
2. **模型加载**：下载并加载预训练的internLM、CLIP模型和其他计算机视觉模型。
3. **服务启动**：运行API服务，接受用户上传的遥感图像并进行分析。

### 使用

1. **上传图像**：用户通过前端界面上传遥感图像（可选择上传空间矢量图）。
2. **任务选择**：选择需要进行的分析任务（地物检测、变化监测或土地利用分类）。
3. **获取结果**：系统进行分析并生成详细的报告，包括图像标注和分类结果，以及专业建议。

## 开发环境

- **编程语言**：Python
- **深度学习框架**：PyTorch
- **数据处理**：OpenCV、GDAL
- **自然语言处理**：Transformers（Hugging Face）

## 未来工作

- **模型优化**：进一步优化视觉语言模型的性能，提升问答系统的准确性。
- **数据扩展**：增加更多的遥感图像数据，提高模型的泛化能力。
- **功能扩展**：开发更多的分析功能，如灾害评估、生态监测等。

---

**目录结构**

```plaintext
project
│   README.md
│   requirements.txt
│
└───data
│   │   sample_data.csv
│
└───models
│   │   internLM_model.pth
│   │   CLIP_model.pth
│
└───src
    │   main.py
    │   data_preprocessing.py
    │   model_training.py
    │   image_analysis.py
    │   VLM_training.py
    │   RAG_system.py
