# Terraform Commands with Examples for Beginners

Terraform is a tool that helps you create, manage, and update infrastructure (like servers, databases, and networks) using code. This document lists common `terraform` commands with beginner-friendly explanations and examples. Before using these commands, make sure you have Terraform installed on your computer and have set up credentials for your cloud provider (e.g., AWS, Azure, or Google Cloud).

## Getting Started: Setting Up Your Project

### Initialize a Terraform Working Directory

This command sets up your Terraform project by downloading the necessary plugins for your cloud provider and preparing your working directory.

- **Why use it?** It’s the first step to start using Terraform in a new project folder.
- **Example:** If you have a file like `main.tf` with AWS resources, this command prepares everything.
  
  ```bash
  terraform init
  ```

### Validate Configuration

Checks if your Terraform configuration files (like `main.tf`) are written correctly and don’t have errors.

- **Why use it?** It helps catch mistakes before you try to create resources.
- **Example:** Run this after writing or editing your Terraform files to ensure they’re valid.
  
  ```bash
  terraform validate
  ```

### Format Configuration Files

Automatically fixes the formatting of your Terraform files to make them neat and consistent.

- **Why use it?** Clean, formatted code is easier to read and maintain.
- **Example:** If your `main.tf` has messy spacing, this command tidies it up.
  
  ```bash
  terraform fmt
  ```

### Upgrade Configuration

Updates the plugins and modules in your project to their latest compatible versions.

- **Why use it?** Ensures you’re using the newest features and bug fixes for your cloud provider.
- **Example:** Run this when you want to update your project to the latest provider versions.
  
  ```bash
  terraform init -upgrade
  ```

## Planning and Creating Resources

### Create an Execution Plan

Shows you a preview of what Terraform will do (create, update, or delete resources) without making any actual changes.

- **Why use it?** It’s like a “dry run” to check what will happen before you commit.
- **Example:** Run this to see what resources Terraform will create based on your `main.tf`.
  
  ```bash
  terraform plan
  ```

### Apply Changes

Executes the plan to create, update, or delete resources in your cloud provider.

- **Why use it?** This is how you actually make changes to your infrastructure.
- **Example:** After checking the plan, run this to create an AWS EC2 instance defined in your configuration.
  
  ```bash
  terraform apply
  ```

### Apply with Auto-Approve

Applies changes without asking for your confirmation.

- **Why use it?** Useful in scripts or automation where you don’t want to manually type “yes.”
- **Example:** Use this to quickly apply changes in a CI/CD pipeline.
  
  ```bash
  terraform apply -auto-approve
  ```

### Generate Plan File

Saves the execution plan to a file so you can review or apply it later.

- **Why use it?** Allows you to save a plan and share it with your team for review.
- **Example:** Save a plan to a file called `tfplan` for later use.
  
  ```bash
  terraform plan -out=tfplan
  ```

### Apply from Plan File

Applies the changes stored in a saved plan file.

- **Why use it?** Ensures you’re applying exactly what was planned, with no surprises.
- **Example:** Apply the plan saved in `tfplan`.
  
  ```bash
  terraform apply tfplan
  ```

## Managing Terraform State

### Show State

Displays the current state of all resources Terraform is managing.

- **Why use it?** Helps you see the details of your infrastructure as Terraform tracks it.
- **Example:** Check the state to see the current configuration of your AWS resources.
  
  ```bash
  terraform state show
  ```

### List Resources in State

Lists all resources that Terraform is tracking in its state file.

- **Why use it?** Useful to quickly see what resources exist in your project.
- **Example:** Run this to see a list of all your managed resources, like EC2 instances or S3 buckets.
  
  ```bash
  terraform state list
  ```

### Move a Resource in State

Renames or moves a resource in the Terraform state file without changing the actual resource.

- **Why use it?** Helpful when you refactor your code and change resource names.
- **Example:** Rename an AWS instance from `aws_instance.example` to `aws_instance.new_example` in the state.
  
  ```bash
  terraform state mv aws_instance.example aws_instance.new_example
  ```

