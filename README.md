# aipojie
aipojie 
# 🚀 tulinTron 波场靓号生成器 使用指南 (v3.4)  免授权

[📖 English](README.md)

> 基于 CUDA GPU 加速的Tron靓号生成工具 | 全网速度最快 | 离线生成无后门

---

## 📋 环境要求

| 项目 | 要求 |
|------|------|
| 操作系统 | Windows 10/11 或 Linux (Ubuntu 20.04+) |
| CUDA 版本 | 12.4 或更高 |
| 显卡架构 | 全系 NVIDIA 显卡适配 (GTX 10 / RTX 20/30/40/50 / A系列 / H系列) |
| 显卡驱动 | 最新 NVIDIA 驱动 |

> 下载 CUDA Toolkit: [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads)

---

## 🎯 快速开始

将 `tulinTron.exe` (Windows) 或 `tulinTron` (Linux) 放在任意目录，打开命令行即可运行。

---

## 📖 全部参数一览

| 参数 | 说明 | 示例 |
|------|------|------|
| `-l N` | 靓号/豹子模式：生成末尾 N 位相同字符的地址 | `-l 7` |
| `-lf N` | 伪靓号模式：生成末尾 N 位视觉相似的地址（大小写混合） | `-lf 7` |
| `-s N` | 顺子模式：生成末尾 N 位连续字符的地址 | `-s 5` |
| `-sn N` | 数字顺子模式：生成末尾 N 位纯数字连续地址（速度极快） | `-sn 8` |
| `-n N` | 数字模式：生成末尾 N 位纯数字地址 | `-n 15` |
| `-ln N` | 数字靓号模式：生成末尾 N 位相同数字的地址 | `-ln 7` |
| `-m FILE` | 匹配模式：根据规则文件进行前后缀精准匹配（最多32条规则） | `-m p.txt` |
| `-auto` | 智能模式：在任意模式后追加，提升出货率 | `-l 9 -auto` |
| `-ar N` | 靓号模式高级参数 | `-ar 1` |
| `-k` | 私钥加密模式：生成结果自动加密存储（启动后输入密码） | `-l 8 -k` |
| `--decrypt` | 解密模式：解密加密的结果文件 | `--decrypt -i result.txt` |
| `-i FILE` | 解密模式输入文件 | `-i result.txt` |
| `-o FILE` | 解密模式输出文件（默认 decrypted.txt） | `-o my_keys.txt` |
| `--pubkey FILE` | 使用 RSA 公钥加密生成的私钥 | `--pubkey public_key.pem` |
| `-p PORT` | 🚧 API 模式监听端口（后续版本将支持） | `-p 8081` |
| `--api` | 🚧 开启 API 服务模式（后续版本将支持） | `--api` |
| `--token TOKEN` | 🚧 API 认证令牌（后续版本将支持） | `--token my_secret_token` |
| `--master URL` | 🚧 集群模式（后续版本将支持） | `--master http://127.0.0.1:8000` |
| `--transfer` | 🚧 移机授权（后续版本将支持） | `--transfer` |

---

## 🔧 各模式详细用法

### 1. 靓号模式（豹子号） `-l`

生成末尾 N 位完全相同的地址，例如 `T...88888888`：

```bash
# Windows
tulinTron.exe -l 7

# Linux
./tulinTron -l 7

# 开启智能模式，提高出货率
tulinTron.exe -l 9 -auto
```

---

### 2. 伪靓号模式 `-lf`

生成末尾 N 位视觉上相似的地址（大小写字母混合），例如 `T...AAAaaAAa`：

```bash
tulinTron.exe -lf 7
```

---

### 3. 顺子模式 `-s`

生成末尾 N 位连续字符的地址，例如 `T...12345678` 或 `T...abcdefgh`：

```bash
tulinTron.exe -s 5
```

---

### 4. 数字顺子模式 `-sn`

生成末尾 N 位纯数字连续的地址（针对性算法优化，速度极快）：

```bash
tulinTron.exe -sn 8
```

---

### 5. 纯数字模式 `-n`

生成末尾 N 位纯数字地址：

```bash
# 生成末尾 15 位纯数字
tulinTron.exe -n 15

# 生成末尾 10 位纯数字
tulinTron.exe -n 10
```

---

### 6. 数字靓号模式 `-ln`

生成末尾 N 位相同数字的地址，例如 `T...7777777`：

```bash
tulinTron.exe -ln 7
```

---

### 7. 匹配模式 `-m`

根据规则文件 `p.txt` 进行前后缀精准匹配，最多支持 32 条规则同时并行：

**p.txt 格式：**
```
前缀*后缀
```
每行一个规则，`*` 前面是前缀，后面是后缀。

