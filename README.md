# Axelerant-CloudAlarm
#Setup Alarm

RAM usage is greater than 60%, disk space usage is greater than 80%, or CPU usage greater than 70%. 
Create EC2 instance - name - Alarmos
Install httpd apache webserver  - yum install httpd -y
start and enable service 

![Capture](https://user-images.githubusercontent.com/51254973/123248913-142dd480-d506-11eb-8672-54d122fea420.PNG)

# CloudWatch
choose Alarms, Create Alarm.
Choose Select metric.
In the All metrics tab, choose EC2 metrics.
Choose a metric category (for example, Per-Instance Metrics).
Find the row with the instance that you want listed in the InstanceId column and CPUUtilization in the Metric Name column. Select the check box next to this row, and choose Select metric.
Under Specify metric and conditions, for Statistic choose Average, choose one of the predefined percentiles, or specify a custom percentile (for example, p95.45).
Choose a period (for example, 5 minutes).

For Whenever CPUUtilization is, specify Greater. Under than..., specify the threshold that is to trigger the alarm to go to ALARM state if the CPU utilization exceeds this percentage. For example, 70.
![cpu utilization](https://user-images.githubusercontent.com/51254973/123249484-a0d89280-d506-11eb-9f8f-741a17e8ccae.PNG)

#Also set SNS
Choose Next.

Under Notification, choose In alarm and select an SNS topic to notify when the alarm is in ALARM state

To have the alarm send multiple notifications for the same alarm state or for different alarm states, choose Add notification.

To have the alarm not send notifications, choose Remove.

When finished, choose Next.

Enter a name and description for the alarm. The name must contain only ASCII characters. Then choose Next.

Under Preview and create, confirm that the information and conditions are what you want, then choose Create alarm.

![SNS](https://user-images.githubusercontent.com/51254973/123249596-c1a0e800-d506-11eb-832a-986d92f6dbb7.PNG)

![subscripti](https://user-images.githubusercontent.com/51254973/123249614-c6659c00-d506-11eb-94aa-0dfdc5dc732a.PNG)

#from AWS CLi

aws cloudwatch put-metric-alarm --alarm-name cpu-mon --alarm-description "Alarm when CPU exceeds 70%" --metric-name CPUUtilization --namespace AWS/EC2 --statistic Average --period 300 --threshold 70 --comparison-operator GreaterThanThreshold --dimensions  Name=InstanceId,Value=i-12345678 --evaluation-periods 2 --alarm-actions arn:aws:sns:us-east-1:111122223333:my-topic --unit Percent

aws cloudwatch set-alarm-state --alarm-name cpu-mon --state-reason "initializing" --state-value ALARM
