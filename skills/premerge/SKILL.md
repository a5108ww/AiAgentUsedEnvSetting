---
name: premerge
description: 檢查來源分支合併到目的分支，所新增、修改或刪除的功能，生成詳細的功能更新報告
---

# Premerge Skill

## 目的

幫助開發者在 IDE 中(VS Code或是Visual Studio)快速了解來源分支合併到目的分支的功能，生成清晰的功能更新報告。

## 功能概述

### 1. 功能變更分析
- 識別新增的功能模塊和特性
- 列出所有改進和優化
- 統計 Bug 修復數量
- 追蹤依賴更新

### 2. 影響分析
- 識別哪些文件被修改
- 分析模塊間的依賴變更
- 檢查 API 或接口變更
- 評估功能對系統的影響

### 3. 功能詳情報告
- 按 Conventional Commits 分類展示變更
- 提取提交信息中的功能描述
- 生成結構化的功能清單
- 提供實施風險評估

## 使用方法

### 基本語法
```
premerge <source-branch> <target-branch>
```

### 參數說明

| 參數 | 說明 | 示例 |
|------|------|------|
| `source-branch` | 來源分支（要合併代碼的來源分支）| `feature/xxx` 或 `hotfix/xxx` |
| `target-branch` | 目標分支（將代碼合併到的分支）| `master` 或 `develop` 或 `uat` 或 `sit` |

### 使用示例

#### 示例 1：檢查 feature/xxx 要合併到 develop 的功能
```
premerge feature/xxx develop
```
**效果**：生成詳細的功能更新報告，用於預發佈檢查

#### 示例 2：檢查 feature/xxx 要合併到 uat 的功能
```
premerge feature/xxx uat
```
**效果**：展示 feature/xxx 分支相對於 uat 分支將要添加的所有功能

#### 示例 3：檢查 feature/xxx 要合併到 sit 的功能
```
premerge feature/xxx sit
```
**效果**：列出所有待合併的新功能、修復和改進

## 功能分類標準

根據 Conventional Commits 規範，功能分為以下幾類：

### 🆕 新功能（feat）
```
feat: 添加用戶認證功能
feat(auth): 實現 JWT token 驗證機制
```
**說明**：
- 引入全新的功能或模塊
- 添加新的 API 端點或方法
- 擴展現有功能的能力

**示例功能**：
- 新的用戶登錄系統
- 新的報表生成模塊
- 新的數據導出功能

---

### 🔧 改進（improve）
```
improve: 優化數據查詢性能
improve(ui): 改進用戶界面響應速度
```
**說明**：
- 優化現有功能的性能
- 改進用戶體驗
- 簡化代碼邏輯

**示例改進**：
- 緩存優化減少數據庫查詢
- UI 動畫優化改善流暢度
- 算法優化提升計算速度

---

### 🐛 Bug 修復（fix）
```
fix: 修復登錄時的空值異常
fix(payment): 解決支付超時問題
```
**說明**：
- 修復已知的 Bug
- 解決報錯的邏輯問題
- 修正數據處理的錯誤

**示例修復**：
- 修復用戶無法登出的問題
- 修復數據導出時的編碼錯誤
- 修復移動端布局破損

---

### 📚 文檔更新（docs）
```
docs: 更新 API 文檔
docs(readme): 添加安裝說明
```
**說明**：
- 更新或新增文檔
- 更新代碼註釋
- 添加使用指南

---

### 🎨 代碼風格（style）
```
style: 統一代碼格式
style: 調整縮進和空格
```
**說明**：
- 代碼格式化（不影響功能）
- 移除不使用的導入
- 統一命名規範

---

### ♻️ 重構（refactor）
```
refactor: 重構用戶服務模塊
refactor(api): 簡化路由定義
```
**說明**：
- 重組代碼結構
- 提高代碼可維護性
- 不改變現有功能的外部行為

---

### ⚡ 性能優化（perf）
```
perf: 優化列表渲染性能
perf(database): 添加索引提升查詢速度
```
**說明**：
- 明確的性能優化
- 提升應用響應速度
- 減少資源消耗

---

### 🧪 測試（test）
```
test: 添加用戶認證的單元測試
test(api): 增加 API 集成測試
```
**說明**：
- 新增或更新測試代碼
- 提高測試覆蓋率

---

### 🚀 CI/CD（ci）
```
ci: 更新 GitHub Actions 工作流
ci: 配置自動部署流程
```
**說明**：
- 更新構建和部署配置
- 修改 CI/CD 流程

