
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

