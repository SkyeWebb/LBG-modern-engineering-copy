Getting Started with Terraform

- [Terraform LAB](#day-04---terraform)

  - [Terraform Lab](#terraform-lab)
    - [Logging into AWS](#logging-into-aws-sso)
    - [Creating the Terraform Manifest](#creating-the-terraform-manifest)
      - [Initializing Terraform](#initializing-terraform)
      - [Practicing Plan and Apply](#practicing-plan-and-apply)
      - [Adding the Resource Blocks](#adding-the-resource-blocks)

This lab introduces you to Terraform, a common tool for automation and infrastructure-as-code.

## Installing Terraform

Terraform can run on Linux, Windows, or macOS. Instructions for installing Terraform are available at https://developer.hashicorp.com/terraform/downloads.

For your Amazon Workspace VM, the ansible script we ran in the previous session installed terraform for
you. To confirm that you have terraform installed, you can run:

```
terraform -v
```

The output should be similar to:

```
Terraform v1.8.5
on linux_amd64
+ provider registry.terraform.io/hashicorp/aws v4.67.0
+ provider registry.terraform.io/hashicorp/random v3.6.2
```

There are basic steps you take each time you are working with a terraform template. In this lab, you will practice getting started with terraform with the basic steps. You will create an DynamoDB instance using terraform.

### Logging into AWS

First things first. Since you will be connecting to AWS from the CLI, you need to get your credentials setup before you can do that.

In this lab, you setup your AWS credentials but the credentials do expire. To start the lab, authenticate to your AWS CLI by typing the command `aws configure` and following the prompts. You'll find the access keys you need in your Whizlabs Custom Sandbox.

**_Log in to whizlabs from your AWS workspace - the access keys are very long, so you'll want to copy/paste them from the browser to the workspace terminal. Trying to type them out will almost certainly end in typos and you'll have to repeat this step._**

### Creating the Terraform Manifest

Here, we are going to create a manifest file to help us create a DynamoDB. Follow the steps below to do that:

1. Create a new directory to store your Terraform manifest in.

```
cd ~/Desktop
mkdir terraform-lab-01
cd terraform-lab-01
```

2. In that directory, open a new file in VS Code called

`code lab.tf`.

3. You'll want to create the following blocks in the Terraform manifest:
   - A `terraform` with an AWS required provider
   - A `provider` block specifying the AWS region you want to deploy in
   - Resource blocks for ECS

Copy and paste the following information inside `lab.tf` file to create the `terraform` and `provider` blocks:

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.16"
    }
  }

  required_version = ">= 1.2.0"
}

provider "aws" {
  region  = "us-east-2"
}

```

4. Save the file and exit `vs code`

5. #### Step 1: Initializing Terraform

Go back to your terminal in the directory that has your `lab.tf` file and run the command:

```
terraform init
```

The output will be similar to this:

```text
Initializing the backend...

Initializing provider plugins...
- Finding hashicorp/aws versions matching "~> 4.16"...
- Installing hashicorp/aws v4.17.0...
- Installed hashicorp/aws v4.17.0 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

If you didn't get a similar output, speak with the instructore for help. It's important you get this step working, otherwise nothing else you do will work.

#### Step 2: Terrafrom Plan

Once you've initialized your Terraform directory, you can start to add resource blocks, plan, and apply them. Try the following:

Step 1: Open your lab.tf and at the end of the file, copy and paste the following resource blocks in your manifest:

```hcl
resource "aws_dynamodb_table" "accounts" {
  name         = "Accounts"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "id"

  attribute {
    name = "id"
    type = "S"
  }

  tags = {
    Name = "AccountsTable"
  }
}
```

Step 2. Run `terraform plan`

- If you get an error, run `terraform init` then `terraform plan` again

```
terraform plan
```

You should see output of Terraform telling you what it _would_ do

#### Step 3: Terraform Apply

1.  Run `terraform apply` to apply those changes. Enter `yes` when prompted.

```
terraform apply
```

2. Run `terraform plan` again. You should see it tell you there is nothing it needs to do

```
terraform plan
```

3. Visit the DynamoDB service in the AWS management console and verify that the database was created

#### Step 3: Terraform Destroy

It's a good practice to cleap up after your exercises so let's destroy the Dynamodb we just created.

Run `terraform destroy -auto-approve` to destroy the infrastructure you made

```
terraform destroy -auto-approve
```

Visit the DynamoDB service in the AWS management console and verify that the database was deleted.

Congratulations, you just used terraform to create a DynamoDB instance on the AWS cloud. Don't forget the steps, `terraform init, terraform plan, terraform apply, and terraform destroy` (when no longer needed)
