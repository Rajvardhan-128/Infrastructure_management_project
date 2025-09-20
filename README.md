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

**Flow of steps**:  
- EC2 creation  
- Install Jenkins  
- Install Terraform  
- **Create S3 bucket + DynamoDB manually**  
- Configure Jenkins pipeline  
- Run Terraform

  
⚙️ Setup Instructions  

1️⃣ Launch EC2 Instance 

1. Go to the AWS Management Console → EC2 → Launch Instance
   
2. Choose Amazon Linux 2 / Ubuntu AMI
     
3. Select instance type (e.g., `t2.medium`)
   
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

3️⃣ Setup Terraform Backend (S3 + DynamoDB)
Before running Terraform, configure remote state management:

1. Create an S3 Bucket (manually via AWS Console)  
   - Bucket name must be globally unique and lowercase  
   - Enable Versioning to keep track of state file history  

2. Create a DynamoDB Table (manually via AWS Console)**  
   - Table name: `terraform-lock` (or any name you prefer)  
   - Partition key: `LockID` (String)  
   - This is used for **state locking** to avoid conflicts during parallel runs  

3. Update your Terraform backend configuration:
   

       terraform {
       backend "s3" {
         bucket         = "your-s3-bucket-name"
         key            = "terraform/state.tfstate"
         region         = "ap-south-1"
         dynamodb_table = "terraform-lock"
         encrypt        = true
       }
     }   



# Download Terraform

    sudo apt update && sudo apt install -y gnupg software-properties-common curl && curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg && echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list && sudo apt update && sudo apt install terraform -y && terraform -version


# Verify installation

    terraform -version



4️⃣ Configure Jenkins Pipeline

  1) Login to Jenkins (http://<EC2_PUBLIC_IP>:8080)
   
  2) Create a New Item → Pipeline
   
  3) In configuration:
   
  4) Select Pipeline script from SCM

  5) SCM: Git
    
  6) Repository URL:
 
    https://github.com/Rajvardhan-128/Terraform_Infrastructure_management_project.git 
   
   7) Branch: main
   
   8) Script Path: Jenkinsfile
   
   9) Save and Build the pipeline


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

        terraform init

4. Validate configuration :
   
       terraform validate

4. Plan infrastructure :
   
       terraform plan


5. Apply changes :
   
       terraform apply --auto-approve


6. Destroy infrastructure :
   
       terraform destroy --auto-approve

 

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

1. Bucket names must be unique and lowercase

2. Security group names should not duplicate existing ones

3. Always run terraform init -reconfigure if backend configuration changes

🤝 Contributing

-> Feel free to fork this repo and submit pull requests to improve infrastructure design and automation.

👤 Author

Rajvardhan Kale 

Terraform | AWS | DevOps | Jenkins
