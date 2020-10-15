---
title: "GnuPG - quick ref"
date: 2020-05-27T12:26:27+01:00
draft: false
toc: false
images:
tags:
  - GnuPG
  - gpg
---

# Using GnuPG - the gpg command line tool
Using a gpg encryption can be a quick and easy way to share secrets on a project.  By encrypting files using a gpg public keychain we can add and remove keys from said keychain to restric access to secrets.

### Install on MacOS
```
brew install gpg
```

### Create your own gpg key
```
$ gpg --full-generate-key
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048) 4096
Requested keysize is 4096 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 1y
Key expires at Wed  1 May 15:36:18 2019 BST
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: Alan Platt
Email address: aplatt@fakeemail.com
Comment:
You selected this USER-ID:
    "Alan Platt <aplatt@fakeemail.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o

# Enter a strong password when prompted
```


#### Exporting a public key 
Run these commands to get a public key
```
mkdir gpg_pub_keys
export KEY='aplatt@fakeemail.com'
gpg --armor --export "${KEY}" > "gpg_pub_keys/${KEY}.pub"
```
Run this command to import a single public key file
```
gpg --import "${KEY}"
```
NOTE: If you add new keys and already have an encrypted file you will need someone with a public key in the old keyring to decrypt and re-encrypt the files with the new keyring.

TIP: Its a good idea to store all the public keys somewhere(git) so that its easy to create a keyring from scratch.

### Encrypting, decrypting and recrypting
Encrypt with one key
```
gpg --encrypt -r aplatt@fakeemail.com "${FILE}"
```

Import keys then encrypt a file
```
KEYS="$(ls gpg_pub_keys/*.pub)"
for key in $KEYS; do
  gpg --import "${key}"
done

GPG_OPTIONS=$(echo $KEYS | sed 's/gpg_pub_keys\//-r /g' | sed 's/.pub//g' )
gpg --encrypt $GPG_OPTIONS "${FILE}"
```
To decrypt
```
FILE=somefile.gpg
gpg --decrypt "${FILE}" > "${FILE%.*}"
```


#### Delete a key
```
gpg --delete-secret-keys alanplatt@fakeemail.com
gpg --delete-keys alanplatt@fakeemail.com
```