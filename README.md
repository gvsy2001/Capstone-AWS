# Capstone-AWS

## Capstone Project


### Summary of the tasks:
- Step 0:  Inspect the archtecture
- Step 1: Create a Cloud9 IDE 
- Step 2: Get the Project Assets 
- Step 3: Install a LAMP web server on CLoud9 IDE
- Step 4: Create a MySQL RDS database instance 
- Step 5: Create an Application Load Balancer 
- Step 6: Importing the data into the RDS database 
- Step 7: Configure the system parameters in Parameter Store Systems Manager 


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Step 0:  Inspect the archtecture 
- Inspect the example VPC. 
- Inspect the subnets. 
- Inspect the Security Groups.
- Inspect the AMI.  


# Step 1: Create a Cloud9 IDE




# Step 2: Get the Project Assets 
1. Clone the repository:
```sh
   git clone https://github.com/baselm/capstoneproject.git
   ```
2. Extract the files to the Apache www folder:
```sh
   unzip Example.zip -d /var/www/html/
   ```
   
# Step 3: Install a LAMP web server on Amazon Linux 2

### LAMP (Linux, Apache HTTP server, MySQL database, and PHP) stack

```sh
sudo yum -y update
sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2

sudo yum install -y httpd mariadb-server
sudo systemctl start httpd

sudo systemctl enable httpd
sudo systemctl is-enabled httpd
```




- Open port 80 from the security group of the Cloud9 EC2 instance
- Get the cloud9 EC2 public instance IP address and test that you can access the website 

# Step 4: Create a MySQL RDS database instance 

with the following specifications.

 -  Create a db subnet group 
 -  Databasetype: MySQL
 -  Template: Dev/Test
 -  DBinstanceidentifier: Example
 -  DB instance size: db.t3.micro
 -  Storage type: General Purpose (SSD)
 -  Allocatedstorage: 20GiB
 -  Storageautoscaling: Enabled
 -  Standbyinstance: Enabled
 -  Virtualprivatecloud: ExampleVPC
 -  Databaseauthenticationmethod: Passwordauthentication 
 -  Initialdatabasename: exampledb
 -  Enhancedmonitoring: Disabled

# Step 5: Create an Application Load Balancer
- Create target group 
- Create an auto scaling group 
- Lunch Web Instances in the private subnet

# Step 6: Importing the data into the RDS database

 Importing the data into the RDS database instance from CLoud9 or by accessing the web instance via bastion host
 
 1. get the SQLDump file:
 
 2. connect to the RDS database, run this command:
```sh
mysql -u admin -p --host <rds-endpoint>
 ```
 
 3. Test that you can access the RDS DB 
 ```sh
 use exampledb;	
 show tables; 

 ```
 4. Import the data into the RDS database.
 ```sh
 
 mysql -u admin -p exampledb --host <rds-endpoint>  < Countrydatadump.sql       
 ```
# Test the ALB 

- Test data was imported 
```sh
 use exampledb;	
 show tables; 
 select *from countrydata_final; 
 ```

# Step 7: Configure the system parameters in Parameter Store Systems Manager

Add the following parameters to the Parameter Store and set the correct values:

1. /example/endpoint 
2. /example/username   
3. /example/password  
4. /example/database exampledb

