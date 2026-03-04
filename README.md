# ZFND Web Key Directory (WKD)

This repository hosts the [Web Key Directory](https://wiki.gnupg.org/WKD) for Zcash Foundation security disclosure keys.

## Usage

Retrieve the ZFND security team's public key automatically:

```bash
gpg --locate-keys security@zfnd.org
```

Or verify WKD is working:

```bash
gpg --auto-key-locate clear,wkd,nodefault --locate-key security@zfnd.org
```

## Structure

```
.well-known/
└── openpgpkey/
    └── zfnd.org/
        ├── policy      # Required empty file
        └── hu/
            └── <hash>  # GPG public key (binary)
```

## Adding/Updating Keys

Requires GPG >= 2.2.12:

1. List installed public keys for security@zfnd.org
```bash
gpg --list-options show-only-fpr-mbox -k "security@zfnd.org"
```
2. Install the key to your local git repo, this will create the correct directory structure and files for the Web Key Directory (WKD)
```bash
$(gpgconf --list-dirs libexecdir)/gpg-wks-client -v --install-key [PRIMARY_KEY_ID] security@zfnd.org
```
3. Update the git repo with the new public key
```bash
cd openpgpkey/
git add zfnd.org
git commit -m "Adding security@zfnd.org public key"
git push origin
```

## DNS Configuration

Requires CNAME record:

```txt
openpgpkey.zfnd.org → zcashfoundation.github.io
```
