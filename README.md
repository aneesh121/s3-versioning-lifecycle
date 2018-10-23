# s3-versioning-lifecycle

<b>This is a CLI friendly guidline for setting up s3 versioning and lifecycle for your objects.</b>

<b>Get list of S3 buckets from Amazon Web Services</b>

``` $ aws s3api list-buckets --query 'Buckets[*].Name' | sed -e 's/[][]//g' -e 's/"//g' -e 's/,//g' -e '/^$/d' -e 's/^[ \t]*//;s/[ \t]*$//' ```

OR

``` $ aws s3 ls | awk {'print $3'} ```

<b>Get the Bucket versioning status</b>

``` aws s3api get-bucket-versioning --bucket "$bucket" | awk '/Status/ {print $2}' | sed 's/"//g' ```

<b>Enable Bucket Versioning</b>

``` aws s3api put-bucket-versioning --bucket "$bucket" --versioning-configuration Status=Enabled ```

<b>Apply Life cycle configuration </b>

``` aws s3api put-bucket-lifecycle --bucket "$bucket" --lifecycle-configuration file://lifecycle.json ```

<b>Reference : </b>

https://docs.aws.amazon.com/cli/latest/reference/s3api/get-bucket-lifecycle-configuration.html
https://docs.aws.amazon.com/cli/latest/reference/s3api/put-bucket-lifecycle.html
https://cloudacademy.com/blog/aws-s3-lifecycle-policies-simple-storage-service-management/
https://derflounder.wordpress.com/2017/06/30/automating-the-enablement-of-object-versioning-on-aws-s3-buckets/
