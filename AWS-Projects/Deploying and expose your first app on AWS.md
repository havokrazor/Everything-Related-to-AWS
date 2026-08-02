# Deploying a Node Js Application on AWS EC2

Today we will be deploying a simple "Hello World" application on the remote instance and exposing it to the world. To follow up on this you can also Fork this repo,

`https://github.com/havokrazor/Everything-Related-to-AWS.git`


### Let's Start with creating and setting up the EC2 Instances

1.Create an IAM user & login to your AWS Console

   -Access Type - Password
   
   -Permissions - Admin

Note - Creating and Managing the access via the IAM profile is the best practice 
   
2.Create an EC2 instance

   -Select an OS image - Ubuntu
   
   -Create a new key pair & download .pem file
   
   -Instance type - t2.micro
   
3.Connecting to the instance using ssh

```
ssh -i keyname.pem ubuntu@public-ip-address
```

### Configure Ubuntu before we deploy the App

1.Updating Outdated packages and dependencies

```
sudo apt update
```

2. Install Git if not installed already

```
sudo apt install git -y

git --version
```

3. Install Node.js and npm (modules needed for the node.js application)

```
sudo apt install nodejs

node -v
```
Installing npm

```
sudo apt install npm
```

### Deploying the project on AWS

1. Create a new directory and file for the project

```
mkdir my-node-app
cd my-node-app
```

2. Create the app code

```
nano app.js
```

and paste the following in that file

```
const http = require('http');
const PORT = process.env.PORT || 3000;

const server = http.createServer((req, res) => {
    // Route: Main landing page
    if (req.url === '/' && req.method === 'GET') {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World! Your native Node.js app is running on AWS Ubuntu.');
    } 
    // Route: Health check endpoint
    else if (req.url === '/health' && req.method === 'GET') {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('OK');
    } 
    // Route: Not Found fallback
    else {
        res.writeHead(404, { 'Content-Type': 'text/plain' });
        res.end('Not Found');
    }
});

server.listen(PORT, () => {
    console.log(`Application is live on port ${PORT}`);
});
```

3. And then Run the app using the Node Runtime

```
node app.js

```

**WARNING -  keep in mind that as soon as you close your SSH terminal window or disconnect from AWS, the node app.js process will automatically shut down.
This is not production ready code**

**NOTE - We will have to edit the inbound rules in the security group of our EC2, in order to allow traffic from our particular port**

**YOUR FIRST PROJECT IS DEPLOYED ON AWS**
