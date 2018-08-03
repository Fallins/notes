# Deploy on Heroku

## Install Heroku
Download on [Heroku](https://devcenter.heroku.com/articles/heroku-cli#download-and-install)

## LOGIN
```shell=
heroku login
```
![](https://i.imgur.com/wBBdNyR.png)


## CREATE
在專案跟目錄執行 create 
```shell=
heroku create
```
![](https://i.imgur.com/NvfS2EE.png)


## PUSH
```shell=
git push heroku master
```

## LOGS
```shell=
heroku logs --tail
```

## ADDONS
check out all addons in your app
```shell=
heroku addons
```
![](https://i.imgur.com/3hKOLmP.png)

### postgres
check your postgres infos.
And the Add-on property is your db url.(`postgresql-adjacent-33845`)
```shell=
heroku pg:info
```
![](https://i.imgur.com/8L7VufR.png)


## NOTE
### Change APP name
It's easy to change App name in heroku web. But need to reset git repo
```shell=
git remote rm heroku
# this rename variable should be you APP's new name
heroku git:remote -a newname

# can use git remote to see all remote you have
git remote
```

### How to deploy a create-react-app with an Express backend to Heroku
[refference](https://medium.com/@chloechong.us/how-to-deploy-a-create-react-app-with-an-express-backend-to-heroku-32decfee6d18)

 
 
 
 
 
 
 
 heroku pg:credentials:url DATABASE_URL