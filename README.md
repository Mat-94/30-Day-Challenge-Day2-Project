NBA Game Day Notifications / Sports Alerts System

Project Overview
The NBA Game Day Notifications System is a real-time alert platform designed to deliver live NBA game updates directly to users via SMS and Email. Built using AWS services such as Amazon SNS, AWS Lambda, Amazon EventBridge, and Python, along with external NBA APIs, this project ensures sports enthusiasts receive timely and accurate game-day information. It showcases modern cloud computing principles, efficient event-driven architecture, and robust notification mechanisms.

Key Features:

Real-Time Score Updates: Fetch live NBA game scores from an external API.

Automated Notifications: Send formatted game updates via SMS and Email using Amazon SNS.

Event-Driven Architecture: Utilize Amazon EventBridge for automated scheduling and event management.

Scalable and Secure Design: Implement IAM roles adhering to the principle of least privilege for enhanced security.

User Subscription Management: Allow users to subscribe and manage their notification preferences seamlessly.

Prerequisites:

Active subscription and API Key from sportsdata.io

AWS Account with permissions for SNS, Lambda, and EventBridge

Basic knowledge of AWS services and Python programming

Technologies
Cloud Provider: AWS
Core Services: SNS, Lambda, EventBridge
External API: NBA Game API (SportsData.io)
Programming Language: Python 3.x
IAM Security:
Least privilege policies for Lambda, SNS, and EventBridge.

Setup Instructions
Clone the Repository
git clone https://github.com/ifeanyiro9/game-day-notifications.git
cd game-day-notifications
Create an SNS Topic
Open the AWS Management Console.
Navigate to the SNS service.
Click Create Topic and select Standard as the topic type.
Name the topic (e.g., gd_topic) and note the ARN.
Click Create Topic.
Add Subscriptions to the SNS Topic
After creating the topic, click on the topic name from the list.
Navigate to the Subscriptions tab and click Create subscription.
Select a Protocol:
For Email:
Choose Email.
Enter a valid email address.
For SMS (phone number):
Choose SMS.
Enter a valid phone number in international format (e.g., +1234567890).
Click Create Subscription.
If you added an Email subscription:
Check the inbox of the provided email address.
Confirm the subscription by clicking the confirmation link in the email.
For SMS, the subscription will be immediately active after creation.
Create the SNS Publish Policy
Open the IAM service in the AWS Management Console.
Navigate to Policies → Create Policy.
Click JSON and paste the JSON policy from gd_sns_policy.json file
Replace REGION and ACCOUNT_ID with your AWS region and account ID.
Click Next: Tags (you can skip adding tags).
Click Next: Review.
Enter a name for the policy (e.g., gd_sns_policy).
Review and click Create Policy.
Create an IAM Role for Lambda
Open the IAM service in the AWS Management Console.
Click Roles → Create Role.
Select AWS Service and choose Lambda.
Attach the following policies:
SNS Publish Policy (gd_sns_policy) (created in the previous step).
Lambda Basic Execution Role (AWSLambdaBasicExecutionRole) (an AWS managed policy).
Click Next: Tags (you can skip adding tags).
Click Next: Review.
Enter a name for the role (e.g., gd_role).
Review and click Create Role.
Copy and save the ARN of the role for use in the Lambda function.
Deploy the Lambda Function
Open the AWS Management Console and navigate to the Lambda service.
Click Create Function.
Select Author from Scratch.
Enter a function name (e.g., gd_notifications).
Choose Python 3.x as the runtime.
Assign the IAM role created earlier (gd_role) to the function.
Under the Function Code section:
Copy the content of the src/gd_notifications.py file from the repository.
Paste it into the inline code editor.
Under the Environment Variables section, add the following:
NBA_API_KEY: your NBA API key.
SNS_TOPIC_ARN: the ARN of the SNS topic created earlier.
Click Create Function.
Set Up Automation with Eventbridge
Navigate to the Eventbridge service in the AWS Management Console.
Go to Rules → Create Rule.
Select Event Source: Schedule.
Set the cron schedule for when you want updates (e.g., hourly).
Under Targets, select the Lambda function (gd_notifications) and save the rule.
Test the System
Open the Lambda function in the AWS Management Console.
Create a test event to simulate execution.
Run the function and check CloudWatch Logs for errors.
Verify that SMS notifications are sent to the subscribed users.
What We Learned
Designing a notification system with AWS SNS and Lambda.
Securing AWS services with least privilege IAM policies.
Automating workflows using EventBridge.
Integrating external APIs into cloud-based workflows.
Future Enhancements
Add NFL score alerts for extended functionality.
Store user preferences (teams, game types) in DynamoDB for personalized alerts.
Implement a web UI
