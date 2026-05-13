* https://docs.python.org/3/library/sqlite3.html
* https://medium.com/@arif.rahman.rhm/technical-guide-building-a-streamlit-app-with-login-and-multi-page-menu-integration-c570e83ef6c7
* https://askubuntu.com/questions/46424/how-do-i-add-ssh-keys-to-authorized-keys-file
* https://gist.github.com/pierrejoubert73/902cc94d79424356a8d20be2b382e1ab
* https://stackoverflow.com/questions/66269402/add-github-ssh-keys-to-ec2-instance
* https://docs.streamlit.io/develop/api-reference/configuration/st.set_page_config
* https://betterstack.com/community/questions/importing-files-from-different-folders-python/
* https://www.youtube.com/watch?v=Dufg-UfP2II
* https://blog.streamlit.io/streamlit-authenticator-part-1-adding-an-authentication-component-to-your-app/
* https://docs.streamlit.io/deploy/tutorials/docker#create-a-dockerfile
* https://github.com/vb64/markdown-pdf

* sudo apt-get install -y tesseract-ocr poppler-utils

* urbex.help (A record) → ELB (Load Balancer) → Target Group → EC2 instance


HTTPS:443
Forward to target group

vva1kerr-target-group : 1 (100%)
Target group stickiness: Off

HTTP:80
Redirect to HTTPS://#{host}:443/#{path}?#{query}

Status code: HTTP_301


https://www.youtube.com/watch?v=JQP96EjRM98&t=707s






# SETUP COMMANDS

