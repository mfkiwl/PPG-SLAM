# PPG-SLAM
PPG-SLAM: Real-Time and Robust Visual-Inertial SLAM with Point-Pair Graph

**Related video:** [PPG-SLAM](https://youtu.be/87kftCq5J2I)

**System Overview:**

![Overview](./misc/SystemOverview.png "System Overview")


## 1. Introduction
Numerous inter-frame feature matching methods and structural landmarks have been proposed to improve the robustness and accuracy of visual SLAM. However, inter-frame matching often overlooks the prior information contained in incrementally updated maps, while incorporating multiple geometric landmarks typically introduces redundancy and slows down map optimization. In this paper, we propose a visual-inertial SLAM system based on a point-pair graph representation. By explicitly expressing feature connections through edge information, our method directly associates images with the map, improving the robustness of feature tracking. Furthermore, we introduce co-linear constraints into the optimization process, which enhance map accuracy without adding redundant landmarks. Extensive experiments demonstrate that our approach achieves high robustness in both complex urban roads and mixed indoor-outdoor environments, achieving over 10% reduction in translation drift compared to other SOTA SLAM methods. Compared to point-line approaches, we reduce back-end optimization time by 21%, improving real-time performance under computational resource constraints. Our implementation is open-sourced.

## 2. Prerequisited

### 2.1 System

- CPU: Intel Core i7-13700
- GPU: NVIDIA RTX 4070
- OS: Ubuntu 22.04

### 2.2 Thirdparties

Eigen >= 3.3, Follow [Eigen Installation](https://eigen.tuxfamily.org/index.php?title=Main_Page).

OpenCV >= 4.2.0, Follow [Opencv Installation](http://opencv.org/).

LibTorch (CUDA >=12.6), Follow [LibTorch Installation](https://pytorch.org/get-started/locally/).

Pangolin, Follow [Pangolin Installation](github.com/stevenlovegrove/Pangolin).

g2o (tag = 20241228_git), Follow[G2o Installation](https://github.com/RainerKuemmerle/g2o).

## 3. Build

install Pangolin
```
git clone github.com/stevenlovegrove/Pangolin
cd ~/Pangolin
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
make -j
sudo make install
```

install g2o
```
git clone --branch 20241228_git --depth 1 https://github.com/RainerKuemmerle/g2o.git
cd ~/g2o
mkdir build
cd build
cmake -DG2O_USE_LOGGING=OFF -DCMAKE_BUILD_TYPE=Release ..
make -j
sudo make install
```

install LibTorch
```
download the libtorch-shared-with-deps-x.x.x%xxx.zip & unzip it
```

Clone the repository and build with cmake:

```
git clone https://github.com/NEU-REAL/PPG-SLAM
cd PPG-SLAM
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
make -j4
```

## 4. Run the package

Working with open access datasets. We provide instructions for [EuRoC MAV](http://robotics.ethz.ch/~asl-datasets/ijrr_euroc_mav_dataset/), [TUM-VI](https://cvg.cit.tum.de/data/datasets/visual-inertial-dataset), and [UMA-VI](https://mapir.isa.uma.es/mapirwebsite/?p=2108&page=2) Please download the zip file and unzip it, then you can play the datasets by:

```
./bin/mono_inertial_euroc Vocabulary/voc_euroc_9x3.gz config/EuRoC.yaml net <Path to dataset>
./bin/mono_inertial_tum Vocabulary/voc_tum_9x3.gz config/TUM-VI.yaml net <Path to dataset>
./bin/mono_inertial_uma Vocabulary/voc_tum_9x3.gz config/UMA.yaml net <Path to dataset>
```

## 5. Run with ROS

We have provided a version under ROS2, which can be switched by:

```
git checkout ROS2
```

## 6. Acknowledgments

Thanks for [ORB_SLAM3](https://github.com/UZ-SLAMLab/ORB_SLAM3), [AirSLAM](https://github.com/sair-lab/AirSLAM), [SOLD2](https://github.com/cvg/SOLD2), and [SuperPoint](https://github.com/magicleap/SuperPointPretrainedNetwork). 

