# SSh setup on Ubuntu server


### Creating RSA key Pair

Create key on local machine

`ssh-keygen`

### Copy Public key using `ssh-copy-id`

`ssh-copy-id username@remote_host`

### Copy Public key using SSH

**NOTE**: If you fo not have `ssh-copy-id` available, you can upload your keys using a comvemtional method. *This will only work if you have password-based SSH access to your server*

On the remote server make sure that the `~/.ssh` directory exists and has the correct permissions under the account in use.

You can then output the content you piped over into a file called `authorized_keys` within the directory.

`cat ~/.ssh/ssh_public_key_here.pub | ssh username@remote_host "mkdir -p ~/ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/.ssh && cat >> ~/.ssh/authorized_keys"`


## Authenticating using ssh keys

`ssh username@remote_host`

## Disabling password authentication on your server

`ssh root@remote_host`

`sudo nano /etc/ssh/sshd_config`

Search for *PasswordAuthentication* in the file and make sure value is  *no*

`sudo systemctl restart ssh`

Note: Open a new terminal before logoff on the other to make sure everything works as expected

`ssh username@remote_host`