* `sudo apt update`
* `sudo apt-get update`
* `sudo apt upgrade -y`
* `sudo apt install git curl unzip tar make sudo vim wget -y`
* `git clone "Your-repository"`
* `sudo apt install python3 python3-pip`
* `sudo apt install python-is-python3`
* `sudo apt install -y libgl1 mesa-utils xvfb`
* `sudo apt-get install -y gdal-bin libgdal-dev`
* `sudo apt-get update && sudo apt-get install ffmpeg libsm6 libxext6 -y` <!-- https://stackoverflow.com/questions/55313610/importerror-libgl-so-1-cannot-open-shared-object-file-no-such-file-or-directo) -->
* `sudo apt-get install gmt gmt-dcw gmt-gshhg`
* `cd "Your-repository"`
* `sudo apt install python<version>-venv` # if on Debian/Ubuntu
* `python -m venv venv`
* `source venv/bin/activate`
* `pip3 install -r requirements.txt`
* `python3 -m streamlit run <app>.py`
* `sudo <path>/venv/bin/python -m streamlit run Home.py --server.port 80`
* `nohup python3 -m streamlit run <app>.py --server.port 80`
### SETUP HTTP ACCESS
#### Install nginx
*  `sudo apt-get install nginx -y`
#### Create nginx
Clear the current configuration of nginx
* `sudo sh -c 'echo -n > /etc/nginx/sites-available/default'`
Open the nginx config file
* `sudo vi /etc/nginx/sites-available/default`
Then paste the following
```c
map $http_upgrade $connection_upgrade {
    default upgrade;
    '' close;
}

upstream backend {
    server 127.0.0.1:8501;
    keepalive 64;
}

server {
    listen 80;
    server_name _;
    location / {
        proxy_pass http://backend;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
Restart your nginx server
* `sudo service nginx restart`

# …or create a new repository on the command line

* echo "# blankslate" >> README.md
* `git init`
* `git add README.md`
* `git commit -m "first commit"`
* `git branch -M main`
* `git remote add origin git@github.com:vva1kerr/blankslate.git`
* `git push -u origin main`

## …or push an existing repository from the command line

* `git remote add origin git@github.com:vva1kerr/blankslate.git`
* `git branch -M main`
* `git push -u origin main`

# CONNECT TO EC2 INSTANCE (in WSL)

* `cd ~/.ssh`
* `ssh-keygen -y -f testing_keypair_aws.pem` -> copy paste that into authorized keys
* `ssh -i "aws_urbexfun.pem" <user>@ec2-<ip>.<region>.compute.amazonaws.com`
1. Open an SSH client.
2. Locate your private key file. The key used to launch this instance is `aws-ec2-ssh.pem`
3. Run this command, if necessary, to ensure your key is not publicly viewable.
4. `chmod 400 "aws-ec2-ssh.pem"`
5. Connect to your instance using its Public DNS: `ec2-3-15-42-90.us-east-2.compute.amazonaws.com`
Example:
`-i "aws-ec2-ssh.pem" ubuntu@ec2-3-15-42-90.us-east-2.compute.amazonaws.com`


pages/ - Contains all Streamlit UI pages (your frontend)


# PYTHON ENVIRONMENT
* (open command line)
* cd ~/Desktop
* mkdir my_streamlit_app
* cd my_streamlit_app
* code .
* (open command line)
* python -m venv myenv
* pip install -r requirements.txt
* streamlit run app.py

# CONFIGURE GIT
git config --global user.email "you@example.com"
git config --global user.name "Your Name"


# PUSH CODE TO GITHUB
* git init
* git add .
* git commit -m "Initial commit"
* git branch -M main
* git remote add origin https://github.com/YOUR_GITHUB_USERNAME/YOUR_REPO_NAME.git
* git push -u origin main

# ADD SSH TO LOCAL AND GITHUB (WINDOWS)
* https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
* ssh-keygen -t ed25519 -C "your_email@example.com"
* eval "$(ssh-agent -s)"
* ssh-add ~/.ssh/id_ed25519
* cat ~/.ssh/id_ed25519.pub  # This displays the key in terminal
* type %userprofile%\.ssh\id_ed25519.pub  # Alternative Windows command
* clip < ~/.ssh/id_ed25519.pub  # This copies the key to clipboard
* ssh -T git@github.com  # Test the connection


# If you want to remove the file from Git but keep it locally
git rm --cached sensitive_file.txt
To remove the file from the Git history (very important for sensitive data), you can use git filter-branch
git push origin --force

# Streamlit secrets
* streamlit secrets write secrets.toml
* streamlit run app.py

# Streamlit config
* streamlit config show

### when to use .streamlit/secrets.toml
# API Keys
openai_api_key = "sk-..."
aws_access_key = "AKIA..."

# Database credentials
db_username = "myuser"
db_password = "mypassword"

# Other configuration
app_mode = "production"
debug = false

src/ - Contains reusable Python modules/classes (your backend logic)
scripts/ - Contains standalone utility scripts (one-off tools)

# HELPFUL WSL
* `explorer.exe .`
* 



# s3fs tutorial

* sudo apt-get update -y
* sudo apt-get install s3fs -y
* sudo apt install python3.12-venv
* cd s3fs_tutorial
* python -m venv venv
* source venv/bin/activate
* pip install boto3 python-dotenv
* .env file
```
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=us-east-1
S3_BUCKET=my-bucket-name
```
* echo "your_access_key:your_secret_key" > ~/.passwd-s3fs
* chmod 600 ~/.passwd-s3fs
* sudo nano /etc/fuse.conf
* `user_allow_other`
* mkdir ~/s3bucket
* s3fs my-bucket-name ~/s3bucket -o passwd_file=${HOME}/.passwd-s3fs -o url=https://s3.us-east-2.amazonaws.com -o endpoint=us-east-2 -o use_path_request_style -o allow_other
* s3fs my-bucket-name ~/s3bucket -o passwd_file=~/.passwd-s3fs -o url=https://s3.amazonaws.com -o use_path_request_style
* sudo /home/ubuntu/s3fs_tutorial/venv/bin/python -m streamlit run app.py --server.port 80


# file support 
#### To count the number of files inside ~/s3bucket/1x1_try2, use:
`find ~/s3bucket/1x1_try2 -type f | wc -l`
#### To output all filenames from ~/s3bucket/1x1_try2 into a file for comparison, use:
`ls ~/s3bucket/1x1_try2 > file_list_1x1_try2.txt`
#### To move a file from 1x1_try2 to ~/s3bucket, use:
`mv ~/s3bucket/1x1_try2/filename ~/s3bucket/`
#### If you need full paths, use:
`find ~/s3bucket/1x1_try2 -type f > file_list_1x1_try2.txt`
#### compare it with another folder's file list using diff
`diff file_list_1x1_try2.txt file_list_other_folder.txt`
#### To move all files from ~/s3bucket/1x1_try2/ to ~/s3bucket/, use:
`mv ~/s3bucket/1x1_try2/* ~/s3bucket/`



# add ssh from github
* cd ~/.ssh
* ssh-keygen -t rsa -C "email" 
* cat {file.pub}
* # copy the cat to the github input box
* cd ~/.ssh
* eval "$(ssh-agent -s)"
* ssh-add "name of the ssh file"
* ssh-add -l
* cd "path to your app"
* ssh -T git@github.com
* git remote set-url origin git@github.com:{username}/{repo}.git
