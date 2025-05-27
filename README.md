🚗 C1-Subject1-QuestionBank Fetcher

Automated downloader for the latest China Mainland C1 驾照科目一 (Subject-1) question bank – powered by the public Jisu Data DriverExam API.

⸻

Features

Capability	Details
Up-to-date	Syncs the official question set (公安部最新版) – typically updated within 24 h of the API provider.
Offline-ready	Saves as questions.jsonl and questions.csv; feed into Anki, Quizlet, a web frontend, or your own CLI quizzer.
Minimal deps	Pure-Python ∶ requests, pandas, tqdm only.
Respectful crawl	Uses API pagination & polite rate limiting (sleep 0.3 s/page).
Easily configurable	Change licence type (A1/B2 …) or subject (1/4) with one flag.


⸻

Quick Start

# 1 - create & activate isolated environment (recommended)
python3 -m venv venv
source venv/bin/activate          # Windows → venv\Scripts\activate

# 2 - install dependencies
pip install -U pip requests pandas tqdm

# 3 - run
python fetch_c1_subject1_bank.py --appkey YOUR_APPKEY

Need an appkey? – Register free on 极速数据·驾考题库接口 and copy your personal key (100 req/day on free tier).

Output directory structure:

output/
├── questions.jsonl   # 1 line = 1 raw JSON record
└── questions.csv     # flat table; open in Excel/Calc or Pandas


⸻

CLI Options

Flag	Default	Purpose
--appkey	(required)	Your Jisu Data API key.
--outdir	output	Where to write downloaded files.
--pagesize	50	Page size ≤ 50 recommended by API.

Example – randomised order & custom dir:

python fetch_c1_subject1_bank.py \
  --appkey $JK_APPKEY \
  --outdir data/2025-05-27 \
  --pagesize 40

To fetch Subject 4 for the same licence type:

# edit script constant or fork – minimal diff:
params = {
    "type": "C1",
    "subject": 4,  # ← here
}


⸻

Security Note

Never commit your APPKEY to a public repo. Use environment variables or a local .env file, e.g.:

export DRIVEREXAM_APPKEY="abcdefg123456"  # in ~/.zshrc or .bashrc


⸻

Roadmap
	•	✏️  Wrap into a lightweight CLI quizzer (pytest-style TUI questions).
	•	📦  Publish to PyPI for pip install driverexam-bank one-liner.
	•	🌐  Small React/Vue front-end consuming the JSONL.
	•	📝  Integration with Anki (apkg auto-export).

PRs & ideas welcome – open an issue to discuss.

⸻

License

MIT License © 2025 [Bin Liu]

本仓库仅用于学习 / 个人备考演示。请在任何商业场景中遵守《极速数据用户协议》及当地法规。