### Remove a Resource from State

Removes a resource from Terraform’s state without deleting it from your cloud provider.

- **Why use it?** Useful when you want Terraform to stop managing a resource but keep it in the cloud.
- **Example:** Stop tracking an AWS instance without deleting it.
  
  ```bash
  terraform state rm aws_instance.example
  ```

### Import Existing Resource

Tells Terraform to start managing an existing resource that wasn’t created by Terraform.

- **Why use it?** Allows you to bring existing cloud resources under Terraform’s control.
- **Example:** Import an existing AWS EC2 instance with ID `i-1234567890abcdef0`.
  
  ```bash
  terraform import aws_instance.example i-1234567890abcdef0
  ```

### Pull State

Downloads the Terraform state file from a remote backend (like S3 or Terraform Cloud) to your local machine.

- **Why use it?** Useful for inspecting or backing up the state file.
- **Example:** Save the remote state to a local file called `terraform.tfstate`.
  
  ```bash
  terraform state pull > terraform.tfstate
  ```

### Push State

Uploads a local state file to a remote backend.

- **Why use it?** Helps restore or migrate state to a remote backend.
- **Example:** Upload a local state file to the remote backend.
  
  ```bash
  terraform state push terraform.tfstate
  ```

## Destroying Resources

### Destroy All Resources

Deletes all resources managed by your Terraform configuration.

- **Why use it?** Cleans up everything when you no longer need the infrastructure.
- **Example:** Remove all resources defined in your `main.tf`, like EC2 instances and S3 buckets.
  
  ```bash
  terraform destroy
  ```

### Destroy with Auto-Approve

Destroys all resources without asking for confirmation.

- **Why use it?** Speeds up cleanup in automated workflows.
- **Example:** Use this in a script to delete resources without manual input.
  
  ```bash
  terraform destroy -auto-approve
  ```

### Destroy Specific Resource

Deletes only a specific resource instead of everything.

- **Why use it?** Allows you to remove just one resource without affecting others.
- **Example:** Delete a single AWS EC2 instance.
  
  ```bash
  terraform destroy -target=aws_instance.example
  ```

## Managing Workspaces

### List Workspaces

Shows all workspaces in your Terraform project.

- **Why use it?** Workspaces let you manage multiple environments (like dev, prod) in one project.
- **Example:** Check which workspaces exist, such as `default`, `dev`, or `prod`.
  
  ```bash
  terraform workspace list
  ```

### Create a Workspace

Creates a new workspace for managing a separate environment.

- **Why use it?** Useful for separating development, staging, and production environments.
- **Example:** Create a workspace called `dev` for development work.
  
  ```bash
  terraform workspace new dev
  ```

### Select a Workspace

Switches to a different workspace.

- **Why use it?** Lets you work on a specific environment, like `dev` or `prod`.
- **Example:** Switch to the `dev` workspace.
  
  ```bash
  terraform workspace select dev
  ```

### Delete a Workspace

Removes a workspace (you can’t delete the `default` workspace).

- **Why use it?** Cleans up unused workspaces to keep your project organized.
- **Example:** Delete the `dev` workspace when it’s no longer needed.
  
  ```bash
  terraform workspace delete dev
  ```

## Working with Modules and Providers

### Get Modules

Downloads and updates any Terraform modules used in your configuration.

- **Why use it?** Modules are reusable pieces of Terraform code, and this ensures you have the latest versions.
- **Example:** Run this if your `main.tf` uses a module from a Git repository or Terraform Registry.
  
  ```bash
  terraform get
  ```

### Show Provider Versions

Lists the versions of all providers (like AWS, Azure) used in your project.

- **Why use it?** Helps you verify which provider versions Terraform is using.
- **Example:** Check the version of the AWS provider in your project.
  
  ```bash
  terraform providers
  ```

