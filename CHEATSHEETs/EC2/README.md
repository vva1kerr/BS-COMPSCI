
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


