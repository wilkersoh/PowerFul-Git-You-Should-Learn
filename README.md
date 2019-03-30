### Multiple SSH KEY Git Bash Window
#教学
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
