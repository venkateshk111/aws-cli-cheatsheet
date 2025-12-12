# AWS CLI Daily Commands Cheatsheet

Quick reference for AWS CLI commands I use regularly.

## Table of Contents
- [Prerequisites](#prerequisites)
- [EC2](#ec2)
- [S3](#s3)
- [IAM](#iam)
- [Lambda](#lambda)
- [RDS](#rds)
- [CloudWatch](#cloudwatch)
- [VPC](#vpc)

## Prerequisites
```bash
# Configure AWS CLI
aws configure

# Set default output format
aws configure set output json
```

## EC2

### List Instances
```bash
# List all running instances
aws ec2 describe-instances --filters "Name=instance-state-name,Values=running" --query 'Reservations[*].Instances[*].[InstanceId,InstanceType,State.Name,PublicIpAddress]' --output table

# Get instance by tag name
aws ec2 describe-instances --filters "Name=tag:Name,Values=MyServer" --query 'Reservations[*].Instances[*].[InstanceId,PublicIpAddress]' --output table
```

### Start/Stop Instances
```bash
# Stop instance
aws ec2 stop-instances --instance-ids i-1234567890abcdef0

# Start instance
aws ec2 start-instances --instance-ids i-1234567890abcdef0
```

## S3

### Bucket Operations
```bash
# List all buckets
aws s3 ls

# List bucket contents
aws s3 ls s3://bucket-name --recursive --human-readable

# Sync local to S3
aws s3 sync ./local-folder s3://bucket-name/path/

# Copy file to S3
aws s3 cp file.txt s3://bucket-name/
```

## IAM

### User Management
```bash
# List users
aws iam list-users --output table

# Get user details
aws iam get-user --user-name username
```

---

## Tips
- Use `--dry-run` flag to test commands safely
- Add `--profile profile-name` to use different AWS profiles
- Use `--region` to specify AWS region
