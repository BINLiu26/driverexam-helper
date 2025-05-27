# 🚗 C1 科目一题库抓取器

> **自动同步中国大陆 C1 驾照科目一（交规理论考试）最新题库**
> 数据来源：*极速数据·DriverExam* 官方接口（与公安部题库保持每日同步）。

---

## 功能亮点

| 能力         | 说明                                                                    |
| ---------- | --------------------------------------------------------------------- |
| **实时更新**   | 调用官方 API，题库更新后 24 h 内自动同步。                                            |
| **离线可用**   | 同时保存为 `questions.jsonl` 与 `questions.csv`，可导入 Anki / Quizlet 或自行开发前端。 |
| **零依赖复杂度** | 仅需 `requests`、`pandas`、`tqdm` 三个第三方库。                                 |
| **温和请求**   | 分页抓取并 `sleep 0.3 s`，避免触发 QPS 限制。                                      |
| **配置灵活**   | 一行参数即可切换驾照类型（A1/B2…）或科目（1/4）。                                         |

---

## 快速开始

```bash
# 1️⃣ 建议创建独立虚拟环境
python3 -m venv venv
source venv/bin/activate      # Windows → venv\Scripts\activate

# 2️⃣ 安装依赖
pip install -U pip requests pandas tqdm

# 3️⃣ 运行脚本
python fetch_c1_subject1_bank.py --appkey 你的APPKEY
```

> **如何获取 APPKEY？**
> 访问 [极速数据·驾考题库接口](https://www.jisuapi.com/api/driverexam/) 注册账号，领取个人免费密钥（每日 100 次调用）。

执行后，将得到以下目录结构：

```text
output/
├── questions.jsonl   # 一行一个 JSON 原始记录
└── questions.csv     # 扁平化表格，可用 Excel / Pandas 浏览
```

---

## 命令行参数

| 参数           | 默认值      | 作用              |
| ------------ | -------- | --------------- |
| `--appkey`   | *(必填)*   | 你的极速数据 API Key。 |
| `--outdir`   | `output` | 保存文件夹路径。        |
| `--pagesize` | `50`     | 分页条数（≤ 50 为佳）。  |

示例：自定义输出目录并随机顺序抓取

```bash
python fetch_c1_subject1_bank.py \
  --appkey $MY_KEY \
  --outdir data/$(date +%F) \
  --pagesize 40
```

若需抓取 **科目四**，只需改动脚本内参数：

```python
params = {
    "type": "C1",
    "subject": 4,  # 修改这里
}
```

---

## 安全提示

请勿把 `APPKEY` 直接提交到公开仓库，可采用环境变量或 `.env`：

```bash
export DRIVEREXAM_APPKEY="abcdef123456"
```

---

## Roadmap

* [ ] 🖥️ 提供简洁的 CLI 练题模式（TUI）。
* [ ] 📦 发布 PyPI 包，一行命令即可安装。
* [ ] 🌐 构建轻量级 Web 前端展示题库。
* [ ] 📝 自动生成 Anki `apkg` 导入包。

欢迎 PR / Issue 交流想法！

---

## 许可证

MIT License © 2025 \[Bin Liu]

> 本项目仅供个人学习与备考示范。任何商业化使用，请遵守《极速数据用户协议》及当地法律法规。
