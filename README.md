
ETL API data to AWS S3 bucket  using Apache Airflow DAG with python 


***************************************************************************
create an ec2 instance in aws console  to store the csv file created when pipeline is created
use the processor as ubuntu
select t2.small/t2.micro prcoessor sub category 
create key pair for the ec2 instance for console login purposes
select pem file to store the key information in downloads folder
Download the pem file to get  key pair
.pem file is stored in downloads folder
 take the security group of the ec2 instance created and keep it as it is
launch instance and create the ec2 object
**************************************************************************
to give permission to the access through browser

check newly created  ec2 instance  in the aws console aand wait till it becomes ready
go to security options of the instance
edit security group inbound rule for the instance
add new inbound rule to login through 8080 port
custom tcp 8080 my ip (select)
save rule
*****************************************************************************
check again if the ec2 instance is running
connect to ubuntu from ec2 connect 

To install dependencies for the web deployment 
*****************************************************************************
take public ip of ec2 nstance created and copy to clipboard
go to the ubuntu terminal

sudo apt update (to update os)
sudo apt install python-pip (to install python pip)
sudo apt install python3.10-venv (install dependency to create virtual environment in python )
create virtual env (command to create virtual environment through terminal)
python3 -m venv airflow_venv
to activate newly created virtual environment
source airflow_venv/bin/activate
***************************************************************************
install required libraries

sudo pip install pandas (for dataframes)
sudo pip install s3fs  (to create s3 bucket)
sudo pip install apache-airflow (to create DAG)
airflow standalone (initailise airflow from terminal)
note username and password of airflow while initialising apache airflow
airflow for development not production environment
copy public ip DNS from ec2 instance created to login through browser 
paste in new browser window with port number 8080 (eg https://xya.com/8080) port 8080 is created in security group of ec2 instance
copy username and password from command line and paste in browser to get DAG in apache
*********************************************************************************
open a new visual studio project and open folder 

take the config file

config
	Host apiairflow
	Hostname 54.242.139.70
	User ubuntu
	Identityfile C:\Users\HP\Downloads\weatherapiairflow.pem

connect to apache airflow at vs code window before proceed further
create new folder DAG under airflow project
***************************************************************************************
create new file under weather_dag.py

ETL pipeline to extract transform and load data
--take the data from a website do the required transofrmation using python code and load the result into the s3 bucket as csv file for loading

How to run DAG 

create new connection from airflow
connection name - weathermap_api
connection type - http
host - https://api.openweathermap.org


Take config file
give the path of dag folder
dags_folder=/home/ubuntu/airflow/dags
 *************************************
now api is ready and is shown in dags
how to run api
************************************************************************************
Create s3 bucket in aws to store csv fileto give access to ec2 instance
to give permission to some users to access s3 bucket contents with required permissions
take ec2 insance -> IAM role->create new IAM role and assign s3 bucket full access priviloeges and 
EC2 full access privileges to the IAM role created and assign those security to EC2 instance in security section as role

update IAM role with new permissions given
change csv file path to s3 bucket name  in python file
create a new secret key for the ec2 intsance

open  terminal
activate venv using following code
source airflow_venv/bin/activate 
install aws client for aws  features
sudo apt install awscli
aws configure 
for the new configuration changes 
aws sts get-session-token
copy secrets keys and token to the weather_dag.py code file to give permission to interact with S3 bucket with specific permissions

*********************************************************
*********************************************************

