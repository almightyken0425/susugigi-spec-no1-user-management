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
  - `iap_entitlements_json`: String | Null - Nullable, JSON, 序列化後的 IAP 權限狀態
  - `iap_active_purchases_json`: String | Null - Nullable, JSON, 序列化後的作用中訂閱
  - `lastLoginAt`: Number, Unix Timestamp ms - Not Null, 使用者最後登入時間
  - `createdOn`: Number, Unix Timestamp ms - Not Null, 使用者首次建立時間
  - `updatedOn`: Number, Unix Timestamp ms - Not Null, 最後更新時間
