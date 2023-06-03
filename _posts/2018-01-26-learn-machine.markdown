---
layout: post
title:  "Tensorflow实践"
date:   2018-01-26
categories: learn-machine
---
使用python库，实现图片识别。
利用TensorFlow实现图片识别分类
1. 安装TensorFlow
2. 克隆google codelab
git clone https://github.com/googlecodelabs/tensorflow-for-poets-2

3. 获取识别图片

    ```$xslt
    curl http://download.tensorflow.org/example_images/flower_photos.tgz | tar xz -C tf_files
    ```
       
4. 重新训练 how_many_training_steps 训练步数可不设 可以一直训练

    ```$xslt
    IMAGE_SIZE=224
    ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}"
    ```
    ```
    python3 -m scripts.retrain \
      --bottleneck_dir=tf_files/bottlenecks \
      --how_many_training_steps=500 \
      --model_dir=tf_files/models/ \
      --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
      --output_graph=tf_files/retrained_graph.pb \
      --output_labels=tf_files/retrained_labels.txt \
      --architecture="${ARCHITECTURE}" \
      --image_dir=tf_files/flower_photos
    ```
5. 使用重新生成的模型
    ```$xslt
    python -m scripts.label_image \
        --graph=tf_files/retrained_graph.pb  \
        --image=tf_files/flower_photos/daisy/21652746_cc379e0eea_m.jpg
    ```

