# aws-boto3-s3-quickstart
## 前置条件
 - 自己创建好AKSK.
 - 自己创建好S3存储地址.

## 存入数据
```
!pip install boto3
import boto3

# 初始化S3客户端
s3_client = boto3.client(
    's3',
    aws_access_key_id='',
    aws_secret_access_key='',
    region_name='us-east-1'
)

# 指定要上传的文件
local_file_path = 'hello.txt'
bucket_name = 'testdata'
s3_file_key = 'hello.txt'

# 上传文件
s3_client.upload_file(local_file_path, bucket_name, s3_file_key)
print(f"File {local_file_path} has been uploaded to {bucket_name}/{s3_file_key}")
```

## 读取数据
```
import boto3
from botocore.exceptions import NoCredentialsError

# 初始化S3客户端
s3_client = boto3.client(
    's3',
    aws_access_key_id='',
    aws_secret_access_key='',
    region_name='us-east-1'
)

bucket_name = 'testdata'  # 你的S3存储桶名称
file_key = 'hello.txt'  # S3存储桶中文件的键名

try:
    # 生成预签名URL
    presigned_url = s3_client.generate_presigned_url(
        'get_object',
        Params={'Bucket': bucket_name, 'Key': file_key},
        ExpiresIn=3600  # 链接有效期，单位为秒
    )
    print(f"Presigned URL to download 'hello.txt': {presigned_url}")
except NoCredentialsError:
    print("Credentials not available")

```
