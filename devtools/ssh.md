__SSH (Secure Shell)__ → protocol used over shell that allow user to share files as well was control and modify remote computers over the internet. The communications are encrypted so bad actors cannot intercept the data being sent.

```
ssh <user>@<host>
```
Afterwards, we can use the command line as we usually do, with `ls` to list files, `mkdir` to create new directories, etc.

_Copy files from our machine to the remote one:_
```
rsync -av <files> <user>@<host>:<folder>
```

## How it works
There are three techniques used in SSH:
1. __symmetrical encryption__ → uses one secret key for both the encryption and decryption by both parties. Anyone who posesses a key can decrypt what's being transferred.
2. __asymmetrical encryption__ → uses two separate keys for encryption and decryption. One of the keys is called *public key* and the other *private key*. Together form a **public-private key pair**. A message that is encrypted by a machine's public key can only be decrypted by the same machine's private key – this is called *one way relationship*. The private key should **never** be shared with anyone.
3. __hashing__ → A hash function generates a unique value (a hash) of fixed length for each input. It's never meant to decrypt anything.

__Difiie-Hellman Key Exchange Algorithm__ → it's a secure way to exchange the secret key without bad actors intercepting it. The two computers share public pieces of data, and then manipulate it to independently calculate the secret key. Without the key exchange algorithm, bad actors will never be able to find out the secret key.

Each key is specific to an SSH session.\
SSH uses asymmetrical encryption during the key exchange algorithm of symmetric encryption. It then switches to symmetrical encryption after the secret key has been generated on each computer.

__HMX__ or __hash-based Message Authentication codes__ → each message that is transmitted must contained a MAC. MAC in SSH is generated from the symmetric key, the packet sequence number, and the message contents that are being sent.

To avoid third parties from trying to pretend they are the host, SSH employs HMX. With them, we are able to verify the authentication of the message. The client generates a MAC, which is sent outside of the symmetrically encrypted area. The host then generates a hash with the same information and compares it with the MAC sent. If they match, it means the message was not tampered with.

## SSH into a server without password
__RSA__ → allows us to provide or prove the identity of the person without a password.

In our client machine, create the *~/.ssh* folder if it doesn't exist.

Start with generating a public-private key pair.
```
$ ssh-keygen -C "user@email.com"
```
- `-C` → provides a comment.
- `-t` → type of key to create.
- `-b` → specifies the number of bits in the key to create. Default for RSA is 2048.

We'll be asked where we want to save the file. We can save it with another name if we have multiple files. It will generate a *id_rsa* file containing the private key, and a *id_rsa.pub* file, with the public key.

Use a command to copy the public key file content to the clipboard.
```
$ pbcopy < ~/.ssh/id_rsa.pub
```

SSH into our server.
```
$ ssh <user>@<host>
```
Create an *~/.ssh* directory if there isn't none. Next, if there isn't one, inside the *~/.ssh* directory create an *authorized_keys* file. Edit this file.
```
$ nano authorized_keys
```
Paste our clipboard contents (the previously copied public key). Save the file.

_If we have multiple RSA keys:_
```
ssh-add ~/.ssh/<private-rsa-key>
```
- `-l` → list all added identities.
- `-D` → remove all identities.

_Setup SSH on GitHub:_
Go to Settings > SSH and GPG keys. Add our SSH public key to it. GitHub recommends generating a key type rsa with 4096 bits.

## Tunneling ourselves through computers
If we know the path, we can tunnel ourselves through multiple computers until we reach our destination.
```
$ ssh -tt pi@10.2.1.12 ssh -tt pi@10.2.3.5 [...]
```

# Keywords
__shell__ → command line. It allows us to talk with the operating system.

__host__ → remote server we're trying to access.

__client__ → computer we're using to access the host.

__encryption__ → way to hide a piece of information, *e.g.* text, into something that is impossible for a third party to read without decrypting it.

# Sources
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie
