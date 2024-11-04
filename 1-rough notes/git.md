# git
---
Date: 09,Oct,2024
subject: source control management and github 
field: [[devops]]
tags: #git #github

---

# VERSION CONTROL SYSTEM




# GIT

git store its conf in 3 location

/etc/gitconfig for systemwide
~/.gitconfig for user wide
.git/config for repo wide changes


`git config --system --edit`
`git config --global --edit`
`git config --local --edit`
  

###### BASIC 
git init
git status
git add 
git add .
git commit -m "my message"
git log
git checkout main
git checkout -f main

repo = local repo / remote repo

git remote add origin 
git push origin main

###### LEVEL 2
git branch branch-name
git checkout branch-name
git checkout -b branch-name  => create and move into it in 1 go

git push --set-upstream origin dev
git push -u origin dev

git pull

### normal workflow

1. clone the repo
2. create a new branch from the main or another repo
3. make your changes
4. push the branch to the remote repo
5. open a pull request
6. merge the changes
7. pull the merged changes in your local repo
8. repeat 


### merge conflicts

  









