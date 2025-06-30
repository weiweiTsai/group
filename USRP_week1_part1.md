---
marp: true
theme: default
paginate: true
class: lead
---
# 學、「作」、寫
# Part 1： VS Code 環境介紹與安裝流程
---
# 一、VS Code 環境介紹：打造你的 AI 數學料理工作坊

將數學推導與數值模擬比喻為製作一道料理，程式工具就是你的廚房與器具！

---

## 🔧 **VS Code**

**Microsoft 開發的開源程式編輯器**，支援多種語言與擴充功能，是目前主流開發環境之一。可整合 Python、Jupyter、Copilot 等套件。

### 在數學廚房中：

**＝ 🏠 廚房的工作檯與工具牆**

> 你在這裡整合所有流程：書寫筆記、撰寫程式、模擬模型，就像在中央料理台上處理所有烹飪任務。

---

## 📓 **Jupyter Notebook**

**互動式筆記本**，可同時包含：

* ✅ 程式碼 (Python)
* ✅ 說明文字（Markdown）
* ✅ 數學公式（$\LaTeX$）
* ✅ 圖表（Matplotlib）

### 在數學廚房中：

**＝ 🥣 鍋具與食譜合一的操作平台**

> 你邊煮邊記筆記，Markdown cell 是寫食譜（數學推導），Code cell 是烹飪動作（數值計算），每一步都能立刻嘗味道（執行結果即時呈現）。

---

## 🤖 **GitHub Copilot**

由 GitHub 與 OpenAI 共同開發的 **AI 程式設計助手**。它能根據你的註解、程式邏輯，自動補全、生成程式碼。

### 在數學廚房中：

**＝ 🧑‍🍳 自動料理助手**

> 你說「我要做反應擴散模擬」，它就幫你遞材料（套件）、預熱爐子（初始化）、甚至寫下食譜（程式架構），大幅加快開發流程。

---

## 📌 結論

| 工具               | 功能說明         | 數學廚房中的角色      |
| ---------------- | ------------ | ------------- |
| VS Code          | 程式與筆記編輯環境    | 工作檯與中央控制中心    |
| Jupyter Notebook | 實作與推導整合的筆記工具 | 鍋具 + 食譜記錄本    |
| GitHub Copilot   | AI 程式碼助理     | 廚師助手，自動遞食材與步驟 |


>有了 VS Code + Jupyter + Copilot，你就擁有一間 **AI 智能加持的數學廚房**，從理論推導到數值模擬，全程親手烹飪、即時品嘗、隨時分享。

---

## 🍛 使用範例

* 使用 Copilot 自動生成數值方法（如有限差分法、PINN）
* 用 Jupyter 寫研究筆記（如用 Markdown 推導 Gray-Scott 模型）
* 利用 matplotlib 視覺化數學圖形（即美味的擺盤）

---

# 二、VS Code 環境安裝與配置教學

打造你的 AI 數學工作坊！

---

## 1. 安裝 Python 與 VS Code

