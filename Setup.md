# SSW security.txt Setup

First make sure you have a GPG tool installed. If you are on Windows, you can use Gpg4win. If you are on Mac, you can use GNU Privacy Guard.

For Windows, you can download Gpg4win from [here](https://gpg4win.org/download.html).

For Mac, you can download GNU Privacy Guard from [here](https://gnupg.org/download/index.html), or install with brew using

```bash
brew install gnupg
```

## Generate key

1. `gpg --full-generate-key`
   1. Select RSA
   2. Select 4096
   3. Specify `13m` for key expiration, we want the key to expire after 13 months but will renew it for 1 July each year
   4. Enter name and email as **SSW** and **security@ssw.com.au**
   5. Enter passphrase (store this in keeper)
   6. O to confirm
2. Export public key with `gpg --armor --export security@ssw.com.au > public_key.asc`
3. Export private key with `gpg --armor --export-secret-keys security@ssw.com.au > private_key.asc`
4. Upload private_key.asc to Keeper (search for `security.txt`, speak to SSW SysAdmin for access)
5.  Upload the public_key.asc to [keys.openpgp.org](https://keys.openpgp.org/) and verify the key
6.  Get a fingerprint for the security.txt file by running `gpg --list-keys --fingerprint security@ssw.com.au`
7.  Update the `.well-known` files with the 
    1.  Fingerprint
    2.  Expiration date
    3.  Public key
8.  Upload public_key.asc alongside the security.txt file on websites at /.well-known/security.txt and /.well-known/public_key.asc

## Import key

1. Download private_key.asc from Keeper
2. `gpg --import path/to/private_key.asc` (use the passphrase from Keeper)

## Decrypting a message

1. `gpg --decrypt path/to/encrypted_file.gpg`

## Sample security.txt

To see a sample file look in `.well-known/security.txt` in this repository.
