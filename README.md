## 【Ubuntu18下环境配置】
1、使用anoconda创建虚拟环境：
```
conda create -n MVS_env
source activate conda
```
2、安装库
```
sudo apt-get update -qq && sudo apt-get install -qq
sudo apt-get -y install git cmake libpng-dev libjpeg-dev libtiff-dev libglu1-mesa-dev
```

3、Eigen
```
git clone https://gitlab.com/libeigen/eigen.git --branch 3.2
mkdir eigen_build && cd eigen_build
cmake . ../eigen
make && sudo make install
cd ..
```
*如果git下载过慢，去网址中直接下载拷贝。

4、安装Boost
```
sudo apt-get -y install libboost-iostreams-dev libboost-program-options-dev
libboost-system-dev libboost-serialization-dev
```

5、安装OpenCV
```
sudo apt-get -y install libopencv-dev
```

6、安装CGAL 
```
sudo apt-get -y install libcgal-dev libcgal-qt5-dev
```

7、安装VCGLib 
```
git clone https://github.com/cdcseacave/VCG.git vcglib
```
*当前vcglib版本不符，会报错，可使用之前的tag1.0.1版本

8、安装OpenMVS
```
git clone https://github.com/electech6/openMVS_comments.git openMVS
mkdir openMVS_build && cd openMVS_build
```

9、生成库文件
```
sudo make -j2 && sudo make install
```

## 【测试数据】
数据下载：https://github.com/cdcseacave/openMVS_sample

0、安装meshlab
```
sudo apt-get install meshlab
```

1、稠密重建
```
/bin/DensifyPointCloud -w /地址/openMVS_sample -i scene.mvs -o test_dense.mvs
```

2、曲面重建
```
./bin/ReconstructMesh -w /地址/data -i test_dense.mvs -o test_mesh.mvs
```

3、网格优化
```
./bin/RefineMesh -w /地址/data -i test_mesh.mvs -o test_refinemesh.mvs
```
4、纹理贴图
```
./bin/TextureMesh -w /地址/data -i test_refinemesh.mvs -o test_texture.mvs
```

# OpenMVS: open Multi-View Stereo reconstruction library

## Introduction

[OpenMVS (Multi-View Stereo)](http://cdcseacave.github.io/openMVS) is a library for computer-vision scientists and especially targeted to the Multi-View Stereo reconstruction community. While there are mature and complete open-source projects targeting Structure-from-Motion pipelines (like [OpenMVG](https://github.com/openMVG/openMVG)) which recover camera poses and a sparse 3D point-cloud from an input set of images, there are none addressing the last part of the photogrammetry chain-flow. *OpenMVS* aims at filling that gap by providing a complete set of algorithms to recover the full surface of the scene to be reconstructed. The input is a set of camera poses plus the sparse point-cloud and the output is a textured mesh. The main topics covered by this project are:

- **dense point-cloud reconstruction** for obtaining a complete and accurate as possible point-cloud
- **mesh reconstruction** for estimating a mesh surface that explains the best the input point-cloud
- **mesh refinement** for recovering all fine details
- **mesh texturing** for computing a sharp and accurate texture to color the mesh

See the complete [documentation](https://github.com/cdcseacave/openMVS/wiki) on wiki.

## Build

See the [building](https://github.com/cdcseacave/openMVS/wiki/Building) wiki page. Windows and Ubuntu x64 continuous integration status [![Build Status](https://ci.appveyor.com/api/projects/status/github/cdcseacave/openmvs?branch=master&svg=true)](https://ci.appveyor.com/project/cdcseacave/openmvs)
Automatic Windows x64 binary builds can be found for each commit on its Appveyor Artifacts page.

## Example

See the usage [example](https://github.com/cdcseacave/openMVS/wiki/Usage) wiki page.

## License

See the [copyright](https://github.com/cdcseacave/openMVS/blob/master/COPYRIGHT.md) file.

## Contact

openmvs[AT]googlegroups.com
