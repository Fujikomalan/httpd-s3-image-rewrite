### Load Website Image From S3 bucket

###### - Package Installation
.
```sh
# yum install httpd -y
# systemctl enable httpd -y
# systemctl restart httpd
```


###### - IAM Bucket Policy To Make Bucket Public 
.
```sh
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::ENTER-YOUR-BUCKET-NAME/*"
            ]
        }
    ]
}
```


##### - httpd.conf rewrite rules
.
```sh

# vim /etc/httpd/conf/httpd.conf
RewriteEngine On
RewriteRule ^/images/(.*)$  https://s3.ap-south-1.amazonaws.com/YOUR-S3-BUCKET-NAME/$1 [L]

# systemctl restart httpd
```

##### - Copying Sample site from git
.
```sh
# git clone https://github.com/Fujikomalan/httpd-s3-image-rewrite.git  /tmp/samplesite
# cp -r /tmp/samplesite/* /var/www/html/
```

##### - Copy Cotents from /var/www/html/images/ to YOUR-S3-BUCKET-NAME

