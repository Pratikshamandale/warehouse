# Motivation

Automate queues and deadLetter queues setup. This is where the workers pull payloads from.

# How to run

1. Create an `.env` file
    ```
    # Must have the appriopriate IAM permissions to manipulate SQS
    AWS_ACCESS_KEY_ID=<fill it in>
    AWS_SECRET_ACCESS_KEY=<fill it in>
    ```
1. Run `. ./setenv.sh`
2. Think of a name for your queue (`Q`) and your deadLetter queue (`DLQ`) based on the environment (`dev/local`, `staging`, `prod`) you are acting in, then:
    * `cd terraform`
    * `terraform plan -out plan.tfplan`
    * `terraform apply plan.tfplan`
    * For more details, refer to the inline comments in `terraform/main.tf`

# Challenges

The [warehouse-workers](https://github.com/ShoppinPal/warehouse-workers) project is meant to work in tandem with [warehouse](https://github.com/ShoppinPal/warehouse) which means that the current implementation lacks the following features:

1. Both `warehouse-workers` and `warehouse` should be provisioned and deployed via terraform
1. The provisioned Q should be automatically added to the environment variables for a `warehouse-workers` deployment
1. The provisioned Q should be automatically added to the environment variables for the corresponding [warehouse](https://github.com/ShoppinPal/warehouse) deployment