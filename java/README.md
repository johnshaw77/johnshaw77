# 內部技術分享 - Java 開發指南與規範&範本說明

## 採用 Framework

<img src="img\java_dev_share10.png" width=200px />

<img src="img\java_dev_share11.png" width=200px />

<img src="img\java_dev_share12.png" width=200px />

<img src="img\java_dev_share13.png" width=200px />


# MyEclipse  - plugin 簡介

<img src="img\java_dev_share16.png" width=500px />

<img src="img\java_dev_share17.png" width=201px />

<img src="img\java_dev_share18.png" width=500px />

### jBPM gpd –流程設計器

<img src="img\java_dev_share19.png" width=500px />

### Spket – Javascript editor外掛

Checkstyle –程式碼規範檢查外掛

<img src="img\java_dev_share20.png" width=500px />

<img src="img\java_dev_share21.png" width=478px />

<img src="img\java_dev_share22.png" width=391px />

** 學會如何單元測試將是一個重要的功課，尤其在撰寫底層、共用元件時，有單元測試將能協助我們在第一時間抓出問題 **

<img src="img\java_dev_share23.png" width=500px />

# 修改設定檔

打開JspPattern\\WebRoot\\WEB\-INF\\appConfig\\config\.properties

修改資料庫連線、專案名稱等設定

# GlobalResources (Web 通用資源庫)

<img src="img\java_dev_share30.png" width=142px />

<img src="img\java_dev_share31.png" width=142px />

各地區會指定一台當主要Server

