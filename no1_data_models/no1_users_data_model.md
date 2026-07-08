# 資料結構

## 使用者自訂資料結構

### 使用者 User

- **欄位:**
  - `uid`: String, Auth UID - Primary Key, Not Null, 與 Document ID 相同
  - `email`: String - Not Null, 使用者 Email
  - `displayName`: String | Null - Nullable, 顯示名稱，來自 Google 帳號
  - `photoURL`: String | Null - Nullable, 大頭照 URL，來自 Google 帳號
  - `provider`: String - Not Null, 認證提供者
  - `preferences.language`: String - Not Null, Default `zh-TW`, 介面語言，支援 `zh-TW` 與 `en`
  - `preferences.currency`: String - Not Null, Default `TWD`, 主要貨幣 ISO 4217 代碼
  - `preferences.timeZone`: String - Not Null, Default `Asia/Taipei`, 時區，採 IANA 格式
  - `preferences.theme`: String - Not Null, Default `theme1`, 主題識別碼
  - `preferences.launchMode`: String - Not Null, Default `home`, 啟動模式，可為 `home`、`expense`、`income`、`transfer`
  - `preferences.weekStart`: String - Not Null, Default `auto`, 週起始日偏好，可為 `auto`、`sunday`、`monday`；`auto` 代表依使用者語系慣例決定
  - `preferences.analyticsConsent`: Boolean - Not Null, Default `true`, 分析同意開關，控制記帳資料是否納入分析管線
  - `iap_entitlements_json`: String | Null - Nullable, JSON, 序列化後的 IAP 權限狀態
  - `iap_active_purchases_json`: String | Null - Nullable, JSON, 序列化後的作用中訂閱
  - `lastLoginAt`: Number, Unix Timestamp ms - Not Null, 使用者最後登入時間
  - `createdOn`: Number, Unix Timestamp ms - Not Null, 使用者首次建立時間
  - `updatedOn`: Number, Unix Timestamp ms - Not Null, 最後更新時間

**偏好欄位性質**: `preferences.*` 群為裝置單向上傳的鏡像，記錄各裝置最後寫入值，僅供資料分析維度。本機為偏好唯一真相，雲端永不下發回裝置。多裝置各自上傳，接受欄位級覆寫不一致。Default 僅在文件建立時套用，裝置不從雲端下載偏好。
