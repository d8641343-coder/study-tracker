# 會考讀書紀錄 — 部署步驟

單一 `index.html`，部署在 GitHub Pages，後端使用 Firebase（Google 登入 + Firestore）。
未填 Firebase 設定時會進入「示範模式」，資料只存在瀏覽器，可先試用所有功能。

## 1. 建立 Firebase 專案（免費 Spark 方案即可）
1. https://console.firebase.google.com → 新增專案
2. **Authentication** → 開始使用 → 登入方式 → 啟用 **Google**
3. **Authentication → 設定 → 授權網域** → 新增 `你的帳號.github.io`
4. **Firestore Database** → 建立資料庫（位置建議 `asia-east1` 台灣）→ 正式版模式
5. **專案設定 → 一般 → 你的應用程式** → 新增「網頁」應用程式 → 複製 `firebaseConfig`

## 2. 修改 index.html 的 CONFIG
```js
firebase: { apiKey: "...", authDomain: "...", projectId: "...", appId: "..." },
adminEmails: ["你的管理者@gmail.com"],
```
會考日期、提醒天數、預設每日目標也在同一區塊。

## 3. 設定 Firestore 規則
把 `firestore.rules` 內的 `d8641343@gmail.com` 改成同一個管理者信箱，
貼到 **Firestore → 規則** → 發布。

## 4. 部署到 GitHub Pages
新 repo（或沿用既有）→ 上傳 `index.html` → Settings → Pages → Branch: main / root。

## 使用流程
- 管理者用名單內的 Gmail 登入 → 自動成為已核准管理者
- 其他人登入 → 狀態「待核准」→ 管理者按右上角「管理」核准
- 管理者可再把其他人「設為管理者」、停用或刪除帳號

## 注意
- 從 LINE 內建瀏覽器開啟時 Google 登入可能失敗，請改用 Chrome / Safari 開啟
- 大頭貼會縮成 160×160 JPEG 存在 Firestore（約 10KB），不需要 Firebase Storage（Storage 需付費方案）
- 計時狀態存在雲端：在手機按開始、電腦上也看得到計時，關掉網頁再開也會繼續
- 首頁載入近 90 天資料；使用人數少（家庭、班級）時免費額度綽綽有餘