---

### 🔒 安全（security）
```
security: 更新依賴以修復漏洞
security: 實現 CSRF 防護
```
**說明**：
- 解決安全漏洞
- 增強安全性

---

## 報告內容詳解

### 1️⃣ 基本信息
```
當前分支: feature/user-dashboard
目標分支: main
領先提交數: 8
總變更行數: 342 (新增) + 89 (刪除)
```

### 2️⃣ 功能變更概览
```
📊 變更統計：
  🆕 新功能: 3 個
  🔧 改進: 2 個
  🐛 Bug 修復: 4 個
  📚 文檔更新: 1 個
  ♻️ 重構: 1 個
```

### 3️⃣ 詳細功能清單

#### 新增功能
```
1. 用戶儀表板模塊
   feat: 實現用戶個人儀表板
   - 顯示用戶統計信息
   - 實時數據更新
   - 可自定義小部件

2. 高級過濾功能
   feat(search): 添加多條件搜索過濾
   - 支持日期範圍篩選
   - 支持標籤組合篩選
   - 儲存常用過濾條件
```

#### 問題修復
```
1. 修復登出後仍可訪問的問題
   fix: 登出時清除所有 session
   優先級: 🔴 高 (安全問題)

2. 修復報表導出時的亂碼
   fix(export): 修復 CSV 編碼問題
   優先級: 🟡 中
```

### 4️⃣ 受影響的文件和模塊
```
前端模塊:
  ✏️ src/pages/Dashboard.tsx (新增)
  ✏️ src/components/UserStats.tsx (新增)
  ✏️ src/styles/dashboard.css (新增)
  ✏️ src/api/user.ts (修改 - 新增 API)

後端模塊:
  ✏️ src/services/dashboard.ts (新增)
  ✏️ src/models/User.ts (修改 - 新增字段)
  ✏️ src/controllers/userController.ts (修改)

共 12 個文件變更
```

### 5️⃣ API 和接口變更
```
新增 API 端點:
  POST /api/users/dashboard/widgets
  GET /api/users/dashboard/stats
  PUT /api/users/preferences

已修改 API:
  GET /api/users/{id} (新增返回字段: lastLogin, preferences)
  POST /api/auth/logout (現在清除所有 session)

數據庫變更:
  User 表新增列: lastLoginAt, preferences (JSON)
```

### 6️⃣ 依賴更新
```
新增依賴:
  📦 recharts@^2.10.0 (用於圖表展示)
  📦 date-fns@^2.30.0 (用於日期處理)

更新依賴:
  📦 react: 18.2.0 → 18.3.0
  📦 typescript: 5.0.0 → 5.2.0

移除依賴:
  📦 moment (已用 date-fns 替代)
```

### 7️⃣ 風險評估
```
🟢 低風險 (2 項):
  - 文檔更新
  - 單元測試新增

🟡 中風險 (3 項):
  - 新的前端模塊
  - 數據庫字段修改
  - 第三方庫依賴新增

🔴 高風險 (1 項):
  - API 端點變更 (會影響現有客戶端)
  - 安全相關的修改 (session 處理)
```

### 8️⃣ 建議檢查清單
```
功能驗證:
  ☐ 驗證新增的儀表板功能是否完整
  ☐ 測試多條件搜索過濾的準確性
  ☐ 驗證修復後的登出功能

向後兼容性:
  ☐ 檢查舊客戶端是否能正常工作
  ☐ 驗證 API 版本管理策略
  ☐ 確認數據遷移方案

性能影響:
  ☐ 檢查新 API 的查詢性能
  ☐ 驗證前端構建大小是否增加過多
  ☐ 進行負載測試

安全審查:
  ☐ 驗證新 API 的權限控制
  ☐ 檢查用戶輸入驗證
  ☐ 確認 session 安全性

測試覆蓋:
  ☐ 確認新增功能有單元測試
  ☐ 運行集成測試
  ☐ 進行回歸測試
```

---

## 提交信息規範

此 Skill 基於 Conventional Commits 規範解析提交信息。標準格式：

```
<type>(<scope>): <subject>

<body>

<footer>
```

### 有效的 type：
- `feat` - 新功能
- `fix` - 修復
- `improve` - 改進/優化
- `refactor` - 重構
- `perf` - 性能優化
- `style` - 代碼風格
- `test` - 測試
- `docs` - 文檔
- `ci` - CI/CD
- `security` - 安全

