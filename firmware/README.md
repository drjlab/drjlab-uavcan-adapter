DrjLab CAN Adapter兼容[Zubax_babel固件](https://github.com/Zubax/zubax_babel.git)，固件编译和烧写可以参考 https://github.com/Zubax/zubax_babel.git。

## 配置编译环境
如果你们没有可用的Linux环境，Zubax提供了一个包含编译环境的虚拟机，请到这里下载 https://files.zubax.com/vm/bistromathic.ova 。虚拟机包含以下开发组件：
- 全功能Ubuntu，带KED桌面
- ARM GCC嵌入式工具链
- 核心开发工具（git,make,cmake等）
- 全功能LaTex（texlive-full）
- Eclipse IDE工具

## 下载代码编译
1. 克隆代码
```
git clone https://github.com/Zubax/zubax_babel --recursive
```
2. 编译代码
```
cd zubax_bael/firmware
make -j8 RELEASE=1  # Omit RELEASE=1 to build the debug version
```
RELEASE=1表示生成RELEASE版固件，RELEASE=0表示生成DEBUG版固件。make之后会同时生成bootloader，最后在build文件夹将生成以下内容：
- com.zubax.*.application.bin，只有firmware
- com.zubax.*.compund.bin，包含了bootloader+firmware，可以只是使用JTAG/SWD工具烧写
- compund.elf，ELF调试文件，包含了bootloader+firmware

3. 烧写固件

建议直接使用JTAG/SWD将com.zubax.*.compund.bin写入到空白的芯片，它包含了bootloader+firmware。

当然您也可以使用下面的脚本，一口气自动完成固件烧写：
```
# 请先切换到firmware文件夹然后再执行下面命令
./zubax_chibios/tools/blackmagic_flash.sh
```
