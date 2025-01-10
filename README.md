# ce8_assignment_2_16

Assignment 2.16

Requirements:

Given the Lambda function and metric filters created in the activity, use terraform to create the alarm.
Create a public github repository that has a terraform code, containing the answer to the above.
Submission is the url to your public github repository.

Answer:

resource "aws_cloudwatch_metric_alarm" "cloudwatch_alarm " {
  alarm_name          = "yl-info-count-breach"
  comparison_operator = "GreaterThanThreshold"
  evaluation_periods  = 1
  metric_name         = "info-count"
  namespace           = "/moviedb-api/yl"
  period              = 60
  statistic           = "Sum"
  threshold           = 10
  alarm_description   = " "
  actions_enabled     = "true"
  alarm_actions       = [aws_sns_topic.topic.arn]
}

resource "aws_sns_topic" "topic" {
  name = "yl_CloudWatch_Alarms_Topic"
}

resource "aws_sns_topic_subscription" "email-target" {
  topic_arn = aws_sns_topic.topic.arn
  protocol  = "email"
  endpoint  = "yllee9127@gmail.com"
}

