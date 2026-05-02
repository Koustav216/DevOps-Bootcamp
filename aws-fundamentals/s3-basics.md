# AWS S3

## What is Amazon S3?

Simple Storage Service is a scalable and secure cloud storage service provided by Amazon Web Services (AWS). It allows us to store and retrieve any amount of data from anywhere on the web.

> S3 is not a filesystem. S3 is object storage.

## What are S3 buckets?
S3 buckets are containers for storing objects (files) in Amazon S3. Each bucket has a unique name globally. The bucket name is part of the URL. We cannot rename a bucket. A bucket is created in one AWS region. It is the highest-level namespace in S3.

## Objects
Objects are the fundamental entities stored in Amazon S3. Objects consist of object data and metadata. The metadata is a set of name-value pairs that describe the object.

An object is uniquely identified within a bucket by a key (name) and a version ID (if S3 Versioning is enabled on the bucket).

## Keys
An object key (or key name) is the unique identifier for an object within a bucket. Every object in a bucket has exactly one key. The combination of a bucket, object key, and optionally, version ID (if S3 Versioning is enabled for the bucket) uniquely identify each object. So we can think of Amazon S3 as a basic data map between "bucket + key + version" and the object itself.

## How data is stored
When we upload an object:
- S3 automatically replicates it across multiple Availability Zones
- You configure nothing

**Important Facts**
- S3 buckets are created in a region
- Data stays in that region unless we replicate it
- The namespace is global, not the data

> Durability: 11 nines (99.999999999%)

## Key benefits of S3 buckets

S3 buckets offer several advantages, including:

- Durability and availability: S3 provides high durability and availability for your data.

- Scalability: We can store and retrieve any amount of data without worrying about capacity constraints. Each object can be up to 50 TB in size.

- Security: S3 offers multiple security features such as encryption, access control, and audit logging.

- Performance: S3 is designed to deliver high performance for data retrieval and storage operations.
    
- Cost-effective: S3 offers cost-effective storage options and pricing models based on our usage patterns.

## S3 Bucket Types
Amazon S3 supports four types of buckets—general purpose buckets, directory buckets, table buckets, and vector buckets. Each type of bucket provides a unique set of features for different use cases. Check out [this](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#BasicsBucket)

## Working with Metadata
There are two kinds of object metadata in Amazon S3: system-defined metadata and user-defined metadata. System-defined metadata includes metadata such as the object's creation date, size, and storage class. User-defined metadata is metadata that we can choose to set at the time that we upload an object. Check out the [docs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingMetadata.html)

## S3 Versioning
We can use S3 Versioning to keep multiple variants of an object in the same bucket. With S3 Versioning, we can preserve, retrieve, and restore every version of every object stored in our buckets. We can easily recover from both unintended user actions and application failures. For more info, check out [this](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html)

## Uploading Objects
When we upload a file to Amazon S3, it is stored as an S3 object. We can upload any file type—images, backups, data, movies, and so on—into an S3 bucket.  Objects consist of the file data and metadata that describes the object. We can have an unlimited number of objects in a bucket. The maximum size of a file that we can upload by using the Amazon S3 console is 160 GB. To upload a file larger than 160 GB, we should use the AWS Command Line Interface (AWS CLI), AWS SDKs, or Amazon S3 REST API. For more info, check out [this](https://docs.aws.amazon.com/AmazonS3/latest/userguide/upload-objects.html). 

## Multipart Uploads
The multipart upload API operation is designed to improve the upload experience for larger objects. We can upload an object in parts. These object parts can be uploaded independently, in any order, and in parallel. Multipart uploads also enable resumable uploads in case of failures. For more info, checkout [this](https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html)

## Data Replication
We can use replication to enable automatic, asynchronous copying of objects across Amazon S3 buckets. Buckets that are configured for object replication can be owned by the same AWS account or by different accounts. We can replicate objects to a single destination bucket or to multiple destination buckets. The destination buckets can be in different AWS Regions or within the same Region as the source bucket. Cross-Region Replication (CRR) provides disaster recovery and compliance benefits, while Same-Region Replication (SRR) can be used for data resilience and low-latency access. For more info, check out [this](https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication.html)

## Lifecycle management
Lifecycle management allows us to define rules for transitioning objects between different storage classes or deleting them automatically based on predefined criteria.
For example, we can move infrequently accessed data to a lower-cost storage class after a specified time or delete objects after a certain retention period.


## Advanced S3 Bucket Features

- S3 Event Notifications and Triggers

  S3 event notifications allow you to configure actions when specific events occur in an S3 bucket. For example, you can trigger AWS Lambda functions, send messages to Amazon Simple Queue Service (SQS), or invoke other services using Amazon SNS when an object is created or deleted.

- S3 Batch Operations

  S3 Batch Operations allow you to perform large-scale batch operations on objects, such as copying, tagging, or deleting, across multiple buckets. It simplifies managing large datasets and automates tasks that would otherwise be time-consuming.

## Security and Compliance in S3 Buckets

- S3 bucket security considerations
  Ensure that S3 bucket policies, access control, and encryption settings are appropriately configured. Regularly monitor and audit access logs for unauthorized activities.

- Data encryption at rest and in transit

  Encrypt data at rest using server-side encryption (SSE) options provided by S3. Additionally, enable encryption in transit by using SSL/TLS for data transfers. SSE options include SSE-S3 (Amazon-managed keys), SSE-KMS (AWS Key Management Service), and SSE-C (customer-provided keys).

- Access logging and monitoring

  Enable access logging to capture detailed records of requests made to your S3 bucket. Monitor access logs and configure alerts to detect any suspicious activities or unauthorized access attempts.


## References
- [Features of S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#S3Features)
- [Data Encryption](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html)