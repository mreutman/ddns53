# ddns53

Dynamic DNS service using Amazon's Route 53 product.

## About

There exist externally hosted services that manage mapping and updating dynamic
IP addresses to domain names, but not near as many that can be run self hosted.
The ddns53 utility allows one to directly update the IP address a registered
domain name should point to provided that the domain is managed in Amazon's
Route 53. In order to acomplish this task, boto3, the official Python library
for accessing AWS, is leveraged.

Note, this utility is not by any means endoursed by Amazon and may violate the
terms of service with your internet service provider. The end user assumes
all responsiblity for the use of this software.

## Set Up

The following steps should briefly outline all that is needed to do in order
to get this utility to work.

1. Install Python.
```
sudo apt install python3
```
2. Install boto3.
```
pip3 install boto3
```
3. Configure AWS IAM user credentials (`~/.aws/credentials`).
```
[default]
aws_access_key_id = YOUR_ACCESS_KEY
aws_secret_access_key = YOUR_SECRET_KEY
```
4. Configure AWS region (`~/.aws/config`).
```
[default]
region=us-west-2
```

## Execution

To run the utility from the command line, all that is needed is to provide the
domain hosted in Amazon's Route 53 that is to be updated.
```
./ddns53 [DOMAIN]
```

For example, if the domain `foo.com` is to be targeted, the utlitlity would be
run as follows.
```
./ddns53 foo.com
```

For best results, this tool can be scheduled to run as a `cron` job to
automatically update the DNS address record if/when your ISP decides to assign
you a new IP address. For an example, here is an entry in `crontab` to run
every hour while logging any errors to a local file.
```
0 * * * * /home/pi/ddns53 foo.com >> /home/pi/ddns53.log 2>&1
```
