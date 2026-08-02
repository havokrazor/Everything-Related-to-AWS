# Deploying a Node Js Application on AWS EC2

Today we will be deploying a simple "Hello World" application on the remote instance and exposing it to the world. To follow up on this you can also Fork this repo,

`https://github.com/havokrazor/Everything-Related-to-AWS.git`


### Let's Start with creating and setting up the EC2 Instances

1.Create an IAM user & login to your AWS Console

   -Access Type - Password
   
   -Permissions - Admin
   
2.Create an EC2 instance

   -Select an OS image - Ubuntu
   
   -Create a new key pair & download .pem file
   
   -Instance type - t2.micro
   
3.Connecting to the instance using ssh

```
ssh -i keyname.pem ubuntu@public-ip-address
