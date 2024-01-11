## How To Implement the ECS using Cloudformation

### Prerequisites:
1. **AWS Account:**
   - Ensure you have an active AWS account with appropriate permissions to create resources.

2. **AWS CLI Installation:**
   - Install AWS CLI on your local machine. Follow the instructions at [AWS CLI Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html).

### Configuration:

1. **Clone Repository:**
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **AWS Credentials:**
   - Ensure your AWS credentials are configured on your machine.

### CloudFormation Setup:

3. **Create ECS Cluster Stack:**
   - Use the provided `ecs-cluster.yaml` CloudFormation template to create the ECS cluster stack.

   ```bash
   aws cloudformation create-stack \
     --stack-name ecs-cluster-stack \
     --template-body file://ecs-cluster.yaml \
     --capabilities CAPABILITY_IAM \
     --parameters file://ecs-cluster-parameters.json
   ```

### ECS Cluster Configuration:

4. **Define ECS Cluster Parameters:**
   - Edit the `ecs-cluster-parameters.json` file to customize ECS cluster parameters such as cluster name, instance type, and desired capacity.

   ```json
   // Example ecs-cluster-parameters.json

   [
     {
       "ParameterKey": "ECSClusterName",
       "ParameterValue": "my-ecs-cluster"
     },
     {
       "ParameterKey": "EC2InstanceType",
       "ParameterValue": "t2.micro"
     },
     {
       "ParameterKey": "EC2InstanceCapacity",
       "ParameterValue": "2"
     }
   ]
   ```

### ECS Service Configuration:

5. **Define ECS Service and Task Definition:**
   - Create an ECS service and task definition using the provided `ecs-service.yaml` CloudFormation template.

   ```bash
   aws cloudformation create-stack \
     --stack-name ecs-service-stack \
     --template-body file://ecs-service.yaml \
     --capabilities CAPABILITY_IAM \
     --parameters file://ecs-service-parameters.json
   ```

6. **Define ECS Service Parameters:**
   - Edit the `ecs-service-parameters.json` file to specify ECS service parameters like task definition, desired count, and load balancer details.

   ```json
   // Example ecs-service-parameters.json

   [
     {
       "ParameterKey": "ECSClusterName",
       "ParameterValue": "my-ecs-cluster"
     },
     {
       "ParameterKey": "TaskDefinition",
       "ParameterValue": "my-ecs-task-definition"
     },
     {
       "ParameterKey": "DesiredCount",
       "ParameterValue": "2"
     },
     {
       "ParameterKey": "LoadBalancerName",
       "ParameterValue": "my-ecs-load-balancer"
     }
   ]
   ```

### Post-Deployment Steps:

7. **Access ECS Cluster:**
   - Access the AWS Management Console, navigate to ECS, and verify the successful creation of your ECS cluster.

8. **Update ECS Configuration (Optional):**
   - If necessary, update ECS configurations such as task definitions, services, or load balancers to align with your application requirements.

   ```yaml
   # Example updated ecs-service.yaml

   Resources:
     FrontendService:
       # Your ECS service configuration
   ```

### Cleanup:

9. **Delete Stacks (Optional):**
   ```bash
   aws cloudformation delete-stack --stack-name ecs-cluster-stack
   aws cloudformation delete-stack --stack-name ecs-service-stack
   ```

   - Confirm with 'yes' when prompted. Note: This will delete all resources created by CloudFormation.

### Conclusion:

Following these step-by-step instructions will help you set up an ECS cluster and service using AWS CloudFormation. Customize the provided example parameter and configuration files according to your specific requirements. Integrate this process into your CI/CD pipeline for seamless application deployment on ECS.
