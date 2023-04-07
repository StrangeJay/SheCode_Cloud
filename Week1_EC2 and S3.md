# Provisioning an EC2 server and creating an s3 bucket 

## Provisioning an EC2 server with Ubuntu AMI 
- Sign into your AWS account, search for EC2 and go top the EC2 page. 

- Click on **"Launch Instance"**  
![launch instance](https://user-images.githubusercontent.com/105195327/230625922-e735e3be-3fb9-465a-88c8-3a84140d9dfe.png)   

- You'll be taking to a setup page. Choose the name of your instance, and select the operating system you would like to use for the EC2 server. I chose an Ubuntu AMI with free tier enabled so i don't get charged as long as i keep the use of the server under 750hours.   
![Name and Tag](https://user-images.githubusercontent.com/105195327/230625947-db0acc8d-853a-4c53-a7ee-1dcb1de9faa4.png)   


- Create a keypair for your EC2 server if you plan to ssh into it. You can use the .pem for open ssh from your devices terminal, or the .ppk for putty.   
![key pair](https://user-images.githubusercontent.com/105195327/230625963-b1b5f181-8a2b-4afe-921c-79989d213498.png)   


- I left the default VPC and Subnet, but i created a security group that allows ssh traffic from anywhere. My EC2 server is not accessible through the internet, because i didn't allow http and https access to it.   
![network setting](https://user-images.githubusercontent.com/105195327/230625980-30237218-f1ad-4919-8d32-e9917b754229.png)   


- I reviewed my settings in the summary page and i launched the instance.   
![launch instance finally](https://user-images.githubusercontent.com/105195327/230625992-f21cf481-f506-4a4c-8e03-48c0e99a78a9.png)   


---
### SSH Into the EC2 Instance
- I waited for my EC2 instance to be created and show the 2/2 status check. Then i clicked into the instance.   
![click into the instance](https://user-images.githubusercontent.com/105195327/230626046-723c8e44-31b6-4bb0-9626-de725412dfa4.png)  


- I clicked on connect to take me to the **"connect to instance"** page.   
![connect](https://user-images.githubusercontent.com/105195327/230626066-17402859-2cae-4663-80b3-9851077b113b.png)   


- I copied the ssh client connection command.  
![ssh client log in](https://user-images.githubusercontent.com/105195327/230626081-9cc81256-50ab-4be0-a0d0-0c1493b705ae.png)   


- I went to "downloads" on my file manager, and i opened the folder in my terminal.   
![open in terminal](https://user-images.githubusercontent.com/105195327/230626097-a7168a97-003f-4b87-9bab-ca73857139a0.png)   


- I pasted the copied ssh client connection command into the terminal, clicked **yes** to accept connection.   
![connect terminal](https://user-images.githubusercontent.com/105195327/230626104-936263ee-6ad3-461f-af54-583078e01fba.png)   


- VOILA!!! I have been connected to my ubuntu server. I tested it out by running a few commands to create a directory and a file and move the file into the directory. 
![ssh'd in](https://user-images.githubusercontent.com/105195327/230626117-4c1a9fe5-879e-48ed-849a-bcdda334ea51.png)   