**示例 p.txt：**
```
TABC*XYZ
T888*666
T999*999
T*123456
```

**运行：**
```bash
tulinTron.exe -m p.txt
```

---

### 8. 多模同开（组合模式）

多个模式可以同时运行，算力零损耗，一网打尽：

```bash
# 同时运行：匹配 + 8位豹子 + 9位顺子 + 15位纯数字
tulinTron.exe -m p.txt -l 8 -s 9 -n 15

# 靓号 + 匹配
tulinTron.exe -m p.txt -l 9

# 靓号 + 数字顺子
tulinTron.exe -sn 9 -l 9

# 全模式开启（匹配 + 靓号 + 纯数字 + 顺子 + 数字顺子）
tulinTron.exe -m p.txt -l 6 -n 10 -s 6 -sn 6
```

---

### 9. 私钥加密模式 `-k`

启动后提示输入密码（输入时不显示字符，防止偷窥），生成的私钥将以加密形式存储：

```bash
tulinTron.exe -l 8 -k
# 按提示输入密码（屏幕上不显示），回车确认
```

---

### 10. 解密模式 `--decrypt`

将加密的结果文件解密还原：

```bash
tulinTron.exe --decrypt -i result.txt
# 按提示输入之前设置的密码
# 解密结果输出到 decrypted.txt

# 指定输出文件名
tulinTron.exe --decrypt -i result.txt -o my_keys.txt
```

> ⚠️ 密码错误时解密出来的私钥将是乱码，请务必记住密码！

---

### 11. RSA 公钥加密 `--pubkey`

使用 RSA 公钥加密生成的私钥，比密码模式更安全：

**生成 RSA 证书（需要 openssl 环境）：**
```bash
# 生成 2048 位私钥
openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048

# 根据私钥导出公钥
openssl rsa -pubout -in private_key.pem -out public_key.pem
```

**使用公钥加密生成：**
```bash
tulinTron.exe -n 10 --pubkey public_key.pem
```

---

### 12. API 模式 🚧

> ⏳ 后续版本将支持

以 HTTP API 服务方式运行，供其他程序调用。

---

### 13. 集群模式 🚧

> ⏳ 后续版本将支持

多台机器协同工作，连接到主节点统一调度。

---

### 14. 移机授权

更换机器时进行授权迁移：

```bash
tulinTron.exe --transfer
```

---

## ⚡ 性能参考 (Benchmarks)

测试环境：CUDA 12.6，暴力匹配模式

| 显卡型号 | 算力 (暴力模式) |
|----------|----------------|
| NVIDIA RTX 5090 | 8.0 GKey/s (80亿/秒) |
| NVIDIA RTX 4090 | 6.2 GKey/s (62亿/秒) |
| NVIDIA RTX 4060 Ti | 1.7 GKey/s (17亿/秒) |

### 产出时间估算（单卡 4090 暴力模式）

| 目标 | 预计时间 |
|------|----------|
| 8A 豹子 (末尾8位相同) | ~5.5 分钟 |
| 9A 豹子 (末尾9位相同) | ~5.3 小时 |
| 10A 豹子 (末尾10位相同) | ~13 天 |

> 公式：T(秒) = 58^(N-1) / (算力 × 1,000,000)
> 多卡并行算力线性叠加，实际时间受运气影响可能有所浮动。

---

## 📁 输出文件说明

生成结果自动分类保存至 `Result/` 目录：

| 文件类型 | 文件名格式 | 说明 |
|----------|-----------|------|
| 豹子号 | `X_A.txt` | 末尾相同字符 |
| 顺子号 | `X_S.txt` | 末尾连续字符 |
| 匹配号 | `X_M.txt` | 规则匹配结果 |
| 纯数字 | `X_N.txt` | 末尾纯数字 |

> 结果文件包含：地址 + 私钥，请妥善保管！

---

## ⚠️ 注意事项

1. **离线运行**：本工具可 100% 物理断网使用，私钥永不触网。
2. **私钥安全**：请务必妥善保存生成的 `Result/*.txt` 文件，丢失无法找回。
3. **高净值账户**：强烈建议配合多签钱包使用。
4. **仅限合法用途**：本工具仅用于技术交流、密码学研究与安全教育，请勿用于任何非法用途。
5. **显卡散热**：长时间运行时请注意显卡温度，确保良好散热环境。

---

## 🆘 常见问题

**Q: 运行提示缺少 CUDA 相关 DLL？**
A: 请安装 CUDA Toolkit 12.4 或更高版本。

**Q: 加密后忘记密码怎么办？**
A: 密码无法找回，加密后的私钥没有密码将永久无法解密，务必妥善保管密码。



**Q: 多显卡如何利用？**
A: 程序自动识别并利用所有可用 NVIDIA GPU，算力线性叠加。

---
