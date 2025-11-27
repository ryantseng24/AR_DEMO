# Dr. T-Bear WebAR Demo

基於 MindAR.js 的圖像追蹤 WebAR 應用程式，用於課堂展示。

## 檔案結構

```
AR_DEMO/
├── index.html                    # 主程式
├── targets.mind                  # MindAR 辨識圖檔 (需自行產生)
├── bear+scientist+3d+model.glb   # 3D 熊模型
├── Target_image.png              # 原始辨識圖
└── README.md                     # 說明文件
```

## 快速開始

### 1. 產生 .mind 辨識圖檔

**方法 A：使用線上工具 (推薦)**

1. 前往 MindAR 官方圖像編譯器：
   https://hiukim.github.io/mind-ar-js-doc/tools/compile

2. 點擊「Select Images」上傳你的 `Target_image.png`

3. 點擊「Start」開始編譯

4. 編譯完成後點擊「Download」下載 `targets.mind`

5. 將下載的 `targets.mind` 放到專案根目錄

**方法 B：使用 Node.js 命令列工具**

```bash
# 安裝 MindAR 編譯工具
npm install -g mind-ar

# 編譯圖像
mindar-compile Target_image.png -o targets.mind
```

### 2. 本機測試

由於 WebAR 需要 HTTPS 或 localhost，請使用本地伺服器：

```bash
# 方法 1：Python
python3 -m http.server 8080

# 方法 2：Node.js
npx serve .

# 方法 3：VS Code Live Server 擴充套件
```

然後在手機瀏覽器開啟：`http://<你的電腦IP>:8080`

**注意：** 手機和電腦需在同一個 Wi-Fi 網路下。

### 3. 部署到 GitHub Pages

詳見下方「GitHub Pages 部署」章節。

## 辨識圖建議

為了獲得最佳追蹤效果，辨識圖應該：

- **高對比度**：有明顯的黑白或顏色對比
- **豐富細節**：避免大面積純色區域
- **非對稱**：圖案不要左右或上下對稱
- **解析度**：建議 512x512 ~ 1024x1024 像素
- **格式**：JPG 或 PNG

## 自訂調整

### 調整模型大小與位置

編輯 `index.html` 中的 `<a-gltf-model>` 標籤：

```html
<a-gltf-model
  src="#bearModel"
  position="0 0 0.1"      <!-- X Y Z 位置 -->
  scale="0.15 0.15 0.15"  <!-- 縮放比例 -->
  rotation="0 0 0"        <!-- 旋轉角度 -->
>
```

### 調整動畫速度

```html
<!-- 旋轉速度：dur 越大越慢 (毫秒) -->
animation__rotate="... dur: 10000; ..."

<!-- 浮動速度：dur 越大越慢 -->
animation__float="... dur: 2000; ..."
```

### 更換 3D 模型

1. 將新的 `.glb` 檔案放入專案目錄
2. 修改 `<a-asset-item>` 的 `src` 屬性：

```html
<a-asset-item id="bearModel" src="./your-model.glb"></a-asset-item>
```

## GitHub Pages 部署

### 步驟 1：建立 GitHub 儲存庫

1. 前往 https://github.com/new
2. 建立新的儲存庫（例如：`ar-demo`）
3. 設為 Public

### 步驟 2：推送程式碼

```bash
cd /Users/ryan/project/Marketing\ Management/AR_DEMO

# 初始化 Git
git init

# 加入所有檔案
git add .

# 提交
git commit -m "Initial commit: WebAR demo with MindAR.js"

# 設定遠端 (替換成你的 GitHub 帳號)
git remote add origin https://github.com/YOUR_USERNAME/ar-demo.git

# 推送
git branch -M main
git push -u origin main
```

### 步驟 3：啟用 GitHub Pages

1. 前往儲存庫的 Settings → Pages
2. Source 選擇「Deploy from a branch」
3. Branch 選擇「main」和「/ (root)」
4. 點擊 Save

### 步驟 4：存取你的 AR 網頁

約 1-2 分鐘後，網頁將可透過以下網址存取：

```
https://YOUR_USERNAME.github.io/ar-demo/
```

## 故障排除

### 相機無法啟動

- 確認瀏覽器已授權相機權限
- iOS Safari 需使用 HTTPS（GitHub Pages 預設提供）
- 嘗試重新整理頁面

### 無法辨識圖像

- 確認 `targets.mind` 檔案存在且路徑正確
- 確保有足夠光線照射辨識圖
- 嘗試調整手機與辨識圖的距離
- 確認辨識圖沒有反光或褶皺

### 模型不顯示或太小

- 檢查 `.glb` 檔案路徑是否正確
- 調整 `scale` 屬性（嘗試 0.5 或 1.0）
- 開啟瀏覽器開發者工具檢查錯誤訊息

### iOS 裝置問題

- 使用 Safari 瀏覽器（Chrome iOS 相機支援有限）
- 確認 iOS 版本 >= 14.0

## 技術架構

- **A-Frame**: 1.5.0 - 3D/VR 框架
- **MindAR**: 1.2.5 - 圖像追蹤引擎
- **WebXR**: 瀏覽器原生 AR API

## 授權

MIT License - 自由使用於教學與商業用途
