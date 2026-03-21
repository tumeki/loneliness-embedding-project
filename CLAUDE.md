# CLAUDE

# 孤独研究プロジェクト — Claude Code 指示書

最終更新：2026-03-21

---

## 研究概要

**修論タイトル（仮）**：日本語における孤独概念の意味空間分析

本研究は、日本語コーパスにおける「孤独」概念の意味空間上の構造を、単語埋め込みモデル（Word2Vec）および文脈化埋め込みモデル（BERT）を用いて明らかにすることを目的とする。主要データは『現代日本語書き言葉均衡コーパス』（BCCWJ）。

理論的立場は**分散意味論**（Firth 1957 → Harris 1954 → Word2Vec）に基づく。語の意味は文脈的共起パターンから創発するという用法基盤モデル（Langacker, 1987; Bybee, 2010）の立場をとり、孤独・孤立・孤高の三概念を「分類ラベル」ではなく、意味空間における**方向ベクトル**として扱う。

**Main Claim：** 日本語における「孤独」概念は語彙・意味レベルで未分化でありつつも、意味空間上では一定の構造的特徴が観察される。その構造には、通時的に安定した**構造的安定層**と、時代ごとの社会変動を反映して移動・変質する**歴史的変動層**が存在する。

---

## 三概念の理論的位置づけ

| 概念 | 英語対応 | 次元 | 主要理論的根拠 |
| --- | --- | --- | --- |
| 孤独 | Loneliness | 主観的・情緒的 | Weiss 1973, Perlman & Peplau 1979, UCLA Loneliness Scale 3rd ed. |
| 孤立 | Isolation | 構造的・社会的 | De Jong Gierveld Scale, Putnam 2000 |
| 孤高 | Solitude | 選択的・自律的 | Arendt 1958, Riesman 1950, LACA |

---

## RQ・仮説

**中心的RQ：** 日本語における「孤独」は、書き言葉において意味空間上どのような構造をもち、どのように変容してきたか

**個別RQ（修論スコープ）：**
- Loneliness / Isolation / Solitudeの三次元で見たとき、近代〜現代において「孤独」の語りはどのように変化してきたか
- 孤独の意味構造には、歴史的変動層と構造的安定層が存在するか
- 社会的属性・階層（Gender / Status軸）と孤独概念の意味空間上の位置との間に構造的関係があるか

**将来的な拡張（修論スコープ外）：**
- YouTubeにおいて、孤独はどのような人々によってどのように表現・受容・消費されているか
- 孤食という実践を通じて、孤独に食べることはYouTube上でどのように語られているか
- 孤独の意味空間上の位置は文化圏ごとに差があるか（日本語圏・英語圏・韓国語圏）

**主要仮説：**
- 日本語では孤独・孤立・孤高が語彙・意味上で分化していない（未分化仮説）
- 孤独の意味空間上の構造は構造的安定層と歴史的変動層の二層で記述できる
- 孤独の意味空間上の位置は時代によって変動している（孤立→孤独→孤高の意味の堆積）
- 孤独の意味空間上の位置は媒体・ジャンルごとに差がある

---

## 分析設計とコーパス計画

> **修論スコープ：Step 1・Step 2 の範囲とする**（Step 3 以降は将来的な拡張として位置づけ）
> 

| ステップ | 内容 |
| --- | --- |
| Step 0 | 青空文庫（予備分析・パイプライン検証） |
| Step 1 | BCCWJ全量取得・媒体×年代でサブコーパス作成 |
| Step 2 | Word2Vec / BERT学習、7軸による意味空間分析（構造的安定層・歴史的変動層の記述） |
| Step 3 | YouTubeコメントコーパスとの意味空間比較（将来的拡張） |
| Step 4 | 英語圏・韓国語圏コーパスとの比較（将来的拡張） |

---

## 確定済みSeed Words（7軸）

### 第一層：孤独概念の内部構造（問い：この孤独はどの種類か）

