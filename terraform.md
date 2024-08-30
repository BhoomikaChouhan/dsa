2

Yahan tumhare dusre tutorial ke steps hain jo tumhe variables aur AWS resources ke saath Terraform ka use karne mein madad karenge:

---

### Step-by-Step Tutorial for Terraform with Variables

#### 1. **Create `variables.tf` File**
   - **File Name**: `variables.tf`
   - **Description**: Is file mein variables define karo, including region, zones, aur AMI.
   - **Example Content**:
     ```hcl
     variable "region" {
       description = "AWS region"
       type        = string
       default     = "us-east-2"
     }

     variable "zones" {
       description = "List of availability zones"
       type        = list(string)
       default     = ["us-east-2a", "us-east-2b"]
     }

     variable "ami" {
       description = "Map of AMIs for each zone"
       type        = map(string)
       default     = {
         "us-east-2a" = "ami-0c55b159cbfafe1f0",
         "us-east-2b" = "ami-0d5d9d301c853c8f7"
       }
     }
     ```

#### 2. **Create `provider.tf` File**
   - **File Name**: `provider.tf`
   - **Description**: AWS provider ko configure karo.
   - **Example Content**:
     ```hcl
     provider "aws" {
       region = var.region
     }
     ```

#### 3. **Create `instance.tf` File**
   - **File Name**: `instance.tf`
   - **Description**: AWS instance resource ko define karo aur variables ka use karo.
   - **Example Content**:
     ```hcl
     resource "aws_instance" "example" {
       ami           = var.ami[var.zones[0]]  # Using AMI for the first zone
       instance_type = "t2.micro"
       availability_zone = var.zones[0]

       key_name = "VPS"  # Replace with your key pair name
       security_groups = ["default"]  # Replace with your security group

       tags = {
         Name    = "ExampleInstance"
         Project = "MyTerraformProject"
       }
     }
     ```

#### 4. **Initialize Terraform**
   - **Command**: `terraform init`
   - **Description**: Terraform project ko initialize karo.

#### 5. **Validate Configuration**
   - **Command**: `terraform validate`
   - **Description**: Configuration file ko validate karo aur syntax errors check karo.

#### 6. **Format Configuration**
   - **Command**: `terraform fmt`
   - **Description**: Configuration files ko standard format mein convert karo.

#### 7. **Plan Changes**
   - **Command**: `terraform plan`
   - **Description**: Changes ka plan dekho aur ensure karo ki sab kuch sahi hai.

#### 8. **Apply Changes**
   - **Command**: `terraform apply`
   - **Description**: Changes ko apply karo aur resources create karo.

#### 9. **Verify in AWS Console**
   - **Action**: AWS Management Console mein jaake resources ko check karo aur ensure karo ki instance create hua hai.

---

Is tutorial ke steps ko follow karke tum Terraform ke saath variables aur AWS resources ko manage kar sakti ho. Agar koi confusion ho toh zaroor batao!