1. 前往 [Python 官網](https://www.python.org/downloads/) 下載並安裝 **Python（建議版本 3.9 ）**

    ✅ **務必勾選「Add Python to PATH」**，才能在終端機使用 `python` 指令
2. 前往 [VS Code 官網](https://code.visualstudio.com/) 下載並安裝 **Visual Studio Code**
3. 安裝完成後，開啟終端機（Command Prompt / Terminal），輸入以下指令確認是否成功安裝：

```bash
python --version
code --version
```

---

## 2. 在 VS Code 中安裝擴充套件

| 平台          | 操作流程                                                              |
| ----------- | ----------------------------------------------------------------- |
| **Windows** | `Ctrl+Shift+X` 開啟擴充套件 → 搜尋並安裝 `Jupyter`、`Python`、`GitHub Copilot` |
| **Mac**     | `⇧⌘X` 開啟擴充套件 → 搜尋並安裝 `Jupyter`、`Python`、`GitHub Copilot`          |

---

## 3. 建立 Python 虛擬環境

* ✅ 每個專案使用獨立套件，避免衝突
* ✅ 提升重現性，團隊協作更穩定
* ✅ 管理簡單，安裝／刪除套件不影響其他專案

```bash
cd 路徑/到/你的專案
# 建立虛擬環境
python3 -m venv .venv    # Mac/Linux
python -m venv .venv     # Windows
```

---

## 4. 啟動虛擬環境

| 平台            | 啟動指令                           |
| ------------- | ------------------------------ |
| **Mac/Linux** | `source .venv/bin/activate`    |
| **Windows**   | `.\.venv\Scripts\Activate.ps1` |

啟動後，終端機提示字元會出現 `.venv`，代表虛擬環境啟動成功。

---

## 5. 安裝 Jupyter 與常用數學套件

```bash
pip install jupyter numpy matplotlib pandas
```

### 🔍 `pip` 是什麼？

* `pip` 是 Python 官方的套件管理工具（Python Package Installer）
* 就像 Python 的「App Store」，幫你下載第三方工具
* 所有套件都安裝在 `.venv` 中，避免污染全域環境

---

### 📦 套件簡介與用途（以數學為料理）

| 套件             | 功能簡介              |  比喻        |
| -------------- | ----------------- | ----------- |
| **jupyter**    | 互動式筆記本，整合程式、公式與圖表 | 食譜記錄本＋料理平台  |
| **numpy**      | 高效數值與矩陣運算工具       | 切菜機（處理數據）   |
| **matplotlib** | 資料視覺化（畫圖、函數圖等）    | 擺盤工具（美化成果）  |
| **pandas**     | 表格資料整理與分析         | 食材分裝盒（整理資料） |

---

## 6. 選擇 Python 解譯器

讓 VS Code 正確使用你的虛擬環境：

1. 按 `Ctrl+Shift+P`（Mac：`⇧⌘P`）開啟命令面板
2. 輸入並選擇 `Python: Select Interpreter`
3. 選擇出現 `.venv` 的項目（通常會顯示路徑）

---

## 7. 建立並執行 Jupyter Notebook

1. 在專案資料夾中新建檔案：`demo.ipynb`
2. 輸入以下程式碼：

```python
print("Hello, Jupyter!")
```

---

## 8. 執行儲存格

| 平台   | 操作說明                            |
| ---- | ------------------------------- |
| 所有平台 | 點擊儲存格左側的 ▶️，或按 `Shift+Enter` 執行 |

---
# 三、深度學習中的「計算圖」與主流工具介紹

---

在深度學習中，**模型是一連串矩陣運算**，這些運算彼此相連、傳遞資料，形成一個有向圖。這就是：

### 🧠 **計算圖（Computational Graph）**

* 每個節點（Node）：表示一個數學操作（如矩陣乘法、激活函數）
* 每條邊（Edge）：表示資料在節點間的流動與傳遞

---

## 🏗️ 計算圖類型與對應框架

### 🔒 **靜態圖 (Static Computational Graph)**

**先定義整張圖，再執行資料流動**
→ 先畫完電路圖再插電

* ✅ 優點：圖可優化、效率高
* ❌ 缺點：不易除錯、不靈活

---
#### 📌 對應框架：**TensorFlow**

```python
import tensorflow as tf

x = tf.placeholder(tf.float32)     # 宣告一個輸入張量（尚未給值）
y = x * 2                          # 定義計算圖：y = x 的兩倍

with tf.Session() as sess:        # 建立 Session 來執行圖
    result = sess.run(y, feed_dict={x: 3.0})
    print(result)                 # 輸出 6.0
```

#### 🔍 說明：

1. `placeholder` 是圖中的「空接點」：x 尚未被賦值
2. 定義了 y = x × 2，是靜態圖的邏輯結構
3. 透過 `Session` 啟動整張圖並指定 x 的數值
4. 最終執行運算並印出結果

---

### 🔄 **動態圖 (Dynamic Computational Graph)**

**邊執行邊建立圖**
→ 邊煮菜邊決定要加什麼調味料，彈性大、好調整。

* ✅ 優點：語法直覺、易除錯
* ❌ 缺點：效率略低

---
#### 📌 對應框架：**PyTorch**

```python
import torch

x = torch.tensor(3.0, requires_grad=True)  # 定義可微分的張量
y = x * 2
print(y.item())                            # 輸出 6.0
```

#### 🔍 說明：

1. `torch.tensor(..., requires_grad=True)` 表示此變數要追蹤梯度（可用於反向傳播）
2. y = x \* 2，動態圖自動在背景建好 y 的圖節點
3. `y.item()` 取出純數字（Python float），方便輸出與觀察

---

### 📊 圖像化比喻

![](image-2.png)

> 左邊：靜態圖（先蓋好模型再倒資料）
> 右邊：動態圖（資料流動即時決定圖形）

---

## 🌍 主流深度學習框架比較

| 特點   | TensorFlow                 | PyTorch (推薦)        |
| ---- | -------------------------- | ------------------- |
| 開發者  | Google                     | Facebook (Meta)     |
| 語法風格 | 靜態圖（舊），新版支援動態圖 | 動態圖             |
| 使用方式 | 定義整體模型後再執行                 | 像 Python 程式一樣邊寫邊執行  |
| 安裝指令 | `pip install tensorflow`   | `pip install torch` |
| 版本相容性 |  版本限制較多、需注意版本相容         | 版本相對單純          |

---

## 🚀 補充介紹：NVIDIA NeMo（語音與語言模型開發工具）

### 🔊 NeMo 是什麼？

> **NVIDIA NeMo** 是一個專門用來建構語音辨識、語音合成、自然語言理解與生成的大型模型框架。

* 基於 PyTorch + Megatron-LM 架構
* 提供訓練、微調與部署大型語言模型的模組化 API
* 可快速建立 GPT、T5、BERT 等語言模型
* 支援多卡訓練與 GPU 加速，搭配 NVIDIA CUDA 架構最佳化

---
### ⚙️ NeMo 特點總覽：

| 功能區塊     | 說明                                                    |
| -------- | ----------------------------------------------------- |
| 語音支援     | 語音辨識（ASR）、語音合成（TTS）、說話人辨識等模組                          |
| LLM 支援   | 建構與訓練 GPT、T5、BERT、Chatbot 等大型模型                       |
| 多 GPU 訓練 | 整合 Megatron-LM 架構，支援分散式訓練                             |
| 安裝方式     | `pip install nemo_toolkit[nlp]` 或 `nemo_toolkit[asr]` |



