AWS CloudWatch Monitoring and Alerting Project

Project Overview

This project demonstrates the implementation of AWS CloudWatch monitoring, logging, dashboards, and alarm notifications for an EC2 instance. The setup includes CPU utilization monitoring, CloudWatch dashboards, SNS email alerts, CloudTrail integration, and CloudWatch Logs configuration.

The project was implemented in the AWS Asia Pacific (Mumbai) Region using Amazon EC2, Amazon CloudWatch, Amazon SNS, and AWS CloudTrail services.


---

Objectives

Monitor EC2 CPU utilization in real time

Configure CloudWatch alarms based on CPU thresholds

Receive email notifications using Amazon SNS

Create custom CloudWatch dashboards

Collect and view system logs using CloudWatch Logs

Track AWS account activity using CloudTrail

Understand infrastructure monitoring and observability concepts



---

AWS Services Used

Service	Purpose

Amazon EC2	Virtual server instance
Amazon CloudWatch	Monitoring metrics, logs, dashboards, alarms
Amazon SNS	Email notifications for alarms
AWS CloudTrail	API activity tracking
IAM	Permissions and access management



---

Architecture

EC2 Instance sends metrics and logs to CloudWatch.

CloudWatch:

Stores metrics

Displays dashboards

Creates alarms

Triggers SNS notifications


SNS:

Sends email alerts when alarm threshold is crossed


CloudTrail:

Captures AWS API events and management activities



---

Step 1: Launch EC2 Instance

Instance Configuration

Parameter	Value

Instance Type	t2.micro
Operating System	Amazon Linux
Region	ap-south-1 (Mumbai)


Verification

After launching the instance:

1. Connect using SSH


2. Verify instance is running


3. Confirm internet connectivity



Example command:

ping google.com


---

Step 2: Install CloudWatch Agent

Install Agent

sudo yum update -y
sudo yum install amazon-cloudwatch-agent -y

Configure Agent

Run the configuration wizard:

sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard

During configuration:

Enable metrics collection

Enable logs collection

Select CPU, disk, and memory metrics

Configure log files



---

Step 3: Start CloudWatch Agent

sudo systemctl enable amazon-cloudwatch-agent
sudo systemctl start amazon-cloudwatch-agent

Verify Agent Status

sudo systemctl status amazon-cloudwatch-agent


---

Step 4: Create SNS Topic

Create Topic

1. Open Amazon SNS Console


2. Create Topic


3. Select Standard Topic


4. Topic Name:



cpu-alert-topic


---

Step 5: Create Email Subscription

1. Open the SNS topic


2. Create subscription


3. Protocol: Email


4. Enter email address


5. Confirm subscription from email inbox




---

Step 6: Create CloudWatch Alarm

Alarm Configuration

Setting	Value

Metric	CPUUtilization
Threshold Type	Static
Condition	Greater than or equal to
Threshold Value	3%
Evaluation Period	1 minute
Notification Target	SNS Topic



---

Alarm Logic

The alarm changes state when:

CPUUtilization >= 3%

for:

1 datapoint within 1 minute


---

Step 7: Trigger Alarm

To increase CPU usage and test alarm:

sudo yum install stress -y
stress --cpu 2 --timeout 120

This artificially increases CPU utilization.


---

Step 8: Verify Alarm State

CloudWatch Alarm states:

State	Meaning

OK	Metric below threshold
ALARM	Metric exceeded threshold
INSUFFICIENT_DATA	No metric data available



---

Alarm Email Notification

When CPU utilization exceeded the threshold:

CloudWatch triggered the alarm

SNS sent an email notification

Alarm transitioned from OK to ALARM


Example notification details:

Alarm Name: alert-cpu-utilisation

Threshold: 3%

Triggered Value: 11.25%



---

Step 9: Create CloudWatch Dashboard

Dashboard Features

The dashboard contains:

CPU Utilization

CPU Credit Usage

CPU Credit Balance

EBS Write Bytes

Disk Metrics

System Metrics


Dashboard Benefits

Real-time monitoring

Centralized visibility

Infrastructure health tracking

Easy troubleshooting



---

Step 10: Configure CloudWatch Logs

Logs Collected

Examples:

Syslog

Systemd logs

EC2 system activity

