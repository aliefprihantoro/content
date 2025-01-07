## how use sshd
1. in server exec `sshd`
2. in client do :
  1. generate ssh `ssh-keygen -t ed25519 -C "your_email@example.com" && mv <name-key> <name-key>.pub ~/.ssh`
  2. add ssh to agent `eval "$(ssh-agent -s)" && ssh-add ~/.ssh/<name-private-key>`
  3. copy to server `ssh-copy-id username@remote_host` or `ssh-copy-id 127.0.0.1 -p8022`
  4. try `ssh username@remote_host` or `ssh 127.0.0.1 -p8022`
  > every quit terminal and before execute ssh, add ssh to agent
3. in server :
  1. edit in `/etc/ssh/sshd_config` or `~/../usr/etc/ssh/sshd_config`
  2. change/add this config `PasswordAuthentication no`
