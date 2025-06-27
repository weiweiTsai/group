---
marp: true
theme: gaia
paginate: true
math: katex
---
# 學、做、「寫｣----施工中
賴敬丰

---
# 在 VS Code 安裝 Marp 擴充套件

  
- 點選左側的「Extensions」也可以使用快捷鍵 Shift + ctrl/command + X。
-  搜尋 Markdown All in One，點擊 Install 安裝。
- 搜尋 Marp for VS Code，點擊 Install 安裝。

---
# 建立 Marp 投影片

-建立資料夾及初始化
1.在電腦上建立一個資料夾，假設命名為 marp-slides-demo。
2.用 VS Code 開啟這個資料夾（File -> Open Folder...）。

-建立 Markdown 檔案
1.在資料夾中新建一個檔案，例如命名為 example **.md**。
2.在檔案開頭，我們需要一段 front matter 來啟用 Marp 的投影片模式並設定。

---
# 標題使用`#`   
#### 小一點就多放幾個`#`
- 無序列表使用`-`或`*`開頭
  * 子項目在前面加上空格`tab`
1. 有序列表使用數字加上`.`開頭


---
# 投影片模式設定
---常用的設定:


marp: true
theme: gaia
paginate: true
math: katex
---

---
# 撰寫投影片內容
---常用到的語法:

# 標題使用 `#`

### 小一點就多放幾個 `#`

- 無序列表使用 `-` 或 `*` 開頭
  * 子項目在前面加上空格 tab

1. 有序列表使用數字加上 `.` 開頭


---

### 表格:使用`|`分隔，第二行加上`-`來分隔表頭與內容 
| 功能 | 說明　| 範例 |      
|-|-|-|
|行內程式碼| 前後加上` | `ABC` |
|程式碼區塊| 前後加上` ``` ` | ```ABC```|
|斜體     | 前後加上`_`或`*`    | text       |
|粗體     | 前後加上`__`或`**`  | **text**     | 
|刪除線   | 前後加上`~~`　　    | ~~text~~     |
|內聯公式 | 前後加上`$`         | $E = mc^2$   |
|區塊公式 | 前後加上`$$`        | $$E = mc^2$$ | 

---

# 輸出投影片內容

View → Command Palette... → 找到 Marp: Export slide deck
或者
Ctrl+Shift+P → 找到 Marp: Export slide deck

---
# Overleaf
### 創建帳號

1.前往 Overleaf 官網。
2.點擊 Sign up。
3.在Email欄位輸入學校的 .edu 信箱，並設定密碼。
4.按下建立帳號後會跑出右圖的驗證。
5.到輸入的信箱確認 Overleaf 寄來的驗證碼。
6.填完資料或skip後就可以開始使用了。

---
# 透過 copilot 轉換 marp

- 在 Overleaf 左邊的  New Project → Blank Project。
- 開啟要轉換的 marp 頁面，點上方搜尋欄右邊的 Toggle Chat。
- 直接要求把該 marp 轉成 beamer。
- 把結果複製到剛開的 Project。

---
# VS code 上直接製作

### VScode配置Latex環境

https://blog.csdn.net/qq_45952740/article/details/131004722


### 下載TeX Live

https://blog.csdn.net/qq_44940689/article/details/140244933

---

# 實作

---

### 用於 PINN 中的硬嵌（Hard Constraint Embedding）

####  什麼是 PINN？

- PINN（Physics-Informed Neural Networks）是一種將物理方程（如偏微分方程）直接融入神經網絡訓練中的方法。
- 它不需大量標註資料，而是透過將 PDE 作為 loss function 的一部分，強化模型對物理規律的理解。

---

## 為什麼 PINN 解帶時間的 PDE 比較困難？


### 🔹 1. 時間導數難學習
- 時間上的變化常呈現高頻或不規則，神經網路不易擬合。
- 自動微分計算時間導數（尤其是高階）容易不穩、數值誤差大。


### 🔹 2. 解具有剛性（Stiffness）
- 初期快速變化（如界面形成），後期變化緩慢（如相分離趨於穩定）。
- 單一網路很難同時學好快變與慢變部分。

---

### 🔹 3. 時間與空間性質不同
- 空間結構通常平滑或周期性，時間方向則劇烈且非平衡。
- PINN 可能傾向先學好空間結構，導致時間行為錯誤。


### 🔹 4. 時間取樣過疏
- 常見隨機取點方法會在時間軸上分布不均。

### 🔹 5. Loss 項比例失衡
- 時間導數項在 loss 中可能權重不足或數值太小。
- 不平衡會導致訓練不穩或某一部分主導 loss。
  
---

# 要怎麼解決?


提供了一項關於硬約束和自適應損失權重的消融研究，研究時間相關偏微分方程的解對其初始條件的依賴性。
硬約束提供的變換顯著緩解了通常與剛性時間相關偏微分方程的訓練挑戰。
研究證明了該方法在1D Cahn-Hilliard和Gray-Scott Equation等不同類型的此類偏微分方程中的有效性。
這種方法不僅提高了訓練效率，還提高了學習到的解的準確性和穩定性，尤其是在存在剛性的情況下，而傳統的PINN通常難以收斂。

---

##  PINN 的挑戰：邊界與初始條件

- 在 PINN 中，除了滿足 PDE，本身也需要滿足：
  - 初始條件（Initial Condition, IC）
  - 邊界條件（Boundary Condition, BC）

---
###  一般處理方式：Soft Constraint（軟約束）

在 PINN 中，常見的做法是將條件以「軟約束」的方式加進損失函數中：

$$
\mathcal{L} =  \lambda_{\text{IC}} \mathcal{L}_{\text{IC}} + \lambda_{\text{BC}} \mathcal{L}_{\text{BC}} + \mathcal{L}_{\text{PDE}}
$$

####  各項解釋：

- **$\mathcal{L}_{\text{IC}}$：初始條件損失**  
  衡量預測值 $u(x, 0)$ 與已知初始函數 $g(x)$ 的差距。

- **$\mathcal{L}_{\text{BC}}$：邊界條件損失**  
  測量解在邊界是否滿足指定條件。

---

- **$\lambda_{\text{IC}}, \lambda_{\text{BC}}$：權重係數**  
  控制初始與邊界條件在整體損失中的權重。  
   權重若選得不好，可能導致訓練發散或收斂過慢。

- **$\mathcal{L}_{\text{PDE}}$：PDE 殘差損失**  
  測量網路預測結果代入偏微分方程後的誤差平方和。  
   確保預測結果「符合物理方程」。



**問題點**：這種方法無法保證條件會被嚴格滿足，且在多項 loss 組合下需小心調整權重 $\lambda$，訓練難度提高。

---

###  什麼是硬嵌入（Hard Constraint Embedding）？

### 定義：
**硬嵌入**是將邊界或初始條件「嵌入」網絡結構中，使得預測結果天生就滿足條件。

### 特點：
- 不需要額外的 loss term 來懲罰偏離條件。
- 條件直接變成網絡的結構限制。

---

#### 初始條件形式

假設初始條件為已知函數：

$$
u(x, 0) = g(x)
$$

####  硬嵌入（Hard Constraint）策略

設計一個新的預測函數：$\hat{u}(x, t) = g(x) + t \cdot N(x, t;\, \theta)$

其中：
$g(x)$ 是初始條件，確保 $u(x,0) = g(x)$ 永遠成立。
$N(x,t)$ 是一個由神經網路建模的函數，學習「偏離初始值的時間演化部分」。

