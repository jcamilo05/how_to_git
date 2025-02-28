# Sections

## 1. and 2. Preparation

Setting up name and email can be pretty straightforward, but what may matter is setting up autocrlf to true on windows and safecrlf to warn. [Read more](https://githowto.com/setup)

git config --global user.name "Andres"

git config --global user.email "nanoandres_24@hotmail.com"

git config core.editor "vim"

## 3. Create a project

- git init
- git add FILE
- git commit

## 6. Staging the changes

A git add can be reverted via git reset. Git reset won't undo commits or pushes

## 10. History

git log 

We can get a simplified log to only yield the commit's key and the commit message by using...

**git log --pretty=oneline**

This can be manipulated further with options like 

```
git log --pretty=oneline --max-count=2
git log --pretty=oneline --since='5 minutes ago'
git log --pretty=oneline --until='5 minutes ago'
git log --pretty=oneline --author=<your name>
git log --pretty=oneline --all
```
### Fancy formatting

git log --all --pretty=format:"%h %cd %s [%an]" --since='7 days ago'

git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short

- %h is the abbreviated hash of the commit
- %d commit decorations (e.g. branch heads or tags)
- %ad is the commit date (%cd is also date, are they the same?)
- %s is the comment
- %an author's name
- --graph tells git to display the commit tree in the form of an ASCII graph layout
- --date=short keeps the date format short and nice

## 11. Aliases
Set up your .gitconfig, if you want to give [aliases to your commands](https://githowto.com/aliases).
Check the *hist* alias in this section to see the long git log command used throughout these lessons. Hereto we can find it anyway, though.

```
hist = log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short
```
In the .gitconfig the " must be escaped with a \

Other interesting commands given aliases are **cat-file -t** and **cat-file -p**
# 12. Getting older versions (checkout)

Using this log

git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short

we can access the hash values(%h) of the commits. The earlier ones will come last, we can travel back in time and see how the branch as well as files used to look back then!

for instance, access first commit...

```
git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short | tail -n1 | awk '{print $1}'
```

Careful with leaving a detached head. Yes you may perform

git checkout <hash>
  
but always try to go back to **git checkout master**

# 13. Git Tags

Added a new v1 tag with  
```git
git tag v1
```
They have to be pushed to the actual github repo with **git push --tags \<remote\>**. But if we are pushing to origin, we can ignore the \<remote\> part

When we push the tags we get the following output

```git
git push --tags
Total 0 (delta 0), reused 0 (delta 0)
To github.com:Zappandy/how_to_git.git 
* [new tag]         v1 -> v1  
```

The generated tag, which was performed with **git tag v1** fetched the previous hash as a reference point!

## Tags for previous versions

We have previously updated the repo, so we can now **git checkout v1** to go to that snapshot. In this case, the hash would be *2837c0b*.

If we want to go to the last hash before the tag, we can use the following commands:

```git
git checkout v1^ # one hash in the past from MAIN BRANCH
git checkout v1~1 # one hash in the past from MAIN BRANCH
git checkout v1~2 # two hashes in the past from MAIN BRANCH
```
I personally prefer the second notation to specify the number of hashes in the past. This is only following the main branch, though. Any sub-branches won't be counted. There may be a way, but we'll look into this later

Of course tags can be created in past commits and we can still refer back to them. This can be really useful in software development

We can look at the list of our tags with **git tag**

# 14. Undoing local changes

Before they are staged, we can go in the working directory and perform a **git checkout FILE** to return the file to its previous state

# 15. Cancel Staged Changes (before committing)

We can reset the buffer zone with 

```git
git restore --staged README.md
git checkout file
```
This is simplifying these steps:
```git
git reset HEAD file
git checkout file
```

# 16. Cancelling commits


