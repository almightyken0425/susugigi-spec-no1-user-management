# CLAUDE.md

本 repo 為 SuSuGiGi 產品的 **Module Spec git**，module_id 為 `no1_user_management`，承載使用者管理的規格描述。

## 多層 git 配對

- **頂層 Product git：**
    - 位於 `../../`
    - 管理決策框架的上游各層
- **對側 Module Design git：**
    - 尚無
    - 本 module 無設計工件
- **本 Module Spec git：**
    - 即本 repo
    - 位於 Product git 的 `no3_product_specs/no1_user_management/`
- **對側 Module Impl git：**
    - 尚無
    - 本 module 屬純規格階段
    - auditor 盤點得 `PLAN_ONLY_DESIGN`，不扣整體評級

完整路徑與配對表由 `decision_framework_router` skill 的 `products_registry.md` 維護。

---

## 撰寫規範

所有規格文件依循以下分層政策。

- Model 層位於 `no1_data_models/`，套用 `spec_writer` 的 model 政策
- 未來若新增 View 層或 Logic 層比照同規範
- 所有 .md 額外套用 `universal_writing_linter` 通用政策

---

## 配對變動規則

本 module 尚無 Design git 與 Impl git，Spec 變動無下游對側檢查。需求根因與 Product Map 配對見頂層 Product git 的 `no2_product_planning/no2_product_map/firebase/authentication.md` 等平台服務文件。

當本 module 進入實作階段，需於 `no5_product_development/no1_user_management/` 建立對應 Impl git 並在 `products_registry.md` 更新。若本 module 進入設計工件階段，需於 `no4_product_designs/no1_user_management/` 建立對應 Design git。
