# MSK Kafka Terraform
 
Terraform configurations for deploying and managing an Amazon Managed Streaming for Apache Kafka (MSK) cluster at WS 2024 whilst using Travis CI. 

## Prerequisites

Before you begin, ensure you have the following installed:

- [Terraform](https://www.terraform.io/downloads.html) v0.12 or later
- [AWS CLI](https://aws.amazon.com/cli/) configured with appropriate credentials
- An AWS account with the necessary permissions to create and manage MSK resources

## Getting Started

### Clone the Repository

```sh
git clone https://github.com/Montana/msk-kafka-terraform.git
cd msk-kafka-terraform
```

### Configure Terraform

1. **Initialize Terraform:**

   Initialize the Terraform working directory, which will download the necessary provider plugins.

   ```sh
   terraform init
   ```
I recommend changing `terraform` to an alias of `tf`, it's a lot quicker especially in front of the audience. 

## Flowchart

Flowchart I made outlining the process: 

```bash
Start
  |
  v
Clone the Repository
  |
  v
+----------------------+
| git clone repository |
+----------------------+
  |
  v
Navigate to Directory
  |
  v
+---------------------+
| cd msk-kafka-terraform |
+---------------------+
  |
  v
Initialize Terraform
  |
  v
+----------------------+
| terraform init       |
+----------------------+
  |
  v
Set Up Backend (if using remote backend)
  |
  v
+------------------------+
| Configure backend.tf   |
+------------------------+
  |
  v
Modify Variables
  |
  v
+-------------------------+
| Edit variables.tf or    |
| create terraform.tfvars |
+-------------------------+
  |
  v
Plan Deployment
  |
  v
+----------------------+
| terraform plan       |
+----------------------+
  |
  v
Review Plan
  |
  v
Apply Deployment
  |
  v
+----------------------+
| terraform apply      |
+----------------------+
  |
  v
Confirm Apply Step
  |
  v
Manage MSK Cluster
  |
  +---------------------------+
  |                           |
  v                           v
Make Configuration Changes   Destroy Resources
  |                           |
  v                           v
+----------------------+     +----------------------+
| Edit .tf files       |     | terraform destroy    |
+----------------------+     +----------------------+
  |                           |
  v                           v
+----------------------+     +----------------------+
| terraform plan       |     | Confirm Destroy Step |
+----------------------+     +----------------------+
  |
  v
+----------------------+
| terraform apply      |
+----------------------+
  |
  v
End
```

2. **Set Up Backend:**

   If you're using a remote backend to store the Terraform state, configure it in `backend.tf`.

3. **Modify Variables:**

   Review and update the variables in the `variables.tf` file or create a `terraform.tfvars` file to set custom values. The variables include configurations for your MSK cluster such as:

   - `cluster_name`: The name of the MSK cluster.
   - `kafka_version`: The version of Kafka to use.
   - `number_of_brokers`: The number of broker nodes in the cluster.
   - `broker_instance_type`: The instance type for the broker nodes.
   - `subnet_ids`: A list of subnet IDs for the MSK cluster.
   - `security_group_ids`: A list of security group IDs to associate with the MSK cluster.

### Deploy the MSK Cluster

1. **Plan the Deployment:**

   Generate and review an execution plan for the infrastructure.

   ```sh
   terraform plan
   ```

2. **Apply the Deployment:**

   Apply the Terraform configuration to create the MSK cluster and related resources.

   ```sh
   terraform apply
   ```

   Confirm the apply step when prompted.

### Managing the MSK Cluster

To make changes to the MSK cluster configuration, update the relevant Terraform files and re-run `terraform plan` and `terraform apply`.

### Destroy the MSK Cluster

To destroy all resources created by this Terraform configuration, run:

```sh
terraform destroy
```

## Configuration Details

### MSK Cluster

- **Cluster Name:** Configurable via the `cluster_name` variable.
- **Kafka Version:** Specify the Kafka version using the `kafka_version` variable.
- **Broker Nodes:** Configure the number and instance type of broker nodes using `number_of_brokers` and `broker_instance_type`.
- **Networking:** Specify the VPC subnets and security groups for the MSK cluster using `subnet_ids` and `security_group_ids`.

### Security

Ensure that the AWS credentials used have the necessary permissions to create and manage the resources defined in this Terraform configuration. Consider using IAM roles and policies to enforce least privilege.

### Monitoring

Integrate AWS CloudWatch for monitoring Kafka metrics and set up appropriate alarms and notifications, I (Michael Mendy) have setup a PagerDuty instance for this run.

### Copyright

* Michael Mendy (c) 2024
* Travis CI, GmbH (c) 2024
