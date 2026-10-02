# 資料結構

## 使用者自訂資料結構

### 使用者 User

- **欄位:**
  - `uid`: String, Auth UID - Primary Key, Not Null, 與 Document ID 相同
  - `email`: String | Null - Nullable, 雲端不保留 Email。新建文件固定為 Null，包含 legacy 登入身分，不從認證資料取得 Email。歷史非空值屬待清理資料
  - `displayName`: String | Null - Nullable, 顯示名稱，來自認證提供者
  - `photoURL`: String | Null - Nullable, 大頭照 URL，來自認證提供者，Apple 帳號無此值
  - `provider`: String - Not Null, 認證提供者識別碼，可為 `anonymous`、`google.com`、`apple.com`。匿名身分使用 `anonymous`，既有 Google 與 Apple 登入身分保留實際提供者
  - `preferences.language`: String - Not Null, 介面語言的 BCP 47 代碼，取本機 Settings 實際值，不另設雲端預設。有效值為 `en`、`zh-Hant`、`zh-Hans`、`ja`、`ko`、`de`、`es`、`fr`、`pt-BR`、`it`、`nl`、`sv`、`da`、`no`、`fi`、`pl`、`id`、`vi`、`th`、`hi`
  - `preferences.currency`: String - Not Null, Default `TWD`, 主要貨幣 ISO 4217 代碼
  - `preferences.timezone`: String - Not Null, Default `Asia/Taipei`, 時區，採 IANA 格式，對應本機 Settings.timeZone
  - `preferences.theme`: String - Not Null, Default `theme1`, 主題識別碼
  - `preferences.launchMode`: String - Not Null, Default `home`, 啟動模式，可為 `home`、`expense`、`income`、`transfer`
  - `preferences.weekStart`: String - Not Null, Default `auto`, 週起始日偏好，可為 `auto`、`sunday`、`monday`；`auto` 代表依使用者語系慣例決定
  - `preferences.analyticsConsent`: Boolean - Not Null, Default `true`, 分析同意開關，控制記帳資料是否納入分析管線
  - `iap_entitlements_json`: String | Null - Nullable, JSON, 序列化後的 IAP 權限狀態
  - `iap_active_purchases_json`: String | Null - Nullable, JSON, 序列化後的作用中訂閱
  - `lastLoginAt`: Number, Unix Timestamp ms - Not Null, 使用者最後登入時間
  - `createdAt`: Number, Unix Timestamp ms - Not Null, 使用者首次建立時間
  - `updatedAt`: Number, Unix Timestamp ms - Not Null, 最後更新時間

**偏好欄位性質**: `preferences.*` 群為裝置單向上傳的鏡像，記錄各裝置最後寫入值，僅供資料分析維度。本機為偏好唯一真相，雲端永不下發回裝置。多裝置各自上傳，接受欄位級覆寫不一致。各欄所列 Default 僅在文件建立時套用，`preferences.language` 不設雲端預設。裝置不從雲端下載偏好。

**與 Accounting App 的關係**: 語系的 20 個有效值與 LanguageSettingScreen 支援清單一致，原值上傳。繁體中文使用 `zh-Hant`，不轉為 `zh-TW`。

- 歷史雲端語系可暫留 `zh-TW`，由裝置正常上傳本機實際語系時覆寫。長期未使用帳號可能持續保留舊值，不進行全庫批次遷移，也不因此遷移本機資料。
- 雲端正式欄位為 `preferences.timezone`、`createdAt` 與 `updatedAt`。歷史別名 `preferences.timeZone`、`createdOn` 與 `updatedOn` 不作為新寫入欄位，本機 `Settings.timeZone` 名稱不變。舊資料查核及必要遷移另案執行。
- 歷史 Email 清理只涵蓋雲端使用者文件的 `email`，目標值為 Null。認證帳號、本機 Email、`displayName` 與 `photoURL` 均不在清理範圍。
