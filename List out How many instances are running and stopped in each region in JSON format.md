```

import boto3
import json

# Initialize EC2 client
ec2 = boto3.client('ec2')

# Get list of regions
regions = [region['RegionName'] for region in ec2.describe_regions()['Regions']]
print(regions)

# Initialize dictionary to store instance details
instances_by_region = {}

# Iterate over each region
for region in regions:
    # Initialize EC2 resource for the region
    ec2_resource = boto3.resource('ec2', region_name=region)
    
    # Get running instances
    running_instances = list(ec2_resource.instances.filter(Filters=[{'Name': 'instance-state-name', 'Values': ['running']}]))
    running_count = len(running_instances)
    running_instances_details = [{'InstanceId': instance.id, 'State': instance.state['Name']} for instance in running_instances]
    
    # Get stopped instances
    stopped_instances = list(ec2_resource.instances.filter(Filters=[{'Name': 'instance-state-name', 'Values': ['stopped']}]))
    stopped_count = len(stopped_instances)
    stopped_instances_details = [{'InstanceId': instance.id, 'State': instance.state['Name']} for instance in stopped_instances]

    # Add counts to dictionary
    instances_by_region[region] = {'running_count': running_count, 'running_instances': running_instances_details, 'stopped_count': stopped_count, 'stopped_instances': stopped_instances_details}

# Convert dictionary to JSON
json_output = json.dumps(instances_by_region, indent=4)

# Print JSON output
print(json_output)

```

Explanation

1.Initializing Boto3 Client:

The script initializes the Boto3 client for EC2.

2.Retrieving Regions:

It retrieves a list of EC2 regions using the describe_regions() method.

3.Printing Regions:

It prints the list of EC2 regions.

4.Iterating Over Each Region:

It iterates over each EC2 region to gather instance details.

5.Initializing EC2 Resource for the Region:

It initializes an EC2 resource for the current region.

6.Getting Running Instances:

It retrieves running instances using the instances.filter() method with a filter for instances in the 'running' state.

7.Getting Stopped Instances:

It retrieves stopped instances using the instances.filter() method with a filter for instances in the 'stopped' state.

8.Storing Instance Details:

It stores instance counts and details (IDs and states) in a dictionary for each region.

9.Converting to JSON:

It converts the dictionary containing instance details into JSON format using the json.dumps() method.

10.Printing JSON Output:

It prints the JSON output containing instance details by region.
