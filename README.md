# 3DReconstruction_indoor-multi-floor
3D geometric reconstruction in indoor multi floor environment

多楼层室内环境下的三维几何重建

# 1.背景介绍

在智能制造、AR、机器人等领域，三维重建都有很广泛的应用前景。随着消费级RGB-D相机的普及，三维重建的应用场景也得到了很大程度的扩展。对多楼层的室内环境进行稠密的三维重建，可以应用于混合现实（MR）、室内装修等领域。

目前，虽然有众多专家学者致力于三维重建的研究，但在诸如多楼层室内的复杂环境下进行稠密三维重建仍然具有以下难点：

**模型更新。**三维重建输入的是图像序列，不仅需要算法能够选择关键帧，而且还需要在检测到新关键帧时，能够根据其位姿融合到三维模型中。

**高质量表面重建。**RGB-D相机获取的是深度图，根据相机内参生成点云，然而完成三维重建最终需要获得连续的表面而非离散的三维点。

针对上述难点，我们使用TSDF（truncated signed distance function）地图来对模型进行更新，采用Marching Cube算法对离散的空间点进行重建获得三角面片。最终，我们使用Zora P1开发板和Astra Pro深度相机，基于ORB-SLAM2框架进行位姿估计并进行扩展，构建了一套完整的多楼层大型室内环境稠密重建的系统。

# Dependencies:

1.

```bsh
sudo apt-get install build-essential freeglut3 freeglut3-dev 
```

2.OpenNI2 SDK

开发版是Arm64 (可通过uname -a查看)

https://developer.orbbec.com.cn/download.html?id=64

编译程序需要其中的Include和Redist，后者是链接库（不能用系统里之前装的OpenNI2的替代）。

3.OpenCV

4.PCL

5.[cpu_tsdf](https://github.com/sdmiller/cpu_tsdf)

# Build Instructions

```bsh
sh build.sh
```

# Usage

连接Orbbec Astra Pro采集数据，保存TUM-RGBD格式数据集

```bash
sh run_cam.sh
```

读取ORB_SLAM2作为基础框架获取的时间戳、关键帧位姿、RGB、深度图作为关键信息对，进行扩展的稠密三维重建

```bash
sh run_reconstruction.sh
```

# Reference

[3D相机D2C对齐](https://developer.orbbec.com.cn/forum_plate_module_details.html?id=185) 

[Ubuntu下Astro Pro配置openni踩坑小记](https://developer.orbbec.com.cn/forum_plate_module_details.html?id=677) 
