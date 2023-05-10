
# heroic-apt
A Github Pages hosted APT/Debian repository for installing Heroic Games Launcher  
Pulls the latest `deb` file from GitHub releases.


## Install
```bash
curl -s --compressed "https://deb.arrow-systems.de/heroicapt.gpg" | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/heroicapt.gpg > /dev/null
sudo curl -s --compressed -o /etc/apt/sources.list.d/heroicapt.list "https://deb.arrow-systems.de/heroicapt.list"
sudo apt update
```
then type
```bash
sudo apt install heroic
```

# Actions Setup

one-time configuration for Actions.

## GPG key setup

Open your Terminal, then type
```bash
gpg --full-generate-key
```

```
root@razuuu:~# gpg --full-generate-key
gpg (GnuPG) 2.2.40; Copyright (C) 2022 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
  (14) Existing key from card
Your selection?
```
Press `1`, then press ENTER.

```bash
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072)
```
Press ENTER.

```
Requested keysize is 3072 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0)
```
Press `0`, then press ENTER.

```bash
Key does not expire at all
Is this correct? (y/N)
```
Press `y`, then press ENTER.

```
GnuPG needs to construct a user ID to identify your key.

Real name: John Doe
Email address: john.doe@example.com
Comment:
```
Enter your name, your email address and left comment empty, after that press ENTER

```
You selected this USER-ID:
    "John Doe <john.doe@example.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit?
```
Press `O`, then ENTER.

```
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
Enter passphrase:
```
Enter your passphrase, after that press ENTER.

```
gpg: revocation certificate stored as '/root/.gnupg/openpgp-revocs.d/BEFB923D97D358E5D15F695C29D0F9D5B60ABE77.rev'
public and secret key created and signed.

pub   rsa3072 2023-05-10 [SC]
      BEFB923D97D358E5D15F695C29D0F9D5B60ABE77
uid                      John Doe <john.doe@example.com>
sub   rsa3072 2023-05-10 [E]
```

Now the GPG Setup is done.

## Setup Actions and Pages

#### Actions
1. Go to the `Settings` tab
2. Down to `Secrets and variables` -> `Actions`
3. Press on `New repository secret`

Name *
`KEY_PASSPHRASE`  
Secret * 
`Your passphrase`

Then press `Add secret`.
<hr>

Now switch to `Variables` tab.

Press on `New repository variable`

Name *
`PRIVATE_KEY`  
Value *
Output of ```gpg --armor --export-secret-key john.doe@example.com -w0```
<hr>

#### Pages

1. Go to the `Settings` tab
2. Down to `Pages`
3. Change Source to `GitHub Actions`
4. (optional) `Custom domain` -> `deb.example.com`
####

## Bind/Named or github.io domain
Change [this](https://github.com/ArrowSystemsDE/heroic-apt/blob/main/.github/workflows/static.yml#LL62C4-L62C4) line to your Domain.

e.g
```echo "deb [signed-by=/etc/apt/trusted.gpg.d/heroicapt.gpg] https://arrowsystemsde.github.io/heroic-apt/ ./" > heroicapt.list```

or
```echo "deb [signed-by=/etc/apt/trusted.gpg.d/heroicapt.gpg] https://deb.arrow-systems.de/ ./" > heroicapt.list```
<hr>
For custom domain purposes:

```bind
deb	IN	CNAME	arrowsystemsde.github.io
```
