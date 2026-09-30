# Project Context

Project Context 是一個 Codex Skill，用來建立及維護專案根目錄的 `PROJECT_CONTEXT.md`。這份檔案記錄後續工作需要、卻不容易每次從程式碼重新查出的專案資訊。使用時仍須核對當前的原始碼、測試與設定檔。

## 功能

| 操作 | 適用情況 | 結果 |
| --- | --- | --- |
| `CREATE` | 想將專案導覽結果保存為長期脈絡 | 先進行唯讀檢查並提出內容草案；取得明確核准後才建立檔案 |
| `ASSESS` | 完成開發工作後，判斷變更是否影響長期脈絡 | 回報是否需要建立或更新 `PROJECT_CONTEXT.md`；不會自行寫入 |
| `UPDATE` | 已知某項重要的專案知識需要修正 | 查證受影響的部分，提出局部修改，取得核准後更新 |
| `REFRESH` | 懷疑現有脈絡已過時，想檢查可信度 | 逐項核對相關內容；需要修復時先提出方案並取得核准 |

操作細節及判斷規則以 [SKILL.md](SKILL.md) 為準。

## 安裝

可以請 Codex 用 `$skill-installer` 從這個 GitHub 倉庫安裝。手動安裝時，把整個 Skill 目錄放到 `$HOME/.agents/skills/project-context/`；若只想在某個 Git 倉庫使用，則放到該倉庫的 `.agents/skills/project-context/`。請保留 `SKILL.md`、`references/` 和 `assets/` 的相對位置。如果 Codex 沒有顯示新 Skill，請重新啟動。

安裝位置與技能探索方式可參考 [OpenAI 的 Skills 說明](https://learn.chatgpt.com/docs/build-skills)。

## 使用方式

在 Codex 對話中明確提及 `$project-context`，例如：

- 「使用 `$project-context` 的 `CREATE`，為這個專案建立 `PROJECT_CONTEXT.md`；請先提出導覽報告與內容草案。」
- 「使用 `$project-context` 的 `ASSESS`，判斷剛完成的變更是否需要更新專案脈絡。」
- 「使用 `$project-context` 的 `REFRESH`，檢查現有 `PROJECT_CONTEXT.md` 是否仍然可靠。」

提問內容符合 Skill 的說明時，Codex 也可能自行選用。一般的程式修改或除錯不會自動觸發 `CREATE` 或 `REFRESH`。

## 工作原則

- 先確認目前處理的是哪個專案，再用原始碼、測試和設定檔查證這次工作需要的資訊。
- 查看專案或檢查內容是否過時時，只讀取檔案；略過建置產物、快取、憑證、個人資料與正式環境資料。
- `CREATE` 會先交出報告，列出準備寫入的內容；使用者核准後才建立檔案。`UPDATE` 和 `REFRESH` 若要修改檔案，也須先讓使用者確認具體要改的部分。
- 保護使用者提供的知識；缺少程式碼證據，不代表該知識是錯的。
- 只記錄日後需要、又不容易重新查得的專案資訊；不把 `PROJECT_CONTEXT.md` 寫成完整檔案清單或程式索引。

## 檔案結構

```text
project-context/
├── SKILL.md                 # 操作流程與邊界
├── references/              # 各操作所需的判斷規則與格式說明
└── assets/
    └── PROJECT_CONTEXT.template.md
```

## 授權

本專案採用 [MIT License](LICENSE)。
