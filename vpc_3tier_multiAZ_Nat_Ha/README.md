Deploy a three tier Multi AZ network in aws vpc with NAT Instance in HA.  Ansible 1.7+
-------------------------------------------------------------------------

Pre-Requisite's:
---------------
Ansible 1.7+
AN IAM role with the following policy:

```

{
 "Statement": [
 {
 "Action": [
 "ec2:DescribeInstances",
 "ec2:CreateRoute",
 "ec2:ReplaceRoute",
 "ec2:StartInstances",
 "ec2:StopInstances"
 ],
 "Effect": "Allow",
 "Resource": "*"
 }
 ]
 }

```
and update the role name in envs/<env name>

Description
-----------



The vpc.yml playbook deploys a three tier multi AZ network vpc in aws with NAT instance in HA. The first tier is a web tier where instances
have public ip's and are directly reachable via internet it also hosts the NAT Instance.

The second and third tier are private only networks, instances here get private addresses hence they are only accesible
withinin the vpc.


To delpoy a vpc use the following command

```

ansible-playbook -i hosts vpc.yml -e environ=stage -vv

```

This would make ansible create a vpc based on the parameters specified in envs/stage (cidr block, number of instances etc..)

If multiple vpc's needs to be created just copy the envs/stage into a new file eg:(test) and change the parmaters as per your
need and run the ansible-playbook with parameter as the newly created filename EG:

```

ansible-playbook -i hosts vpc.yml -e environ=test -vv

```