Agent logs


View Logs

Navigate to:

CloudWatch → Logs → Log Groups

Example Log Group:

syslog


---

Step 11: Configure CloudTrail

Purpose

CloudTrail records:

AWS API calls

User activity

Resource changes

Account operations


Trail Configuration

Setting	Value

Trail Type	Multi-region
Region	Mumbai
Log Storage	CloudWatch Logs



---

Observations

Successful Alarm Trigger

The CPU alarm successfully:

Detected high CPU usage

Entered ALARM state

Sent SNS email notification


CloudWatch Dashboard

Dashboard displayed:

Real-time CPU metrics

EBS statistics

Credit utilization

Performance data


CloudWatch Logs

Logs were successfully collected from:

EC2 instance

System services

CloudWatch Agent


CloudTrail Integration

CloudTrail successfully tracked:

AWS management events

Console activities

API operations



---

Issues Encountered

No Data Available in Dashboard

Cause

Metric namespace mismatch or incorrect time range.

Solution

Adjust dashboard time range

Verify CloudWatch Agent configuration

Confirm correct namespace selection



---

Alarm Showing Insufficient Data

Cause

Metrics were not being received initially.

Solution

Restart CloudWatch Agent

Verify IAM permissions

Wait for metric propagation



---

IAM Permissions Required

Attach the following policy to the EC2 instance role:

CloudWatchAgentServerPolicy


---

Key Learning Outcomes

Practical understanding of AWS monitoring services

CloudWatch metrics and alarms configuration

SNS notification workflow

Log management using CloudWatch Logs

Infrastructure observability concepts

CloudTrail auditing and activity tracking

Real-time dashboard creation



---

Commands Used

Install CloudWatch Agent

sudo yum install amazon-cloudwatch-agent -y

Start Agent

sudo systemctl start amazon-cloudwatch-agent

Check Status

sudo systemctl status amazon-cloudwatch-agent

Install Stress Tool

sudo yum install stress -y

Generate CPU Load

stress --cpu 2 --timeout 120


---

Project Outcome

Successfully implemented a complete AWS monitoring and alerting solution using:

Amazon CloudWatch

Amazon SNS

AWS CloudTrail

CloudWatch Logs

EC2 Monitoring Dashboards


The system was able to:

Monitor infrastructure metrics

Generate alarms automatically

Send real-time email alerts

Store and analyze logs

Track AWS activities



---

Future Enhancements

Add memory utilization monitoring

Configure Auto Scaling triggers

Integrate Lambda for automated remediation

Create custom metrics

Add Slack or Microsoft Teams notifications

Implement centralized logging architecture



---

Conclusion

This project demonstrates a practical implementation of AWS observability and monitoring services. By integrating CloudWatch, SNS, Logs, and CloudTrail, the infrastructure becomes easier to monitor, troubleshoot, and maintain.

The setup provides:

Real-time monitoring

Automated alerting

Centralized logging

Activity auditing
<img width="1359" height="585" alt="1000180640" src="https://github.com/user-attachments/assets/4db98a9a-a969-488f-aae8-4cdd167e1af9" />
<img width="1362" height="585" alt="1000180626" src="https://github.com/user-attachments/assets/0eb921aa-1420-4ba3-885e-af80252f205b" />
<img width="1359" height="586" alt="1000180627" src="https://github.com/user-attachments/assets/9aaa02e7-507f-4dc0-ae98-7bde026dff40" />
<img width="1357" height="596" alt="1000180628" src="https://github.com/user-attachments/assets/9844de81-d179-43a0-a021-244543d7fb0f" />
<img width="1356" height="590" alt="1000180629" src="https://github.com/user-attachments/assets/926a65c8-a1ec-40af-a2a2-b7c631604773" />
<img width="1357" height="588" alt="1000180630" src="https://github.com/user-attachments/assets/155743d8-cf6a-4180-8a23-86a556dea4f8" />
<img width="720" height="924" alt="1000180624" src="https://github.com/user-attachments/assets/6f224f1b-41c4-49ba-9bca-0c56f3d200d2" />
<img width="1355" height="584" alt="1000180637" src="https://github.com/user-attachments/assets/c02174d4-d6de-4370-a8a7-4fd7a73dce48" />



