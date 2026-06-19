# PikPak 轉 Google Drive 完整教學：三種方法實測對比，哪種最穩、最省事？（含 PikPak 免費試用邀請碼與套餐一覽）

你有沒有遇過這樣的狀況：PikPak 裡存了一堆離線下載的影片、資料，但總覺得放在 Google Drive 更安心——畢竟 Google 的協作和備份生態更成熟。

問題來了：PikPak 轉 Google Drive，到底怎麼搞？

這篇文章就是要把這件事講清楚。三種主流方法，各自的優缺點和適合的人，一篇搞定。

---

## 為什麼有人想把 PikPak 的檔案搬到 Google Drive？

先說說背景，不然有些人可能不太理解這需求從哪裡來。

PikPak 是一個來自新加坡的私密雲端硬碟，最大特色是「雲端離線下載」——你把磁力連結、BT 種子、甚至 Twitter/Telegram 上的影片連結丟進去，PikPak 的伺服器幫你把檔案抓下來，存到你的網盤裡。速度極快，超過 80% 的檔案幾秒內就能完成。Premium 會員還有 10TB 的超大儲存空間。

但 PikPak 的定位是「下載與媒體儲存」，協作功能很弱，也沒有 Google Docs / Sheets 那種整合生態。所以很多人的使用習慣是：用 PikPak 抓資源，再搬到 Google Drive 長期備份或分享。

另外，Google Drive 提供更完善的安全機制（SSL 加密、兩步驟驗證），對於把檔案長期保存的需求來說，更讓人放心。

