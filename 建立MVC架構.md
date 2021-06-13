
###### tags: `PHP` `Git`

# PHP 初入門(2) - 建立MVC架構資料庫

## 1. 了解Laravel預設路徑及其檔案位置(這裡影響了網站網址)
![](https://i.imgur.com/9OEgfAn.png)


* > routes資料夾下的web.php為預設指定路徑及檔案(預設為welcome[歡迎頁])
* > 檔案位置對應在resources資料夾裡的welcome.blade.php(只要是Laravel所建的專案，網頁副檔名都是blade.php)
> ###  (頁面基本上都寫在web.php裡面，有存取資料的都寫在api.php中)
![](https://i.imgur.com/zl1yAsl.png)
![](https://i.imgur.com/hYYuzKd.png)


---


## 2. 接外部api資料 - 在api.php中 get 外部api
![](https://i.imgur.com/qFFaKyM.png)

### (1) 建立新的controller 
**在command-line輸入** 
`php artisan make:controller NewsController --resource`
> 建立NewsController，加了–resource代表會在controller內建基本API。

![](https://i.imgur.com/97Il0ae.png)

#### 此時Http檔案裡的Controllers資料夾已新增出NewsController.php檔案
![](https://i.imgur.com/GJ3rRVu.png)


#### 補充
`php artisan make:controller NewsController --model=News --resource`
> 建立NewsController，加了–resource代表會在controller內建基本API，–model=News代表會建立一個名為News 的 model。

### (2) 指定到新建的controller - 在routes資料夾中的api.php檔案引入新建的controller路徑，並指定抓取的function路徑 - [Laravel官方文件](https://laravel.com/docs/8.x/routing)

#### (2-1) 
引入新建的controller
> `use App\Http\Controllers\{controller名稱};`
#### (2-2) 
引入新建的controller
> `Route::get('/{自訂}', [{controller名稱}::class, '{自訂}']);`
> 
![](https://i.imgur.com/oUL51rz.png)

### (3) 試用新建的controller中的function回傳值(確定要對應到function名稱)
![](https://i.imgur.com/LUrfyeC.png)

回傳成功
![](https://i.imgur.com/szUw7pM.png)

### (3) 將API放到env檔案中，之後只要呼叫就好

![](https://i.imgur.com/UyBlqdj.png)

### *補充 - 要先下載[ngrok](https://blog.alantsai.net/posts/2018/04/devtooltips-5-ngrok-allow-public-to-access-localhost-website-and-sql-server)

並輸入
```
ngrok http 80
```
![](https://i.imgur.com/N0lDeX3.png)

並將此網址複製到browser上(**每一次重啟ngrok網址都不同**)
![](https://i.imgur.com/9xoxktN.png)

![](https://i.imgur.com/3ykTo9J.png)

### (4) 繞過SSL憑證，否則無法抓取外部API
```
withOptions([
            "verify" => false
        ])
```
![](https://i.imgur.com/nluRBXZ.png)

![](https://i.imgur.com/nVQgR8t.png)


#### *補充 - 輸入 `dd($response)` 可看到變數形態與內容值，用來debug(dd會強制中斷程式)
![](https://i.imgur.com/sg4O5dg.png)

![](https://i.imgur.com/bvOtANw.png)

> 成功接到資料
>
![](https://i.imgur.com/P9nhOAG.png)



---

## 3. 建立資料庫&資料表欄位
![](https://i.imgur.com/edj5utA.png)



### (1)在網址列打: {網域}/phpmyadmin

![](https://i.imgur.com/4mlvW0G.png)

### (2)新增資料庫

![](https://i.imgur.com/28Z3KKd.png)

建立資料庫成功
![](https://i.imgur.com/Umk5N7l.png)

### (3)到env修改database名稱(你所建立的資料庫名稱)
![](https://i.imgur.com/O42tbOx.png)

### (4)建立資料表migration模組
需在VSCode CMD輸入
```
php artisan make:migration create{資料表名稱}sTable
```
![](https://i.imgur.com/asYRrWO.png)

**成功建立migration模組**
![](https://i.imgur.com/19zWx8E.png)


### (5)新增資料表欄位
```
Schema::create('free_data', function (Blueprint $table) {
            $table->id();
            $table->string('year');
            $table->string('goldprice_global')->unique();
            $table->timestamp('goldprice_taipei')->nullable();
            $table->string('rate_ntusd');
            $table->timestamps();
        });
```

![](https://i.imgur.com/aG19h6e.png)

**在VSCode CMD輸入建立資料表指令**
```
php artisan migrate
```
![](https://i.imgur.com/IlPcBbx.png)

**此時已成功建立資料表**
![](https://i.imgur.com/OCGe4rL.png)

### *補充
> 若要更新欄位，需再下指令rollback資料表+重啟migrate
```
php artisan migrate:rollback

php artisan migrate
```
![](https://i.imgur.com/aALvWps.png)



---


## 4. 建立Model將接到的API中資料存入所建立的資料表中
![](https://i.imgur.com/ZWmKgQg.png)




### (1) 建立Model模組
需在VSCode CMD輸入
```
php artisan make:model {資料表名稱}
```
![](https://i.imgur.com/WYiXE5t.png)

成功建立
![](https://i.imgur.com/KZ4BV2s.png)

### (2) 建立的model中指定存入欄位

![](https://i.imgur.com/Y5McJ6P.png)

### (3) 在controller引入model，及將資料存入DB

![](https://i.imgur.com/pUTQTy2.png)

**成功存入DB**
![](https://i.imgur.com/j1sMQK6.png)
![](https://i.imgur.com/zFEDyQZ.png)


## 5. 建立新的View，並將route指定路徑，讓browser可以顯示
![](https://i.imgur.com/YbOitJ4.png)

### (1) 將css、js、fonts資料夾放置public
![](https://i.imgur.com/nLmRFxx.png)


### (2) 將index檔案放至views，並將附檔名改為.blade.php
![](https://i.imgur.com/SCBjM4P.png)

### (3) 增加routes資料夾web.php檔案中的路徑(web.php主要是顯示views)
![](https://i.imgur.com/7xmL4T0.png)

#### 此時browser可顯示畫面
![](https://i.imgur.com/kkACZI7.png)


### *補充: 記得修改html中引用JS、CSS的路徑



---

## 6. 資料庫資料顯示到畫面上(執行如附圖)
![](https://i.imgur.com/5kJUBMu.png)

### (1)在routes>web.php引入Newscontrollers，並將原先指定view的方式改成指定controller
![](https://i.imgur.com/EfJMUPw.png)

### (2)至controller檔案中return view(index)
![](https://i.imgur.com/60qfb4g.png)

### (3)將資料指定到view中
![](https://i.imgur.com/M49IkRu.png)

**把資料表標題欄位取出**
![](https://i.imgur.com/Lw2klhm.png)


### (4)至index.blade.php中指定資料位置

> 把剛轉成Array型態的值寫入標題中

![](https://i.imgur.com/Bduq0kK.png)

> 用blade的foreach語法將資料庫的值顯示於畫面

![](https://i.imgur.com/xa0NXc6.png)

> 把顏色寫入欄位

![](https://i.imgur.com/UrAc1Hc.png)

### 成功寫入且更改表格顏色
![](https://i.imgur.com/7UXK77l.png)


---


## 最後記得將專案update到git上
![](https://i.imgur.com/jUV0l82.png)

![](https://i.imgur.com/Mls8fhX.png)

![](https://i.imgur.com/ucquOoj.png)


---





## 下一章: [ 前端及資料庫增刪改查](https://hackmd.io/jduLF-3FQl-W1Vo0uifKwg)












