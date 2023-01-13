# How to secure Git repository

1. Sometimes you can add sensitive files in your Git repo by error or by out of ignorance.
2. That information, once you've updated your remote, is not enough just deleting it.
3. Git, tracks all history of your repository and you can go back in time.

## How to proceed

1. Download [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/)

```bash
curl https://repo1.maven.org/maven2/com/madgag/bfg/1.14.0/bfg-1.14.0.jar -o bfg.jar
```

2. You can then delete files that have existed in the repository at some point in time. For instance, following files:
* usernames.txt
* passwords.txt

*If you're in repository, just use `./`*

```bash
java -jar bfg.jar --delete-files "{passwords,username}.txt"
git push --force
```

3. You can update also information that have been stored in the past, taking that info from a file.
Passwords_to_replace.txt contains text you want to delete from Git history. Those strings will be replaced by `***REMOVED***` string.

```bash
java -jar bfg.jar --replace-text Passwords_to_replace.txt
git push --force
```

3. You can also delete files bigger than any size.

```bash
java -jar bfg.jar --strip-blobs-bigger-than 10M
git push --force
```

> INFO:
> If you have following message:
> `Warning : no large blobs matching criteria found in packfiles - does > the repo need to be packed?`
> You must type
> ```bash
> git gc
> ```
> 