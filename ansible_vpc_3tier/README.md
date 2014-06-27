Deploy a three tier network in aws vpc with Ansible 1.7+
-----------------------------------------------------------

The vpc.yml playbook deploys a three tier network vpc in aws. The first tier is a web tier where instances
have public ip's and are directly reachable via internet.

The second and third tier are private only networks, instances here get private addresses hence they are only accesible
withinin the vpc.

A NAT instance is being deployed so that the instances in private network can access internet via this nat instance.
Security groups are also implemented so that traffic to these instances are controlled.

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