### Lock Providers

Creates a lock file to pin provider versions, ensuring consistency across runs.

- **Why use it?** Prevents unexpected changes when provider versions update.
- **Example:** Generate a lock file for your providers.
  
  ```bash
  terraform providers lock
  ```

## Viewing Outputs and Inspecting Resources

### Show Outputs

Displays the output values defined in your Terraform configuration.

- **Why use it?** Outputs are useful for showing important information, like an EC2 instance’s IP address.
- **Example:** View all outputs, such as an instance’s public IP.
  
  ```bash
  terraform output
  ```

### Show Specific Output

Displays a single output value by name.

- **Why use it?** Quickly get a specific piece of information, like a resource ID.
- **Example:** Show the `instance_id` output defined in your configuration.
  
  ```bash
  terraform output instance_id
  ```

### Refresh State

Updates the Terraform state file to match the real-world state of your resources.

- **Why use it?** Ensures Terraform’s state reflects any manual changes made outside Terraform.
- **Example:** Run this if someone manually updated an AWS resource in the AWS console.
  
  ```bash
  terraform refresh
  ```

### Graph Dependencies

Creates a visual graph showing how your resources depend on each other.

- **Why use it?** Helps you understand the relationships between resources in complex projects.
- **Example:** Generate a graph to visualize dependencies (you can view it with tools like Graphviz).
  
  ```bash
  terraform graph
  ```

## Debugging and Troubleshooting

### Enable Detailed Logging

Turns on detailed debug logs to help diagnose issues.

- **Why use it?** Useful when Terraform isn’t working as expected and you need more information.
- **Example:** Enable debugging before running `apply` to see detailed logs.
  
  ```bash
  export TF_LOG=DEBUG
  terraform apply
  ```

### Show Version

Displays the Terraform version and the versions of all providers in use.

- **Why use it?** Helps you confirm you’re using the right Terraform and provider versions.
- **Example:** Check if you’re on the latest Terraform version.
  
  ```bash
  terraform version
  ```

### Taint a Resource

Marks a resource as “tainted,” forcing Terraform to recreate it on the next `apply`.

- **Why use it?** Useful if a resource is misconfigured and needs to be replaced.
- **Example:** Taint an AWS EC2 instance to recreate it.
  
  ```bash
  terraform taint aws_instance.example
  ```

### Untaint a Resource

Removes the “tainted” status from a resource so it won’t be recreated.

- **Why use it?** Reverses a taint if you marked a resource by mistake.
- **Example:** Untaint an AWS EC2 instance to keep it as is.
  
  ```bash
  terraform untaint aws_instance.example
  ```

### Force Unlock State

Manually unlocks the Terraform state if it’s stuck in a locked state.

- **Why use it?** Fixes issues when Terraform thinks the state is locked (e.g., after a crashed run).
- **Example:** Unlock the state using the lock ID shown in the error message.
  
  ```bash
  terraform force-unlock LOCK_ID
  ```

## Working with Remote Backends and Collaboration

### Configure Remote Backend

Sets up or migrates your project to use a remote backend (like S3 or Terraform Cloud) for storing state.

- **Why use it?** Remote backends allow teams to collaborate and keep state files safe.
- **Example:** Configure an S3 bucket called `my-terraform-state` as the backend.
  
  ```bash
  terraform init -backend-config="bucket=my-terraform-state"
  ```

### Login to Terraform Cloud/Enterprise

Authenticates with Terraform Cloud or Terraform Enterprise for remote state and collaboration.

- **Why use it?** Required to use Terraform Cloud’s features, like remote runs and state management.
- **Example:** Log in to your Terraform Cloud account.
  
  ```bash
  terraform login
  ```

### Logout from Terraform Cloud/Enterprise

Logs you out of Terraform Cloud or Enterprise.

- **Why use it?** Useful when switching accounts or securing your session.
- **Example:** Log out after finishing your work.
  
  ```bash
  terraform logout
  ```