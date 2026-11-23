# 《原神》LLM Wiki 維護日誌 (Log)

本文件為時間序列的追加日誌（Append-only Log），按時間記錄知識庫的所有入庫（Ingest）、檢索與綜合（Query）、健檢（Lint）、簡報審查（Check）、修復（Fix）與簡報產出（Generate）操作。

格式規範：
`## [YYYY-MM-DD] <操作類別> | <標題與簡述>`

支援類別：
- `ingest`: 新文獻資料入庫與條目增修
- `query`: 具備深度綜合價值之答疑紀錄
- `lint`: 知識庫定期或觸發式健檢報告
- `check`: 簡報或條目來源嚴格審查結果
- `fix`: 因衝突、年代偏誤、實體重複或來源缺失之修復紀錄
- `generate`: 互動式 HTML 投影片或教學講稿生成

---

## [2026-11-23] system | Wiki 系統初始化
- 確立 Karpathy LLM Wiki 架構與三層模型（Raw Sources $\rightarrow$ Wiki $\rightarrow$ Presentations）。
- 導入「Ingest $\rightarrow$ Query $\rightarrow$ Lint $\rightarrow$ Generate $\rightarrow$ Check」閉環工作流與 Fallback 退回機制。
- 建立專案目錄結構：`raw/01-mondstadt/`, `wiki/regions/`, `wiki/entities/`, `wiki/cosmology/`, `wiki/timeline/`, `presentations/scripts/`, `presentations/html/`。
- 撰寫並正式實施系統憲法 [AGENTS.md](file:///c:/Users/Aerith/Downloads/Genshin-LLM-Wiki/AGENTS.md)。
- 建立並規範 `index.md` 內容目錄與 `log.md` 日誌。
- 確立第一階段里程碑：專注於蒙德（風之國），收集並入庫至少 5 篇核心原始資料，在此之前不生成任何 HTML 簡報。

## [2026-11-23] fix | 修訂 AGENTS.md 年代錨點、隨選 Query 與實體去重規範
- **年代切分修正**：嚴格區分「古蒙德時期（約 2600 年前高塔孤王與安德留斯對峙、孤王隕落）」與「舊蒙德貴族時期（約 1000 年前勞倫斯等貴族腐化、溫妮莎起義）」，避免年代混淆與無來源定論。
- **YAML 格式相容性驗證**：確保範本符合 Obsidian 標準 YAML Frontmatter 語法與字串陣列格式。
- **Loop/Graph 流程優化**：將 Query 改為隨選發起分支，Lint 明確設定於每次 CommitWiki 後執行健康檢查。
- **實體唯一性與去重**：明定單一實體唯一主頁規範（如統一於 `[[巴巴托斯]]` 主頁），禁止為同一人物建立重複檔案，透過 YAML Aliases 繁簡英別名涵蓋「溫迪」等日常化身。

## [2026-11-23] ingest | 《古恩希爾德小傳》文獻入庫與 5 篇 Wiki 條目建立
- **原始資料**：[01-biography-of-gunnhildr.md](file:///c:/Users/Aerith/Downloads/Genshin-LLM-Wiki/raw/01-mondstadt/01-biography-of-gunnhildr.md)（官方一手書籍文本）。
- **新建頁面**：`[[巴巴托斯]]`、`[[迭卡拉庇安]]`、`[[古恩希爾德家族]]`、`[[蒙德]]`、`[[古蒙德起義事件]]`。
- **目錄更新**：同步更新 `index.md`，將 5 個條目轉為正式收錄。

## [2026-11-23] lint | 第 1 次知識庫全面健檢
- **來源可考性**：5 個新條目均具備明確的 `raw/` 來源標註與作者立場 Alert，無脫韁或無中生有之客觀設定（通過）。
- **年代與事件一致性**：嚴格依循「三千年前」魔神混戰與冰原環境，明確區隔孤王時期與後續貴族時期，將「約 2600 年前」起義終結定論標註為待考證推估（通過）。
- **Wikilinks & Aliases**：雙向連結與 YAML Aliases 語法相容 Obsidian，實體「巴巴托斯」已包含「溫迪」別名，無重複條目（通過）。
- **孤島與待建條目（Stubs）**：無任何孤島頁面；檢測到 3 個前置待建實體（`[[安德留斯]]`、`[[勞倫斯家族]]`、`[[西風騎士團]]`），確認留待後續 4 篇文獻逐步填補（通過）。

## [2026-11-23] ingest | 《高塔孤王系列武器素材》入庫與 Wiki 條目更新
- **原始資料**：[02-decarabians-materials.md](file:///c:/Users/Aerith/Downloads/Genshin-LLM-Wiki/raw/01-mondstadt/02-decarabians-materials.md)（官方武器突破素材《高塔孤王的破瓦/殘垣/斷片/碎夢》共 4 篇文本）。
- **新增條目**：建立先前待建的魔神主頁 [wiki/entities/安德留斯.md](file:///c:/Users/Aerith/Downloads/Genshin-LLM-Wiki/wiki/entities/%E5%AE%89%E5%BE%B7%E7%95%99%E6%96%AF.md)。
- **更新條目**：`[[迭卡拉庇安]]`、`[[古蒙德起義事件]]`、`[[蒙德]]`、`[[巴巴托斯]]`。
- **目錄更新**：同步更新 `index.md`，將 `[[安德留斯]]` 轉為正式收錄。

## [2026-11-23] lint | 第 2 次定向健檢報告（孤王素材組）
- **受測頁面**：`安德留斯.md`、`迭卡拉庇安.md`、`古蒙德起義事件.md`、`蒙德.md`、`巴巴托斯.md`。
- **結論**：來源標註齊全，視角互補無矛盾，成功消解 `安德留斯` 待建條目（通過）。

## [2026-11-23] ingest | 《溫妮莎傳奇》上下卷入庫與條目增修
- **原始資料**：[03-legend-of-vennessa.md](file:///c:/Users/Aerith/Downloads/Genshin-LLM-Wiki/raw/01-mondstadt/03-legend-of-vennessa.md)（官方一手書籍文本：民間傳唱詩歌）。
- **新建頁面**：`[[溫妮莎]]`、`[[勞倫斯家族]]`、`[[西風騎士團]]`、`[[舊蒙德貴族起義事件]]`。
- **更新頁面**：`[[巴巴托斯]]`、`[[蒙德]]`。
- **目錄更新**：同步更新 `index.md`，將溫妮莎、勞倫斯家族、西風騎士團與貴族起義轉為正式收錄。

## [2026-11-23] lint | 第 3 次定向健檢報告（溫妮莎與舊蒙德貴族組）
- **受測頁面**：`溫妮莎.md`、`勞倫斯家族.md`、`西風騎士團.md`、`舊蒙德貴族起義事件.md`、`巴巴托斯.md`、`蒙德.md`。
- **結論**：嚴格區隔古蒙德高塔倒塌與貴族高塔倒塌兩次不同起義；成功清空殘留待建詞條（通過）。

## [2026-11-23] ingest | 《林間風·龍之書》與武器《天空之傲》入庫與條目增修
- **原始資料**：
  - [04-breeze-amidst-the-trees-dragon.md](file:///c:/Users/Aerith/Downloads/Genshin-LLM-Wiki/raw/01-mondstadt/04-breeze-amidst-the-trees-dragon.md)（書籍文獻）
  - [04-skyward-pride.md](file:///c:/Users/Aerith/Downloads/Genshin-LLM-Wiki/raw/01-mondstadt/04-skyward-pride.md)（5星雙手劍武器故事）
- **新建頁面**：`[[特瓦林]]`、`[[四風守護]]`、`[[杜林]]`、`[[坎瑞亞災變與杜林之戰]]`。
- **更新頁面**：`[[巴巴托斯]]`、`[[蒙德]]`。
- **目錄更新**：同步更新 `index.md`，將特瓦林、四風守護、杜林與災變之役轉為正式收錄。

## [2026-11-23] lint | 第 4 次定向健檢報告（特瓦林、杜林與災變雪山之戰組）
- **受測頁面**：`特瓦林.md`、`四風守護.md`、`杜林.md`、`坎瑞亞災變與杜林之戰.md`、`巴巴托斯.md`、`蒙德.md`。
- **結論**：嚴格區分 500 年前災變屠龍與現代風魔龍危機；消解所有前置待建詞條（通過）。

## [2026-11-23] ingest | 《微風與少年》PV與任務文本入庫與條目增修
- **原始資料**：[05-the-boy-and-the-whirlwind.md](file:///c:/Users/Aerith/Downloads/Genshin-LLM-Wiki/raw/01-mondstadt/05-the-boy-and-the-whirlwind.md)（官方劇情PV、傳說任務「若你困於無風之地」與溫迪角色故事四）。
- **新建頁面**：`[[無名少年]]`。
- **更新頁面**：`[[巴巴托斯]]`、`[[古蒙德起義事件]]`。
- **目錄更新**：同步更新 `index.md`，將無名少年轉為正式收錄。

## [2026-11-23] lint | 第 5 次定向健檢報告（無名少年與溫迪外貌原型組）
- **受測頁面**：`無名少年.md`、`巴巴托斯.md`、`古蒙德起義事件.md`。
- **結論**：嚴格維持巴巴托斯唯一主頁與別名去重；兩千年歷史原型與神明回憶界限分明；無任何孤島頁面與待建 Stubs（通過）。

## [2026-11-23] query | 蒙德自由理念之歷史演進脈絡
- **查詢主題**：「蒙德的自由理念，是如何從古蒙德起義發展到現代蒙德的？」
- **查閱條目**：`[[蒙德]]`、`[[巴巴托斯]]`、`[[無名少年]]`、`[[迭卡拉庇安]]`、`[[古蒙德起義事件]]`、`[[溫妮莎]]`、`[[勞倫斯家族]]`、`[[西風騎士團]]`、`[[舊蒙德貴族起義事件]]`、`[[特瓦林]]`、`[[四風守護]]`。
- **綜合檢驗**：依序整理萌芽、蛻變與昇華三大階段，論點 100% 來源可考，史料一致性檢查通過。

## [2026-11-23] generate | 教學型 HTML 簡報與結構化講稿生成
- **講稿大綱存檔**：[01-mondstadt-freedom-history.md](file:///c:/Users/Aerith/Downloads/Genshin-LLM-Wiki/presentations/scripts/01-mondstadt-freedom-history.md)（12 頁完整講稿、逐頁 Wiki 溯源對照與史料層級聲明）。
- **互動 HTML 簡報存檔**：[01-mondstadt-freedom-history.html](file:///c:/Users/Aerith/Downloads/Genshin-LLM-Wiki/presentations/html/01-mondstadt-freedom-history.html)（現代單檔案獨立網頁，深色奇幻 UI，支援鍵盤翻頁、進度條、目錄抽屜與 SVG 圖表）。
- **引用圖片資源**：全數使用 `assets/` 現存 9 張圖片（`monstadt.jpeg`、`venti.jpeg`、`decarabian.jpeg`、`old-monstadt.jpeg`、`nameless-bard.jpeg`、`vennessa.jpeg`、`favonius.jpeg`、`dragonspine.jpeg`、`dvalin.jpeg`）。

## [2026-11-23] check | 簡報溯源、路徑與翻頁功能審查報告
- **零幻覺準則（Zero Hallucination）**：12 頁投影片的核心論點與年代事件 100% 對應至 `wiki/` 條目與 `raw/` 原始資料；頁面底部均標註 Wiki 溯源信息（審查通過）。
- **教學架構聲明**：首頁與第 11 頁明確加上 Alert 標註「萌芽、蛻變、昇華」為教學分析架構，非遊戲官方名詞（審查通過）。
- **圖片路徑與存在性**：引用的 9 張圖片路徑均為 `../../assets/<name>.jpeg`，已核對磁碟檔案完全存在且長度無損，無引用不存在檔案（審查通過）。
- **互動功能檢查**：鍵盤（方向鍵、空白鍵、Home/End、Escape）與畫面上 Prev/Next 按鈕、進度條、目錄大綱跳轉功能健全（審查通過）。
