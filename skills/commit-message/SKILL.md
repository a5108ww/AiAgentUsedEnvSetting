---
name: commit-message
description: 分析當前分支與前次 commit 的差異，生成符合 Conventional Commits 格式的 commit message。列出異動類型、改動項目和詳細說明。讓我預覽完後再決定是否提交。Use when asking "create commit message", "generate commit", or "review changes before commit"
user-invocable: true
---

# Commit Message Generator

## 目的
分析當前分支與前次 commit 的差異，自動生成清晰的 commit message，幫助開發者記錄改動內容。

## 異動類型標準

按照 Conventional Commits 規範：

- **feat**: 新功能（用戶可見的新特性）
- **fix**: 修復 bug
- **refactor**: 代碼重構（不改變功能）
- **perf**: 性能優化
- **test**: 測試相關（新增或修改測試）
- **docs**: 文檔更新
- **style**: 代碼風格（格式、分號、空格等，不改變邏輯）
- **chore**: 構建工具、依賴更新、配置等
- **ci**: CI/CD 流程相關

## 訊息格式
```
<type>(<scope>): <subject>

<body>

<footer>
```

### 格式說明

- **type**: 從上面的異動類型選擇
- **scope**: 影響範圍（可選，如 `auth`, `api`, `ui`）
- **subject**: 簡潔描述（命令式，小寫，不超過 50 字）
- **body**: 詳細說明（可選，解釋 why 而不是 what）
- **footer**: 相關 issue（可選，如 `Closes #1234`）

## 檢查清單

1. **類型正確** - 選擇最符合的異動類型
2. **Subject 清晰** - 簡潔描述改動內容
3. **Body 完整** - 說明改動原因和影響
4. **檔案數合理** - 避免一次改動超過 10 個檔案
5. **測試涵蓋** - 新功能應該有測試

## 輸出格式

### 單一異動
```
feat(auth): add two-factor authentication

Changes:
- Add TOTP-based 2FA support
- Create verification flow in login
- Store encrypted secrets in database

Impact:
- User login flow extended by 1-2 seconds
- New dependencies: pyotp (0.5 MB)

Files changed: 5
Insertions: 156
Deletions: 23
Related issue: Closes #1234
```

### 多個異動
```
feat(auth): add two-factor authentication
fix(api): resolve rate limiting bug
test(user): improve coverage

Changes:
✨ feat(auth): Add TOTP-based 2FA support
  - 3 files changed
  - 89 insertions
  - 12 deletions

🐛 fix(api): Resolve rate limiting on /auth endpoint
  - 1 file changed
  - 15 insertions
  - 8 deletions

✅ test(user): Improve test coverage from 72% to 85%
  - 8 files changed
  - 130 insertions
  - 67 deletions

Summary:
- Total files changed: 12
- Total insertions: 234
- Total deletions: 87
```

## 檢查步驟

1. **讀取差異** - 執行 git diff 與前次 commit
2. **分類改動** - 按異動類型分組
3. **撰寫 Subject** - 簡潔描述主要改動
4. **撰寫 Body** - 詳細說明改動原因和影響
5. **統計資訊** - 提供檔案數、插入/刪除行數
6. **關聯 Issue** - 如有相關 issue，在 footer 中引用

## 邊界情況

### 新檔案
- 列為「新增」
- 如果只有新增檔案，通常是 `feat` 類型

### 刪除的檔案
- 列為「移除」
- 如果刪除舊功能，使用 `refactor` 或 `feat` 取決於上下文

### 配置檔案
- 修改通常是 `chore` 類型
- 如果涉及重大變化（如遷移），使用 `feat`

### 自動生成代碼
- 標記為「自動生成」
- 如非必要，避免在 commit message 中詳細列出

### 大型重構
- 拆分成多個小 commit
- 每個 commit 代表一個邏輯步驟
- 不要一次 commit 超過 20 個檔案

## 範例：實際使用

**情景：修復登錄 bug 並添加日誌**
```
fix(auth): resolve session timeout edge case
chore(logging): improve debug output

Changes:
🐛 fix(auth): Resolve session timeout edge case
  - Fixed condition where session expires but user not logged out
  - Added timeout check before token validation
  
📝 chore(logging): Improve debug output
  - Added timestamp to auth logs
  - Reduced log verbosity for production

Files changed: 3
Insertions: 47
Deletions: 15
Related issue: Closes #456
```

## 規則

✅ **應該做**：
- 使用命令式動詞（add, fix, refactor，而不是 added, fixed）
- 小寫開頭，除非是專有名詞
- Subject 不超過 50 字
- Body 不超過 72 字/行
- 說明 why 而不是 what

❌ **不應該做**：
- 不要改動任何檔案（僅預覽）
- 不要執行 git 命令
- 不要在 subject 加句號或冒號
- 不要寫得太簡略（「update stuff」不好）
```

---

## 主要優化點總結

| 原始 | 優化後 |
|------|--------|
| Description 模糊 | 清晰說明用途和觸發條件 |
| 沒有類型定義 | 詳列 8 種異動類型 |
| 沒有輸出範例 | 提供單一和多重異動的範例 |
| 行為描述簡短 | 增加 6 個檢查步驟 |
| 缺少邊界情況 | 詳列 5 種邊界情況處理 |
| 沒有規則說明 | 清列 do's 和 don'ts |

---

## 互動流程

生成 commit message 後，系統會提供三個選項讓使用者選擇：

### 選項 1：✅ 提交 (Commit)
- 直接執行 `git commit`
- 立即完成 commit

### 選項 2：✏️ 編輯 (Edit)
- 複製 commit message 到剪貼板
- 系統提示「message 已複製到剪貼板，請編輯後貼到 chat 對話框中」
- 使用者手動編輯 message，並貼回 chat
- AI 驗證編輯後的 message 是否符合 Conventional Commits 規範
- 驗證無誤後再次確認是否提交
  - **確認提交** - 執行 `git commit -m "[編輯後的 message]"`
  - **修正** - 返回編輯，再次貼新的 message
  - **放棄** - 取消本次操作，保留改動

### 選項 3：❌ 取消 (Cancel)
- 不執行任何 git 操作
- 保留所有改動在工作區

## 驗證編輯後的 Message

當使用者貼回編輯後的 message，AI 需要驗證：

✅ **驗證項目**：
1. **格式正確** - 符合 `<type>(<scope>): <subject>` 格式
2. **類型有效** - 使用允許的類型（feat, fix, refactor 等）
3. **Subject 清晰** - 簡潔、使用命令式、不超過 50 字
4. **Body 質量** - 如有 body，不超過 72 字/行
5. **結構完整** - 如有多個異動，正確列出所有 type

⚠️ **如果驗證失敗**：
- 指出具體問題（如「Subject 超過 50 字」、「type 無效」）
- 提供修正建議
- 詢問是否要再次編輯或使用原本的 message

## 所需權限

此 skill 需要以下 Git 權限（需在 settings.json 中配置）：
- `Bash(git commit *)` - 執行 commit
- `Bash(git add *)` - 暫存改動
- `Bash(git diff *)` - 讀取差異
- `Bash(git status *)` - 檢查狀態

## 使用方式

```
/commit-message

或

請幫我生成 commit message
或
檢查這次改動要如何描述