預設會放置於[http://sitename/globalresources](http://sitename/globalresources)統一存取

# Web.xml - DirectJNgine( for Ajax) 設定

<img src="img\java_dev_share33.png" width=1024px />

<img src="img\java_dev_share34.png" width=500px />

<span style="color:#FF0000">要讓</span>  <span style="color:#FF0000">Javascript</span>  <span style="color:#FF0000">認識可呼叫的</span>  <span style="color:#FF0000">Method</span>  <span style="color:#FF0000">的類別</span>

目的:簡化Client端Ajax的操作 

# Struts.xml 設定

# URL Rewrite pattern – web.xml 設定

必須在Struts2 filter mapping加上這二行

<img src="img\java_dev_share35.png" width=800px />

Url Rewrite Filter設定

# URL Rewrite pattern

<img src="img\java_dev_share36.png" width=296px />

利用URL Rewrite機制及strut2的dynamic method invokation來對應action及method， <span style="color:#0070C0"> _減少_ </span>  <span style="color:#0070C0"> _config_ </span>  <span style="color:#0070C0"> _的設定量_ </span> 。

需要轉至JSP Page的網址規範

/ <span style="color:#FF0000">views</span> /Action1/index

需要Ajax\(JSON Data\)的網址規範

/ <span style="color:#FF0000">ajax</span> /Action1/getData

# Brevis 核心函式庫

此專案為底層函式庫，例如util程式類、ORM操作類等等，此專案需要多人維護，所以必須確實做好版本控管。

Package名稱以 <span style="color:#FF0000"> _com\.fox\.core_ </span> 為開始

引用的jar檔放置於lib資料夾

必須加入版本控管

# 目錄架構

# Server 架構(佈署)
Local 架構(開發)

目錄架構區分為兩種，一種是Server端真正執行使用的目錄，另一種則是Local端開發工作的目錄。在Server上正式運作的時候並不需要程式原始碼，也不需要一些我們開發過程中產生的檔案，所以目錄的架構較少；在Local端開發的工作目錄則需要較多，以儲存一些工作過程所產生的中 介檔。等到開發完成的時候，再將開發好的執行檔以及設定檔部署到Server上正確的位置即可。

# Server 架構

<span style="color:#FF0000"> __appConfig__ </span> :

此為系統參數設定檔存放的目錄。

<span style="color:#FF0000"> __css__ </span> :

此為放置各AP使用的CSS樣式檔案，例如AP專用的樣式，跨專案使用的統一風格樣式、小圖示樣式則先從GlobalResources存取。

<span style="color:#FF0000"> __scripts__ </span> :

此為放置各AP使用的Javascript檔案，例如AP專用的UI類別檔，跨專案使用的Script framework或是類別庫則統一到GlobalResources存取。

<span style="color:#FF0000"> __images__ </span> :

此為系統預設圖檔以及系統專屬圖檔存放的目錄，各AP的圖檔存放在自己的系統目錄下。

<span style="color:#FF0000"> __public__ </span> ：

此為各AP產生的暫存檔存放的目錄。各AP產生的暫存檔存放在自己的系統目錄下。要注意的是此目錄下 的檔案可供使用者下載使用\(也就是可以用Hyperlink的方式讓使用者連結\)，必須定時清除此目錄下的檔案。

<span style="color:#FF0000"> __WEB\-INF\\work__ </span> :

此為各AP產生的工作檔存放的目錄。在目錄底下以系統別作為區分，各AP產生的工作檔存放在自己的系統目錄下。要注意此目錄下的檔案只供系統使用\(也就是無法用Hyperlink的方式讓使用者連結\)。

<span style="color:#FF0000"> __WEB\-INF\\jsp__ </span> :

此目錄存放不被外界直接存取的JSP頁面檔案。

<span style="color:#FF0000"> __WEB\-INF\\classes__ </span> :

各AP compile之後的class檔，屬於零散的或獨立的servlet \(建議將servlet視為一般的class，也壓到jar檔裡\)。存放在WEB\-INF/classes/目錄下按照程式的package目錄存放。

<span style="color:#FF0000"> __WEB\-INF\\lib__ </span> :

各AP的執行檔，壓製成jar檔。存放在WEB\-INF/lib/目錄下。

<span style="color:#FF0000"> __WEB\-INF\\tld__ </span> :

所有taglib的設定檔\(\.tld\)，統一存放在WEB\-INF/tld/目錄。

# Local系統開發的目錄架構

<span style="color:#00B0F0"> _package_ </span>  <span style="color:#00B0F0"> _名稱統一以_ </span>  <span style="color:#00B0F0"> _com\.nwing_ </span>  <span style="color:#00B0F0"> _為起始_ </span>

<span style="color:#FF0000"> __action__ </span> :

存放Strut2應用的action java檔案

<span style="color:#FF0000"> __common__ </span> :

存放dao\,domain應用層\,服務層

<span style="color:#FF0000"> __report__ </span> :

存放報表相關的程式檔

<span style="color:#FF0000"> __utility__ </span> :

存放工具程式檔

<img src="img\java_dev_share37.png" width=32px />

<img src="img\java_dev_share38.png" width=86px />

# SiteMesh 介紹

[http://www\.opensymphony\.com/sitemesh/](http://www.opensymphony.com/sitemesh/)

<img src="img\java_dev_share39.png" width=500px />

Sitemesh應用Decorator模式，用filter截取request和response\,把頁面组件head\,content\,banner結合為一個完整的視圖。

通常我們都是用include標籤在每個jsp頁面中來不斷的包含各種header\, stylesheet\, scripts and footer，現在，在sitemesh的幫助下，我們可以開心的删掉他們了

# SiteMesh 設定

<span style="color:#0070C0">一、在</span>  <span style="color:#0070C0">WEB\-INF/web\.xml</span>  <span style="color:#0070C0">中</span>  <span style="color:#0070C0">filter</span>  <span style="color:#0070C0">的定義</span>  <span style="color:#0070C0">:</span>  <span style="color:#0070C0">\(</span>  <span style="color:#0070C0">已寫在範本專案中</span>  <span style="color:#0070C0">\)</span>

<img src="img\java_dev_share40.png" width=500px />

# SiteMesh – MasterPage + 自訂標籤

配合目錄規範之自訂資源引入Tag

<img src="img\java_dev_share41.png" width=186px />

__When AppEnvironment=__  <span style="color:#FF0000"> __debug__ </span>

\<script language="javascript" src="http://localhost:8081/JspPattern/scripts/direct/Api\.js">\</script>

__When AppEnvironment=__  <span style="color:#FF0000"> __production__ </span>

<script language="javascript" src="http://localhost:8081/JspPattern/scripts/direct/Api <span style="color:#FF0000">\.</span>  <span style="color:#FF0000">min\.</span> js">\</script>

# Javascript 文件製作原則

## 使用 Extjs

<img src="img\java_dev_share42.png" width=500px />

# API 文件製作 – 總覽

<img src="img\java_dev_share43.png" width=800px />

<img src="img\java_dev_share44.png" width=800px />

# API 文件製作 – 編輯器設定

<img src="img\java_dev_share45.png" width=459px />

<img src="img\java_dev_share46.png" width=461px />

<img src="img\java_dev_share47.png" width=500px />

<span style="color:#0070C0">Extdoc</span>  <span style="color:#0070C0">執行時需要的設定、參數、樣版</span>  <span style="color:#0070C0">\.\.</span>  <span style="color:#0070C0">等都已經設定好，你只需要正確設定批次檔位置。</span>

<img src="img\java_dev_share48.png" width=800px />

<img src="img\java_dev_share49.png" width=429px />

<img src="img\java_dev_share50.png" width=500px />

# API 文件製作 – ExtDoc 工具說明

<img src="img\java_dev_share51.png" width=500px />

# API 文件製作 – ExtDoc 定義檔

<img src="img\java_dev_share52.png" width=317px />

<img src="img\java_dev_share53.png" width=192px />

<img src="img\java_dev_share54.png" width=500px />

<img src="img\java_dev_share55.png" width=317px />

# API 文件製作 – 規範

<img src="img\java_dev_share56.png" width=141px />

<img src="img\java_dev_share57.png" width=500px />

_ExtDoc_  _統一存放於_  <span style="color:#FF0000"> __專案__ </span>  <span style="color:#FF0000"> __\\docs\\api\\extjs__ </span>  _目錄下_

_元件預覽圖存放於_  <span style="color:#FF0000"> __pic__ </span>  _目錄下_

_@author \(_  _開發者_  _\)_  _必寫。_

_Public_  _的_  _config\, method\,event_  _的說明必寫_

<img src="img\java_dev_share58.png" width=500px />

# API 文件撰寫範例 一

<img src="img\java_dev_share59.png" width=500px />

<img src="img\java_dev_share60.png" width=368px />

Foxconn NWInG Confidential

# API 文件撰寫範例 二

<img src="img\java_dev_share61.png" width=500px />

<img src="img\java_dev_share62.png" width=500px />

