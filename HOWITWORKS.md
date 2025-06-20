# 项目原理

AmiiboConverter 是一个使用 Python 编写的命令行工具，用于在不同的 amiibo 数据格式之间进行转换。程序依赖 `pyamiibo` 库来解析和重建 amiibo dump，通过 `argparse` 接收命令行参数。

工具可以读取 `.bin`、`.nfc` 文件，也能直接从文本或 JSON 文件中取得 amiibo ID。根据选择的模式，脚本会解析源数据并在需要时进行解密，然后重新加密并写入目标格式。除纯粹的 bin 与 nfc 转换外，所有操作都要求脚本目录下存在 `unfixed-info.bin` 与 `locked-secret.bin`（或合并后的 `key_retail.bin`）以完成加解密。

在生成文件时，AmiiboConverter 会保持输入文件的目录结构，也可以写入指定的输出目录。可选的 UID 随机化功能会在解锁 amiibo 数据后生成新的 UID 并重新加密，配合 "duplicate" 参数可以一次性生成多份带不同 UID 的文件。

整体流程如下：
1. 解析命令行参数并确定工作模式；
2. 扫描输入路径或读取给定的 ID/JSON；
3. 如果需要，加载密钥并解密 amiibo 数据；
4. 随机化 UID 或根据 ID 创建新的 amiibo dump；
5. 按指定格式重新加密并输出到文件。
