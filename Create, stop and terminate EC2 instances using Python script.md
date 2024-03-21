Creating an EC2 instance using Python script with IAM credentials involves using the Boto3 library, the AWS SDK for Python. Below is a step-by-step guide along with explanations:

Step 1: Install Boto3

Ensure you have Boto3 installed. If not, you can install it via pip:
```
pip install boto3
```

Step 2: Configure IAM Credentials

Create IAM credentials with appropriate permissions to create EC2 instances. You'll need an Access Key ID and a Secret Access Key. Make sure to keep these credentials secure.

Step 3: Write Python Script

Create a Python script (e.g., create_ec2.py) with the following code:
```
import boto3
```
```
# Specify the region to use
region = 'us-east-1'

# Create an EC2 client
ec2 = boto3.client('ec2', region_name=region)

# Specify the parameters for the instance
instance_params = {
    'ImageId': 'ami-0c7217cdde317cfec',  # Specify the AMI ID of the instance
    'InstanceType': 't2.micro',  # Specify the instance type
    'SecurityGroupIds': ['sg-05fa0909b9c63ef98'],  # Specify the security group IDs
    'SubnetId': 'subnet-024801561c110b242',  # Specify the subnet ID
    'MaxCount': 1, # Specify the number of instances to launch
    'MinCount': 1
}
# Provision the instances
response = ec2.run_instances(**instance_params)
instance_id = response['Instances'][0]['InstanceId']

# Wait for the instance to be running
ec2.get_waiter('instance_running').wait(InstanceIds=[instance_id])
print(f'Instance {instance_id} is launching...')
print(f"Instance {instance_id} is now running.")
```

Step 4: Script Explanation

import boto3

This line imports the boto3 library, which is the AWS SDK for Python. It allows you to interact with various AWS services, including EC2.

Specify the region to use     :  region = 'us-east-1 '
This line defines the AWS region where you want to perform your operations. Replace 'us-east-1' with the desired region.

Create an EC2 client : ec2 = boto3.client('ec2', region_name=region)

This line creates an EC2 client using Boto3. The boto3.client() function initializes a client for the specified service, in this case, 'ec2'. The region_name parameter specifies the AWS region for the client.

Specify the parameters for the instance
This section defines the parameters required to launch an EC2 instance:

'ImageId': Specifies the Amazon Machine Image (AMI) ID for instance.

'InstanceType': Specifies the instance type, such as 't2.micro'.

'SecurityGroupIds': Specifies the security group IDs associated with the instance. It controls inbound and outbound traffic.

'SubnetId': Specifies the subnet ID in which to launch the instance.

'MaxCount': Specifies the maximum number of instances to launch. Here, it's set to 1.

'MinCount': Specifies the minimum number of instances to launch. Here, it's also set to 1.

Provision the instances

response = ec2.run_instances(**instance_params)
This line launches the EC2 instance(s) with the specified parameters using the run_instances() method of the EC2 client. It returns a response object containing information about the launched instances.

Wait for the instance to be running

instance_id = response['Instances'][0]['InstanceId']
ec2.get_waiter('instance_running').wait(InstanceIds=[instance_id])

This section waits for the instance to reach the running state. The get_waiter() method retrieves a waiter object, and wait() method blocks until the specified waiter condition is met. Here, it waits until the instance with the specified ID is running.

Print status
print(f'Instance {instance_id} is launching...')
print(f"Instance {instance_id} is now running.")

These lines print messages indicating the launch status of the instance. It prints the instance ID and confirms when the instance is running.

Step 5: Run the Script

Execute the Python script:
python create_ec2.py

Step 6: Verify
Go to the AWS Management Console or use the AWS CLI to verify that the instance has been created successfully.


2.Stopping an EC2 instance using Python script
```
instance_id = ‘instance_id’
# Stop running instance
ec2.stop_instances(InstanceIds=[instance_id])
print("Instance stopped")
```

3.Terminate an EC2 instance using Python script
```
instance_id = ‘instance_id’
# terminate instance
ec2.terminate_instances(InstanceIds=[instance_id])
print("Instance terminated")
```

