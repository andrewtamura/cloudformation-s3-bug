# Cloudformation S3 Bucket Bug
An S3 bucket with the following properties cannot be created by a Cloudformation
template.

- [`AccelerateConfiguration`](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket.html#cfn-s3-bucket-accelerateconfiguration)
- [`VersioningConfiguration`](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket.html#cfn-s3-bucket-versioning)
- [`CorsConfiguration`](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket.html#cfn-s3-bucket-crossoriginconfig)
- [`BucketEncryption`](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket.html#cfn-s3-bucket-bucketencryption)

See [template.yaml](./template.yaml) for the full Cloudformation template.

# Deploy Stack
```
aws cloudformation deploy --template-file template.yaml \
    --stack-name  s3-bucket-bug \
    --capabilities CAPABILITY_IAM 
```

# Cloudformation Error
Your stack will fail to create the S3 bucket with the error message

```
A conflicting conditional operation is currently in progress against this resource. Please try again.
```

![alt error screenshot][screenshot]

# Workaround
Modify your template so that is includes a single S3 property and deploy that
stack. After it succeeds, continue to add properties to your stack one at a time
deploying each changeset as you go. Eventually your template and stack will have
all the properties that you want.

[screenshot]: ./screenshot.png
