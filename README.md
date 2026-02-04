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

```bash
gpg --list-options show-only-fpr-mbox -k "@zfnd.org" | \
  $(gpgconf --list-dirs libexecdir)/gpg-wks-client -v --install-key
```

## DNS Configuration

Requires CNAME record:

```txt
openpgpkey.zfnd.org → zcashfoundation.github.io
```
