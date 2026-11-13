# 權重裡的晶片指紋：六個中國前沿模型的起點，對上受管制的 NVIDIA Blackwell

深度導讀。原報告由 Will DePue 發表於 Unemployment Labs（2026 年 11 月 12 日），從中國實驗室公開的模型權重還原初始化時的 GPU 執行緒排列，指出 DeepSeek、月之暗面、MiniMax、螞蟻集團共六個模型的起點符合受管制的 NVIDIA Blackwell。

線上閱讀：https://lushinshang.github.io/checkpoint-forensics-blackwell/

## 200字介紹

模型開始訓練前，每個權重都要先有初始值，PyTorch 在 NVIDIA GPU 上用平行執行緒填這些值，執行緒數取決於晶片的 SM 數，所以同一個種子在 Hopper（132 個 SM）與 Blackwell（148／152 個 SM）上填出的位置不同。作者從公開權重裡沒被訓練動過的列，反推種子與排列，再拿沒參與搜尋的權重驗證，認出四家中國實驗室的六個新模型起點是 Blackwell。這份證據只證明初始化用了哪類晶片，不能證明晶片在哪裡、怎麼取得，也不是違法認定。導讀逐項交代這些邊界，並依官方文件補述現行出口規則管得到什麼。

## 檔案

| 檔案 | 說明 |
|---|---|
| `index.html` | 發布網頁本體（含頁首互動格狀圖與 SM 數互動元件） |
| `images/` | 網頁用圖：封面與概念圖各含橫式／直式，SVG 圖各含桌面／手機版 |
| `checkpoint-forensics-blackwell.md` | 導讀 Markdown 原稿 |

## 原始素材與查證來源

- 原報告：https://unemploymentlabs.com/checkpoint-forensics
- 重現用程式碼：https://github.com/macrogrants/checkpoint-forensics
- 其餘新聞與官方文件來源列在導讀文末「來源」。

## 製作說明

本文由 AI（Claude）閱讀原報告後撰寫，未經人工逐句審稿；原報告的實驗沒有另行重跑。
