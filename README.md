# sshscript

Set up SSH key-based login in one command:

```sh
./ssh-setup user@example.com
```

The command:

1. Creates `~/.ssh/id_ed25519` if it does not already exist.
2. Installs the public key in the remote user's `~/.ssh/authorized_keys`.
3. Verifies that login works without a password.

The initial connection may ask for the remote account's password. This is
necessary to install the key; subsequent connections use the key instead.

The generated private key has no passphrase so automated connections do not
prompt. Protect the machine and the private key carefully. To use a different
key location:

```sh
./ssh-setup --key ~/.ssh/work_ed25519 user@example.com
```

To remove that key from the remote account's `authorized_keys` file without
deleting the local key files:

```sh
./ssh-setup --remove-key --key ~/.ssh/work_ed25519 user@example.com
```

Without `--key`, removal looks for `~/.ssh/id_ed25519`. If that key pair is
not found, the script asks for the private-key path to use instead.

The script requires Bash, OpenSSH (`ssh` and `ssh-keygen`), and an account that
can initially authenticate to the remote host.
