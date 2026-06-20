# codewhale_winarm：CodeWhale（Deepseek TUI） Unofficial Build for Windows on Arm (ARM64)
CodeWhale（DeepSeek TUI） Unofficial Build for Windows on Arm (ARM64)

CodeWhale（原DeepSeek TUI） 的 Windows on Arm (ARM64) 非官方编译版

由于官方暂时没有提供 Windows on Arm 的编译二进制包，我为 CodeWhale 手动编译了一个 ARM64 版本，方便在Windows ARM 设备上原生运行CodeWhale。

### 源项目：[CodeWhale](https://github.com/Hmbown/DeepSeek-TUI)，官网：[CodeWhale](https://codewhale.net)
### 下载编译好的程序:
https://github.com/letmuts/codewhale_winarm/releases
## 编译与构建流程
无论使用哪种方案，都要安装rust
#### 方案一:Visual Studio Installer 添加需要的构建依赖
此方案较简单,但安装的依赖较多.

首先要下载如下内容:
- [CodeWhale](https://github.com/Hmbown/CodeWhale)
- 下载并安装rust
- 下载visual studio installer

然后打开vs installer-----单个组件,安装如下组件:
- 适用于x64/x86的MSVC生成工具（最新版）
- 适用于ARM64/ARM64EC的MSVC生成工具
- 适用于Windows的C++Clang 编译器
- Windows 11 SDK

cd到你下载的codewhale源码路径,然后执行`cargo build --release`,输出的编译结果会提示你编译好的exe所在的路径.

或者你直接运行`cargo install codewhale`也可以,cargo会为你配置一切,这样做你就可以直接打开powershell执行`codewhale`(也可以用旧版指令`deepseek`)就可以使用了.

如果在更新完rust工具链后发现系统无法检测到clang依赖，可以执行如下命令。将clang的路径临时添加为环境变量（注意命令中的路径是你设备中llvm中的实际的路径）：

`$env:PATH += ";C:\Program Files\Microsoft Visual Studio\18\Community\VC\Tools\Llvm\bin"`

#### 方法二：单独安装 LLVM（包含 clang-cl）
此方案较复杂,但此方案使用的是开源工具链,编译出的二进制可以应用于商业环境中,而不必担心通过微软visualstudioinstaller安装build tools造成的可能侵权的问题.(当然你前期配置rust环境也要使用gun工具链)

首先需前往[llvm project](github.com/llvm/llvm-project),在release中下载`clang+llvm-22.1.6-aarch64-pc-windows-msvc.tar`.

将压缩包解压,确保`bin\\clang-cl.exe`存在.

现在有两个小方案:
1.直接在设备上安装deepseek-tui:
临时设置变量
```
$env:CC = "C:\Users\fulde\projects\deepseek-tui\llvm\bin\clang-cl.exe"
$env:CXX = "C:\Users\fulde\projects\deepseek-tui\llvm\bin\clang-cl.exe"
$env:PATH = "C:\Users\fulde\projects\deepseek-tui\llvm\bin;$env:PATH"  # 可选，方便 clang-cl 被调用
```

执行:`cargo clean`和`cargo install codewhale`

<br>
<br>

2.或者可以先克隆[codewhale](https://github.com/Hmbown/codewhale)源代码,cd到下载目录,执行`cargo build --release`.

完成.


