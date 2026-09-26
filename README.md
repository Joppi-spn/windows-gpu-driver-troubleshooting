# Windows GPU Driver Troubleshooting

Windows 11 下 Lenovo Legion R9000P / RTX 4060 Laptop GPU 的黑屏闪烁与游戏崩溃排查记录。

> 本仓库记录一次真实故障的排查过程。结论会区分「已观察到的事实」与「目前推测」，避免把一次成功的回退测试直接当成已经证明的因果关系。

## 当前结论

在 NVIDIA GeForce Game Ready Driver **610.62 / 32.0.16.1062** 下，系统出现了明显的 NVIDIA 显示驱动异常：

- 点击任务栏时出现黑屏/闪烁；
- `Win + Tab` 出现类似现象；
- `Win + Ctrl + Shift + B` 也会触发类似的黑屏恢复；
- 事件查看器出现大量 `nvlddmkm` Event ID **153**，其中包含 `\\Device\\Video3` 和 `Error occurred on GPUID: 100`；
- 在相同时间段，《正义之怒》曾出现 `Wrath.exe` / `UnityPlayer.dll` / `0xc0000005` 崩溃。

随后通过 NVIDIA App 将驱动重新安装为此前安装过的 **581.29**：

- 任务栏点击恢复正常；
- `Win + Tab` 恢复正常；
- 《正义之怒》随后也恢复到可以正常启动的状态。

因此目前的工作假设是：**610.62 与这台笔记本的 Windows/图形链路之间可能存在兼容性或稳定性问题，并可能与《正义之怒》的启动崩溃存在关联。**

但目前仍需要更长时间的回归测试，才能判断《正义之怒》的崩溃是否与 NVIDIA 驱动问题属于同一个根因。

## 设备环境

- 笔记本：Lenovo Legion R9000P
- 机器类型：82WM
- GPU：NVIDIA GeForce RTX 4060 Laptop GPU
- 系统：Windows 11
- 当前测试驱动：581.29
- 出问题的驱动：610.62 / 32.0.16.1062

## 文档

- [详细排查过程](troubleshooting.md)

## 注意

这是一份个人故障排查记录，不代表所有 RTX 4060 Laptop 或所有 Legion R9000P 都会出现相同问题。
