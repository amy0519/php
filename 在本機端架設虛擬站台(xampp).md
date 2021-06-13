---
tags: PHP, Git
---

# PHP 初入門(1) - 在本機端架設虛擬站台(並同步專案至git)

## 1.	安裝所需環境
* ### XAMPP(同時會在本機端幫你裝好Apache、MariaDB)
裝好後啟動Apache、MySQL
![](https://i.imgur.com/I6LfbNq.png)

* ### COMPOSER
![](https://i.imgur.com/dw9Ysa2.png)


* ### VSCODE(含多套件)
    *	beautify
    *	DotENV
    *	EditorConfig for VS Code
    *	GitLens — Git supercharged
    *	Kite AutoComplete AI Code: Python, Java, Go, PHP, C/C#/C++, Javascript, HTML/CSS, Typescript, React, Ruby, Scala, Kotlin, Bash, Vue, React
    *	Laravel Exter
    *	Laravel Artisan
    *	Laravel Blade Snippets
    *	Laravel Blade Spacer
    *	Laravel Extra Intellisense
    *	Laravel goto view
    *	Laravel Helpers
    *	Laravel Snippets
    *	laravel-blade
    *	laravel-goto-controller
    *	php cs fixer
    *	PHP Debug
    *	PHP Intelephense
    *	PHP IntelliSense
![](https://i.imgur.com/nxzWJKo.png)


---


## 2.	開始建立Laravel框架專案(PHP MVC)
> 	使用power shell建立專案，cd進入放專案之路徑，輸入以下
 	
`composer create-project laravel/laravel {專案名稱}`

* 圖中忘記+composer
![](https://i.imgur.com/VT50yIy.png)


---


## 3.	上傳到git(從本機端上到GIT)
*	在VSCODE的CMD輸入 {git init} 做初始化git(初建專案時只需做一次)
![](https://i.imgur.com/KToK233.png)

*	點選左下角雲圖示，同步本機的專案至git
![](https://i.imgur.com/4aRSXXx.png)


---


## 4.	指定專案在browser要輸入的網址(XAMPP的Apache Config改路徑)
### (1). 從XAMPP找config
> XAMPP >  Config  >  Browse[Apache]
![](https://i.imgur.com/DVGzmQx.png)


### (2). 從對應路徑找檔案
`C:\xampp\apache\conf\extra`
![](https://i.imgur.com/1OoFUZK.png)

### (3). 打開檔案，並將一個站台的註解取消並更改(這個動作是讓APACHE指定對應domain要去的專案路徑)
![](https://i.imgur.com/SB8jqGX.png)

> DocumentRoot指定路徑為index.php所在的檔案夾(Laravel所建專案中一定是在public裡面)
```
\{專案位置}\{專案名稱}\public
```

> ServerName 為Domain名稱

![](https://i.imgur.com/9y1o0wA.png)

### (4). 在本機指定DNS去的IP位置
> 在檔案夾輸入以下路徑`C:\Windows\System32\drivers\etc`，並開啟hosts檔案
![](https://i.imgur.com/vXkO3U6.png)

> 將DNS指定本機端IP
![](https://i.imgur.com/c9bkTqS.png)

### (5). 修改Apache存取權限
> 找到權限檔案
![](https://i.imgur.com/BSJnrhx.png)

> AllowOverride改成All(預設路徑可被改寫)
![](https://i.imgur.com/8ekuhWT.png)

> 按下Ctrl+h，尋找 `Require all denied` 取代成 `Require all granted`
將Apache預設路徑以外的路徑可被存取的權限打開
![](https://i.imgur.com/8a09Aa5.png)


---


## 5. 此時重啟Apache並在browser輸入你指定的Domain，就可以成功在本機端建立一個你的站台
![](https://i.imgur.com/iD0y9j5.png)





---

# *下一章節會簡略教學如何在MVC架構下如何修改網站顯示畫面*

#### 可先參考網路上介紹MVC架構的文章  
-->[「PHP」MVC框架是什麼？為什麼要用它](https://kknews.cc/zh-tw/code/2bgekez.html)
![](https://i.imgur.com/GKhQd2F.png)


## [下一章: 建立MVC架構資料庫](https://hackmd.io/qhshSQVDT4W5PSx1ANlAvw)












