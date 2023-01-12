# Gitlab config to connect with ssh

## add new host to ssh known hosts
```
ssh-keyscan -H gs.parstechai.ir >> ~/.ssh/known_hosts
```
# Github config to connect with ssh
## after create ssh key you should add it to ssh with this command
```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed......
```

