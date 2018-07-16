# Deploy APP to Heroku

## GIT
1. 將 GIT 加入專案，在專案目錄下輸入 
```
$git init 
```
2. 在根目錄下加入 .gitignore 檔案，將不需要的檔案 ignore
```
node_modules/
*.log
package-*.json
```
3. First commit
```
git status
git add [file]
git add .
git commit -m "first commit"
```
4. connect to Github and Generate SSH keys

    1. [Checking for existing SSH keys](https://help.github.com/articles/checking-for-existing-ssh-keys)
    2. [Generating a new SSH key and adding it to the ssh-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
    3. [Adding a new SSH key to your GitHub account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)
    4. [Testing your SSH connection](https://help.github.com/articles/testing-your-ssh-connection/)

5. Create a new repository and push code to it
```
git remote add origin [your git url]
git push -u origin master
```

## Heroku
1. [download heroku-cli](https://devcenter.heroku.com/articles/heroku-cli#windows)

2. Login
```
heroku login
```

3. add ssh keys to heroku
```
# 會自動取得 ssh keys
heroku keys:add

# delete keys
heroku keys:remove [email]
```

4. connet to Heroku by using ssh
```
ssh -v git@heroku.com
```

5. Setup start script and port for Heroku
```javascript=
const port = process.env.PORT || 3456
app.listen(port, ()=>{
  console.log(`Server is running in port ${port}`);
})
```
```javascript=
  //package.json
  "start": "node server.js"
```

6. Create a new Heroku APP

```
//by using command line
heroku create
```
```
//在web 建立專案後，鍊結 git repo
git remote add heroku [heroku git url]
```

7. push code to Heroku git repo
```
git push heroku
```

8. open App
```
heroku open
```

9. Setting own domain
[Reference](https://medium.com/@wutingyu/godaddy-dns%E8%A8%AD%E5%AE%9A-%E8%BD%89%E5%90%91heroku-9d2cce7d3bc6)

10. Setting env configs
Add a env 'JWT_SECRET' to heroku by using web
![](https://i.imgur.com/kzf1JSO.png)

```javascript=
//by using command line

// show all configs
heroku config

//set env NAME to Ben
heroku config:set NAME=Ben

//get env NAME
heroku config:get NAME

//unset env NAME
heroku config:unset NAME

```

