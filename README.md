# API Gateway IP Filtering

Use an API Gateway Resource Policy to restrict consumption of your APIs to certain IPs.

## AWS Costs

By following these instructions you will create an API Gateway API and a Lambda in your AWS account.
Consumption of the API Gateway endpoint and invocation of the Lambda will result in AWS costs.
It is recommended that you delete the CloudFormation for this example once you have finished experimenting with it.

## Getting Started

### Prerequisites

1. [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)

## Deploying to AWS

```
aws cloudformation deploy \
--template-file cloudformation.yaml \
--stack-name api-gateway-ip-filtering \
--capabilities CAPABILITY_IAM \
--parameter-overrides \
AllowedIpsList=<YOUR COMMA SEPARATED LIST OF ALLOWED IPS GO HERE>
```

## Consume the API

Retrieve your API Gateway URL using the [AWS Console](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-call-api.html#apigateway-how-to-call-rest-api)

```
curl https://<YOUR API GATEWAY URL GOES HERE>/live/api/example
```

If you invoke this from an allowed IP then you should receive the following response:

```
{
    "message": "Hello World"
}
```

If you invoke this from an IP that's not in the `AllowedIpsList` then you should receive the following response:

```
{
    "Message": "User: anonymous is not authorized to perform: execute-api:Invoke on resource: <YOU API GATEWAY API ARN>/live/GET/api/example"
}
```
 