**軸1 Loneliness ↔︎ Companionship**（情緒的次元）
- 正極：寂しい、空虚、心細い、憂鬱、憂い、煩悶
- 負極：充実、心強い、慰む、親睦、安堵、温もり

**軸2 Isolation ↔︎ Belonging**（構造的次元）
- 正極：孤立、断絶、隔絶、疎外、排除
- 負極：交わり、親交、有縁、縁故

**軸3 Solitude ↔︎ Conformity**（自律的次元）
- 正極：孤高、独立、隠遁、独善、隠棲、高潔
- 負極：従順、出仕、媚びる

### 第二層：孤独の意味様態の補助次元 / auxiliary dimensions（問い：その孤独はどちらに向いているか）

第一層の三分類仮説を実証するための検証軸。孤独研究固有の理論（Weiss 1973 / Arendt 1958 等）から導出。概念内部の構造を記述し、**三分類の実証的根拠**として機能する。

**軸4 Valence 苦痛↔︎快** / 正極：苦しい、辛い、悲しい　負極：楽しい、嬉しい

**軸5 Agency 強制↔︎選択** / 正極：強制、束縛、服従、拘束、圧迫　負極：自由、意志、決意、自発、選択

### 第三層：社会的意味空間における位置（問い：その孤独は誰のものか）

社会が意味を構造化する軸。Kozlowski et al. 2019 の枠組みに準拠。「孤高は男性的か」「孤独は低地位的か」という問いへの答えとして、孤独の社会的意味位置を記述する。

**軸6 Gender 男性↔︎女性** / 正極：男性、少年、紳士、青年、息子、彼、僕、俺　負極：女性、少女、乙女、祖母、女児、彼女

**軸7 Status 高地位↔︎低地位** / 正極：高貴、貴族　負極：貧しい、卑しい、下僕

Seed word設計の検証は三層で実施：心理測定尺度（UCLA / DJG / LACA）→ 分類語彙表（WLSP）→ 先行計算言語学研究（Kozlowski et al. 2019）

---

## 方法論上の注意事項

- **Word2Vec選択の正当化**：研究対象は「語の関係的構造（習慣的使用パターン）」。分布仮説（Firth 1957, Harris 1954）を計算論的に実装した静的埋め込みは、意味の通時的比較（Hamilton et al. 2016スタイル）に適合し、本研究の問いに整合する
- **BERT併用の位置づけ**：文脈化埋め込みとして補完的に使用。Word2Vecが「型としての意味構造（習慣的共起）」を捉えるのに対し、BERTは文脈依存的な意味分布の把握に用いる
- **時代比較**：Hamilton et al. 2016スタイルの静的埋め込み時系列比較を採用
- **Belongingは孤立の負極**、**Companionshipは孤独の負極**（Weiss 1973の区分に準拠）

---

## 技術スタック

| 役割 | ツール |
| --- | --- |
| 実行環境 | Google Colab（大学Google Workspace） |
| バージョン管理 | GitHub（public）`github.com/tumeki/loneliness-embedding-project` |
| 形態素解析 | fugashi + unidic-lite |
| 静的埋め込み | gensim Word2Vec |
| 文脈化埋め込み | BERT（`cl-tohoku/bert-base-japanese-whole-word-masking`） |
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
- Perlman, D., & Peplau, L. A. (1979). Toward a social psychology of loneliness. *Social Exchange in Developing Relationships.*
- De Jong Gierveld, J. (1985). Loneliness and the degree of intimacy in interpersonal relationships.
- Arendt, H. (1958). *The Human Condition.*
- Riesman, D. (1950). *The Lonely Crowd.*
- Putnam, R. D. (2000). *Bowling Alone.*
- Van de Velde, C. (2026). Sociology of Loneliness: An Introduction. *Acta Sociologica*, 69(1): 3–18.
- 五十嵐祐（2024）日本における孤独・孤立研究の現状と課題：研究動向と測定の問題を中心として.
- 国立国語研究所（2004）分類語彙表（WLSP）