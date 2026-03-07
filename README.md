# loneliness-embedding-project

日本語コーパスにおける「孤独」概念の意味変容・意味構造分析プロジェクト（修士論文）

## 概要

「孤独」という概念が、時代・メディア・社会集団によってどのように異なる意味を持ち、
どのように変容してきたかを、コーパス言語学的手法と単語埋め込みによって明らかにする。

### 三分類フレームワーク

| 概念 | 水準 | 系譜 |
|------|------|------|
| **Loneliness**（主観的孤独） | 感情・心理 | Weiss, Cacioppo |
| **Isolation**（社会的孤立） | 構造・ネットワーク | Durkheim, Putnam |
| **Solitude**（選択的孤高） | 実践・価値づけ | Thoreau, Winnicott |

## 分析コーパス

- **Phase 1**：青空文庫（予備分析・手法確認）
- **Phase 2**：現代日本語書き言葉均衡コーパス BCCWJ（本分析）
- **Phase 3**：YouTube コメント（SNS受容分析）

## 環境

Google Colab + GitHub によるノートブック管理。

```bash
# ローカル実行の場合
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## ディレクトリ

```
notebooks/   # 分析ノートブック（Colab）
scripts/     # 再利用可能なスクリプト
data/        # raw・processed（gitignore済み）
docs/        # 研究メモ・文献整理
results/     # 図表・出力（gitignore済み）
```

## 注意

- `data/raw/`, `data/processed/`, `results/` はgit管理外
- BCCWJデータは国立国語研究所の利用規約に従い非公開
