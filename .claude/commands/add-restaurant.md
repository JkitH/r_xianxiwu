# 新增餐廳頁面

使用者會提供一間餐廳的 Google Maps 資訊（可能是連結、截圖、或文字描述）。你需要完成以下三個步驟：

## 輸入參數
$ARGUMENTS - 使用者提供的 Google Maps 餐廳資訊（連結、文字、或截圖描述）

## 步驟一：從 Google Maps 資訊中提取餐廳資料

從使用者提供的資訊中，盡可能提取以下欄位：
- **餐廳名稱**（必填）
- **地址**（完整中文地址 + 英文地址）
- **電話**
- **營業時間**
- **Google 評分** 與 評論數
- **料理類型 / 分類標籤**（例如：日式豬排、拉麵、夜市小吃）
- **價格範圍**
- **菜品名稱與描述**（如有）
- **圖片**（如有提供圖片，存到 `images/` 資料夾）
- **Google Maps 連結**
- **其他平台評分**（Uber Eats、Facebook 等，如有）
- **交通 / 位置描述**
- **特色描述**

如果資訊不足，主動詢問使用者補充。至少需要：餐廳名稱、地址、料理類型。

## 步驟二：建立餐廳子頁面

1. 在專案根目錄建立以餐廳名稱命名的資料夾：`{餐廳名稱}/index.html`
2. 頁面結構必須參考現有的 `饗食屋/index.html` 作為模板，保持一致的設計風格
3. 重要注意事項：
   - 圖片路徑使用 `../images/xxx.jpg`（因為在子資料夾）
   - Google AdSense 代碼保留：`ca-pub-8324776235187705`
   - 必須包含 Schema.org Restaurant 結構化資料
   - 必須包含麵包屑導航，連結回首頁
   - 配色方案可以根據餐廳風格微調，但整體設計語言保持一致
   - meta description、keywords、og tags 都要針對該餐廳 SEO 優化

### 子頁面必備區塊（參考饗食屋模板）：
- `<header>` — 餐廳名稱 + 副標題
- 麵包屑導航（含返回首頁連結）
- Hero 圖片區
- 資訊卡片（地址、電話、營業時間、價格範圍、交通、餐廳類型）
- 評分與評論區
- 關於餐廳介紹
- 推薦菜品
- 餐廳圖片 gallery（如有多張圖片）
- 顧客評論
- CTA 區塊（致電、線上訂餐、Google 地圖）
- Footer

## 步驟三：在首頁新增餐廳卡片

1. 讀取根目錄的 `index.html`
2. 在 `<div class="restaurant-grid">` 中，在「更多餐廳 Coming Soon」佔位卡片**之前**插入新的餐廳卡片
3. 卡片格式參考以下模板（根據實際資料填入）：

```html
<!-- {餐廳名稱} -->
<a href="./{餐廳名稱}/" class="restaurant-card" aria-label="前往{餐廳名稱}介紹頁面">
    <img src="images/{圖片檔名}" alt="{餐廳名稱}招牌菜" class="card-image" loading="lazy">
    <div class="card-body">
        <div class="card-tags">
            <span class="tag">{料理類型}</span>
            <span class="tag area">{區域}</span>
        </div>
        <h3>{餐廳名稱}</h3>
        <p class="subtitle">{一句話描述}</p>
        <div class="card-meta">
            <span>📍 {城市}{區域}</span>
            <span>⏰ {營業時間}</span>
        </div>
        <div style="margin-bottom: 14px; display: flex; gap: 10px; flex-wrap: wrap;">
            <span class="rating-badge">⭐ {評分} <small style="font-weight:400;">{平台}</small></span>
        </div>
        <div class="card-footer">
            <span class="price-range">💰 {價格範圍}</span>
            <span class="read-more">查看詳情 →</span>
        </div>
    </div>
</a>
```

4. 同時更新首頁的以下內容：
   - Schema.org `ItemList` 的 `numberOfItems` 數字 +1，並新增 `ListItem`
   - `header-stats` 中的餐廳數量
   - 如果新餐廳屬於新地區或新料理類型，更新對應分類的計數
   - Footer 的精選餐廳連結清單

## 步驟四：驗證

1. 確認子資料夾和檔案已建立
2. 確認圖片路徑正確（子頁面用 `../images/`，首頁用 `images/`）
3. 確認首頁卡片連結可正確指向子頁面
4. 如果有 preview 功能，開啟預覽檢查頁面外觀

## 範例互動

使用者：`/add-restaurant https://maps.app.goo.gl/xxxxx`

你應該：
1. 從連結中擷取餐廳資訊（如需要可使用 WebFetch）
2. 向使用者確認提取的資訊是否正確，是否需要補充
3. 執行步驟二和步驟三
4. 回報完成結果
