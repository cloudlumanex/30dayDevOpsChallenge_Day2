# NBA Game Day Notifications / Sports Alerts System

## Architectural Drawing
![Screenshot 2025-01-08 070014](https://github.com/user-attachments/assets/073dd5a8-8b9f-4c31-abc0-b233fbf0610f)

This project is a real-time alert system that delivers NBA match day score notifications to subscribed users via SMS and email. It utilizes Amazon SNS, AWS Lambda, Python, Amazon EventBridge, and NBA APIs to keep sports fans informed with the latest game updates. The project showcases cloud computing concepts and effective notification delivery methods.


![Screenshot 2025-01-08 164718](https://github.com/user-attachments/assets/003f65fd-af31-48af-964e-145019b99d11)

![Screenshot 2025-01-08 165103](https://github.com/user-attachments/assets/c5a60e6e-6242-487d-8541-a5acf2b2f1cf)


# SETUP 
Create an SNS Topic
1. Open the AWS Management Console.
2. Navigate to the SNS service.
3. Click 'Create Topic' and select 'Standard' as the topic type.
4. Name the topic (e.g., gd_topic) and note the ARN.
5. Click 'Create Topic'.

Add Subscriptions to the SNS Topic
1. Click on the topic name from the list.
2. Navigate to the Subscriptions tab and click 'Create subscription'.
3. Select a Protocol:
   - For Email: Choose Email and enter a valid email address.
   - For SMS: Choose SMS and enter a valid phone number in international format (e.g., +234123456789 for Nigerian numbers).
4. Click 'Create Subscription'.
5. If you added an Email subscription:
   - Check the inbox of the provided email address and confirm the subscription by clicking the confirmation link.
   - For SMS, the subscription will be immediately active after creation.

Create the SNS Publish Policy
1. Open the IAM service in the AWS Management Console.
2. Navigate to Policies → Create Policy.
3. Click 'JSON' and paste the JSON policy from gd_sns_policy.json file.
4. Replace REGION and ACCOUNT_ID with your AWS region and account ID.
5. Click 'Next: Tags' (you can skip adding tags).
6. Click 'Next: Review'.
7. Enter a name for the policy (e.g., gd_sns_policy).
8. Review and click 'Create Policy'.

Create an IAM Role for Lambda
1. Open the IAM service in the AWS Management Console.
2. Click 'Roles' → 'Create Role'.
3. Select 'AWS Service' and choose 'Lambda'.
4. Attach the following policies:
   - SNS Publish Policy (matchinfo_sns_policy) created in the previous step.
   - Lambda Basic Execution Role (AWSLambdaBasicExecutionRole) (an AWS managed policy).
5. Click 'Next: Tags' (you can skip adding tags).
6. Click 'Next: Review'.
7. Enter a name for the role (e.g., matchinfo_lambda_role).
8. Review and click 'Create Role'.
9. Copy and save the ARN of the role for use in the Lambda function.

Deploy the Lambda Function
1. Open the AWS Management Console and navigate to the Lambda service.
2. Click 'Create Function'.
3. Select 'Author from Scratch'.
4. Enter a function name (e.g., matchinfo_notifications).
5. Choose Python 3.x as the runtime.
6. Assign the IAM role created earlier (matchinfo_lambda_role) to the function.
7. Under the Function Code section:
   - Copy the content of the src/matchinfo_notifications.py file from the repository.
   - Paste it into the inline code editor.
8. Under the Environment Variables section, add:
   - NBA_API_KEY: your NBA API key.
   - SNS_TOPIC_ARN: the ARN of the SNS topic created earlier.
9. Click 'Create Function'.

Set Up Automation with EventBridge
1. Navigate to the EventBridge service in the AWS Management Console.
2. Go to Rules → Create Rule.
3. Select Event Source: Schedule.
4. Set the cron schedule for when you want updates (e.g., hourly Nigerian time).
5. Under Targets, select the Lambda function (matchinfo_notifications) and save the rule.

Test the System
1. Open the Lambda function in the AWS Management Console.
2. Create a test event to simulate execution.
3. Run the function and check CloudWatch Logs for errors.
4. Verify that SMS notifications are sent to the subscribed users.

What i Learned
- Designing a notification system with AWS SNS and Lambda.
- Securing AWS services with least privilege IAM policies.
- Automating workflows using EventBridge.
- Integrating external APIs into cloud-based workflows.







