# 孤独研究プロジェクト — Claude Code 指示書

## 研究概要

日本語コーパスにおける「孤独」概念の意味変容・意味構造を、
単語・文章埋め込み（Word2Vec / Sentence-BERT）によって明らかにする修士論文プロジェクト。

主な問い：
- 日本語の「孤独」は意味空間上でどのように立ち現れるか
- 孤独の意味は時代によって変動しているか（歴史変動層 vs 構造的安定層）
- 書き言葉・話し言葉・SNSで意味空間はどう異なるか

## 三分類（分析の核心軸）

| ラベル | 概念 | 水準 | 系譜 |
|--------|------|------|------|
| Loneliness | 主観的孤独（心理） | 感情・知覚 | Weiss, Cacioppo, UCLA尺度 |
| Isolation | 社会的孤立（構造） | ネットワーク・配置 | Durkheim, Putnam |
| Solitude | 選択的孤高（実践） | 自発性・価値づけ | Thoreau, Winnicott, Arendt |

**重要**：この三分類は「教師ラベル」ではなく「意味空間上の方向ベクトル」として扱う。
辞書＝分類器ではなく、辞書＝意味空間のナビゲーション装置。

## 分析フェーズ

### Phase 1（現在）：青空文庫での予備分析
- 目的：手法の習得・パイプラインの構築
- データ：青空文庫（明治〜昭和〜戦後の文学テキスト）
- 主な分析：
  1. 孤独関連語の時代別意味変化（Word2Vec）
  2. 孤独・孤立・孤高の共起語比較
  3. 埋め込み可視化（UMAP / t-SNE）
  4. Loneliness / Isolation / Solitude 方向ベクトルの試作

### Phase 2（BCCWJ取得後）：本分析
- 均衡コーパスでの本格的通時分析
- 媒体×年代のサブコーパス比較

### Phase 3：YouTubeコメント分析
- 孤食動画のコメントにおける孤独の語られ方
- 表現（動画）× 受容（コメント）× 露出面の比較

## 実行環境

Google Colab をメインに使用（GPUランタイム推奨）。
ノートブックは `notebooks/` に保存してGitHub管理。

### 主要ライブラリ
```
gensim          # Word2Vec
fugashi + unidic # MeCab形態素解析（Colab対応）
sentence-transformers  # Sentence-BERT
umap-learn      # 次元削減・可視化
matplotlib / seaborn
pandas / numpy
```

### インストールコマンド（Colabセル先頭）
```python
!pip install fugashi unidic-lite gensim umap-learn sentence-transformers -q
```

## ディレクトリ構造

```
loneliness-embedding-project/
├── CLAUDE.md           # この指示書
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   ├── raw/            # gitignore済み
│   │   ├── aozora/
│   │   ├── bccwj/
│   │   └── youtube/
│   └── processed/      # gitignore済み
│       ├── aozora/
│       ├── bccwj/
│       └── youtube/
│
├── scripts/
│   ├── aozora/
│   │   ├── 01_download.py      # 青空文庫取得
│   │   ├── 02_preprocess.py    # 前処理・トークナイズ
│   │   └── 03_train_w2v.py     # Word2Vec学習
│   ├── bccwj/
│   └── utils/
│       ├── text_cleaner.py     # テキスト正規化共通処理
│       └── embed_utils.py      # 埋め込み共通処理
│
├── notebooks/
│   ├── aozora/
│   │   ├── 01_data_exploration.ipynb
│   │   ├── 02_word2vec_training.ipynb
│   │   └── 03_embedding_visualization.ipynb
│   └── bccwj/
│
├── results/            # gitignore済み（ローカル・Driveに保存）
│
└── docs/
    ├── research_notes.md   # 分析メモ・気づき
    └── references.md       # 文献整理
```

## コーディング規則

- ファイル名：番号プレフィックス（01_, 02_, ...）
- 変数名：snake_case
- 乱数シード：`RANDOM_SEED = 42` で統一（再現性確保）
- コメント：日本語でOK（研究ノート的に残す）
- 各ノートブックの先頭に「このノートブックの目的」を Markdown で記載

## よく使うキーワード集

孤独語彙（分析対象の中心）：
- 孤独、孤立、孤高、寂しさ、さみしい、ひとり、独り、一人
- 疎外、断絶、虚しさ、空虚、取り残される
- 静謐、内省、自由、ひとり時間（Solitude側）

共起で見たい文脈語：
- 感情：悲しみ、苦しみ、安らぎ、平和、恐れ
- 社会：家族、友人、群衆、都市、社会、共同体
- 実践：食べる、飲む、眠る、歩く、読む

## 注意事項

1. raw dataはgit管理外。GitHubにはコード・ノートブック・ドキュメントのみpush
2. 大きなモデルファイル（.bin, .model）もgit管理外
3. 結果の図表はresults/にローカル保存し、論文用はdocs/に整理
4. BCCWJのデータは利用規約に従い、外部共有・公開リポジトリへのアップ不可
