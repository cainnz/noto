### Creating new user/settings
*add new user*
```bash
adduser username #adds new user
```  
*change user group to* `sudo` 
```bash
usermod -aG sudo user_name #changes user group to a different one, in this case `sudo`
```
*check how many users are using the same machine*
```bash
cat /etc/passwd
```


