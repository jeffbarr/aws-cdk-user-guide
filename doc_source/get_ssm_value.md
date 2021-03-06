--------

This documentation is for the developer preview release \(public beta\) of the AWS Cloud Development Kit \(CDK\)\. Releases might lack important features and might have future breaking changes\.

--------

# Get a Value from a Systems Manager Parameter Store Variable<a name="get_ssm_value"></a>

You can get the value of an AWS Systems Manager Parameter Store variable, depending on whether you want the latest version of a plain string, a particular version of a plain string, or a particular version of a secret string\. It isn't possible to retrieve the latest version of a secure string\. To read the latest version of a secret, you have to read the secret from AWS Secrets Manager \(see [Get a Value from AWS Secrets Manager](passing_secrets_manager.md)\)\.

To read a particular version of a Systems Manager Parameter Store plain string value at AWS CloudFormation deployment time, use [ssm\.ParameterStoreString](https://awslabs.github.io/aws-cdk/refs/_aws-cdk_aws-ssm.html/#parameterstorestring)\. If you don't supply a `version` value, you get the latest version\.

```
import ssm = require('@aws-cdk/aws-ssm');

const parameterString = new ssm.ParameterStoreString(this, 'MyParameter', {
    parameterName: 'my-parameter-name',
    version: 1,
});

const myvalue = parameterString.stringValue;
```

To read a particular version of a Systems Manager Parameter Store `SecureString` value at AWS CloudFormation deployment time, use [ssm\.ParameterStoreSecureString](https://awslabs.github.io/aws-cdk/refs/_aws-cdk_aws-ssm.html/#parameterstoresecurestring)\. You must supply a `version` value\.

```
import ssm = require('@aws-cdk/aws-ssm');

const secureString = new ssm.ParameterStoreSecureString(this, 'MySecretParameter', {
    parameterName: 'my-secret-parameter-name',
    version: 1,
});

const myvalue = secureString.stringValue;
```