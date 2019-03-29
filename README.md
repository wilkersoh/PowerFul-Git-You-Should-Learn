### git bash Window
<p>ls -a -l ~/.ssh</p>
#  ssh-keygen -t rsa -b 4096 -C "emailAdress@hotmail.com"
* $ eval "$(ssh-agent -s)"
* ssh-add ~/.ssh/id_rsa
-----
<p>github remoto code</p>
*$ git remote add origin git@github.com:xxxxxxxx

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
