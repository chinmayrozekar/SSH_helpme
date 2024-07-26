# Passwordless SSH Login Setup Guide

This guide will help you set up passwordless SSH login from your local machine to your remote machine.

## Prerequisites
- Local machine with SSH installed
- Remote machine with SSH installed
- Basic knowledge of command-line interface

## Steps

1. **Generate an SSH Key Pair on Your Local Machine**


```sh
$ mkdir ~/.ssh
$ chmod go-w ~                # $HOME should not be writable by anybody else!
$ chmod 700 ~/.ssh            # $HOME/.ssh should be private
 
# create a private & public key pair:
# *NOTE*: From a RHEL8 host, add '-m PEM' to the options, otherwise your key won't be compatible with RHEL6
$ ssh-keygen -t rsa -N ""     # accept prompts without specifying a passphrase, if prompted for a file hitting enter will use the file specified in the parentheses
$ cd ~/.ssh
$ cat id_rsa.pub >> authorized_keys
$ chmod 600 authorized_keys   # authorized_keys should also not be writable by anybody else
```

2. **Copy Your Public Key to the Remote Machine**

   You can copy your public key using the `ssh-copy-id` command or manually. Follow one of the methods below:

   **Method 1: Using `ssh-copy-id`**

   ```sh
   ssh-copy-id username@remote_host
   ```
   - Enter the password for the remote machine when prompted.

   **Method 2: Manually Copying the Key**

   a. **Print Your Public Key**

      On your local machine:
      ```sh
      cat ~/.ssh/id_rsa.pub
      ```

   b. **Log In to the Remote Machine**

      ```sh
      ssh username@remote_host
      ```

   c. **Create the `.ssh` Directory on the Remote Machine**

      ```sh
      mkdir -p ~/.ssh
      chmod 700 ~/.ssh
      ```

   d. **Append Your Public Key to the `authorized_keys` File**

      On the remote machine, open the `authorized_keys` file in an editor, or use the following command to append the key:
      ```sh
      echo "<your-public-key>" >> ~/.ssh/authorized_keys
      ```
      Replace `<your-public-key>` with the actual key content copied from the local machine.

   e. **Set the Correct Permissions**

      ```sh
      chmod 600 ~/.ssh/authorized_keys
      ```

3. **Verify the Setup**

   Attempt to log in from your local machine without a password:
   ```sh
   ssh username@remote_host
   ```

   If everything is set up correctly, you should be able to log in without being prompted for a password.

## Troubleshooting

If you encounter any issues, ensure the following:

- The content of your `id_rsa.pub` key on your local machine is correctly copied to the `~/.ssh/authorized_keys` file on the remote machine.
- The permissions on the remote machine are set correctly:
  ```sh
  chmod 700 ~/.ssh
  chmod 600 ~/.ssh/authorized_keys
  chmod go-w ~
  ```

- The SSH configuration on the remote machine allows key-based authentication. Check the SSH configuration file (`/etc/ssh/sshd_config`):
  ```sh
  sudo nano /etc/ssh/sshd_config
  ```
  Ensure the following settings are enabled (uncommented):
  ```sh
  PubkeyAuthentication yes
  AuthorizedKeysFile .ssh/authorized_keys
  ```
  Restart the SSH service to apply any changes:
  ```sh
  sudo systemctl restart sshd
  ```

- Enable verbose mode for SSH to get more details about the authentication process:
  ```sh
  ssh -v username@remote_host
  ```

Following these steps should set up a passwordless SSH login from your local machine to your remote machine.
