
# Utilities
The [utilities](https://github.com/Cyber-Defense-Legion/utilities)
toolkit is developed by the Cyber Defense Legion for the general
public.

## Features
Currently, file encryption and decryption scripts are the only
completed utilities. The secure password generator is based on
Ruby's [SecureRandom](https://ruby-doc.org/stdlib-2.7.1/libdoc/securerandom/rdoc/SecureRandom.html)
standard library module, so while it isn't complete, it does
generate passwords as cryptographically strong as it is possible
to generate on the host operating system.

### File Operations
The primary design goal of the encryption and decryption scripts
was to provide a simple API by which to convert any file into an
easy to transmit format; that is to say, an ASCII hex-encoded
string.

The scripts use [OpenSSL](https://www.openssl.org/) for the
encryption and decryption, and the `base64` [coreutils](https://www.gnu.org/software/coreutils/)
utility.

Encryption is done using AES-256 in CBC mode.

#### Encryption
To encrypt a file, simply pass in the filename as an argument
to the `encrypt-file` script. The script will request (and
re-request, for confirmation) a password from you.
```bash
 $ ./encrypt-file test-file.txt
enter aes-256-cbc encryption password:
```
After confirming the encryption password, the file is encrypted
and written out to a `.enc` file and piped to standard output
as well.
```bash
 $ ./encrypt-file test-file.txt
enter aes-256-cbc encryption password:
Verifying - enter aes-256-cbc encryption password:
U2FsdGVkX19F3M/zTGUkNFdD/outDjJS8t6KLUf8c/I5F+ZwTRu1+oDfghBuZ+h8
```
The `.enc` extension is nothing special. In fact, the files
themselves are simply base64-encoded ASCII text. This allows
you to simply email files to yourself or others, or store
them in otherwise less-than-secure locations without having
to stress too much about it.

#### Decryption
Decryption is analogous to encryption; simply call the
`decrypt-file` utility with the encrypted file's name as an
argument.
```bash
 $ ./decrypt-file test-file.txt.enc
enter aes-256-cbc encryption password:
```
Just as before, type in the encryption password.

If you get the password wrong, you'll get a message like this:
```bash
bad decrypt
140453899920704:error:06065064:digital envelope routines:EVP_DecryptFinal_ex:bad decrypt:crypto/evp/evp_enc.c:583:
%5(I!p�)Zq2�{
```
Simply rerun the decryption-command with the filename as an
argument again, making sure to use the correct password the
next time.
