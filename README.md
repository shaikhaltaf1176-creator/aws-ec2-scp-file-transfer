Task 1: Launch an EC2 Instance and Transfer a File with SCP

A hands-on exercise in launching an AWS EC2 instance, connecting to it over SSH, and copying a file from a local Windows machine to the server using scp.

Overview
Item	Details
Cloud provider	AWS
Service	EC2
Region	us-east-1 (N. Virginia)
Instance name	my-server
Instance type	t3.micro
OS user	ubuntu
Local machine	Windows (Command Prompt)
Transfer tool	scp
Prerequisites
An AWS account
A key pair (.pem file) created for the instance
An SSH client (Git Bash, OpenSSH, etc.)
OpenSSH scp available in Windows Command Prompt
Steps
1. Launch the EC2 instance

Launched a t3.micro instance named my-server in us-east-1. The instance reached the Running state (status checks were still initializing in the screenshot) and was assigned a public IPv4 address.

EC2 instance running

2. Connect via SSH and check existing files

Connected to the instance as ubuntu and ran ls. Only altaf.txt existed at this point.

bash
ls

Output:

altaf.txt

Initial ls output

3. Copy a file from local machine to EC2 using SCP

From Windows Command Prompt, copied Vcube.txt to the server's home directory:

bat
scp -i "C:\Users\altaf\Desktop\<your-key>.pem" C:\Users\altaf\Desktop\Vcube.txt ubuntu@<EC2_PUBLIC_IP>:/home/ubuntu/

The transfer completed at 100%.

SCP transfer

4. Verify the file on the server

Back in the SSH session, ran ls again. Vcube.txt now appears next to altaf.txt.

bash
ls

Output:

Vcube.txt  altaf.txt

Final ls output

Result

The file was transferred from the local Windows machine to the EC2 instance and confirmed on the server.

Key Commands
Command	Purpose
ls	List files in the current directory
scp -i <key.pem> <local-file> <user>@<ip>:<remote-path>	Copy a local file to a remote server over SSH
Notes
Replace <your-key> and <EC2_PUBLIC_IP> with your own values.
The public IP changes each time the instance is stopped and started, unless you attach an Elastic IP.
Never commit your .pem private key to Git.
Stop or terminate the instance when finished to avoid charges.
Author

Altaf
