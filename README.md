# Terraform Infrastructure Management Project 

This project demonstrates how to use Terraform for provisioning and managing cloud infrastructure on AWS.  
It automates the creation of resources like EC2, S3, Security Groups, and VPC, and integrates with Jenkins for CI/CD automation.

---

 🚀 Features :
- Infrastructure as Code (IaC) using Terraform  
- Automated provisioning of AWS resources:
  - EC2 Instances
  - Security Groups
  - S3 Buckets
  - VPC Networking  
- Remote backend configuration with S3 + DynamoDB for state management  
- Jenkins Pipeline for continuous integration and deployment  

---

🛠️ Prerequisites
Make sure you have:
- [Terraform](https://developer.hashicorp.com/terraform/downloads) installed  
- [AWS CLI](https://aws.amazon.com/cli/) configured with proper credentials  
- [Jenkins](https://www.jenkins.io/) (if running pipeline)  

---

⚙️ Setup Instructions

1. Clone the repository :
   ```bash
   git clone https://github.com/Rajvardhan-128/Terraform_Infrastructure_management_project.git
   cd Terraform_Infrastructure_management_project

2. Initialize Terraform :
--> terraform init

3. Validate configuration :
--> terraform validate

4. Plan infrastructure :
--> terraform plan


5. Apply changes :
--> terraform apply --auto-approve


6. Destroy infrastructure
--> terraform destroy --auto-approve

📂 Project Structure

.
├── main.tf          # Main resources (EC2, VPC, etc.)
├── s3.tf            # S3 bucket for state management
├── variables.tf     # Input variables
├── terraform.tfvars # Variable values
├── outputs.tf       # Outputs
└── Jenkinsfile      # Jenkins pipeline for automation

🔒 State Management

Terraform state is stored remotely in an S3 bucket

DynamoDB table is used for state locking

📌 Notes

Bucket names must be unique and lowercase

Security group names should not duplicate existing ones

Always run terraform init -reconfigure if backend configuration changes

🤝 Contributing

Feel free to fork this repo and submit pull requests to improve infrastructure design and automation.

👤 Author

Rajvardhan Kale 

Terraform | AWS | DevOps | Jenkins
