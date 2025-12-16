# AWS CLI Cheat Sheet 🚀

A comprehensive collection of AWS CLI commands for daily DevOps and cloud operations. This repository serves as a quick reference guide for common AWS CLI operations.

[![AWS](https://img.shields.io/badge/AWS-CLI-orange?style=flat&logo=amazon-aws)](https://aws.amazon.com/cli/)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](CONTRIBUTING.md)

## 📋 Table of Contents

- [What is AWS CLI?](#what-is-aws-cli)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Global Flags](#global-flags)
- [Profiles](#profiles)
- [Account Information](#account-information)
- [IAM - Identity and Access Management](#iam---identity-and-access-management)
- [EC2 - Elastic Compute Cloud](#ec2---elastic-compute-cloud)
- [EKS - Elastic Kubernetes Service](#eks---elastic-kubernetes-service)
- [RDS - Relational Database Service](#rds---relational-database-service)
- [S3 - Simple Storage Service](#s3---simple-storage-service)
- [Lambda](#lambda)
- [Secret Manager](#secret-manager)
- [CloudWatch](#cloudwatch)
- [VPC - Virtual Private Cloud](#vpc---virtual-private-cloud)
- [Other Useful Commands](#other-useful-commands)
- [Contributing](#contributing)

---

---

## 🎯 What is AWS CLI?

### Three Ways to Access AWS Services

1. **AWS Management Console** - Web-based GUI interface
2. **AWS CLI** - Command Line Interface
3. **AWS SDK** - Software Development Kit for programmatic access

### About AWS CLI

AWS CLI is a unified tool to manage your AWS services that:
- Enables you to interact with AWS services using commands from your terminal
- Allows you to control multiple AWS services from the command line
- Automates AWS operations through scripts and workflows

### Supported Terminals

| Platform | Supported Terminals |
|----------|-------------------|
| **Linux/Mac** | bash, zsh, tcsh |
| **Windows** | GitBash, Command Prompt (cmd), PowerShell |
| **Remote (AWS EC2)** | PuTTY, MobaXterm, AWS Systems Manager |

---

## ✅ Prerequisites

Before installing AWS CLI, ensure you have:

1. **AWS Account** - An active AWS account
2. **IAM User** - IAM user with programmatic access (Access Key ID and Secret Access Key)
3. **Terminal Access** - Command line access on your system

---

## 🔧 Installation

### Official Documentation
- [AWS CLI Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- [Command Completion Setup](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-completion.html)

### Quick Install

**Linux:**
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

**macOS:**
```bash
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
```

**Windows (PowerShell):**
```powershell
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
```

**Verify Installation:**
```bash
aws --version
```

### Offline Installation Files

If you need to download the installer for offline installation:

| Platform | Download URL |
|----------|-------------|
| **Linux** | https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip |
| **macOS** | https://awscli.amazonaws.com/AWSCLIV2.pkg |
| **Windows** | https://awscli.amazonaws.com/AWSCLIV2.msi |

---

## ⚙️ Configuration

| Command | Description |
|---------|-------------|
| `aws configure` | Configure AWS credentials and settings |
| `aws configure sso` | Configure AWS IAM Identity Center credentials |
| `aws configure list` | Show current configuration data |
| `aws configure set <key> <value>` | Set a configuration value |
| `aws configure get <key>` | Show a configuration value |

**Example:**
```bash
aws configure
# AWS Access Key ID: YOUR_ACCESS_KEY
# AWS Secret Access Key: YOUR_SECRET_KEY
# Default region name: us-east-1
# Default output format: json
```

---

## 🌐 Global Flags

| Flag | Description |
|------|-------------|
| `--profile <name>` | Run a command using the specified profile |
| `--output <style>` | Format output as (json/text/table/yaml/yaml-stream) |
| `--help` | Show help |
| `--endpoint-url <url>` | Override default API endpoint |
| `--region <region>` | Override default region |
| `--version` | Show version of AWS CLI |
| `--query <query>` | Filter output using JMESPath query |
| `--debug` | Turn on debug logging |
| `--no-cli-pager` | Disable pager output |

**Example:**
```bash
aws ec2 describe-instances --profile production --region us-west-2 --output table
```

---

## 👤 Profiles

| Command | Description |
|---------|-------------|
| `aws configure --profile <name>` | Create a new profile |
| `aws configure list-profiles` | Show available profiles |
| `export AWS_PROFILE=<name>` | Set default profile for current session |

**Example:**
```bash
aws configure --profile dev
aws s3 ls --profile dev
```

---

## 🔐 Account Information

| Command | Description |
|---------|-------------|
| `aws sts get-caller-identity` | Retrieve account information (Account ID, User ARN) |
| `aws sts get-session-token` | Get temporary session token |
| `aws sts assume-role --role-arn <arn> --role-session-name <name>` | Assume an IAM role |

**Example:**
```bash
aws sts get-caller-identity
# Output: Account ID, User ID, ARN
```

---

## 🔑 IAM - Identity and Access Management

### Users
| Command | Description |
|---------|-------------|
| `aws iam list-users` | List all IAM users |
| `aws iam create-user --user-name <name>` | Create a new user |
| `aws iam delete-user --user-name <name>` | Delete a user |
| `aws iam get-user --user-name <name>` | Get user details |

### Groups
| Command | Description |
|---------|-------------|
| `aws iam list-groups` | List all groups |
| `aws iam create-group --group-name <name>` | Create a new group |
| `aws iam delete-group --group-name <name>` | Delete a group |

### Roles
| Command | Description |
|---------|-------------|
| `aws iam list-roles` | List all roles |
| `aws iam create-role --role-name <name> --assume-role-policy-document file://policy.json` | Create a role |
| `aws iam delete-role --role-name <name>` | Delete a role |
| `aws iam attach-role-policy --role-name <name> --policy-arn <arn>` | Attach policy to role |

### Policies
| Command | Description |
|---------|-------------|
| `aws iam list-policies` | List all policies |
| `aws iam create-policy --policy-name <name> --policy-document file://policy.json` | Create a policy |
| `aws iam delete-policy --policy-arn <arn>` | Delete a policy |
| `aws iam get-policy --policy-arn <arn>` | Get policy details |

---

## 💻 EC2 - Elastic Compute Cloud

### Instances
| Command | Description |
|---------|-------------|
| `aws ec2 describe-instances` | List all instances |
| `aws ec2 run-instances --image-id <ami-id> --instance-type <type> --key-name <key>` | Launch an instance |
| `aws ec2 start-instances --instance-ids <id>` | Start an instance |
| `aws ec2 stop-instances --instance-ids <id>` | Stop an instance |
| `aws ec2 reboot-instances --instance-ids <id>` | Reboot an instance |
| `aws ec2 terminate-instances --instance-ids <id>` | Terminate an instance |

## EBS - Elastic Block Store

### Volumes
| Command | Description |
|---------|-------------|
| `aws ec2 describe-volumes` | List all volumes |
| `aws ec2 create-volume --size <size> --availability-zone <zone>` | Create a volume |
| `aws ec2 delete-volume --volume-id <id>` | Delete a volume |

### Check Encrypted Volumes by tag

```bash
  aws ec2 describe-volumes \
  --filters "Name=tag:AppName,Values=myapp" \
  --query "Volumes[*].{VolumeName:Tags[?Key=='Name']|[0].Value,VolumeId:VolumeId,Encrypted:Encrypted,KmsKeyId:KmsKeyId}" \
  --output table
```

### Key Pairs
| Command | Description |
|---------|-------------|
| `aws ec2 describe-key-pairs` | List all key pairs |
| `aws ec2 create-key-pair --key-name <name> --query 'KeyMaterial' --output text > key.pem` | Create a key pair |
| `aws ec2 delete-key-pair --key-name <name>` | Delete a key pair |

### Security Groups
| Command | Description |
|---------|-------------|
| `aws ec2 describe-security-groups` | List all security groups |
| `aws ec2 create-security-group --group-name <name> --description "<desc>"` | Create a security group |
| `aws ec2 authorize-security-group-ingress --group-id <id> --protocol tcp --port 22 --cidr 0.0.0.0/0` | Add inbound rule |
| `aws ec2 delete-security-group --group-id <id>` | Delete a security group |

### AMIs
| Command | Description |
|---------|-------------|
| `aws ec2 describe-images --owners self` | List your AMIs |
| `aws ec2 create-image --instance-id <id> --name <name>` | Create an AMI from instance |
| `aws ec2 deregister-image --image-id <ami-id>` | Delete an AMI |

---

## ☸️ EKS - Elastic Kubernetes Service

| Command | Description |
|---------|-------------|
| `aws eks list-clusters` | List all EKS clusters |
| `aws eks describe-cluster --name <name>` | Describe a cluster |
| `aws eks create-cluster --name <name> --role-arn <arn> --resources-vpc-config subnetIds=<ids>` | Create a cluster |
| `aws eks delete-cluster --name <name>` | Delete a cluster |
| `aws eks update-kubeconfig --name <name>` | Update kubeconfig for cluster access |
| `aws eks list-nodegroups --cluster-name <name>` | List node groups |

---

## 🗄️ RDS - Relational Database Service

| Command | Description |
|---------|-------------|
| `aws rds describe-db-instances` | List all DB instances |
| `aws rds describe-db-clusters` | List all DB clusters |
| `aws rds create-db-instance --db-instance-identifier <id> --db-instance-class <class> --engine <engine>` | Create a DB instance |
| `aws rds delete-db-instance --db-instance-identifier <id> --skip-final-snapshot` | Delete a DB instance |
| `aws rds create-db-snapshot --db-snapshot-identifier <id> --db-instance-identifier <db-id>` | Create a snapshot |
| `aws rds create-db-cluster-snapshot --db-cluster-snapshot-identifier <id> --db-cluster-identifier <cluster-id>` | Create a cluster snapshot |
| `aws rds stop-db-instance --db-instance-identifier <id>` | Stop a DB instance |
| `aws rds start-db-instance --db-instance-identifier <id>` | Start a DB instance |

---

## 📦 S3 - Simple Storage Service

### Bucket Operations
| Command | Description |
|---------|-------------|
| `aws s3 ls` | List all buckets |
| `aws s3 ls s3://<bucket>` | List objects in a bucket |
| `aws s3 ls s3://<bucket> --recursive` | List all objects recursively |
| `aws s3 ls s3://<bucket> --recursive --human-readable --summarize` | List with size and summary |
| `aws s3 mb s3://<bucket>` | Create a bucket |
| `aws s3 mb s3://<bucket> --region <region>` | Create a bucket in specific region |
| `aws s3 rb s3://<bucket>` | Delete an empty bucket |
| `aws s3 rb s3://<bucket> --force` | Delete a bucket and all contents |

### S3 API Bucket Operations
| Command | Description |
|---------|-------------|
| `aws s3api create-bucket --bucket <bucket> --region <region> --create-bucket-configuration LocationConstraint=<region>` | Create bucket using S3 API |
| `aws s3api list-buckets` | List buckets with detailed info |
| `aws s3api get-bucket-versioning --bucket <bucket>` | Get bucket versioning status |
| `aws s3api put-bucket-versioning --bucket <bucket> --versioning-configuration Status=Enabled` | Enable versioning |

**Example - Create Bucket:**
```bash
aws s3api create-bucket --bucket simples3staticwebsite.com --region ap-south-1 --create-bucket-configuration LocationConstraint=ap-south-1
# Output:
# {
#     "Location": "http://simples3staticwebsite.com.s3.amazonaws.com/"
# }
```

### Object Operations
| Command | Description |
|---------|-------------|
| `aws s3 cp <local-file> s3://<bucket>/` | Upload a file to S3 |
| `aws s3 cp <local-dir> s3://<bucket>/ --recursive` | Upload directory recursively |
| `aws s3 cp s3://<bucket>/<file> <local-path>` | Download a file from S3 |
| `aws s3 cp s3://<bucket>/ <local-dir> --recursive` | Download all objects recursively |
| `aws s3 cp s3://<bucket1>/<file> s3://<bucket2>/` | Copy file between S3 buckets |
| `aws s3 cp s3://<bucket1> s3://<bucket2> --recursive` | Copy all objects between buckets |
| `aws s3 mv <source> s3://<bucket>/` | Move local file to S3 |
| `aws s3 mv s3://<bucket>/<file> <local-path>` | Move file from S3 to local |
| `aws s3 mv s3://<bucket1>/<file> s3://<bucket2>/` | Move file between S3 buckets |
| `aws s3 mv <local-dir> s3://<bucket>/ --recursive` | Move local directory to S3 |
| `aws s3 mv s3://<bucket1> s3://<bucket2> --recursive` | Move all objects between buckets |
| `aws s3 rm s3://<bucket>/<object>` | Delete an object |
| `aws s3 rm s3://<bucket> --recursive` | Delete all objects in bucket |

### Sync Operations
| Command | Description |
|---------|-------------|
| `aws s3 sync <local-dir> s3://<bucket>` | Sync local directory to S3 bucket |
| `aws s3 sync s3://<bucket> <local-dir>` | Sync S3 bucket to local directory |
| `aws s3 sync s3://<bucket1> s3://<bucket2>` | Sync between two S3 buckets |

**Example - Sync Between Buckets:**
```bash
aws s3 sync s3://www.simples3staticwebsite.com s3://simples3staticwebsite.com
# Output:
# copy: s3://www.simples3staticwebsite.com/awss3.png to s3://simples3staticwebsite.com/awss3.png
# copy: s3://www.simples3staticwebsite.com/error.html to s3://simples3staticwebsite.com/error.html
# copy: s3://www.simples3staticwebsite.com/index.html to s3://simples3staticwebsite.com/index.html
```

### Static Website Hosting
| Command | Description |
|---------|-------------|
| `aws s3 website s3://<bucket>/ --index-document index.html --error-document error.html` | Configure bucket for static website hosting |

### Presigned URLs
| Command | Description |
|---------|-------------|
| `aws s3 presign s3://<bucket>/<object>` | Generate presigned URL (default: 3600 seconds) |
| `aws s3 presign s3://<bucket>/<object> --expires-in <seconds>` | Generate presigned URL with custom expiration |

**Example:**
```bash
aws s3 presign s3://mys3bucket/dnsrecords.txt --expires-in 60
# Generates a URL valid for 60 seconds
```

### Advanced S3 API
| Command | Description |
|---------|-------------|
| `aws s3api get-object --bucket <bucket> --key <key> <output-file>` | Get an object |

---

## ⚡ Lambda

| Command | Description |
|---------|-------------|
| `aws lambda list-functions` | List all Lambda functions |
| `aws lambda get-function --function-name <name>` | Get function details |
| `aws lambda invoke --function-name <name> output.txt` | Invoke a function |
| `aws lambda create-function --function-name <name> --runtime <runtime> --role <arn> --handler <handler> --zip-file fileb://function.zip` | Create a function |
| `aws lambda delete-function --function-name <name>` | Delete a function |
| `aws lambda update-function-code --function-name <name> --zip-file fileb://function.zip` | Update function code |

---

## 🔐 Secrets Manager

### Secret Operations
| Command | Description |
|---------|-------------|
| `aws secretsmanager list-secrets` | List all secrets |
| `aws secretsmanager describe-secret --secret-id <name>` | Get secret details |
| `aws secretsmanager get-secret-value --secret-id <name>` | Retrieve secret value |
| `aws secretsmanager create-secret --name <name> --secret-string <value>` | Create a new secret |
| `aws secretsmanager create-secret --name <name> --secret-string file://secret.json` | Create secret from file |
| `aws secretsmanager update-secret --secret-id <name> --secret-string <value>` | Update secret value |
| `aws secretsmanager put-secret-value --secret-id <name> --secret-string <value>` | Put new secret value |

### Secret Deletion
| Command | Description |
|---------|-------------|
| `aws secretsmanager delete-secret --secret-id <name>` | Delete secret (30-day recovery window) |
| `aws secretsmanager delete-secret --secret-id <name> --recovery-window-in-days <days>` | Delete secret with custom recovery window (7-30 days) |
| `aws secretsmanager delete-secret --secret-id <name> --force-delete-without-recovery` | Delete secret immediately (no recovery) |
| `aws secretsmanager restore-secret --secret-id <name>` | Restore deleted secret within recovery window |
| `aws secretsmanager list-secrets --filters Key=deleted,Values=true` | List secrets marked for deletion |

### Secret Rotation
| Command | Description |
|---------|-------------|
| `aws secretsmanager rotate-secret --secret-id <name>` | Rotate secret immediately |
| `aws secretsmanager cancel-rotate-secret --secret-id <name>` | Cancel secret rotation |

**Example:**
```bash
# Create a database password secret
aws secretsmanager create-secret --name prod/db/password --secret-string "MySecurePassword123"

# Delete secret immediately (use with caution!)
aws secretsmanager delete-secret --secret-id prod/api-key --force-delete-without-recovery
```

## 📊 CloudWatch

### Logs
| Command | Description |
|---------|-------------|
| `aws logs describe-log-groups` | List all log groups |
| `aws logs describe-log-streams --log-group-name <name>` | List log streams |
| `aws logs tail <log-group-name> --follow` | Tail logs in real-time |
| `aws logs filter-log-events --log-group-name <name> --filter-pattern "<pattern>"` | Filter log events |

### Metrics
| Command | Description |
|---------|-------------|
| `aws cloudwatch list-metrics` | List all metrics |
| `aws cloudwatch get-metric-statistics --namespace <namespace> --metric-name <name> --start-time <time> --end-time <time> --period <seconds> --statistics Average` | Get metric statistics |

---

## 🌐 VPC - Virtual Private Cloud

| Command | Description |
|---------|-------------|
| `aws ec2 describe-vpcs` | List all VPCs |
| `aws ec2 create-vpc --cidr-block <cidr>` | Create a VPC |
| `aws ec2 describe-subnets` | List all subnets |
| `aws ec2 create-subnet --vpc-id <vpc-id> --cidr-block <cidr>` | Create a subnet |
| `aws ec2 describe-route-tables` | List route tables |
| `aws ec2 describe-internet-gateways` | List internet gateways |

---

## 🛠️ Other Useful Commands

| Command | Description |
|---------|-------------|
| `aws --version` | Show AWS CLI version |
| `aws help` | Show help including all available commands |
| `aws <service> help` | Show help for a specific service |
| `aws <service> <command> help` | Show help for a specific command |
| `aws configure export-credentials` | Export current credentials |
| `aws sts decode-authorization-message --encoded-message <message>` | Decode authorization failure messages |

---

## 🎯 Pro Tips

### Using JMESPath for Query Filtering
```bash
# Get only instance IDs
aws ec2 describe-instances --query 'Reservations[*].Instances[*].InstanceId' --output text

# Get running instances only
aws ec2 describe-instances --query 'Reservations[*].Instances[?State.Name==`running`]'
```

### Using AWS CLI with Pagination
```bash
# Automatically handle pagination
aws s3api list-objects-v2 --bucket <bucket> --max-items 1000
```

### Output Formatting
```bash
# Table format for better readability
aws ec2 describe-instances --output table

# YAML format
aws ec2 describe-instances --output yaml
```

---

<!-- ## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. 

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### How to Contribute:
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/new-commands`)
3. Commit your changes (`git commit -m 'Add some commands'`)
4. Push to the branch (`git push origin feature/new-commands`)
5. Open a Pull Request -->

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## ⭐ Star This Repository

If you find this cheat sheet helpful, please give it a star! It helps others discover this resource.

---

## 📚 Additional Resources

- [AWS CLI Official Documentation](https://docs.aws.amazon.com/cli/)
- [AWS CLI Command Reference](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html)
- [AWS CLI GitHub Repository](https://github.com/aws/aws-cli)

<!-- ---

**Last Updated:** October 2025

**Maintained by:** [Venkatesh K](https://github.com/venkateshk111] -->
