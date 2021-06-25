# Instruções para atividade prática
Repositório para a Live de 24/06/2021

### Kinesis Delivery Stream

- AWS Console -> Kinesis -> Create Firehose Delivery Stream "StreamName" -> Direct PUT -> Next -> Choose Destination -> Create S3 Bucket “covid-vaccines-logs-diolive” -> Configure settings -> buffer size 5mb -> buffer interval 60s -> IAM Role -> create new role -> Review and create

### EC2

- AWS Console -> EC2 -> Amazon Linux 2 AMI -> t2micro -> review and launch -> create new key pair -> download .pem file -> download putty -> puttygen -> load.pem file -> save .ppk file -> putty copy dns -> paste hostname -> SSH -> auth -> load ppk file -> login “ec2-user”

  - _sudo yum install -y aws-kinesis-agent_
  - _sudo yum install -y git_
  - _git clone https://github.com/cassianobrexbit/dio-live-aws-bigdata-2.git_
  - _unzip Dataset.zip_
  - _chmod a+x LogGenerator.py_
  - _nano LogGenerator.py_
  - _less country_vaccinations.csv_
  - _sudo mkdir /var/log/diolive_
  - _cd /etc/aws-kinesis_
  - _sudo nano agent.json_
  - Copiar conteúdo do arquivo agent.json
  - agent.json -> "kinesis.endpoint": "kinesis.<region>.amazonaws.com"
  
- AWS Console -> EC2 -> Instances -> Select Instance -> Security -> Modify IAM Role -> Create New Role -> EC2 -> Administrator Access -> rolename “ec2-admin-role” -> save
  - _sudo service aws-kinesis-agent start_
  - _sudo chkconfig aws-kinesis-agent on_ (start with instance)
  - _cd ~_
  - _sudo ./LogGenerator.py 500000_
  - _tail -f /var/log/aws-kinesis-agent/aws-kinesis-agent.log_

### S3
- AWS Console -> S3 -> select bucket -> selecionar arquivo e download

### SSH EC2
  - _sudo service aws-kinesis-agent restart_
  - _sudo ./LogGenerator.py_
  - _tail -f /var/log/aws-kinesis-agent/aws-kinesis-agent.log_
  - AWS Console -> Kinesis Streams -> select stream -> monitoring
  
### AWS Glue
- AWS Console -> glue databrew -> create new project -> create new role -> create project
- Create dataset -> S3 -> formato CSV
