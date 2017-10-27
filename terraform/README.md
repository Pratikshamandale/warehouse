# Motivation

Automate queues and deadLetter queues setup. This is where the workers pull payloads from.

# How to run

1. git clone --recursive git@github.com:ShoppinPal/warehouse.git

2. Copy the templates for configuring environment variables
cp .env.example .env
cp worker.env.example worker.env

3. Then fill in the values for env variables into `.env` and `worker.env` files

4. cd into **$PROJECT_ROOT/terraform/** directory.

5. Create **terraform.tfvars** under **$PROJECT_ROOT/terraform/** directory. (Use **$PROJECT_ROOT/terraform/example.tfvars.file** as template.)
    Below is example.tfvars.file
    ```
        # Must have the appriopriate IAM permissions to manipulate SQS
        aws_iam_access_key      = ""
        aws_iam_secret_key      = ""
        Q                       = "terraform_warehouse_workers_Q"   # use whatever name you find useful
        DLQ                     = "terraform_warehouse_workers_DLQ" # use whatever name you find useful
    ```
    Note: File name should be **terraform.tfvars** so that terraform can autoload this file.
6. Run these commands under **$PROJECT_ROOT/terraform/** directory:
    ```
        1. docker-compose run terraform init
        2. docker-compose run terraform get    // used to download and update modules mentioned in the root module (main.tf).
        3. docker-compose run terraform plan
        4. docker-compose run terraform apply
        5. docker-compose run terraform destroy // to destroy your infrastructure!
    ```


Note: This is for local development setup. Once terraform creates queues, appropriate AWS_SQS_URL and AWS_SQS_REGION will be added to .env and worker.env. Tested with **Terraform v0.10.8** as of this commit.