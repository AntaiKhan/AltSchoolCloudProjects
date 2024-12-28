# AltSchool Second Semester Project Submission

## URL: webantai.tech
## Public IP: 34.213.62.106
## Screenshot of URL 

<img width="1059" alt="image" src="https://github.com/user-attachments/assets/c937009c-9efc-4443-92a6-1a3555f5f024" />


## STEP 0 - PREPPING AWS
We need to set up an EC2 instance. You do that by using the search bar to search for EC2 and clicking on **Launch Instance**. Then follow the steps below:

- Select a free tier Ubuntu image as the AMI (Amazon Machine Image).
- Select the Instance type next, I used free tier eligible t2.micro.
- Create security key pair for secure connection to your instance (ensure to pick your .pem file very safe).
- Ensure you create a security group to allow SSH connection to your instance using your .pem file.
- You can use default settings to configure instance details.
- Launch Instance.

Ensure your status check shows "2/2 checks passed" as seen in the screenshot below:
<img width="1194" alt="image" src="https://github.com/user-attachments/assets/087d6b43-a5ac-4716-8f8b-307f6d646fb7" />

Connect to AWS EC2 Instance using code below (for SSH Client):

`chmod 400 "second-sem-project.pem"` (for MacOS Users only)

`ssh -i "second-sem-project.pem" ubuntu@ec2-34-213-62-106.us-west-2.compute.amazonaws.com`

## STEP 1  - UPDATE PACKAGE AND INSTALL NGINX

Run the command below to update the list of packages in package manager.

`sudo apt update`

<img width="566" alt="image" src="https://github.com/user-attachments/assets/74bbd83e-c158-43d9-a750-961e64f82f65" />

Run the command below to install nginx (option `-y` is to automatically say yes to the permission requested during installation)

`sudo apt install nginx -y`

<img width="566" alt="image" src="https://github.com/user-attachments/assets/a0a5da18-64ef-4298-b04f-526a59eab738" />

After installing the nginx service, you use the command below to start the nginx service.

`sudo systemctl start nginx`

The enable command below is to add nginx as part of the system services and ensure that whenever you restart your instance, the nginx service is restarted along side.

`sudo systemctl enable nginx`

<img width="567" alt="image" src="https://github.com/user-attachments/assets/71fd294b-ee2a-4fa5-983c-c7650546f421" />

Check the status of your nginx status to ensure it is active with below

`sudo systemctl status nginx`

<img width="569" alt="image" src="https://github.com/user-attachments/assets/065fff40-9c16-43a3-9f01-ac59b7d405ce" />

## STEP 3 - CREATE YOUR HTML FILE

First, we will navigate to the var directory which is the root path for your HTML files.

`cd /var/www/html`

Then create and write to your html file using vim with command below.

`sudo vim index.html`

You press "I" on your keyboard to change into insert mode and insert your code.

Press the esc key to leave insert mode and :wq to write/save and quit.

Now that your index.html file is created, you can view this via the public IP as seen in the screenshot below.
(Ensure you set up your Security Group to allow traffic on port 80 so the website can be accessed on the internet via the public IP.)

<img width="1059" alt="image" src="https://github.com/user-attachments/assets/c937009c-9efc-4443-92a6-1a3555f5f024" />


## STEP 4 - CONFIGURING SSL USING LET'S ENCRYPT

First,we install certbot using the script below:

`installed certbot`

Then, we obtain and deploy the certificate to our server using:

`sudo certbot --nginx`

Note: A prompt would come up requesting the domain name of your website to deploy the certificate to.

<img width="565" alt="image" src="https://github.com/user-attachments/assets/b5e7f192-c1c5-48f6-9366-d875458bfe4e" />

After deploying certificate is successfully deployed, go to your security group and update your inbound rule to allow access from port 443 (HTTPS).

Your site should come up successfully after that as seen below.

<img width="1048" alt="image" src="https://github.com/user-attachments/assets/fd3ed5d1-8777-4002-8dae-6acaaa1d338f" />

