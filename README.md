# 線上求籤系統 — 快速換廟指南

## 檔案結構

```
temple-oracle/
├── index.html      ← 主程式（不需修改）
├── config.js       ← 宮廟設定（唯一需要改的檔案）
├── logo.png        ← 替換為各廟 Logo（選填）
├── temple-bg.jpg   ← 替換為廟宇背景圖（選填）
└── README.md
```

---

## 換廟流程（5 分鐘完成）

### Step 1：修改 config.js 頂部基本資訊
```js
name:     "你的廟名",
subtitle: "線上求籤解籤服務",
deity:    "主神名稱",
```

### Step 2：修改主題色
```js
theme: {
  primary:   "#8B1A1A",   // 主色（深廟紅）← 依廟調整
  secondary: "#C8960C",   // 輔色（金）
  bg:        "#1a0a00",   // 頁面底色
  cardBg:    "#2a1200",   // 卡片底色
}
```

常見廟色參考：
| 廟宇類型   | primary     | bg        |
|-----------|-------------|-----------|
| 紅廟（一般）| #8B1A1A    | #1a0a00   |
| 藍廟（媽祖）| #1A3A6B    | #000a1a   |
| 黃廟（土地）| #8B6914    | #1a1200   |
| 綠廟（藥王）| #1A5C2A    | #001a08   |

### Step 3：加入籤詩資料庫
在 `lots` 陣列中加入該廟的籤詩，每首格式：
```js
{
  id: 1,                      // 籤號
  level: "大吉",               // 吉凶等級
  poem: "籤詩原文四句",         // 支援 \n 換行
  meaning: "籤詩解義說明",
  advice: "神示建議",
  fortune: {
    overall: "總運說明",
    love:    "感情運",
    career:  "事業運",
    health:  "健康運",
    wealth:  "財運"
  }
}
```

### Step 4：設定 Logo 與背景圖（選填）
```js
logoUrl:    "./logo.png",       // 廟方 Logo（建議 400×400px）
bgImageUrl: "./temple-bg.jpg",  // 廟宇背景圖（會以低透明度疊加）
```

### Step 5：上傳至主機
直接上傳整個資料夾到任何靜態主機即可，無需後端：
- GitHub Pages
- Netlify（拖曳上傳）
- 傳統虛擬主機（FTP 上傳）

---

## 之後接 LLM 解籤（選填升級）

在 `index.html` 底部已有預留 hook：
```js
async function getLLMInterpretation(lot, userQuestion) {
  // 接入 Claude API 或自建後端
}
```

升級時只需：
1. 架設後端（Node.js / Python）
2. 在 `showResult()` 函式中呼叫此函式
3. 將 LLM 結果渲染到 `.meaning-text` 與 `.advice-text`

---

## 吉凶等級對照

| 等級 | 顏色   | 說明             |
|------|--------|-----------------|
| 大吉 | 金黃色 | 最佳運勢         |
| 中吉 | 橙色   | 運勢良好         |
| 小吉 | 淺綠色 | 小有吉象         |
| 平   | 棕色   | 平穩無大起伏     |
| 小凶 | 淡紫色 | 稍需注意         |
| 中凶 | 淺紅色 | 需謹慎           |
| 大凶 | 亮紅色 | 最需謹慎         |
