socool
===
socool是一款基于tensorflow机器学习平台的，用于图片标签自动化以及图片识别推荐的系统。
该系统支持可定制的多种图像语音算法，以及自定义训练过程。基于此应用可以很方便的搭建自己的机器学习平台及应用。
## 在线用例

http://42.123.114.162:30001

## 系统特点
1. UI基于springboot，轻便小巧，便于部署
2. 基于tensorflow平台，便于迭代
3. 基于tensorflow serving，成熟的模型上下线框架
4. 基于docker的系统组件，便于集成
5. 训练预测代码完全模块化，支持grpc调用，方便复用

## 系统架构

## 部署指南
1. 安装训练服务    
    下载[image-grpc-server训练代码](https://github.com/yony228/image-grpc-server)并部署。<br>
    ```
    nohup python server.py>log.txt 2>&1 ＆
    ```
2. 安装预测服务    
    预测服务使用[tensorflow-serving](https://github.com/tensorflow/serving)，如果使用ubuntu16.04可以直接下载编译好的可执行文件    
    下载tensorflow_model_server并启动    
    ```Bash
    ###
    # $MODEL_PORT 预测服务端口
    # $MODEL_NAME 模型名称
    # $MODEL_BASE_PATH  模型存放目录
    ###
    tensorflow_model_server --port=$MODEL_PORT --model_name=$MODEL_NAME --model_base_path=$MODEL_BASE_PATH &>/serving.log &
    ```
3. 安装图片服务器    
    图片服务器默认安装NFS存储图片，nginx对外代理图片浏览    
    NFS请自行安装保证上下文中的其他服务可以看到。源码默认的NFS目录是/data    
    nginx这里提供了docker镜像
4. 安装mysql数据库    
    自行安装mysql数据库并运行init脚本或者使用提供的docker构建
5. 安装socool的web服务    
    下载[源码](https://github.com/yony228/image-web)并编译部署


