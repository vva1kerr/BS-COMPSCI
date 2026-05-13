# new vps setup
* sudo useradd -m -s /bin/bash <yourusername>
* or if on ubuntu `sudo adduser yourusername`
* sudo passwd <yourusername>
* usermod -aG sudo username

### if already used `useradd `
* sudo mkdir -p /home/yourusername
* sudo chown yourusername:yourusername /home/yourusername
* sudo chmod 755 /home/yourusername
### then add the associated ssh key to the new user
* /home/<newuser>/.ssh/associated_keys

# create new ssh key
* `ssh-keygen -t ed25519 -C "your_email@example.com"`
* `ssh-keygen -t rsa -C "your_email@example.com"`

# start ssh agent
* `eval "$(ssh-agent -s)"`

# add a ssh key to the ssh agent
* `ssh-add ~/.ssh/id_ed25519`

# test the ssh key with connection
* `ssh -T git@github.com`

# add ssh from github
* `cd ~/.ssh`
* `ssh-keygen -t rsa -C "email"`
* `cat {file.pub}`
copy the cat to the github input box`
* `cd ~/.ssh`
* `eval "$(ssh-agent -s)"`
* `ssh-add "name of the ssh file"`
* `ssh-add -l`
* `cd "path to your app"`
* `ssh -T git@github.com`
* `git remote set-url origin git@github.com:{username}/{repo}.git`
