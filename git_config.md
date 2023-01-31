# Gitlab config to connect with ssh

### create new ssh key 
```
ssh-keygen -t rsa -b 2048 -C "comment"
cat ~/.ssh/id_ed....pub
```
### Copy public key to the gitlab ssh config

## add new host to ssh known hosts (linux)
```
ssh-keyscan -H gitlab.company.com >> ~/.ssh/known_hosts
```

## add new host to ssh known hosts (windows)
```
ssh-keyscan -H gitlab.company.com >> /c/Users/<user name>/.ssh/known_hosts
```

# Github config to connect with ssh

### create new ssh key 
```
ssh-keygen -t rsa -b 2048 -C "comment"
cat ~/.ssh/id_ed....
```

## after create ssh key you should add it to ssh with this command
```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed......
```

## add GPG key to github
```
$ gpg --full-generate-key
$ gpg --list-secret-keys --keyid-format=long

sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
uid                          Hubot <hubot@example.com>
ssb   4096R/4BB6D45482678BE3 2016-03-10

$ gpg --armor --export 3AA5C34371567BD2

```


# Check connect with ssh

```
ssh -T git@github.com
```
