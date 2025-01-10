# NBA Game Day Notifications System

## **Overview**
The NBA Game Day Notifications System is a sophisticated alert mechanism designed to keep basketball enthusiasts updated with real-time game scores via SMS and Email. This system leverages **AWS Lambda**, **Amazon SNS**, **Amazon EventBridge**, and **NBA APIs** to deliver timely notifications.

---

## **Features**
- **Real-Time Updates**: Fetches live NBA game scores from an external API.
- **Multi-Channel Notifications**: Sends updates via SMS and Email using Amazon SNS.
- **Automated Scheduling**: Uses Amazon EventBridge to schedule regular updates.
- **Secure Architecture**: Implements least privilege IAM roles for enhanced security.

---

## **Prerequisites**
- **API Key**: Obtain a subscription and API Key from [sportsdata.io](https://sportsdata.io/).
- **AWS Account**: Ensure you have an AWS account with basic knowledge of AWS services and Python.

---

## **Architecture Diagram**
![Architecture Diagram](/images/arch.jpg)

---

## **Technologies Used**
- **Cloud Provider**: AWS
- **Core Services**: AWS Lambda, Amazon SNS, Amazon EventBridge
- **External API**: NBA Game API from SportsData.io
- **Programming Language**: Python 3.x
- **Security**: IAM roles with least privilege policies

---

## **Project Structure**
```bash
nba-game-day-notifications/
├── src/
│   ├── notifications.py              # Main Lambda function code
├── policies/
│   ├── sns_policy.json               # SNS publishing permissions
│   ├── eventbridge_policy.json       # EventBridge to Lambda permissions
│   └── lambda_policy.json            # Lambda execution role permissions
├── .gitignore
└── README.md                         # Project documentation
```

## **Setup Instruction**
## **Clone the Repository**
```
git clone https://github.com/yourusername/nba-game-day-notifications.git
cd nba-game-day-notifications
```
## **Create an SNS Topic**
1. Open the AWS Management Console.
2. Navigate to the SNS service.
3. Click Create Topic and select Standard.
4. Name the topic (e.g., **nba_notifications**) and note the ARN.
5. Click Create Topic.

## **Add Subscriptions to the SNS Topic**
1. Click on the topic name from the list.
2. Go to the Subscriptions tab and click Create subscription.
3. Choose a Protocol:
For **Email**: Enter a valid email address.
For **SMS**: Enter a valid phone number in international format.
4. Click **Create Subscription.**
5. Confirm the subscription via email if necessary.
   
## **Create the SNS Publish Policy**
1. Open the IAM service in the AWS Management Console.
2. Navigate to **Policies → Create Policy.**
3. Click **JSON** and paste the JSON policy from policies/sns_policy.json.
Replace REGION and ACCOUNT_ID with your AWS region and account ID.
Click Next: Tags, then Next: Review.
Name the policy (e.g., nba_sns_policy) and click Create Policy.

## **Create an IAM Role for Lambda**
1. Open the IAM service in the AWS Management Console.
2. Click Roles → Create Role.
3. Select AWS Service and choose Lambda.
4. Attach the following policies:
SNS Publish Policy (nba_sns_policy).
Lambda Basic Execution Role (AWSLambdaBasicExecutionRole).
5. Click Next: Tags, then Next: Review.
6. Name the role (e.g., nba_lambda_role) and click Create Role.
7. Copy the ARN of the role for use in the Lambda function.
   
## **Deploy the Lambda Function**
1. Open the AWS Management Console and navigate to the Lambda service.
2. Click **Create Function.**
3. Select **Author from Scratch.**
4. Enter a function name (e.g., **nba_notifications**).
5. Choose Python 3.x as the runtime.
6. Assign the IAM role created earlier (**nba_lambda_role**) to the function.
7. Under the Function Code section:
Copy the content of the **src/notifications.py** file from the repository.
Paste it into the inline code editor.
8. Under the **Environment Variables** section, add:
**NBA_API_KEY:** your NBA API key.
**SNS_TOPIC_ARN:** the ARN of the SNS topic created earlier.
 
  Click **Create Function.**
## **Set Up Automation with EventBridge**
1. Navigate to the EventBridge service in the AWS Management Console.
2. Go to **Rules → Create Rule.**
3. Select **Event Source**: Schedule.
4. Set the cron schedule for updates (e.g., hourly).
5. Under Targets, select the Lambda function (**nba_notifications**) and save the rule.
   
## **Test the System**
1. Open the Lambda function in the AWS Management Console.
2. Create a test event to simulate execution.
3. Run the function and check CloudWatch Logs for errors.
4. Verify that notifications are sent to the subscribed users.

## **Lessons Learned**
1. Building a notification system with AWS SNS and Lambda.
2. Implementing secure IAM roles with least privilege.
3. Automating workflows using Amazon EventBridge.
4. Integrating external APIs into cloud-based solutions.

