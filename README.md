# deepseek-tui_winarm
deepseek-tui build release on windows on arm

### 源项目：[Deepseek-TUI](https://github.com/Hmbown/DeepSeek-TUI)


### 编译与构建流程

**方法1**
准备:
- 下载并安装rust
- 从源项目下载仓库到本地。
- 下载visual studio installer

一,打开vs installer-----单个组件,安装如下组件:
- 适用于x64/x86的MSVC生成工具（最新版）
- 适用于ARM64/ARM64EC的MSVC生成工具
- 适用于Windows的C++Clang 编译器
- Windows 11 SDK

二,
执行`cd <your code path>`

`cargo build --release`

-
