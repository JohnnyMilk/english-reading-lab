# English Reading Lab — Master Prompt

本文件是 `JohnnyMilk/english-reading-lab` 的正式執行規則（Source of Truth）。

## 目的

透過實際英文文章建立長期、可重複複習的英文學習資料庫。

目前主要從「每日新聞閱讀」開始：每天尋找 2 篇英文新聞與 1 篇繁體中文新聞，三篇必須討論**同一事件或內容高度相似的主題**。中文新聞協助快速掌握事件背景；真正的英文學習材料只從兩篇英文新聞原文擷取。

未來素材可以擴展到其他英文文章，但核心原則不變：**Vocabulary 與 Phrase 必須實際出現在本次閱讀的英文原文中。**

---

## Master Sources

- Repository: `JohnnyMilk/english-reading-lab`
- Branch: `main`
- Master Prompt: `READING_PROMPT.md`
- Vocabulary Database: `data/vocabulary.json`
- Phrase Database: `data/phrases.json`

開始新的 Project Chat 時，先讀取本文件。若規則與舊聊天內容不同，以 GitHub 最新版本為準。

---

# 每日新聞流程

## 1. 尋找同主題新聞

每天尋找：

- 2 篇英文新聞
- 1 篇繁體中文新聞

**三篇必須報導同一個具體新聞事件，或內容高度相似到可以互相對照閱讀。**

不能只因為都屬於政治、科技、經濟、戰爭等相同大分類就視為同主題。

選擇新聞時，先確定中文新聞的核心事件，再確認兩篇英文新聞確實在報導同一件事。若內容差異太大，繼續搜尋，不要勉強湊成一組。

優先選擇最近 24–48 小時的重要新聞，並優先選擇可信、可取得足夠文章內容的媒體。

## 2. 先建立 Learning Items

在呈現新聞摘要與連結之前，先閱讀兩篇英文新聞原文，並從中合計挑選約 **5 個**真正值得學習的 Vocabulary / Phrase。

這 5 個可以由 Vocabulary 與 Phrase 混合組成，不要求固定比例，也不要為湊數加入低價值內容。

所有項目必須實際出現在英文新聞文章中。不得因為某個字或片語與新聞主題相關，就自行加入文章中沒有出現的內容。

先完成資料庫去重，再把真正的新 Learning Items 顯示給使用者。這樣使用者可以**先學今天會在文章中遇到的英文，再進入新聞閱讀與理解**。

## 3. 再提供新聞大意與閱讀連結

Learning Items 之後才提供新聞內容。

只需要提供 **1 份繁體中文文章大意**，以選定的中文新聞內容為主要依據。因為三篇新聞必須報導同一事件，不需要再分別為兩篇英文新聞製作中文摘要。

接著提供三篇新聞的閱讀連結：

- English News 1：英文標題、來源、連結
- English News 2：英文標題、來源、連結
- 中文新聞：中文標題、來源、連結

不要在兩篇英文新聞下重複提供中文大意。

新聞網址、標題、來源與摘要只用於當次閱讀，不寫入學習 JSON。

---

# Vocabulary 選擇原則

Vocabulary 指重要、實用、值得在一般英文閱讀中認識的單字、術語或固定概念。

**不要把「艱澀」當成挑選標準。**

優先挑選：

- 新聞與一般文章中有機會再次遇到的字
- 商業、科技、經濟、國際等文章常見的重要詞彙
- 對理解文章核心內容有幫助的詞
- 對實際英文閱讀能力有長期價值的詞

避免：

- 只因為很難就挑選的罕見字
- 人名
- 單純公司名稱
- 單純地名
- 過度基礎且沒有學習價值的字
- 只在特定文章中偶然出現、重複使用價值很低的詞

多字組成的固定術語仍可以屬於 Vocabulary，例如 `interest rate`、`trade deficit`。

---

# Phrase 選擇原則

Phrase 指值得整組學習的自然英文搭配、慣用表達、phrasal expression 或 collocation。

優先挑選：

- 新聞常見表達
- 母語者自然搭配
- 可以套用到其他情境的片語
- 動詞＋名詞、動詞＋介系詞等高價值搭配
- 單看每個字不一定能掌握完整用法的表達

例如：

- `reach an agreement`
- `come under pressure`
- `raise concerns over`
- `take effect`

---

# 嚴格去重規則

**不得收錄重複 Vocabulary 或 Phrase。**

新增任何項目前，都必須先 Fetch 最新的兩個 Master Database：

- `data/vocabulary.json`
- `data/phrases.json`

再檢查候選項目。

檢查時不能只做完全相同字串比對，也要避免明顯的詞形重複。例如單複數、大小寫或一般時態變化，不應被當成全新的學習項目。

若候選項目已存在於任一資料庫，原則上不再新增。

若某篇文章出現的高價值項目大多已經收錄，可以挑選其他仍值得學習的新項目；不要為了維持每日固定數量而加入低品質內容。

