# MANDO 月營運報表

以週為單位的月度營運數據儀表板，部署在 GitHub Pages 上供股東查閱。

---

## 第一次設定（只需做一次）

### 1. 建立 GitHub Repo

1. 登入 [github.com](https://github.com) → 點右上角 **+** → **New repository**
2. Repository name 填 `mando-dashboard`（或任何名稱）
3. 選 **Public**（GitHub Pages 免費方案需要 Public）
4. 按 **Create repository**

### 2. 上傳所有檔案

把這個資料夾的所有內容上傳到 repo：

```
mando-dashboard/
├── index.html
├── data/
│   ├── index.json
│   └── 115-5月-銷售及庫存.xlsx
└── .github/
    └── workflows/
        └── update-index.yml
```

> 上傳方式：repo 頁面 → **Add file** → **Upload files** → 把整個資料夾拖進去

### 3. 開啟 GitHub Pages

1. repo 頁面 → **Settings** → 左側選單 **Pages**
2. Source 選 **Deploy from a branch**
3. Branch 選 **main**，資料夾選 **/ (root)**
4. 按 **Save**

幾分鐘後網址就會出現：`https://你的帳號.github.io/mando-dashboard/`

### 4. 開啟 Actions 權限

1. repo 頁面 → **Settings** → **Actions** → **General**
2. 往下找 **Workflow permissions**
3. 選 **Read and write permissions**
4. 按 **Save**

---

## 每週更新（日常操作）

### 上傳新的 Excel 檔

1. 進入 repo 的 `data/` 資料夾
2. 點 **Add file** → **Upload files**
3. 把新的 `.xlsx` 拖進去，檔名格式：`115-6月-銷售及庫存.xlsx`
4. 按 **Commit changes**

GitHub Actions 會自動更新 `index.json`，約 1 分鐘後網頁就會出現新月份。

### 檔名規則

```
115-5月-銷售及庫存.xlsx   ✅
115-6月-銷售及庫存.xlsx   ✅
116-1月-銷售及庫存.xlsx   ✅
```

年份-月份 開頭即可，後面的名稱不影響解析。

---

## Excel 格式說明

每個工作表代表一週，名稱格式為 `0427-0503`（月日-月日）。

網頁會自動讀取以下工作表，其他工作表（如彙總頁、計算機）會自動略過。

---

## 常見問題

**網頁顯示「找不到 data/index.json」**
→ 確認 `data/index.json` 已上傳，且 GitHub Actions 有執行權限。

**上傳新 Excel 後月份沒有出現**
→ 等待約 1 分鐘讓 Actions 執行完畢，再重新整理網頁。
→ 也可以到 repo 的 **Actions** 頁籤確認執行狀態。

**想手動更新 index.json**
→ 直接編輯 `data/index.json`，格式：
```json
[
  "115-5月-銷售及庫存.xlsx",
  "115-6月-銷售及庫存.xlsx"
]
```