👉 [先用邀請碼 74098243 免費試用 PikPak，體驗離線下載功能](https://mypikpak.com?invitation-code=74098243)

---

## 方法一：用 CloudsLinker 傳輸（最省事，適合不想碰命令列的人）

這是目前最直觀的方式，整個過程在瀏覽器裡完成，不用裝軟體、不用碰命令列。

CloudsLinker 是一個雲端對雲端的檔案傳輸工具，支援超過 30 種雲端服務之間的直接轉移，不會佔用你本機的網路頻寬。

**步驟大致如下：**

1. 登入 CloudsLinker，把你的 Google Drive 帳號連結進去（授權 OAuth 即可）。
2. 新增 PikPak 帳號：在介面裡選 PikPak，輸入你的帳號和密碼。
   - 注意：如果你是用 Google 帳號登入 PikPak 的，PikPak 本身沒有密碼，需要先到 PikPak 網頁版 → 帳號與安全 → 設定密碼，才能在 CloudsLinker 裡登入。
3. 進入「Transfer」功能，設定來源為 PikPak、目標為 Google Drive，選好你要搬移的資料夾。
4. 可以設定篩選條件（比如只搬特定類型的檔案），也可以排程定期自動同步。
5. 在 Task 頁面追蹤傳輸進度，完成後到 Google Drive 確認檔案都到位了。

**優點：** 圖形介面，操作直覺，零技術門檻。  
**缺點：** 免費版只有 10GB 傳輸量，大量資料需要付費方案。

---

## 方法二：用 RiceDrive 搭配 PikPak WebDAV（中等難度，適合有一點技術基礎的人）

這個方法利用 PikPak 的 WebDAV 功能作為橋樑，再用 RiceDrive 把兩個雲端連起來。

**第一步：開啟 PikPak 的 WebDAV 功能**

PikPak 官方在網頁版提供了 WebDAV 支援（實驗室功能），進入路徑是：設定 → 實驗室功能 → 啟用 WebDAV。啟用後可以看到連接地址、帳號和密碼。

需要注意的是，PikPak 官方的 WebDAV 目前只支援「讀取」操作，而且只對 Premium 會員開放。Windows 資源管理器連接時偶爾也會有相容性問題。

**第二步：用 RiceDrive 連接兩端**

登入 RiceDrive，在「Link Storage」裡分別新增 PikPak 帳號和 Google Drive 帳號。連接成功後，你可以直接在 RiceDrive 介面裡把 PikPak 的檔案複製或移動到 Google Drive。

**優點：** 穩定度不錯，同樣不需要下載到本機。  
**缺點：** 需要 PikPak Premium 才能使用官方 WebDAV；免費傳輸流量有上限。

---

## 方法三：用 Rclone 直接操作（最靈活，適合技術用戶）

Rclone 是一個開源的命令列工具，原生支援 PikPak 作為後端，也支援 Google Drive。這意味著你可以直接用一條命令，把 PikPak 的資料夾複製到 Google Drive，整個過程在雲端之間完成，不需要本機暫存。

**基本流程：**

1. 安裝 Rclone，執行 `rclone config` 建立 PikPak 遠端配置，輸入你的郵箱和密碼。
2. 再次執行 `rclone config` 建立 Google Drive 遠端配置，完成 OAuth 授權。
3. 使用複製指令：


rclone copy pikpak:"My Pack" gdrive:"PikPak Import" -P


這條指令會把 PikPak 裡的 My Pack 目錄複製到 Google Drive 的 PikPak Import 資料夾，`-P` 參數顯示進度。

如果你覺得命令列太麻煩，也可以用 **RcloneView**——Rclone 的圖形介面版本，內建 rclone，雙欄瀏覽器設計，左邊 PikPak、右邊 Google Drive，拖拉或用 Job Wizard 設定傳輸任務都可以。建議先跑一次 dry run（模擬執行），確認沒問題再正式開始。

**優點：** 完全免費、靈活度最高、支援自動排程（配合 cron）。  
**缺點：** 需要一點命令列基礎；配置步驟比前兩種方法繁瑣。

---

## 三種方法快速對比

| 方法 | 難度 | 是否免費 | 需要 Premium？ | 適合對象 |
|------|------|----------|----------------|----------|
| CloudsLinker | ⭐ 低 | 限量免費（10GB） | 否 | 技術小白 |
| RiceDrive + WebDAV | ⭐⭐ 中 | 限量免費（10GB） | 是（官方 WebDAV） | 有基礎的用戶 |
| Rclone / RcloneView | ⭐⭐⭐ 中高 | 完全免費 | 否 | 技術用戶 |

如果你的資料量不大（幾十 GB 以內），CloudsLinker 免費額度基本夠用，最省事。資料量大的話，Rclone 是最划算的選擇，長期沒有費用限制。

---

## 開始之前：先確認你的 PikPak 帳號狀態

不管用哪種方法，有幾件事要提前確認：

**1. 密碼設定**  
如果你是用 Google 帳號快速登入 PikPak 的，你的 PikPak 帳號本身沒有獨立密碼。CloudsLinker、RiceDrive 等工具需要帳號密碼才能連接。解決方法：到 PikPak 網頁版 → 頭像 → 帳號與安全 → 重設密碼，設定一個密碼即可。

**2. 確認 Google Drive 儲存空間**  
Google Drive 免費提供 15GB，如果你要搬移的 PikPak 資料超過這個容量，需要先訂閱 Google One 擴充空間。

**3. 建立目標資料夾**  
在 Google Drive 裡先建立一個「PikPak Import」或類似名稱的資料夾，讓搬移過來的檔案統一落在一個地方，方便後續確認完整性。

---

## PikPak 套餐一覽

還沒有 PikPak 帳號的話，這裡是目前的方案資訊：

| 套餐 | 儲存空間 | 價格 | 購買連結 |
|------|----------|------|----------|
| 免費版 | 6GB | 免費 |  [免費注冊（邀請碼 74098243）](https://mypikpak.com?invitation-code=74098243) |
| Premium 月費 | 10TB | $10.00 / 月 |  [訂閱月費 Premium](https://mypikpak.com?invitation-code=74098243) |
| Premium 年費 | 10TB | $100.99 / 年（約 $8.42 / 月） |  [訂閱年費 Premium（省約 16%）](https://mypikpak.com?invitation-code=74098243) |

> 價格可能依地區和匯率有所不同，以購買頁面顯示為準。用邀請碼 **74098243** 注冊有機會獲得免費 Premium 體驗天數。

Premium 和免費版的核心差異就在儲存空間（6GB vs 10TB）以及下載速度優先級。如果你主要用 PikPak 來離線下載大型媒體檔案，Premium 幾乎是必要的。年費方案比月付省了大約 16%，長期使用的話明顯更划算。

---

## 幾個實際使用中的注意事項

**關於 WebDAV 的穩定性**

PikPak 官方的 WebDAV 實現目前有些不成熟的地方：Windows 資源管理器偶爾會把資料夾顯示成檔案、隨機性連接失敗等問題都有人反映過。如果遇到這些問題，用 Rclone 作為 WebDAV 後端是一個更穩定的替代方案——Rclone 支援 PikPak 完整的讀寫操作，比官方 WebDAV 更強大，而且免費。

**關於傳輸速度**

雲端對雲端的傳輸速度取決於兩個平台的伺服器之間的帶寬，和你本機網路關係不大。CloudsLinker 和 Rclone 理論上都不需要佔用你的本機流量，適合大量資料搬移。

**關於資料完整性**

無論用哪種工具，傳輸完成後都建議做一次比對：對比 PikPak 和 Google Drive 目標資料夾的檔案數量和總大小。Rclone 的 `rclone check` 指令可以做 MD5 校驗，確保每個檔案都完整複製過去。

---

總結來說，PikPak 轉 Google Drive 這件事沒有想象中複雜——工具已經把門檻降得很低了。你只需要根據自己的資料量和技術熟悉度，選一個最順手的方式就行。

👉 [用邀請碼 74098243 注冊 PikPak，有機會獲得免費 Premium 試用](https://mypikpak.com?invitation-code=74098243)
