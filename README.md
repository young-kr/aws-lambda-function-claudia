# aws-lambda-function-claudia
Deployment AWS Lambda function with ClaudiaJS

1. Make directory for AWS Lambda Function.
ex) mkdir aws-lambda-function-test && cd aws-lambda-function-test

2. Initialize directory. The package name will be AWS Lambda Function name and AWS role name refer the package name too.
ex) npm init

3. Install node modules what you need. In this case I'm going to use AWS Layer for share node_modules to another AWS Lambda functions. You can see how to make AWS Lambda Layer on https://github.com/young-kr/aws-lambda-layer-claudia
You have to install node modules with optional package.
ex) $ npm i -O moment

4. Now create app.js and write code below.
  const moment = require('moment');
  
  exports.handler = async (event, context) => {
    try {
      return {code: "200", message: "Success - " + moment().format()};
    } catch(error) {
      return {code: "400", message: "Error"};
    }
  };

5. Install ClaudiaJS
ex) $ npm i -g claudiajs

6. Generate AWS Lambda wrapper with ClaudiaJS
ex) $ claudia generate-serverless-express-proxy --express-module app

7. Set up AWS credential
ex) cd ~ && mkdir .aws && cd .aws && vi credentials
  [default]
  aws_access_key_id = ENTER_YOUR_PRIMARY_ACCESS_KEY_ID
  aws_secret_access_key = ENTER_YOUR_PRIMARY_SECRET_ACCESS_KEY

  [young]
  aws_access_key_id = ENTER_YOUR_SECONDARY_ACCESS_KEY_ID
  aws_secret_access_key = ENTER_YOUR_SECONDARY_SECRET_ACCESS_KEY

8. Deploy this Express app with AWS API Gateway and AWS Lambda Function. ## Excludes optional packages.
ex) $ claudia create --handler lambda.handler --deploy-proxy-api --region ap-northeast-2 --profile young --no-optional-dependencies

9. Now you can see the endpoint of your app on end of the logs.
