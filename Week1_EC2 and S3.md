# Provisioning an EC2 server and creating an s3 bucket 

## Provisioning an EC2 server with Ubuntu AMI 
- Sign into your AWS account, search for EC2 and go top the EC2 page. 

- Click on **"Launch Instance"**  
![launch instance](https://user-images.githubusercontent.com/105195327/230625922-e735e3be-3fb9-465a-88c8-3a84140d9dfe.png)   

- You'll be taking to a setup page. Choose the name of your instance, and select the operating system you would like to use for the EC2 server. I chose an Ubuntu AMI with free tier enabled so i don't get charged as long as i keep the use of the server under 750hours.   
![Name and Tag](https://user-images.githubusercontent.com/105195327/230625947-db0acc8d-853a-4c53-a7ee-1dcb1de9faa4.png)   


- Create a keypair for your EC2 server if you plan to ssh into it. You can use the .pem for open ssh from your devices terminal, or the .ppk for putty.   
![key pair](https://user-images.githubusercontent.com/105195327/230625963-b1b5f181-8a2b-4afe-921c-79989d213498.png)   


- I left the default VPC and Subnet, but i created a security group that allows ssh traffic from anywhere. My EC2 server is not accessible through the internet, because i didn't allow http and https access to it. Your settings would depend on its intended use.  
![network setting](https://user-images.githubusercontent.com/105195327/230625980-30237218-f1ad-4919-8d32-e9917b754229.png)   


- Review your settings in the summary page and launch the instance.   
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

---

## Provisioning an s3 bucket
### Create the s3 bucket
- Search for s3 in your management console.  
![create bucket](https://user-images.githubusercontent.com/105195327/230633758-f346dbd8-70e7-4a61-84c4-fa82395a1365.png)  


- Choose a bucket name that is globally unique, meaning it is not presently being used by anyone else.  
![bucket name](https://user-images.githubusercontent.com/105195327/230634005-318c74b1-9f6a-43c2-a002-9beee161d429.png)   


- I left the object ownership field on the default setting. You can do something different depending on your usage.    
![befor access pic](https://user-images.githubusercontent.com/105195327/230634651-dbf206dd-d3c3-4dfd-9736-c07f3c105acf.png)  


- For the block public access settting, it's usually a good idea to block public access to your s3 bucket for security reasons, but i plan on using this s3 bucket to host a static website so i'll uncheck this field and enable mine.  
![block public access](https://user-images.githubusercontent.com/105195327/230634310-bf094a71-fb91-486d-8d0c-92d0996f965b.png)  


- I left bucket versioning and other settings on default too.  
![other settings on default](https://user-images.githubusercontent.com/105195327/230634799-27b6a4d2-5724-4492-ad1c-483cc101d210.png)   


- Click on the **"create bucket"** sign and create your bucket.  
  ![create bucket finally](https://user-images.githubusercontent.com/105195327/230635091-565917d6-d9d8-4820-ad5e-b2fb47ea373e.png)   
  
### Setup the s3 bucket for Static Website Hosting
- Click into the s3 bucket  
![enter ze bucket](https://user-images.githubusercontent.com/105195327/230635313-36043c99-aab4-4785-854d-4462c802fc82.png)   


- Click on the properties tab   
![click properties](https://user-images.githubusercontent.com/105195327/230635380-1d2339bb-df3e-4934-8d0f-d792eba70713.png)  


- Scroll down and click on enable static website hosting.   
![enable static web hosting](https://user-images.githubusercontent.com/105195327/230635466-b5d5826c-a1e4-4eb7-89df-6f56823257e2.png)


- Enable your s3 bucket to host a static website, set the name of the index file that the endpopint would serve as the home page.   
![static web enabling](https://user-images.githubusercontent.com/105195327/230635646-a4881c7b-0529-498a-b178-3873916f8c45.png)   


- Go to the permissions tab.   
![click permisions](https://user-images.githubusercontent.com/105195327/230635699-74019561-3f05-4a21-8ec0-cd8a9e980cba.png)   


- Scroll down to the bucket policy field and edit it.   
![bucket policy](https://user-images.githubusercontent.com/105195327/230635785-2f05f965-2899-4b50-967e-e877536bdc6e.png)   


- Type the code below in the bucket policy field, to grant read access to the public. This enables them view the website through the internet.   
```
{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Sid":"AddPerm",
      "Effect":"Allow",
      "Principal": "*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::DOC-EXAMPLE-BUCKET/publicprefix/*"]
      }
  ]
}
```   
after typing, save your policy.   

![added policy](https://user-images.githubusercontent.com/105195327/230636102-cde4bbe9-35d6-42f9-aafc-0d96cb693214.png)   


- Go to the **objects** tab and upload the html templates.   
![upload template files](https://user-images.githubusercontent.com/105195327/230636271-8e5110d0-1391-4222-9dff-ededc624f0c0.png)   


- Upload the necessary files and folders needed to get your website up and running.  
![upload files and folders](https://user-images.githubusercontent.com/105195327/230636350-d9569873-c185-4d2e-bd13-091f19f145c4.png)   


- Go to the **"properties tab"** and scroll down to copy your website endpoint, this is the link you would use to access your static website.  
![website endpoint in properties](https://user-images.githubusercontent.com/105195327/230636574-62867d1a-299c-4cfc-b358-22e1d78c27cf.png)   


- Voila!!! Your static website is up and running. If you have a domain name you can set it up to use that instead of the AWS given endpoint.   
![functioning website](https://user-images.githubusercontent.com/105195327/230636740-eb546373-3806-486f-9139-80bac1bd1e0a.png)   

