# Manage_ec2_using_python
## Python-  This python code is written to stop/start the AWS ec2 instance from terminal. This code will list the available instances first and ask you for the instance ID and state like start or stop.

```python
import boto3
import sys

def list_all_ec2():
    aws_ec2=boto3.resource("ec2",region_name="us-east-2")
    for instance in aws_ec2.instances.all():
         print(
             "Id: {0}\nPlatform: {1}\nType: {2}\nPublic IPv4: {3}\nAMI: {4}\nState: {5}\n".format(
             instance.id, instance.platform, instance.instance_type, instance.public_ip_address, instance.image.id, instance.state
             )
         )

def startInstance():
    print("Starting the instance...")

    try:
        response = ec2.start_instances(InstanceIds=[ec2_id], DryRun=False)
        print(response)
    except:
        print("Instance start failed")
        sys.exit(0)

def stopInstance():
    print("Stopping the instance...")

    try:
        response = ec2.stop_instances(InstanceIds=[ec2_id], DryRun=False)
        print(response)
    except:
        print("Instance stop failed")
        sys.exit(0)

        
list_all_ec2()

ec2=boto3.client("ec2",region_name="us-east-2")
action = input('Please enter stop/start:::')
ec2_id = input('Please provide the instance id:::')


if action == "start":
    startInstance()
elif action == "stop":
    stopInstance()
else:
    print("Incorrect usage")
```

### The output of the code will looks like as follows

```
ubuntu@ip-172-31-22-203:~$ python3 ec2_action.py
Id: i-0a70d15b4******
Platform: None
Type: t2.micro
Public IPv4: None
AMI: ami-0d8f6eb4f641ef691
State: {'Code': 80, 'Name': 'stopped'}

Id: i-0eb4a34fee0******
Platform: None
Type: t2.micro
Public IPv4: 18.188.189.194
AMI: ami-05c1fa8df71875112
State: {'Code': 16, 'Name': 'running'}

Id: i-0b059ebc35c******
Platform: None
Type: t2.micro
Public IPv4: 3.16.150.173
AMI: ami-00c03f7f7f2ec15c3
State: {'Code': 16, 'Name': 'running'}

Id: i-0124fcbad4******
Platform: None
Type: t2.micro
Public IPv4: None
AMI: ami-0d8f6eb4f641ef691
State: {'Code': 80, 'Name': 'stopped'}

Please enter stop/start:::stop
Please provide the instance id:::i-0b059ebc35c******
Stopping the instance...
{'StoppingInstances': [{'CurrentState': {'Code': 64, 'Name': 'stopping'}, 
'InstanceId': 'i-0b059ebc35c03a3c4', 
'PreviousState': {'Code': 16, 'Name': 'running'}}], 
'ResponseMetadata': {'RequestId': 'f24ade82-79e8-4825-9326-355ab4ddb6ad', 'HTTPStatusCode': 200, 
'HTTPHeaders': {'content-type': 'text/xml;charset=UTF-8', 
'content-length': '579', 'date': 'Sun, 08 Sep 2019 07:46:25 GMT', 
'server': 'AmazonEC2'}, 'RetryAttempts': 0}}
```
