# ssh

ssh into a server

```bash
ssh username@server_ip
```

ssh into a server with a specific port

```bash
ssh -p 2222 username@server_ip
```

send a command to a server

```bash
ssh username@server_ip "ls"
```

send a file to a server

```bash
scp file.txt username@server_ip:/home/username/
```

get a file from a server

```bash
scp username@server_ip:/home/username/file.txt .
```

## ssh keys

You can generate SSH keys (on your machine) by running:

```bash
ssh-keygen
```

This will generate a private key and a public key. The private key is stored in `~/.ssh/id_rsa` and the public key is stored in `~/.ssh/id_rsa.pub`.

You can then copy the public key to the server by running:

```bash
ssh-copy-id username@server_ip
```

Now you can ssh into the server without a password.
