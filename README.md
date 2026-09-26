# English Reading Lab

A lightweight English reading and vocabulary-learning database built from real English articles.

目前第一階段以 **英文新聞（English news articles）** 為主要閱讀來源；未來也可以延伸到其他英文文章、報告或閱讀材料。

這個 Repository 的核心不是保存文章本身，而是從實際閱讀過的英文文章中，挑選真正值得長期學習的：

- **Vocabulary** — 重要、實用、會再次遇到的英文單字與術語
- **Phrases** — 常用片語、collocations 與自然英文搭配

這些資料會提供給未來的 iPad / iOS Widget 與其他英文學習工具直接讀取。

---

## Learning Principle

> Read real English → Understand the context → Extract useful English → Review repeatedly

本專案不是「艱澀單字收藏庫」。

挑選內容時，優先考慮 **實用性、重複出現機率與閱讀價值**，而不是單字有多困難。

### Vocabulary selection

收錄的英文單字／術語必須：

1. **實際出現在本次閱讀的英文文章中。**
2. 對理解文章內容有幫助。
3. 在新聞、商業、科技、國際事件或一般英文閱讀中具有再次遇到的可能性。
4. 適合英文學習者主動記憶與使用。
5. 不因為單字艱澀、罕見或看起來高級就收錄。

優先收錄像 `tariff`、`ceasefire`、`inflation`、`revenue` 這類具有實際閱讀價值的字詞，而不是低頻、文學性或只在特定文章中偶然出現的艱澀單字。

### Phrase selection

片語必須同樣 **實際出現在英文文章中**。

優先收錄：

- 常用片語
- Collocations
- Phrasal expressions
- 新聞常見表達
- 動詞＋名詞的自然搭配
- 可以套用到其他情境的英文表達

例如：

- `reach an agreement`
- `come under pressure`
- `raise concerns over`
- `take effect`
- `pave the way for`

---

## Source Rule

目前新聞學習模式中：

- Vocabulary 必須來自當天選定的 **英文新聞文章原文**。
- Phrases 必須來自當天選定的 **英文新聞文章原文**。
- 中文新聞只用來協助理解相同事件與語意，不作為英文 Vocabulary / Phrase 的來源。
- 不可以因為某個字或片語「跟主題有關」就自行加入；必須能在實際英文文章中找到。

未來若本專案延伸至其他英文文章，原則相同：**學習項目必須來自實際閱讀的英文原文。**

---

## No Duplicates

資料庫不收錄重複 Vocabulary 或 Phrase。

每次新增資料必須遵循：

**Fetch → Check → Build → Merge → Update**

在新增任何項目前：

1. Fetch GitHub 上最新版本的資料庫。
2. 檢查 Vocabulary 是否已存在於 `vocabulary.json`。
3. 檢查 Phrase 是否已存在於 `phrases.json`。
4. 已存在的項目不得再次新增。
5. 只建立真正的新項目。
6. 保留所有既有資料後再 Merge。
7. Update 原本的 Master JSON，不另外建立每日 JSON。

大小寫或基本詞形差異不應被當成不同學習項目。例如文章中的 `Tariffs`，若資料庫已有基本型 `tariff`，就不再次新增。

---

## Repository Structure

```text
english-reading-lab/
├── README.md
├── READING_PROMPT.md
└── data/
    ├── vocabulary.json
    └── phrases.json
```

### `data/vocabulary.json`

保存重要英文單字與術語。

預定資料內容：

```json
{
  "tariff": {
    "definition_en": "a tax imposed on goods imported from another country",
    "zh": "關稅",
    "example_en": "The government introduced new tariffs on imported steel.",
    "example_zh": "政府對進口鋼鐵徵收新的關稅。"
  }
}
```

### `data/phrases.json`

保存常用片語與自然英文搭配。

```json
{
  "reach an agreement": {
    "definition_en": "to successfully come to a shared decision or arrangement",
    "zh": "達成協議",
    "example_en": "The two sides reached an agreement after several days of negotiations.",
    "example_zh": "雙方經過數日協商後達成協議。"
  }
}
```

學習例句用來展示自然用法，不需要直接複製新聞原句。

---

## Why Two JSON Files?

Vocabulary 與 Phrase 分開保存，讓未來的學習工具可以直接提供：

- Vocabulary Mode
- Phrase Mode
- Mixed Review
- English → Chinese
- Chinese → English
- English Definition
- Example Sentence
- Flash Cards
- Multiple Choice
- Cloze Test
- Random Review

`cloze` 不需要存進 JSON。未來程式可利用 JSON Key 與 `example_en` 動態產生填空題。

---

## Public Data / Widget Use

Repository 採 Public，資料設計成靜態 JSON，方便 iPad / iOS Widget 或其他前端程式透過 HTTPS 直接取得。

GitHub Pages 可直接發布 Repository 中的靜態檔案，因此 JSON 可以作為簡單的唯讀資料來源使用。

Master data files：

- `data/vocabulary.json`
- `data/phrases.json`

Widget 應只依賴 JSON 本身即可完成主要學習功能，不應要求執行時再呼叫 AI 產生 definition、翻譯或例句。

---

## Core Principle

**少量、高價值、來自真實閱讀內容，而且不重複。**

我們不是建立最大的英文單字庫，而是建立一份真正由自己的英文閱讀逐步累積、可以長期反覆練習的個人 English Reading Database。