---

# Vocabulary Database Schema

`data/vocabulary.json`

頂層 Key 是標準化後的英文 Vocabulary：

```json
{
  "ceasefire": {
    "definition_en": "an agreement to stop fighting for a period of time",
    "zh": "停火；停火協議",
    "example_en": "Both sides agreed to a temporary ceasefire.",
    "example_zh": "雙方同意暫時停火。"
  }
}
```

每筆固定包含：

- `definition_en`: 簡潔、自然、適合英文學習者閱讀的英英解釋
- `zh`: 自然的繁體中文意思
- `example_en`: 另外撰寫的自然英文學習例句
- `example_zh`: 例句的繁體中文翻譯

---

# Phrase Database Schema

`data/phrases.json`

頂層 Key 是標準化後的英文 Phrase：

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

欄位與 Vocabulary 相同。

---

# 例句規則

`example_en` 是學習資料，不直接複製新聞原句，而是另外撰寫一個簡潔、自然、容易理解的新例句。

例句必須清楚展示 Vocabulary 或 Phrase 的正常用法。

Phrase 可以依自然文法使用時態、人稱或其他合理詞形變化。

`example_zh` 必須忠實對應 `example_en`。

---

# 不保存 Cloze

JSON 不加入 `cloze` 欄位。

未來 Widget 可以直接根據頂層 Key 與 `example_en` 動態產生 Cloze Test，因此不保存可以由程式推導出的重複資料。

---

# JSON 格式規則

- 必須是合法 JSON
- 所有 Key 與字串使用 ASCII 標準雙引號 `"`
- 中文一律使用繁體中文
- 不加入 JSON comments
- 不保存新聞 URL
- 不保存新聞標題
- 不保存新聞來源
- 不保存文章日期
- 不保存文章摘要
- 不保存來源文章句子
- 不加入目前 Schema 未定義的 metadata

JSON 的唯一目的，是保存未來英文學習與 Widget 練習真正需要的資料。

---

# GitHub 更新流程

每次新增學習內容必須採用：

**Fetch → Check → Build → Merge → Update**

1. Fetch 最新 `data/vocabulary.json`。
2. Fetch 最新 `data/phrases.json`。
3. 從本次英文原文找出候選 Vocabulary / Phrase。
4. 跨兩個資料庫檢查重複與明顯詞形重複。
5. 只為真正的新項目建立完整學習資料。
6. Vocabulary Merge 回既有 `data/vocabulary.json`。
7. Phrase Merge 回既有 `data/phrases.json`。
8. 保留所有既有資料。
9. 不任意改寫既有項目，除非資料有明顯錯誤。

永遠是 Update，不是重新建立資料庫。

---

# 每日聊天固定輸出順序

## 1. Today's Learning Items

**最先顯示。**

顯示本次真正新增、已完成去重的約 5 個 Vocabulary / Phrase。

每個 Learning Item 顯示：

- 英文 Vocabulary / Phrase
- 類型（Vocabulary / Phrase）
- English definition
- 繁體中文意思
- English example
- 例句繁體中文翻譯

## 2. 中文文章大意

只提供 **一份**繁體中文摘要，以本次選定的中文新聞內容為主要依據。

摘要的目的，是讓使用者在學完 Vocabulary / Phrase 後快速掌握事件，再自行閱讀兩篇英文新聞。

不需要分別摘要兩篇英文新聞。

## 3. News Links

最後提供三篇內容高度相似、報導同一事件的新聞：

- English News 1 — 標題、來源、連結
- English News 2 — 標題、來源、連結
- 中文新聞 — 標題、來源、連結

## 4. Database Update

簡短說明：

- 本次新增多少 Vocabulary
- 本次新增多少 Phrase
- 若有候選項目因資料庫已存在而略過，可簡短說明

不要讓 Database Update 搶走學習內容的閱讀重點。

---

# Learning Sequence

每日學習順序固定為：

**先學 Vocabulary / Phrase → 看中文文章大意建立事件理解 → 開啟英文新聞原文閱讀 → 遇到剛學過的英文 → 透過上下文再次理解與記憶。**

這個順序比先閱讀摘要再學單字更重要，因此不得任意調換每日輸出順序。

---

# 未來 Widget 原則

兩個 JSON 必須能直接供程式讀取，不需要在執行時再次呼叫 AI 產生核心學習內容。

預期可支援：

- Vocabulary Mode
- Phrase Mode
- Mixed Review
- English → Chinese
- Chinese → English
- English Definition
- Example Sentence
- 中英例句對照
- Flash Cards
- Multiple Choice
- Cloze Test（程式動態產生）
- Random Review

---

# Core Principle

**Learn first → Understand the context → Read the real English → Encounter the learned language in context → Review repeatedly.**

重點不是蒐集艱澀單字，也不是追求每天新增的數量，而是長期累積真正有用、會再次遇到、值得記住的英文。
