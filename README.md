# Git 笔记
``` bash
           |         |
Modified   | Staging |    Commited     |   Push to Remote
           |         |                 |
  working  |  after  |     after       |     git push
 directory | git add |   git commit    |     
           |    .    | -m "description"|
           |         |                 |
           |         |                 |
           |         |                 |
           |         |                 |
               vvv          vvv                  vvv
//         index/staging    HEAD      Github-origin / heroku-heroku
```        

### 基礎操作
* git clone SSH-URL
* git add . 
* git status
* git commit -m "寫入詳細的更改，方便以後更改回來的時候，清楚這是哪裡被更改"
* git log 可以查出history commit的資料
* git log --oneline 簡寫版的 history資料
* git checkout 751401d - 使用這個版本之前commit的資料
* git checkout master 
* git revert abbc091
* git reset 34cs322 - 跑回去 34cs322 那時的file沒改變 但是在commit stage里 它之後的都還沒commit
* git reset 34cs322 --hard 就會更改資料 然後commit那些在34cs322之後也被刪了

``` bash 
--commit 1 ----commit 2 ---------------------------------------------------merge commit
                         \                                           /
                          \         /* Feature branch */            /
                           \---commit 1----commit2-----commit 3----/
 ```
 ### Create另外一個 Branch
 * git pull -更新remote的资料，拉remote里的资料过来，如果remote里和现在不同
 * git branch nameBranch - create另一個 branch
 * git checkout nameBranch - 跑去nameBranch 之前是(master)
 * git checkout master - 跑去master，然後newBranch的時，寫的文件會消失，他是屬於newBranch的
 * git branch -d nameBranch -刪除branch，也刪除了newBranch里創建的資料,除非merge它
 * git branch -a -檢查有多少個branch
 * git checkout -b nameBranch - create另一個branch 然後跑過去 
 
 ### Merge Branch！
 *如果merge A 文件和 B文件起衝突的話就要需要去看下Visual Code里看下 和選擇
 * git merge nameBranch - 那樣就會把newBranch的commit也和master結合了，在newBranch寫的文件也會出現了
 
 -------------------------------
 
 ### 上傳到Github，和設置以後更改也能快速更新
 -master是代表上傳master的 
 ``` bash
 $ git push URL From Your Repository master
 ```
 上傳后，以後也需要更改資料 ，你不會像每次都輸入 URL 一遍又一遍吧
 -設置遠端連接 Github default alias是origin
 ``` bash
 $ git remote add origin URL 
 $ git push origin master 
 ```
 
#### 第二個方法
當從Github Clone文件下來，執行的方法能使用這個，記得過後要進入那個文件夾
在當前文件做了更改想要上傳到Github 不必使用第一方法了
``` bash
$ git add .
$ git commit -m "updated weather api"
```
檢查
``` bash
$ git remote -v
```
上傳commit的資料去Gtihub，因為它clone資料下來就有記錄下了
``` bash
$ git push origin master
```
### 合作完成專案 需要使用的技能
工作上需要的給同事看你code，他們覺得code沒問題才讓你merge之前的文件
當你clone下那文件后 :fire:
老闆叫你做些更改，當你上傳資料去Github，不會去merge 之前資料的文件，不然之前的code可能還比你的還好呢，亂亂merge不就是死掉嗎
``` bash
$ git pull origin master
$ git checkout -b index-html
```
上面步驟是做個newBranch叫做index-html，把你要寫的code寫在裡面
然後在上傳這個 index-html的 newBranch去 Github
```
$ git add .
$ git commit -m "porfolio html code"
$ git push origin index-html
```
大概就那樣把~可以登錄進去Github看看，它上傳后長什麼樣子

 ### 也能在Github里创建多个branch
 <p>就先create new branch，然后在newBranch里 push它</p>
 <p>要回去主要的branch再输入，回去master branch</p>
 *git checkout master
 <p>要把newBranch和master结合，也能够在bash处理,记得要在master位子上处理这</p>
 ``` bash
 git merge newBrachName
 git push 
 ```

-----------------------------------------

# 使用Git期間，被困在裡面 那個叫做Vim editor！聽說這個入門門檻有點不友善，所以去理解一點它就好了 =)


* :q   退出
* :q!  退出但沒save
* :wq  能編寫然後退出
* :wq! 能編寫就算那個文件只是能讓你去讀，但他會強制去編寫它，然後退出
* :x    和wq一樣，我也有點不清楚 
* :exit 和:x一樣 
* :qa   退出全部-
* :cq   退出沒save然後使Vim 返回一個 non-zero error




-----------------------------------------

                            

### Multiple SSH KEY Git Bash Window
先產生 SSH KEY - ssh-keygen -t rsa -b 4096 -C "emailAdress@hotmail.com"
##### 彈出來的 資料 一定要 更改 folder名 不然 它會覆蓋你之前的 ssh key file
``` bash
Enter file in which to save the key (/c/Users/YongYee/.ssh/id_rsa): /c/Users/YongYee/.ssh/id_rsa_newone

```
把 pub key 放進Github里
*  cat ~/.ssh/id_rsa_newone.pub
記得一定要輸入 eval "$(ssh-agent -s)"
 
接下來在 存放 ssh key的文件夾里 create一個.config file
.config 範例
* github - yourname
  Host github.com
  HostName github.com
  IdentityFile ~/ssh/id_rsa
  IdentitiesOnly yes
  User yourname

* github - otherName
  Host abc.github.com
  HostName github.com
  IdentityFile ~/.ssh/id_rsa_newone
  IdentitiesOnly yes
  User otherName
  
接下來可以指定測試它 
ssh -T git@github.com
它跳出 Hi yourname! .....
or
ssh -T git@abc.github.com
他跳出 Hi otherName! .....

* --global 目錄底下有設定 它會使用目錄底下的先 不然他就會使用你 yourname的那個
``` bash
 git config user.name "otherName"
 git config --global user.name
 ```
 過後開啟 你clone文件的folder 進入git文件夾(記得打開隱藏版)，點擊裡面的config更改
 * remote “origin”下的 url
 把它更改成和你設置config里的Host相同 
 eg: git@abc.github.com:xxxxx 
 
 

*如果不會跳出任何資料可以試看看debug它
``` bash
  ssh -vT git@github.com
```


### clone 文件
``` bash
git clone github clone key
```


<p>ls -a -l ~/.ssh</p>
#  ssh-keygen -t rsa -b 4096 -C "emailAdress@hotmail.com"
* eval "$(ssh-agent -s)"
* ssh-add ~/.ssh/id_rsa
-----
<p>github remoto code</p>
* git remote add origin git@github.com:xxxxxxxx

然后检查自己的pub key 放进去 github *setting里设置
*  cat ~/.ssh/id_rsa.pub

* ssh -T git@github.com
* git push -u origin master



<p>After commit those file</p>
*  $ ssh-add ~/.ssh/id_rsa 

### 查看自己现有的SSH key
* 直接 在 git bash 里面 第一层 cat ~/.ssh/id_rsa.pub

``` bash
1. cd ~/.ssh
2. vim id_rsa.pub || cat id_rsa.pub
```

-----------------------------------


# else
### git cmd :rocket:
### upload file from git
* git config --global user.name "githubname"
* git config --global user.email "email of github"
* git clone repository_url_https 
* git add filename
* git commit -m "command description" filename
* git push -u origin master

* git status --check the status now
