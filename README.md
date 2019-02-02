# AWS VPC

![cli](https://github.com/abiydv/ref-docs/blob/master/images/logos/aws-cli_small.png)
![cf](https://github.com/abiydv/ref-docs/blob/master/images/logos/aws-cf_small.png)
![vpc](https://github.com/abiydv/ref-docs/blob/master/images/logos/aws-vpc_small.png)

Use this template to create a VPC with 2 public and 2 private subnets. 

Specify VPC Cidr and Subnet Cidr bit to get desired number of IPs distributed in the 4 subnets. 
Some reference values below 
> - VPCcidr 10.0.0.0/26 and Cidrbit 4 - will generate 4 /28 subnets with 14 usable hosts in each
> - VPCcidr 10.0.0.0/24 and Cidrbit 6 - will generate 4 /26 subnets with 62 usable hosts in each
> - VPCcidr 10.0.0.0/22 and Cidrbit 8 - will generate 4 /24 subnets with 254 usable hosts in each

## Prerequisites
(Optional) Configure AWS Cli access for the AWS account you want to create the VPC in. You can skip this if you want to create the stack from the Cloudformation console
```
$ aws configure --profile aws-dev-account
AWS Access Key ID [None]: ACCESS_KEY
AWS Secret Access Key [None]: SECRET_KEY
Default region name [None]: us-east-1
Default output format [None]:
```

## How to use
Checkout the repository and execute from cli
```
cd cloudformation/vpc/
aws cloudformation validate-template --template-body file://vpc-stack.yaml \
  --profile aws-dev-account --region us-east-1 
```
This should display the parameters - validating the template syntax is fine. Next, create the stack

```
aws cloudformation create-stack --stack-name vpc-stack --template-body file://vpc-stack.yaml \
  --parameters ParameterKey=VPCcidr,ParameterValue="10.0.0.0/26" \
               ParameterKey=CidrBit,ParameterValue="4" \
               ParameterKey=EnvironmentName,ParameterValue="dev" \
  --profile  aws-dev-account --region us-east-1
```
Alternatively, copy the template and create the stack from Cloudformation console.

## Contact
Drop me a note or open an issue if something doesn't work out.

Cheers! :thumbsup:
