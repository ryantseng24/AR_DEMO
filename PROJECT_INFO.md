# Dr. T-Bear WebAR Demo - 專案資訊

## 專案概述

課堂展示用的 WebAR 應用程式，使用 MindAR.js 進行圖像追蹤，當手機掃描特定海報時顯示 3D 熊模型。

---

## 線上網址

| 項目 | 網址 |
|------|------|
| **GitHub Pages (AR 網頁)** | https://ryantseng24.github.io/AR_DEMO/ |
| **GitHub 儲存庫** | https://github.com/ryantseng24/AR_DEMO |

---

## 檔案結構

```
AR_DEMO/
├── index.html                    # 主程式 (WebAR 應用)
├── targets.mind                  # MindAR 辨識圖檔 (編譯後)
├── bear+scientist+3d+model.glb   # 3D 熊模型 (26 MB)
├── Target_image.png              # 原始辨識圖 (6 MB)
├── README.md                     # 使用說明
├── PROJECT_INFO.md               # 本檔案 - 專案資訊
└── .gitignore                    # Git 忽略設定
```

---

## 技術規格

| 項目 | 版本/值 |
|------|---------|
| A-Frame | 1.5.0 |
| MindAR | 1.2.5 |
| 3D 模型格式 | GLB (glTF Binary) |
| 模型縮放 | 0.5 |
| 部署平台 | GitHub Pages |

---

## 目前動畫設定

```html
<!-- 旋轉：Y 軸 360 度，10 秒一圈 -->
animation__rotate="property: rotation; to: 0 360 0; dur: 10000; loop: true"

<!-- 浮動：上下移動 0.05 單位，2 秒一次 -->
animation__float="property: position; from: 0 0 0.1; to: 0 0.05 0.1; dur: 2000; dir: alternate; loop: true"

<!-- 出現動畫：彈性縮放 -->
animation__scale-in="property: scale; from: 0 0 0; to: 0.5 0.5 0.5; dur: 800; easing: easeOutElastic"
```

---

## 燈光設定

| 類型 | 強度 | 位置/說明 |
|------|------|----------|
| Ambient | 1.5 | 環境光 |
| Hemisphere | 1.5 | 天空反射 |
| Directional | 2.0 | 右上前方 (1, 2, 2) |
| Directional | 1.5 | 左側 (-2, 1, 1) |
| Directional | 1.0 | 後方 (0, 1, -2) |

**渲染器設定：**
- `exposure: 2` - 曝光度
- `toneMapping: ACESFilmic` - 色調映射
- `physicallyCorrectLights: false` - 關閉物理正確光照

---

## 常用調整

### 調整模型大小
編輯 `index.html` 第 206 行：
```html
scale="0.5 0.5 0.5"  <!-- 改成 1.0 會變 2 倍大 -->
```

### 調整旋轉速度
編輯 `animation__rotate` 的 `dur` 值：
```html
dur: 10000  <!-- 毫秒，數字越大轉越慢 -->
```

### 調整亮度
編輯第 175 行的 `exposure` 值：
```html
exposure: 2  <!-- 數字越大越亮 -->
```

---

## 更換辨識圖

1. 準備新的圖片 (建議 512x512 ~ 1024x1024)
2. 前往 https://hiukim.github.io/mind-ar-js-doc/tools/compile
3. 上傳圖片，點擊 Start
4. 下載 `targets.mind` 並取代舊檔案
5. 推送到 GitHub：
   ```bash
   cd "/Users/ryan/project/Marketing Management/AR_DEMO"
   git add targets.mind
   git commit -m "Update target image"
   git push
   ```

---

## 更換 3D 模型

1. 準備新的 `.glb` 檔案
2. 放到專案目錄
3. 編輯 `index.html` 第 185 行：
   ```html
   <a-asset-item id="bearModel" src="./your-new-model.glb"></a-asset-item>
   ```
4. 推送到 GitHub

---

## 可用動畫效果

### 位置動畫
```html
<!-- 左右移動 -->
animation="property: position; from: -0.2 0 0.1; to: 0.2 0 0.1; dur: 2000; dir: alternate; loop: true"
```

### 旋轉動畫
```html
<!-- 搖擺 -->
animation="property: rotation; from: 0 -30 0; to: 0 30 0; dur: 1000; dir: alternate; loop: true"
```

### 縮放動畫
```html
<!-- 呼吸效果 -->
animation="property: scale; from: 0.45 0.45 0.45; to: 0.55 0.55 0.55; dur: 1500; dir: alternate; loop: true"
```

### 組合多個動畫
使用不同的 `animation__名稱` 即可同時播放多個動畫。

---

## 本機測試方式

```bash
cd "/Users/ryan/project/Marketing Management/AR_DEMO"

# Python 伺服器
python3 -m http.server 8080

# 或 Node.js
npx serve .
```

手機瀏覽器開啟：`http://<電腦IP>:8080`

---

## Git 常用指令

```bash
cd "/Users/ryan/project/Marketing Management/AR_DEMO"

# 查看狀態
git status

# 提交變更
git add .
git commit -m "描述訊息"
git push

# 查看歷史
git log --oneline
```

---

## 疑難排解

| 問題 | 解決方案 |
|------|----------|
| 相機無法啟動 | 確認已授權相機權限，iOS 用 Safari |
| 無法辨識圖像 | 確保光線充足，避免反光 |
| 模型太暗 | 增加 `exposure` 值或燈光 `intensity` |
| 模型太小 | 增加 `scale` 值 |
| GitHub Pages 沒更新 | 等 1-2 分鐘，或強制重整 (Ctrl+Shift+R) |

---

## 建立日期

2024-11-27

---

## 相關資源

- [MindAR 官方文件](https://hiukim.github.io/mind-ar-js-doc/)
- [MindAR 圖像編譯器](https://hiukim.github.io/mind-ar-js-doc/tools/compile)
- [A-Frame 文件](https://aframe.io/docs/)
- [A-Frame 動畫組件](https://aframe.io/docs/1.5.0/components/animation.html)
