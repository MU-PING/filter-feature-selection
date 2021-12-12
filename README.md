# filter-feature-selection
## 程式簡介
### 簡述
* 使用 sklearn 實作 Feature Selection 中的 **Filter methods【過濾器法】**

## Feature Selection
* 又稱為 variable selection、attribution selection 或 subset selection

* 指從資料集中選出最重要、最相關的特徵來給機器學習建立模型，大部分時候，這樣做可以增加機器學習的效能

* Feature selection 不等於 Dimensionality Reduction

### WHY
機器學習的實際應用中，特徵數量往往較多，可能存在不相關的特徵，特徵之間也可能存在相互依賴，容易導致：

* 特徵個數越多，分析特徵、訓練模型所需的時間也就越長。

* 特徵個數越多，容易引起【維度災難】
#### 維度災難
* 特徵維度超過一定界限後，分類器的效能隨著特徵維度的增加反而下降，如下圖
  ![image](https://user-images.githubusercontent.com/93152909/145701552-148a6354-f79c-4310-b047-619353903b76.png)
  > 原因往往是因為這些高維度特徵中含有「無關特徵」和「冗餘特徵」

* 無關特徵  
該特徵所提供的資訊對於當前學習任務無用，如對於「學生成績」而言，「學號」則是無關特徵。
* 冗餘特徵  
該特徵所包含的資訊能從其他特徵推演出來，如「面積」特徵，能從「長」和「寬」得出，則它是冗餘特徵。
### HOW
一般 Feature selection 的演算法分為三類：

* Filter methods【此篇介紹】

* Wrapper methods

* Embedding methods

## Filter methods【過濾器法】
> 選擇特徵子集時，只考慮特徵內部的特點【評價函數】，不考慮將來要使用哪一種模型進行學習

* 步驟
  1. 【搜索策略】從原始特徵中挑出特徵子集

  2. 【評價函數】分析特徵子集中特徵的相關性、離散程度或其他指標來衡量其好壞

  3. 重複1.2步，直到達到停止條件

* 概念圖  
  <img src="https://user-images.githubusercontent.com/93152909/145709033-69aa23a8-518c-44b5-b332-38a72a376474.png" width="300">

* 優點
  * 選出的特徵子集合可以被用在任何機器學習演算法
  
  * 不會耗費大量電腦資源
  
### 【搜索策略】
搜索策略分為3大類
> 策略眾多，不詳述，詳細可參考：[特徵選擇常用演算法綜述 - IT閱讀](https://www.itread01.com/content/1550470354.html)

* 完全搜尋(Complete)

* 啟發式搜尋(Heuristic)

* 隨機搜尋(Random) 

> 注意⚠在Filter methods中，搜索策略可以簡化，ex：方差過濾，算出所有特徵的方差，刪除低於閥值的即可

### 【評價函數】
依它處理特徵的方式型態 可分為 Univariate 和 Multivariate 兩種：
> 以下僅列出程式中有使用的幾種，其他種類可以上網查詢或查詢參考資料

* Univariate methods：只考慮單一特徵的統計特點，例如：方差
  * 方差過濾
  
    ```python
    from sklearn.feature_selection import VarianceThreshold
    ```
* Multivariate methods：評估全部的特徵，考慮到變數之間的關係，例如：卡方檢定
   * 卡方過濾
   
     ```python
   	 from sklearn.feature_selection import SelectKBest
     from sklearn.feature_selection import chi2
     ```

## 參考
* [特徵選擇(feature selection) - IT閱讀](https://www.itread01.com/content/1547263108.html)
* [特徵選擇常用演算法綜述 - IT閱讀](https://www.itread01.com/content/1550470354.html)
* [Day28 - Feature Selection -- 1. Filter methods(過濾器法) - iT 邦幫忙__一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10245037)
* [Feature Selection 特徵選取 -Filter(ㄧ) Python sklearn 實作 _ by Jasmine＿ _ Medium](https://jasmine880809.medium.com/feature-selection-%E7%89%B9%E5%BE%B5%E9%81%B8%E5%8F%96-filter-%E3%84%A7-python-sklearn-%E5%AF%A6%E4%BD%9C-2797b941c6a9)
* [機器學習之特徵選擇（Feature Selection）_實用技巧_程式人生](https://www.796t.com/article.php?id=173751)
* [特徵工程之特徵選擇概念. 特徵選擇是特徵工程裡的一個重要問題，其目標是尋找最優特徵子集。特徵選擇能剔除不相… _ by Ryan Lu _ AI反斗城 _ Medium](https://medium.com/ai%E5%8F%8D%E6%96%97%E5%9F%8E/%E7%89%B9%E5%BE%B5%E5%B7%A5%E7%A8%8B%E4%B9%8B%E7%89%B9%E5%BE%B5%E9%81%B8%E6%93%87%E6%A6%82%E5%BF%B5-ca11745db63c)

> 備份於 Reference 資料夾中
