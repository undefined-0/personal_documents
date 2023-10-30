## 如何在 Visual Studio Code (VSCode) 中构建一个 C++ 项目(Windows)：

#### 1. 安装CMake:

* 1.安装 MinGW: MinGW（Minimalist GNU for Windows）是一个在 Windows 平台上编译 C++ 代码的工具集。你可以从 [MinGW 官网](http://www.mingw.org/) 下载安装程序，并按照安装指南进行安装。
  2.在 [VSCode 官网](https://code.visualstudio.com/) 下载Visual Studio Code安装程序并安装。
  3.安装 C/C++ 插件: 打开 VSCode，点击左侧的扩展（Extensions）图标，搜索并安装 Microsoft 的 C/C++ 扩展。这个插件提供了 C++ 开发所需的基本功能，例如代码补全、调试等。

- 从 [CMake 官网](https://cmake.org/download/) 下载 CMake 安装程序。
- 运行安装程序，按照提示进行安装。注意：在安装过程中选择添加 CMake 到系统环境变量。

#### 2. 检查 CMake 可执行文件路径:

- 打开cmd。
- 运行 `cmake --version` 命令，如果 CMake 已正确安装，应该显示版本信息。
- 如果 `cmake` 命令无法执行，说明 CMake 的可执行文件路径没有被正确添加到系统的环境变量。你需要手动将 CMake 的安装路径添加到系统的 PATH 环境变量中。

#### 3. 手动添加 CMake 到 PATH:

- 打开系统环境变量设置：
  - 在 Windows 10 上，右键点击“此电脑”（或“计算机”），选择“属性”（Properties），然后点击“高级系统设置”（Advanced system settings）。
  - 在“高级”选项卡下，点击“环境变量”（Environment Variables）。
  - 在“系统变量”（System Variables）部分，找到名为 `Path` 的变量，然后点击“编辑”（Edit）。
  - 在编辑环境变量窗口中，点击“新建”（New），然后添加 CMake 的可执行文件路径，通常是类似 `C:\Program Files\CMake\bin` 的路径。确保路径是正确的，根据你的 CMake 安装位置进行调整。
  - 点击所有窗口右下角的“确认”，然后重新启动 Visual Studio Code。

#### 4. 重启 Visual Studio Code:

* 有时候，系统环境变量的更改需要重新启动应用程序才能生效。在添加 CMake 到系统 PATH 后，请重新启动 Visual Studio Code。

在 Visual Studio Code（VSCode）中构建一个包含多个 .cpp 和 .h 文件的 C++ 项目可以通过配置编译任务（tasks）和使用 CMake 来实现。以下是一种基于 Windows 平台的方法：
#### 5. 安装工具和插件

1.安装 MinGW: 如果你还没有安装 MinGW（Minimalist GNU for Windows），你需要先安装它。MinGW 是一个在 Windows 平台上编译 C++ 代码的工具集。你可以从 [MinGW 官网](http://www.mingw.org/) 下载安装程序，并按照安装指南进行安装。
2.安装 Visual Studio Code: 如果你还没有安装 VSCode，你需要在 [VSCode 官网](https://code.visualstudio.com/) 下载安装程序并安装。
3.安装 C/C++ 插件: 打开 VSCode，点击左侧的扩展（Extensions）图标，搜索并安装 Microsoft 的 C/C++ 扩展。这个插件提供了 C++ 开发所需的基本功能，例如代码补全、调试等。

#### 6. 创建 CMakeLists.txt 文件
在你的项目文件夹中创建一个 CMakeLists.txt 文件，用于配置 CMake 构建你的项目。一个简单的示例 CMakeLists.txt 文件如下：

````cmake
cmake_minimum_required(VERSION 3.0)

project(YourProjectName)

# 添加所有的 .cpp 文件
file(GLOB SOURCES *.cpp)

# 添加头文件目录
include_directories(${CMAKE_SOURCE_DIR})

# 生成可执行文件
add_executable(YourExecutable ${SOURCES})
````
在这个文件中，将 YourProjectName 替换为你的项目名称，将 YourExecutable 替换为你的可执行文件的名称。
#### 7. 配置 tasks.json 文件
在 VSCode 中，你需要配置一个 tasks.json 文件来定义构建任务。在你的项目文件夹下创建一个 .vscode 文件夹，然后在该文件夹中创建一个 tasks.json 文件，并添加以下内容：

````json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build",
            "type": "shell",
            "command": "cmake",
            "args": [
                "--build",
                "${workspaceFolder}",
                "--target",
                "YourExecutable",
                "--config",
                "Debug"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
````
在这个文件中，将 "YourExecutable" 替换为你在 CMakeLists.txt 文件中定义的可执行文件的名称。
#### 8. 构建和运行

1. 打开 VSCode，点击左侧的“文件”（File）&gt; “打开文件夹”（Open Folder），选择你的项目文件夹
2. 依次点击下图中1-CMake、2-生成所有项目
3. 构建成功后，项目文件夹中会生成可执行文件（通常在 debug 或 build 文件夹中）
   *  可以`cd`进入可执行文件所在目录后使用`./your-program.exe`命令在终端中运行它。

<img src="https://raw.githubusercontent.com/undefined-0/image-store/main/PicGo/202310302016729.png" alt="在VScode中使用CMake构建C++工程（编辑后）" style="zoom: 67%;" />