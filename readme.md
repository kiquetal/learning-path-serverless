#### AWS Lambda definitions

#### Difference IAM Resource Policy and IAM Execution Role

 - IAM Resource Policy: Permission to invoke the funciton
 - IAM Execution Role: Permission to access AWS resources

#### IAM Resource Policy

    Associated with a "push" event source such as Amazon API Gateway
    Created when you add a trigger to a lambda function
    Allows the event source to take the lambda:InvokeFunction action

#### IAM Execution Role

    Role selected or created when you create a lambda function
    Trust Policy that allows Lambda to AssumeRole
    Creator must have permission for iam:PassRole

