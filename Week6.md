<script type="text/javascript" async src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML"> </script>
# Week6 笔记
本周课程的内容都是围绕优化方法展开的，即各种对梯度下降方法的改良，以寻求更好的优化效果。
- Mini-Batch梯度下降（Gradient descent）
- 带动量（momentum）的梯度下降
- RMSprop算法（与带动量的梯度下降类似）
- Adam算法（综合带动量的梯度下降和RMSprop）

接下来开始总结课程内容
##### Mini-Batch梯度下降
&emsp;&emsp;Mini-Batch梯度下降是介于Batch梯度下降（BSD）和随机梯度下降（SGD）之间的。Batch梯度下降一次迭代中（指进行一次梯度下降）利用向量化操作同时遍历所有样本，SGD则一次迭代中对单个样本进行操作。当数据集样本数小的时候（如1000个样本），这两种方法效果都不错。但当数据集样本数很大时（如1,000,000），那么用BSD迭代一次耗时很久而且容易溢出，SGD遍历每一个就会抖动的非常厉害，相当于引入了噪声。Mini-Batch梯度下降就是将这一百万的样本划分成多个小样本集，比如每组的Mini-size取为1000，共1000组。然后利用每组进行一次梯度下降。所以三种的区别总结起来就是：  

| |SGD|Mini-Batch GD|BGD|
|:-|:-:|:-:|:-:|
|样本数|1|mini-size|m|
|缺点|不能利用向量化加速学习，而且要调小学习率|-|训练时间太久|
|特点|搜索路径曲折(图1紫)|搜索路径相对曲折（图1绿）|搜索路径相对平滑（图1蓝）|
|特点|-|代价函数抖动着下降|代价函数光滑下降|
<caption><center> <u>Table 1</u>: 三种梯度下降比较</center></caption>

<img src="https://github.com/Anglepsw/Notebook-on-Deep-Learning-Study/raw/week6_temp/images/06-01-搜索路径.PNG " style="width:200px;height:200px;">
<caption><center> <u>Figure 1</u>: 三种梯度下降搜索路径(引自DL课程PPT)</center></caption>
<img src="https://github.com/Anglepsw/Notebook-on-Deep-Learning-Study/raw/week6_temp/images/06-02-代价函数下降.PNG" style="width:700px;height:250px;">
<caption><center> <u>Figure 2</u>: 代价函数下降(引自DL课程PPT)</center></caption>

##### Mini-Batch size的选择
##### Mini-Batch算法实现

##### 带动量（momentum）的梯度下降
&emsp;&emsp;在理解带动量的梯度下降之前，需要先理解指数权重平均或者滑动平均，用公式表示就是
$$v=\beta v+(1-\beta)v$$
<img src="http://chart.googleapis.com/chart?cht=tx&chl= v=\beta v+(1-\beta)v" style="border:none;">
