## Create a new repository on the command line
```shell=
echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/Fallins/test.git
git push -u origin master
```

## Push an existing repository from the command line
```shell=
git remote add origin https://github.com/Fallins/test.git
git push -u origin master
```