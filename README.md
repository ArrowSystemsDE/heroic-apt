# heroic-apt
A Github Pages hosted APT/Debian repository for installing Heroic Games Launcher  

Pulls the latest `deb` file from GitHub releases.


## Setup
```bash
curl -s --compressed "https://razuuu.github.io/heroic-apt/heroicapt.gpg" | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/heroicapt.gpg > /dev/null
sudo curl -s --compressed -o /etc/apt/sources.list.d/heroicapt.list "https://razuuu.github.io/heroic-apt/heroicapt.list"
sudo apt update
```

## Install
```bash
sudo apt install heroic
```

## GPG key setup
```bash
gpg --full-generate-key
```

Select the default options  
After it's done:  

```bash
gpg --list-secret-keys
```


sec   rsa3072 2023-04-27 [SC]  
      ABCDEFGHIJKLMNOPQRSTUVWXYZ   
uid           [ultimate] Heroic Games Launcher <mail@example.com>  
ssb   rsa3072 2023-04-27 [E]  

Copy ABCDEFGHIJKLMNOPQRSTUVWXYZ for Actions  
Also don't forget you're passphrase  

## Setup Actions

1. Go to settings
2. Down to "Secrets and variables"
3. "New repository secret"
Name: KEY_PASSPHRASE  
Secret: your passphrase  

4. Now click on variables and select "New repository variable"
Name: PRIVATE_KEY  
Value: your private key  

## Actions run
Every night or manual  
