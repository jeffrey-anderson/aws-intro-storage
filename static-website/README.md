# Create a static website using Amazon S3

## Prerequisites

* You are logged into [AWS console](https://console.aws.amazon.com/)
* You are in the desired region

## Demo

### 1. Create a bucket for your website

1. From the AWS Services menu choose **S3**
1. Press **+ Create bucket**
1. Name your bucket (remember your S3 bucket names must be globally unique)
1. Check or change the region
1. Press **Create**

### 2. Upload the content

1. Click on the bucket name
1. Choose **Upload**
1. Using drag and drop or the **Add files** button, add [index.html](./index.html) from this directory
1. Click **Upload**
1. After a few moments you will see index.html as the only file in the bucket

### 3. Turn on static website hosting

1. From the bucket's file listing choose **Properties**
1. Click on Static website hosting
1. Make a note of the "Endpoint" URL
1. Choose "Use this bucket to host a website"
1. Enter "index.html" in the index document field
1. Press **Save**

### 4. Allow access to your website

Visit the endpoint URL from the previous step. If you forgot it, click on Static website hosting 
then click on the endpoint URL. Instead of a web page, you should get a "403 Forbidden" page. 

To correct this, we need to give public access to the files in our bucket.

1. Click on the **Permissions** tab
1. Click on **Bucket Policy**
1. Copy the JSON policy document shown below into the Bucket policy editor field
1. Replace "your-bucket-name-here" with your actual bucket name
1. Make sure the rest of the resource property string is unchanged including the trailing /*
1. Click **Save**

```
{
  "Version":"2012-10-17",
  "Statement":[{
	"Sid":"PublicReadGetObject",
        "Effect":"Allow",
	  "Principal": "*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::your-bucket-name-here/*"
      ]
    }
  ]
}
```

NOTE: You should get a "this bucket has public access" warning which, in this case, is fine since we must
provide public access for our website to work. 

### 5. Verify the website is now accessible

1. Revist or refresh the bucket endpoint URL and you should see a snazzy new web page! 

# Optional Cleanup

Follow the steps below to remove everything created above.  

1. From the AWS Services menu choose **S3**
1. From the list of buckets, click row (not on the name) for the bucket you created above
1. With the row highlighted, click **Delete bucket**
1. Type the name of the bucket in the Delete bucket dialog
1. Click **Confirm**
