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

1️⃣ Launch EC2 Instance 

1. Go to the AWS Management Console → EC2 → Launch Instance
   
2. Choose Amazon Linux 2 / Ubuntu AMI
     
3. Select instance type (e.g., `t2.micro`)
   
4. Configure security group → Allow All Traffic (0.0.0.0/0) for testing purposes
    
5. Launch the instance and connect via SSH
   ```bash
      ssh -i your-key.pem ec2-user@<EC2_PUBLIC_IP>


2️⃣ Install Jenkins on EC2
   # Update system
    sudo apt update
    
   # Install Java (required for Jenkins)
    sudo apt install fontconfig openjdk-21-jre
    java -version
    openjdk version "21.0.3" 2024-04-16
    OpenJDK Runtime Environment (build 21.0.3+11-Debian-2)
    OpenJDK 64-Bit Server VM (build 21.0.3+11-Debian-2, mixed mode, sharing)


   # Add Jenkins repo & Install Jenkins

    sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
    https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
    echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt update
    sudo apt install jenkins

   # Start and enable Jenkins
   
    sudo systemctl start jenkins
    sudo systemctl enable jenkins

   Access Jenkins in your browser:
      
      http://<EC2_PUBLIC_IP>:8080

# Download Terraform

    sudo apt update && sudo apt install -y gnupg software-properties-common curl && curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg && echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list && sudo apt update && sudo apt install terraform -y && terraform -version


# Verify installation
terraform -version



4️⃣ Configure Jenkins Pipeline

  1) Login to Jenkins (http://<EC2_PUBLIC_IP>:8080)
   
  2) Create a New Item → Pipeline
   
  3) In configuration:
   
   1. Select Pipeline script from SCM
      SCM: Git
   
   2. Repository URL:
 
    https://github.com/Rajvardhan-128/Terraform_Infrastructure_management_project.git 
   
   Branch: main
   
   Script Path: Jenkinsfile
   
   Save and Build the pipeline


 5️⃣ Run Terraform from Jenkins

   Jenkins will automatically run:
   
      terraform init
      
      terraform plan
      
      terraform apply --auto-approve
      
   This provisions infrastructure automatically using your repo.


# If You want to run Manually on local machine by Terrafrom Use This commands 

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


6. Destroy infrastructure :
   
 --> terraform destroy --auto-approve
 

📂 Project Structure


├── main.tf                   # Main resources (EC2, VPC, etc.)

├── s3.tf                     # S3 bucket for state management

├── variables.tf              # Input variables

├── terraform.tfvars          # Variable values

├── outputs.tf                # Outputs

└── Jenkinsfile               # Jenkins pipeline for automation


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
