---
title: AWS S3 Cannot Delete Objects (even with Full S3 Permissions)
date: 2022-09-07
tags: [cloud, AWS]
image: "s3.jpg"
---

I pulled my hair for 3 hours before solving this. Now here's the solution so that you don't have to pull yours.

Here's the scenario:
* There is a S3 bucket
* There is an IAM user whose purpose is to access the bucket (create/update/delete objects)
* The IAM user has full S3 permissions on the bucket
* The IAM user can create/update objects but cannot delete objects (WTF???)

Yes, you read that right. The IAM user has full **S3:*** permissions to access the bucket but it cannot delete objects. If you're not convinced, here's the terraform config of the policy attached to the IAM:

```terraform
data "aws_iam_policy_document" "bucket_permissions" {
  statement {
    actions   = ["kms:*"]
    resources = ["*"]
    effect = "Allow"
  }
  statement {
    actions   = ["s3:*"]
    resources = [
        aws_s3_bucket.bucket.arn,
        "${aws_s3_bucket.bucket.arn}/*",
    ]
    effect = "Allow"
  }
}
```

Finally I noticed something strange after over an hour of digging around.

![AWS S3 bucket object cannot be deleted AWS Key compromised](./compromised.png)

The IAM user has a policy attached to it that I hadn't seen before. I was pretty sure I didn't add it. A quick google search showed that when an AWS access key and secret key is leaked, and AWS discovers this leaked keys, they attach this policy to the IAM so that deletion permissions are revoked and the IAM cannot wreak havoc in the account.

Kudos to AWS for keeping an eye out for us. It would have been easier if there was a way to know this from the dashboard.

So finally, I created a new IAM user and attached a role to access the bucket. Everything worked fine.