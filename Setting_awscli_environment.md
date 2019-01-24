## Preparing aws tools

## On instances with Amazon Linux AMI, aws is pre-installed. In that case skip installation step and Go to configuration of aws.  
## pip is normally preloaded on systems by default. If not use below comand to install pip:
    sudo apt-get install -y python-pip 
    OR
    yum install -y python-pip
 
 ## Use pip to install awscli
    sudo pip install awscli
 
 
## Add the secret aws access key in config file: $HOME/.aws/config 
    aws_access_key_id = <access key id>
    aws_secret_access_key = <secret access key>
    region = us-west-1

 An alternative way is to configure the credentials using aws cli. Shoot following command from $HOME
 aws configure
 It is an interactive command and shall ask for access key ID, secret access key and default region.
 Sample output on my machine:

     C:\Users\Ashish> aws configure
     AWS Access Key ID [None]: ****************************
     AWS Secret Access Key [None]: *****************************
     Default region name [None]: ap-south-1   ## For mumbai
     Default output format [None]:           ## Just press Enter
     C:\Users\Ashish>

 Protect the file:
    
    $chmod 600 $HOME/.aws/config

 Tell your bash about it by adding this line in $HOME/.bashrc
    
    $export AWS_CONFIG_FILE=$HOME/.aws/config

 for installing auto-complete for aws commands. 
 This will enable you to auto-complete aws commands by hitting tab

    $which aws_completer
    It will give you path of aws_completer say "/usr/bin/aws_completer". Provide this path in following command:
    $complete -C '/usr/bin/aws_completer' aws

For some system aws_completer is in /usr/local/bin. Modify your command accordingly.
Check if evertything is working fine

    $aws ec2 describe-regions --output table

      ----------------------------------------------------------
      |                     DescribeRegions                    |
      +--------------------------------------------------------+
      ||                        Regions                       ||
      |+-----------------------------------+------------------+|
      ||             Endpoint              |   RegionName     ||
      |+-----------------------------------+------------------+|
      ||  ec2.ap-south-1.amazonaws.com     |  ap-south-1      ||
      ||  ec2.eu-west-2.amazonaws.com      |  eu-west-2       ||
      ||  ec2.eu-west-1.amazonaws.com      |  eu-west-1       ||
      ||  ec2.ap-northeast-2.amazonaws.com |  ap-northeast-2  ||
      ||  ec2.ap-northeast-1.amazonaws.com |  ap-northeast-1  ||
      ||  ec2.sa-east-1.amazonaws.com      |  sa-east-1       ||
      ||  ec2.ca-central-1.amazonaws.com   |  ca-central-1    ||
      ||  ec2.ap-southeast-1.amazonaws.com |  ap-southeast-1  ||
      ||  ec2.ap-southeast-2.amazonaws.com |  ap-southeast-2  ||
      ||  ec2.eu-central-1.amazonaws.com   |  eu-central-1    ||
      ||  ec2.us-east-1.amazonaws.com      |  us-east-1       ||
      ||  ec2.us-east-2.amazonaws.com      |  us-east-2       ||
      ||  ec2.us-west-1.amazonaws.com      |  us-west-1       ||
      ||  ec2.us-west-2.amazonaws.com      |  us-west-2       ||
      |+-----------------------------------+------------------+|

 aws command's output often gives Jason data, which is cumbersome to read to extract the desired Info.
 jq is used to parse Jason data.
 jq is not installed by default in Amazon Linux or Ubuntu. It can be installed as:

    sudo apt-get install jq

 Typical use of jq; The below command will extract name of the hosted zones only
    
    $ aws route53 list-hosted-zones | jq '.HostedZones[].Name'
    "epitech.nl."
    "awssystemadministration.com."

Some people prefer "--query" option than jq


###  Congratulation you are good to go to the next level.