### 示例提交信息：
```
feat(auth): 實現 JWT 認證機制

添加基於 JWT 的用戶認證系統，包括：
- Token 生成和驗證
- Token 刷新機制
- 登出時 Token 撤銷

Closes #123
```

---

## 報告生成流程

1. **收集提交信息** - 獲取當前分支相對於目標分支的所有提交
2. **解析提交** - 按照 Conventional Commits 分類解析
3. **提取功能** - 從提交信息中提取功能描述
4. **分析文件** - 統計變更的文件和模塊
5. **評估影響** - 評估對現有系統的影響
6. **生成報告** - 創建結構化的功能更新報告

---

## 最佳實踐

### 1. 編寫清晰的提交信息
```
✅ 好的例子：
feat(dashboard): 添加用戶統計小部件
improve(api): 優化用戶列表查詢性能
fix(auth): 修復 Token 過期後無法自動刷新的問題

❌ 不好的例子：
update code
fix stuff
changes
```

### 2. 一次提交解決一個問題
```
✅ 合理的提交：
- feat: 添加儀表板頁面
- feat: 添加統計圖表組件
- test: 添加儀表板測試

❌ 不合理的提交：
- feat: 添加儀表板、優化 API、修復 Bug、更新文檔
```

### 3. 使用 scope 標明模塊
```
feat(auth): 新增登錄功能
fix(payment): 修復支付超時問題
improve(database): 優化查詢索引
```

### 4. 在提交體中提供詳細說明
```
feat(dashboard): 實現用戶儀表板

新增用戶個人儀表板頁面，包含：
- 用戶基本信息展示
- 最近活動統計
- 快速操作菜單

相關 API 端點：
- GET /api/users/{id}/dashboard
- PUT /api/users/{id}/preferences
```

---

## 常見問題

### Q: 為什麼某些提交沒有被分類？
**A**: 檢查提交信息是否遵循 Conventional Commits 規範。不符合規範的提交會被列為"其他變更"

### Q: 如何在報告中看到更詳細的功能描述？
**A**: 在提交信息的 body 中添加詳細說明，例如：
```
feat(feature-name): 簡短描述

這是詳細的功能描述，會在報告中展示
- 功能特性 1
- 功能特性 2
- 功能特性 3
```

### Q: 風險評估是如何計算的？
**A**: 根據以下因素：
- 涉及的文件數量
- API 變更的範圍
- 數據庫結構變更
- 安全相關修改
- 依賴版本更新

---

## 工作流示例

### 典型的功能開發和發佈流程

```
1. 創建功能分支
   git checkout -b feature/new-dashboard main

2. 開發功能並提交（遵循 Conventional Commits）
   git commit -m "feat: 添加儀表板頁面"
   git commit -m "feat: 添加統計圖表"
   git commit -m "improve: 優化加載性能"

3. 準備合併時檢查功能
   features main

4. 查看功能報告，驗證所有內容
   - 確認功能完整性
   - 檢查影響範圍
   - 評估風險等級

5. 根據報告進行測試和調整
   npm test
   npm run lint

6. 如果一切正常，創建 MR
   glab mr create -f --reviewer team-members

7. 經過代碼審查後合併
   glab mr merge
```

---

## 相關命令

與此 Skill 配合使用：

```bash
# 查看具體的代碼變更
git diff main feature/branch-name

# 查看提交詳情
git log main..feature/branch-name --oneline

# 運行測試
npm test

# 檢查代碼風格
npm run lint

# 創建 Merge Request
glab mr create -f --reviewer team-members
```

---

## 輸出示例

執行 `features main` 後的報告片段：

```
當前分支: feature/user-dashboard
目標分支: main
領先提交數: 8

📊 變更統計：
  🆕 新功能: 3
  🔧 改進: 2
  🐛 Bug 修復: 1
  📚 文檔: 1

🆕 新增功能：

1. 用戶儀表板
   feat: 實現用戶個人儀表板
   提交: abc1234
   
   功能描述：
   - 用戶統計信息展示
   - 實時數據更新
   - 可自定義小部件配置
   
   受影響文件: 5 個
   新增代碼: 342 行
   
   檢查建議:
   ✓ 驗證儀表板加載性能
   ✓ 測試小部件自定義功能
   ✓ 確認移動端適配

...
```

---

## 更新日誌

**v1.0.0** (2024-03-18)
- 首次發布
- 支持功能變更分析
- 支持 Conventional Commits 分類
- 支持風險評估和建議清單