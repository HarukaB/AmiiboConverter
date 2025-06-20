# 使用教程

## 环境准备
1. 安装 Python 3.8 及以上版本；
2. 在仓库目录执行 `pip install -r requirements.txt` 安装依赖；
3. 若需要生成新的 amiibo 文件或随机 UID，请准备 `unfixed-info.bin` 与 `locked-secret.bin`（或 `key_retail.bin`）并放在脚本所在目录。

## 基本用法
在终端中运行：

```bash
python AmiiboConverter.py -m <模式> -i <输入> [选项]
```

### 可选模式
- `bin2bin`
- `bin2nfc`
- `id2bin`
- `id2nfc`
- `nfc2bin`
- `nfc2nfc`
- `json2bin`
- `json2nfc`

### 主要参数
- `-i` / `--input`：待处理的文件、文件夹或 amiibo ID；多个输入以空格分隔；
- `-o` / `--output`：输出目录或文件，若省略则与输入位置相同；
- `-r` / `--random-uid`：随机化输出文件的 UID；
- `-d` / `--duplicate-files`：为每个输入生成多份结果，启用时自动随机 UID；
- `-v`：输出更多运行信息，`-vv` 显示调试信息；
- `-h`：显示帮助。

### 实例
```bash
python AmiiboConverter.py -m bin2nfc -i bin -o nfc
python AmiiboConverter.py -m id2bin -i id.txt -d 3
python AmiiboConverter.py -m json2nfc -i mario.json -o nfc -d 3
```

在以 amiibo ID 作为输入时，可以在 ID 前加上名称并以冒号分隔，如 `Luigi:0x00010000...`。若只提供 ID，则生成文件名也将使用该 ID。
