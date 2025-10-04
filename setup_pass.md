# Password Store Setup Guide

This repository contains instructions for setting up and transferring a password store between machines using `pass` and GPG keys.

## Prerequisites
	sudo apt-get install -y git pass

## Setup Instructions

### On New Machine

1. Install the password manager:
```bash
sudo apt-get install pass -y
```

2. Clone the password store repository:
```bash
git clone git@github.com:gilflorida2023/passwords.git .password-store
```

### Exporting Keys (On Old Machine)

1. Create and navigate to export directory:
```bash
mkdir export_keys
cd export_keys
```

2. Export your GPG keys:
```bash
# Export public key
gpg --output public.gpg --armor --export gilflorida2023@gmail.com

# Export private key
gpg --output private.gpg --armor --export-secret-key gilflorida2023@gmail.com
```

### Importing Keys (On New Machine)

After transferring the key files to the new machine:

```bash
# Import private key
gpg --import private.gpg

# Import public key
gpg --import public.gpg
```

### Up the key's trust level on the new machine
```bash
#responses to prompts
gpg --edit-key gilflorida2023@gmail.com
trust
5
y
save
```

## Security Note

Please ensure you keep your GPG keys secure and never share your private key with anyone. The private key should be transferred between machines through a secure method.
