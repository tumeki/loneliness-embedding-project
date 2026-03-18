# 孤独研究プロジェクト — Claude Code 指示書

最終更新：2026-03-18

---

## 研究概要

**修論タイトル（仮）**：日本語における孤独概念の意味空間分析

「孤独」という概念が、個人・社会集団・時代によってどのような差異を持ち、どのように変化・変容してきたかを、先行研究のレビューと、複数のコーパスにおける計算言語学的分析を通じて明らかにする。

孤独・孤立・孤高の三概念は「分類ラベル」ではなく、意味空間における**方向ベクトル**として扱う。孤独は「定義できる対象」ではなく「意味が分散したネットワーク」として存在するという分散意味論の立場（Wittgenstein → Firth/Harris → 認知言語学 → Word2Vec）をとる。

---

## 三概念の理論的位置づけ

| 概念 | 英語対応 | 次元 | 主要理論的根拠 |
|------|----------|------|----------------|
| 孤独 | Loneliness | 主観的・情緒的 | Weiss 1973, UCLA Loneliness Scale 3rd ed. |
| 孤立 | Isolation | 構造的・社会的 | De Jong Gierveld Scale, Putnam 2000 |
| 孤高 | Solitude | 選択的・自律的 | Arendt 1958, Riesman 1950, LACA |

---

## RQ・仮説

**中心的RQ：** 日本語における「孤独」は、書き言葉・話し言葉において意味空間上どのように立ち現れる現象なのか

**個別RQ：**
- Loneliness / Isolation / Solitudeの三次元で見たとき、近代〜現代において「孤独」の語りはどのように変化してきたか
- 孤独の意味構造には、歴史的変動層と構造的安定層が存在するか
- YouTubeにおいて、孤独はどのような人々によってどのように表現・受容・消費されているか
- 孤食という実践を通じて、孤独に食べることはYouTube上でどのように語られているか

**主要仮説：**
- 日本語では孤独・孤立・孤高が語彙・意味上で分化していない
- 孤独の意味空間上の位置は時代によって変動している（孤立→孤独→孤高の意味の堆積）
- 孤独の意味空間上の位置は文化圏ごとに差がある（日本語圏・英語圏・韓国語圏）
- 孤独の意味空間上の位置は媒体ごとに差がある（書籍・YouTube）

---

## 分析設計とコーパス計画

| ステップ | 内容 |
|----------|------|
| Step 0 | 青空文庫（予備分析・パイプライン検証） |
| Step 1 | BCCWJ全量取得・媒体×年代でサブコーパス作成 |
| Step 2 | Word2Vec / BERT学習、7軸による意味空間分析 |
| Step 3 | YouTubeコメントコーパスとの意味空間比較 |
| Step 4 | 英語圏・韓国語圏コーパスとの比較（将来的拡張） |

---

## 確定済みSeed Words（7軸）

### 第一層：孤独固有の三軸

**軸1 Loneliness ↔ Companionship**（情緒的次元）
- 正極：寂しい、空虚、心細い、憂鬱、憂い、煩悶
- 負極：充実、心強い、慰む、親睦、安堵、温もり

**軸2 Isolation ↔ Belonging**（構造的次元）
- 正極：孤立、断絶、隔絶、疎外、排除
- 負極：交わり、親交、有縁、縁故

**軸3 Solitude ↔ Conformity**（自律的次元）
- 正極：孤高、独立、隠遁、独善、隠棲、高潔
- 負極：従順、出仕、媚びる

### 第二層：普遍的社会次元（Kozlowski et al. 2019準拠）

**軸4 Valence 苦痛↔快** / 正極：苦しい、辛い、悲しい　負極：楽しい、嬉しい

**軸5 Agency 強制↔選択** / 正極：強制、束縛、服従、拘束、圧迫　負極：自由、意志、決意、自発、選択

**軸6 Gender 男性↔女性** / 正極：男性、少年、紳士、青年、息子、彼、僕、俺　負極：女性、少女、乙女、祖母、女児、彼女

**軸7 Status 高地位↔低地位** / 正極：高貴、貴族　負極：貧しい、卑しい、下僕

Seed word設計の検証は三層で実施：心理測定尺度（UCLA / DJG / LACA）→ 分類語彙表（WLSP）→ 先行計算言語学研究（Kozlowski et al. 2019）

---

## 方法論上の注意事項

- **Word2Vec選択の正当化**：研究対象は「語の関係的構造（習慣的使用パターン）」であり、文脈内での個別的意味分布（BERTが対象とするもの）ではない。静的埋め込みは分散意味論系譜上にあり、本研究の問いに適合する
- **時代比較**：Hamilton et al. 2016スタイルの静的埋め込み時系列比較を採用
- **Belongingは孤立の負極**、**Companionshipは孤独の負極**（Weiss 1973の区分に準拠）

---

## 技術スタック

| 役割 | ツール |
|------|--------|
| 実行環境 | Google Colab（大学Google Workspace） |
| バージョン管理 | GitHub（public）`github.com/tumeki/loneliness-embedding-project` |
| 形態素解析 | fugashi + unidic-lite |
| 埋め込み | gensim Word2Vec |
| 次元削減・可視化 | UMAP、matplotlib |
| 言語資源 | 分類語彙表（WLSP）`https://raw.githubusercontent.com/masayu-a/WLSP/master/bunruidb.txt` |

---

## ファイル構成

```
loneliness-embedding-project/
├── notebooks/
│   └── aozora/
│       └── 01_aozora_analysis.ipynb   # 青空文庫予備分析
├── docs/
│   ├── setup_guide.md
│   └── research_notes.md
├── data/                               # .gitignore済み
│   ├── raw/
│   └── processed/
├── CLAUDE.md
├── README.md
├── requirements.txt
└── .gitignore
```

---

## 命名規則・コーディング規約

- スクリプト・ノートブック：番号プレフィックス（`01_xxx`, `02_xxx`）
- 変数：snake_case
- 乱数シード：42（再現性統一）
- `data/raw/` および `data/processed/` はgit管理外（.gitignore済み）

---

## 主要参照文献

- Kozlowski, A. C., Taddy, M., & Evans, J. A. (2019). The geometry of culture. *American Sociological Review.*
- Hamilton, W. L., Leskovec, J., & Jurafsky, D. (2016). Diachronic word embeddings. *ACL.*
- Weiss, R. S. (1973). *Loneliness: The experience of emotional and social isolation.*
- De Jong Gierveld, J. (1985). Loneliness and the degree of intimacy in interpersonal relationships.
- Arendt, H. (1958). *The Human Condition.*
- Riesman, D. (1950). *The Lonely Crowd.*
- Putnam, R. D. (2000). *Bowling Alone.*
- 国立国語研究所（2004）分類語彙表（WLSP）
