# Add SSH keys in Github

## Generate ssh keys

**STEP 1 : generate keys**

```ssh-keygen -t rsa -b 4096 -C "GitHub email address"```

**STEP 2 : save in the default path**
(/Users/you/.ssh/id_rsa)

## Adding SSH key to the ssh-agent

**STEP 1 : Ensure the ssh-agent is running**

```eval $(ssh-agent -s)```

**STEP 2 : add SSH private key to the ssh-agent**

```ssh-add ~/.ssh/id_rsa```

`Tips: Must run all these command in git bash`
![](https://i.imgur.com/O1GojFR.png)


## Add to GitHub account

**STEP 1 : Run this command to clip keys or open with your editor to copy it**
`clip < ~/.ssh/id_rsa.pub`

**STEP 2 : Go to Settings -> New SSH key to add keys in github**

**STEP 3 : Test**
```ssh -T git@github.com```
![](https://i.imgur.com/7RrplaW.png)


The key icon will become green after test success 
![](https://i.imgur.com/j93XNky.png)





[refference](https://help.github.com/articles/connecting-to-github-with-ssh/)