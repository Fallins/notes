# Gatsby

---
### Get Started

##### Install
```bash
npm install --global gatsby-cli
```

##### Usage
```bash
# create a new site by using default starter
gatsby new gatsby-site

# start a hot-reloading server on port 8000
gatsby develop

# generate static HTML and JavaScript code bundles for production
gatsby build

# starts a local HTML server for testing your built site
gatsby serve
```

##### Starters
[Docs](https://www.gatsbyjs.org/docs/gatsby-starters/)
```bash
# gatsby new [SITE_DIRECTORY] [URL_OF_STARTER_GITHUB_REPO]
gatsby new blog https://github.com/gatsbyjs/gatsby-starter-blog
```

---
###  Tutorial

#### Create project
```bash
gatsby new project-name
gatsby develop
```

#### Create a new page
> To create a new page, you have to create a new file under this path ```src/pages/```
> and file name will be the route name

##### Step 1
 Create a new file ```src/pages/test.js``` 
![](https://i.imgur.com/QtHIda7.png)

##### Step 2
File name will be the route name [http://localhost:8000/test/](http://localhost:8000/test/)

##### Step 3
return a react component ( can be a stateless comp or class comp)
![](https://i.imgur.com/3ES86jg.png)
    

####  GraphQL
> You can access it when your site’s development server is running—normally at [http://localhost:8000/___graphql](http://localhost:8000/___graphql).

![](https://i.imgur.com/KTpQhQk.png)

---

![](https://i.imgur.com/4F0Ef3G.png)

![](https://i.imgur.com/qbPFU4g.png)

![](https://i.imgur.com/TIkavQs.png)

---
### Notice
>If you can't clone a repository with a "git://" url because of a proxy or firewall, here is a little git configuration that will force git to use "https://" even when you'll type "git://" URL.

Rewrite any git:// urls to be https:// but, it won't touch sshurls (git@github.com:)

```bash
git config --global url."https://github".insteadOf git://github
```
#### or replace with ssh
Use ssh instead of https://

```bash
git config --global url."git@github.com:".insteadOf "https://github.com/"
```