# OpenCV Pre-built for gocv

预构建的 OpenCV 库，专为 [gocv](https://gocv.io/) 优化，只包含必需的模块。

## 包含的模块

- **core** - 核心功能
- **imgproc** - 图像处理
- **imgcodecs** - 图像编解码
- **features2d** - 特征检测（AKAZE, BRISK, ORB, KAZE）
- **flann** - 快速近似最近邻
- **calib3d** - 相机标定和 3D 重建
- **objdetect** - 目标检测
- **dnn** - 深度神经网络
- **video** - 视频分析
- **photo** - 计算摄影
- **highgui** - 高层 GUI
- **videoio** - 视频 I/O

## 下载

从 [Releases](../../releases) 页面下载预构建包：

| 平台 | 文件 |
|------|------|
| macOS ARM64 | `opencv-4.10.0-macos-arm64.tar.gz` |
| Windows x64 | `opencv-4.10.0-windows-x64.zip` |

## 使用方法

### macOS

```bash
# 下载并解压
curl -sL https://github.com/YOUR_ORG/opencv-prebuilt/releases/download/v4.10.0/opencv-4.10.0-macos-arm64.tar.gz | tar xz -C ~/opencv-minimal

# 设置环境变量
export PKG_CONFIG_PATH=~/opencv-minimal/lib/pkgconfig
export CGO_CPPFLAGS="-I$HOME/opencv-minimal/include/opencv4"
export CGO_LDFLAGS="-L$HOME/opencv-minimal/lib -lopencv_core -lopencv_imgproc -lopencv_imgcodecs -lopencv_features2d -lopencv_flann -lopencv_calib3d -lopencv_objdetect -lopencv_dnn -lopencv_video -lopencv_photo -lopencv_highgui -lopencv_videoio"

# 构建 Go 项目
go build -tags customenv ./...
```

### Windows (MSYS2)

```bash
# 下载并解压
curl -sL https://github.com/YOUR_ORG/opencv-prebuilt/releases/download/v4.10.0/opencv-4.10.0-windows-x64.zip -o opencv.zip
unzip opencv.zip -d /c/opencv-minimal

# 设置环境变量
export PKG_CONFIG_PATH=/c/opencv-minimal/lib/pkgconfig
export CGO_CFLAGS="-I/c/opencv-minimal/include/opencv4"
export CGO_LDFLAGS="-L/c/opencv-minimal/lib -lopencv_core -lopencv_imgproc -lopencv_imgcodecs -lopencv_features2d -lopencv_flann -lopencv_calib3d -lopencv_objdetect -lopencv_dnn -lopencv_video -lopencv_photo -lopencv_highgui -lopencv_videoio"

# 构建 Go 项目
go build -tags customenv ./...
```

## 构建新版本

1. 修改 workflow 中的 `OPENCV_VERSION`
2. 打 tag 触发构建：`git tag v4.10.0 && git push origin v4.10.0`
3. 或手动触发 workflow dispatch

## 为什么不用官方预编译包？

- 官方包包含所有模块，体积大
- gocv 需要特定的编译配置
- 需要 pkgconfig 文件支持 `customenv` build tag
