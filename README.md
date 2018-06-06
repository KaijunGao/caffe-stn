# caffe-stn
主要是为了记录stn移植到最新caffe中的过程


参考的caffe实现 https://github.com/happynear/SpatialTransformerLayer 
因为时间比较久，所以不适用于新版的caffe
另外，移植过程参考了 https://blog.csdn.net/kuaitoukid/article/details/51035028
同时记录了一些自己的理解

1.首先，编译一个全新的caffe-master。
第一个链接中下载的有3个文件夹：examples、include和src

2.将STN/include/caffe中的.hpp（除filler.hpp）复制到 caffe-master/include/caffe/layers/ 中；
将.hpp中的 #include "caffe/neuron_layers.hpp" 改为 #include "caffe/layers/loss_layer.hpp"；

3.将STN/include/caffe/filler.hpp中修改的部分加入到caffe-master/include/caffe/filler.hpp 中。

4.将STN/src/caffe/layers/ 中的文件复制到 caffe-master/src/caffe/layers/ 中；

loc_loss_layer.cpp:
#include "caffe/vision_layers.hpp" -> //#include "caffe/vision_layers.hpp"
#include "caffe/loc_loss_layer.hpp" -> #include "caffe/layers/loc_loss_layer.hpp"

power_file_layer.cpp:
#include "caffe/power_file_layer.hpp" -> #include "caffe/layers/power_file_layer.hpp"

st_layer.cpp:
#include "caffe/st_layer.hpp" -> #include "caffe/layers/st_layer.hpp"

st_loss_layer.cpp：
#include "caffe/vision_layers.hpp" -> //#include "caffe/vision_layers.hpp"
#include "caffe/st_loss_layer.hpp" -> #include "caffe/layers/st_loss_layer.hpp"

.cu 和 .cpp 做相同的修改

5.重新编译即可
