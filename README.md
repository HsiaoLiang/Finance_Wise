# Finance Wise

把 Wise 匯出的交易 CSV，變成一頁看得懂的消費總覽。整個 App 就是**一個 `index.html`**：沒有後端、沒有建置流程、沒有依賴套件，資料不會離開你的瀏覽器。

## 功能

- **消費分析** — 支出趨勢、類別占比、商家排行、一週消費節奏、累計支出、異常交易偵測
- **帳務總覽** — 帳戶餘額、收入來源分類、收支流向、本月預估
- **預算** — 依幣別與類別設定預算，追蹤使用進度
- **交易紀錄** — 搜尋、篩選日期區間、逐筆明細、自訂分類與標籤規則
- 深淺色主題、匯出篩選後的 CSV

## 使用方式

### 1. 線上直接開

開 [GitHub Pages 頁面](https://hsiaoliang.github.io/Finance_Wise/)，點「選擇檔案」或直接把 Wise 的 CSV 拖進頁面。檔案只在瀏覽器本機解析，不會上傳到任何伺服器。

### 2. 在本機跑（可自動讀取資料夾裡的 CSV）

```bash
git clone https://github.com/HsiaoLiang/Finance_Wise.git
cd Finance_Wise
python3 -m http.server 8777
```

然後開 http://localhost:8777 。

把 Wise 匯出的檔案放成 `Sources/Wise Transaction History.csv`，頁面載入時就會自動讀取，按「重新讀取」可更新到最新內容。

## 取得 Wise CSV

Wise → Balances → Statement → 選擇幣別與日期區間 → 下載 **CSV**。

## 設定檔

規則、預算、偏好存在 `finance-wise-settings.json`（與 `index.html` 同層）。複製範本開始：

```bash
cp finance-wise-settings.example.json finance-wise-settings.json
```

在 Chrome / Edge 可以用設定面板的「連結設定檔」直接寫回這個檔案；其他瀏覽器則用「下載一份」再覆蓋。

## 隱私

`Sources/*.csv` 和 `finance-wise-settings.json` 已列入 `.gitignore`，不會被提交。這個 repo 裡沒有任何真實交易資料。
