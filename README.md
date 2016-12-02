# Ansible: AWS EC2 instance control scripts

Scripts for starting and stopping AWS EC2 instances. You can place these scripts in your cron and manage instance usage during weekends for example.

## Requirements

* Make scripts executables

```shell
chmod +x ec2_start_instances.yml
chmod +x ec2_stop_instances.yml
```

* [Ansible](https://www.ansible.com/)
* [boto3](https://github.com/boto/boto3)

* Or just run:

```shell
virtualenv pyenv
pip install -r requirements.txt
```

## Variables

### AWS credentials

* [aws_config.yml](vars/aws_config.yml)

### Variable file

* [ec2_instances.yml](vars/ec2_instances.yml)
* AWS region:

```yaml
region: eu-west-1
```

* Instance IDs to control:

```yaml
instance_ids:
  - i-XXXXXX
  - i-XXXXXX
```

* Project name for control over `vars/ec2_instances<project>.yml`

```yaml
project: '_myProject'
```

## Running

* Start instances

```shell
./ec2_start_instances.yml
# or
./ec2_start_instances.yml -e project=<project>
```

* Stop instances

```shell
./ec2_stop_instances.yml
# or
./ec2_stop_instances.yml -e project=<project>
```

## Examples

Edit `/etc/crontab` and place the following lines for auto stop-start on the weekends. With `vars/ec2_instances_myProject.yml`:

```
0 1 15 ? * FRI *  ./ec2_stop_instances.yml -e project=_myProject
0 1 9 ? * MON *   ./ec2_start_instances.yml -e project=_myProject
```

* [HELP](http://www.cronmaker.com/)

# Author

* Carles San Agustin - carlessanagustin.com
* MIT [License](LICENSE)
