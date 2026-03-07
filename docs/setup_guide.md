# セットアップ・運用ガイド

## GitHubとColabの連携

### 1. GitHubからColabで開く

ColabはGitHubのノートブックを直接開ける。

```
https://colab.research.google.com/github/tumeki/loneliness-embedding-project/blob/main/notebooks/aozora/01_aozora_analysis.ipynb
```

または Colab を開いた後、
`ファイル → GitHubからノートブックを開く`
からリポジトリを指定。

---

### 2. Colabでの作業後にGitHubへpushする

Colab上で編集したノートブックをGitHubに反映するには：

**方法A（推奨）：Google DriveにCloneしてCLIで管理**

```python
# Colabのセルで実行
from google.colab import drive
drive.mount('/content/drive')

# Google DriveにCloneしておく（初回のみ）
!git clone https://github.com/tumeki/loneliness-embedding-project.git \
    /content/drive/MyDrive/loneliness-embedding-project
```

作業後：
```python
import os
os.chdir('/content/drive/MyDrive/loneliness-embedding-project')

!git config user.email "your@email.com"
!git config user.name "Your Name"
!git add notebooks/
!git commit -m "aozora: Word2Vec初期実験"
!git push
```

**方法B：Colabのメニューから直接保存**
`ファイル → GitHubにコピーを保存`
でPRやコミットメッセージを指定して保存できる。

---

## データの扱い方

### raw データは Google Drive に保存する

```python
# Colabの先頭で実行
from google.colab import drive
drive.mount('/content/drive')

# データ保存先をGoogle Driveに変更
DATA_DIR = Path('/content/drive/MyDrive/loneliness-research-data')
RAW_DIR = DATA_DIR / 'raw' / 'aozora'
PROCESSED_DIR = DATA_DIR / 'processed' / 'aozora'
RAW_DIR.mkdir(parents=True, exist_ok=True)
PROCESSED_DIR.mkdir(parents=True, exist_ok=True)
```

こうすることで、Colabのセッションが切れてもデータが消えない。

---

## Claude Codeの使い方

Claude Code はターミナルから呼び出せるCLIツール。
スクリプトの自動生成・修正・デバッグに使う。

```bash
# インストール
npm install -g @anthropic-ai/claude-code

# プロジェクトルートで起動
cd loneliness-embedding-project
claude
```

起動後、Claude は `CLAUDE.md` を読み込み、
プロジェクトのコンテキストを自動的に把握する。

**活用例：**
```
> scripts/aozora/02_preprocess.py の形態素解析部分をリファクタリングして
> 孤独語を含む文だけを抽出するフィルタを追加して
> 昨日のエラーを修正して（エラーログをペーストする）
```

---

## ディレクトリ管理のルール

| 場所 | 管理方法 | 内容 |
|------|----------|------|
| `notebooks/` | Git管理 | Colabノートブック |
| `scripts/` | Git管理 | 再利用スクリプト |
| `docs/` | Git管理 | メモ・文献整理 |
| `data/raw/` | Google Drive | 生データ（Git対象外） |
| `data/processed/` | Google Drive | 処理済みデータ（Git対象外） |
| `results/` | Google Drive | 図表・出力（Git対象外） |

---

## コミットメッセージの規則

```
[コーパス]: 内容の一言メモ

例：
aozora: Word2Vec初期実験・UMAP可視化追加
aozora: 時代別モデル比較（明治〜昭和）
bccwj: 前処理パイプライン実装
docs: 研究メモ更新（指導教官コメント反映）
```
