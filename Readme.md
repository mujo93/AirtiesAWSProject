# VPC Creation

### 1- Create a VPC
<img width="1005" alt="Screenshot 2022-11-30 at 12 43 32 am" src="https://user-images.githubusercontent.com/34121683/204657665-c3608e97-d520-4cd4-a07e-34b1fa4577ba.png">

### 2- The above VPC has 2 subnets which are private and public
<img width="1005" alt="Screenshot 2022-11-30 at 12 43 32 am" src="https://user-images.githubusercontent.com/34121683/204658236-212d6311-1b54-4d20-8f4e-d416997bfb5b.png">

### 3- Create EC2 instances with a security group which specifies the port 22 for ssh and port 80 for http requests coming from public
![Screenshot 2022-11-30 at 1 08 21 am](https://user-images.githubusercontent.com/34121683/204659071-594d5250-ba4d-4268-b39b-3c13931b929e.png)
<img width="1213" alt="Screenshot 2022-11-30 at 1 10 47 am" src="https://user-images.githubusercontent.com/34121683/204659465-a165a84c-10d4-45f0-97ee-79af07bd72e5.png">
<img width="1171" alt="Screenshot 2022-11-30 at 1 11 52 am" src="https://user-images.githubusercontent.com/34121683/204659667-aaf7c1e0-0fd9-478d-aea9-a8193bd95c50.png">

### 4- SSH into the created instances with a created key pair. Now we get into the running instance. We are ready for installing a web server.
`ssh -i "amazonlinux-key.pem" ec2-user@ec2-107-22-134-209.compute-1.amazonaws.com ` <img width="994" alt="Screenshot 2022-11-29 at 11 50 30 pm" src="https://user-images.githubusercontent.com/34121683/204660288-ea505046-d256-422d-aa51-ce842660c58f.png">

### 5- Setup the server by installing apache server. 
- Run the command `sudo yum install -y httpd.x86_64` to install the web server in the instance.
<img width="1092" alt="Screenshot 2022-11-29 at 11 49 51 pm" src="https://user-images.githubusercontent.com/34121683/204660912-946c7b30-bc32-4b67-8890-854a6425a238.png">

- Run the command `systemctl start httpd.service` to start the web server.
- Run the command `systemctl enable httpd.service` to start the server automatically. 
- Now we should be able to see our web server running once we enter the public IP provided us by the instance. 
<img width="1447" alt="Screenshot 2022-11-30 at 1 26 54 am" src="https://user-images.githubusercontent.com/34121683/204662110-5a771d20-06bd-4c19-b329-3d7fb76170bc.png">

![Screenshot 2022-11-30 at 1 27 59 am](https://user-images.githubusercontent.com/34121683/204668059-d74d7c26-d843-44bb-8be4-1753ceaa19b0.png)


### 6- Create a bucket 
<img width="1176" alt="Screenshot 2022-11-30 at 1 30 37 am" src="https://user-images.githubusercontent.com/34121683/204662619-7b1e07a4-4752-4054-8287-fb44c57e32b6.png">

### 7- Access bucket from the instance

- We need to create a role with a S3 policy and assign it to the instance to access the S3 bucket that we created.
- We first create a policy called `s3-full-access` which grants all permissions to manipulate s3 bucket

<img width="1161" alt="Screenshot 2022-11-30 at 1 34 46 am" src="https://user-images.githubusercontent.com/34121683/204664098-354d16b9-566d-4cca-98c0-41e24a315795.png">

- We create `myS3role` role and add the policy to the role.

<img width="1173" alt="Screenshot 2022-11-30 at 1 43 09 am" src="https://user-images.githubusercontent.com/34121683/204664586-6566ee59-e665-405e-96a5-4b6e341aeeed.png">

- Now we attach the role to our instance.

![Screenshot 2022-11-30 at 1 44 49 am](https://user-images.githubusercontent.com/34121683/204665583-02049938-a6f6-4db1-9c5a-14861a2a0b2d.png)


- After all we are ready to upload a file which was created in our running instance to the bucket. 
- First we create a demo.txt file in our instance

<img width="520" alt="Screenshot 2022-11-30 at 1 47 19 am" src="https://user-images.githubusercontent.com/34121683/204665148-88966f3d-190f-428c-8259-8abb9f891cb4.png">

- `aws s3 cp demo.txt to s3://first-instance-bucket` run this command upload `demo.txt` to the s3 bucket.

<img width="581" alt="Screenshot 2022-11-30 at 1 53 14 am" src="https://user-images.githubusercontent.com/34121683/204666074-7703a382-d99c-4459-bb9c-8a42270bf9ce.png">

- demo.txt file created in our instance now been uploaded to first-instance-bucket.

<img width="1173" alt="Screenshot 2022-11-30 at 1 54 45 am" src="https://user-images.githubusercontent.com/34121683/204666607-e3c240ec-c20a-42fa-be89-8e9547c5b3bb.png">
