# Generate a DSA key pair
```bash
# https://support.atlassian.com/bitbucket-cloud/docs/configure-ssh-and-two-step-verification/
ssh-keygen -t rsa -b 4096 -C "walker@domain.tld"
```

# Output of key generation
```bash
Your identification has been saved in /home/unix_wrh/.ssh/id_rsa
Your public key has been saved in /home/unix_wrh/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:nk/19B77xPjIZfduhd6AJCFGw9yxu/n2ljYistU/ASA walker@domain.tld
The key's randomart image is:
+---[RSA 4096]----+
|       +o...     |
|        E.+.     |
|       . o.o     |
|          ..o    |
|        S .o.o.. |
|       . . =.o++.|
|        o = ..o*O|
|        .+..ooBBB|
|        .o.o.==*B|
+----[SHA256]-----+
```

```bash
# View your public key
cat ~/.ssh/id_rsa.pub

# Verify the SSH key is loaded by the SSH agent
ssh-add -l

# If your key is not listed, add it again
ssh-add ~/.ssh/id_rsa

# Add the following configuration for Bitbucket
Host bitbucket.org
  HostName bitbucket.org
  User git
  IdentityFile ~/.ssh/id_rsa

# Test SSH connection to Bitbucket
ssh -T git@bitbucket.org

# Verbose SSH connection test
ssh -vT git@bitbucket.org

# Ensure file permissions
chmod 600 ~/.ssh/id_rsa
chmod 600 ~/.ssh/id_rsa.pub

# Re-add SSH key to the agent
ssh-add ~/.ssh/id_rsa

# Check for multiple SSH keys
ssh -i ~/.ssh/id_rsa -T git@bitbucket.org

# Start the SSH agent in the background
eval "$(ssh-agent -s)"

# Add your private key to the SSH agent
ssh-add ~/.ssh/id_rsa

# Change your Git remote URL from HTTPS to SSH
git remote set-url origin git@bitbucket.org:username/repository.git

# Use the Git credential cache (Linux)
git config --global credential.helper cache

# Change credential cache timeout to 1 hour (3600 seconds)
git config --global credential.helper 'cache --timeout=3600'
```




# Add ssh on Ubuntu for Github
## Enter the ssh folder

```bash
cd ~/.ssh
```

## generate the key
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

## Enter file in which to save the key 
```bash
(/home/username/.ssh/id_rsa): key-name
```

## check that you're the owner
```bash
ls -l key-name
```

## Enhance/fix permissions for the Parent Directory
```bash
chmod 755 /mnt/c/Users/device-name
```

## Enhance/fix permissions
```bash
chmod 600 key-name
```

## Create symbolic links in Windows to the WSL .ssh directory:
```bash
mklink C:\Users\razer\.ssh\key-name \\wsl$\Ubuntu\home\unix_wrh\.ssh\key-name
mklink C:\Users\razer\.ssh\key-name.pub \\wsl$\Ubuntu\home\unix_wrh\.ssh\key-name.pub
```

## Add the SSH Key to the SSH Agent
```bash
ps aux | grep ssh-agent
killall ssh-agent
eval "$(ssh-agent -s)"
```

# Add to ~/.bashrc or ~/.zshrc to start ssh-agent on login
```bash
echo 'eval "$(ssh-agent -s)"' >> ~/.bashrc
# or
echo 'eval "$(ssh-agent -s)"' >> ~/.zshrc
# To disable, remove or comment out the line from ~/.bashrc or ~/.zshrc
# eval "$(ssh-agent -s)"
#This way, you can manage the ssh-agent service in your WSL environment effectively.
```

## Add your new SSH key to the agent
```bash
ssh-add id_rsa_thinkpad
```

## Get and copy the ssh key to your clipboard
```bash
cat id_rsa_thinkpad.pub
```

## Go to GitHub -> settings -> add ssh keys
## Name ssh key "id_rsa_thinkpad"
## Paste value of key








## Steps to Create Symbolic Links in PowerShell Administrator
## Remove existing keys if necessary
## Create symbolic links to WSL keys
```powershell
### Windows (PowerShell as Administrator)

```powershell
# Remove existing keys in the Windows .ssh directory if necessary
Remove-Item -Force -Recurse C:\Users\razer\.ssh\key-name
Remove-Item -Force -Recurse C:\Users\razer\.ssh\key-name.pub

# Create symbolic links to the WSL keys
New-Item -ItemType SymbolicLink -Path C:\Users\razer\.ssh\key-name -Target \\wsl$\Ubuntu\home\unix_wrh\.ssh\key-name
New-Item -ItemType SymbolicLink -Path C:\Users\razer\.ssh\key-name.pub -Target \\wsl$\Ubuntu\home\unix_wrh\.ssh\key-name.pub
```

```powershell
PS C:\Users\razer\.ssh> dir


    Directory: C:\Users\razer\.ssh


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----          8/3/2024   2:24 PM              0 .sshkey-name
-a---l          8/3/2024   2:26 PM              0 key-name
-a---l          8/3/2024   2:26 PM              0 key-name.pub


PS C:\Users\razer\.ssh>
```



























git remote -v
origin  git@github.com:username/username.github.io.git (fetch)
origin  git@github.com:username/username.github.io.git (push)
ssh-add -l
The agent has no identities.

ssh-add ~/.ssh/key-name
Identity added: /home/unix_wrh/.ssh/key-name (username@gmail.com)

git status
On branch main
nothing to commit, working tree clean

ssh -T git@github.com
Hi username! You've successfully authenticated, but GitHub does not provide shell access.

push origin main
Enumerating objects: 977, done.


# Update the remote URL of your Git repository to use SSH:
```bash
git remote set-url origin git@github.com:username/username.github.io.git
```
