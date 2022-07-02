# Infrastructure description

Backend and Frontend are hosted on AWS.

## Udagram API

The backend uses Amazon Relational Database Service (RDS) to host the PostgreSQL database, Elastic Beanstalk (EB) to host the Server
and Simple Storage Service (S3) to save images.

### Amazon Relational Database Service (RDS)

RDS is used to host the PostgreSQL database.

The service is configured as follows:
- **Standard** creation mode
- Database engine: **PostgreSQL 13**
- Templates: **Free tier**
- DB instance identifier: **database-1**
- Credentials: set master **username** and **password**
- DB instance classes: **Burstable** classes: smallest size, e.g.: **db.t3.micro**
- Connectivity:
    - Public access: **Yes**
    - Leave rest at defaults
- Addtional configuration > Initial database name: **postgres**

### Elastic Beanstalk (EB)

EB is used to host the API running on Node.js.

The service is configured as follows:
- Application name: **udagram-api**
- Platform: **Node.js**
- Platform branch: **Node.js 14 running on 64bit Amazon Linux 2**
- Platform version: **5.5.4 (Recommended)**
- After creation set these environment variables (*Configuration > Software > Environment properties*):
    - `AWS_BUCKET` : arn:aws:s3:::mymediabucket456456456
    - `AWS_PROFILE` : default
    - `AWS_REGION` : us-east-1
    - `JWT_SECRET` : *your secret string*
    - `POSTGRES_DB` : postgres
    - `POSTGRES_HOST` : *endpoint of database*
    - `POSTGRES_PASSWORD` : *your master password*
    - `POSTGRES_USERNAME` : *your master username*
    - `AWS_ACCESS_KEY_ID` : *your aws access key*
    - `AWS_SECRET_ACCESS_KEY` : *your secrect aws key*

### Simple Storage Service (S3)

S3 is used to store images posted by the user.

The bucket is configured as follows:
- Bucket name: **mymediabucket456456456**
- AWS region: **default**
- Object ownership: **ACLs enabled**, **Bucket owner preferred**
- Allow all public access
- Permissions:
    - Bucket policy (Provided by Udacity):
        ```json
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Sid": "Stmt1625306057759",
                    "Principal": "*",
                    "Action": "s3:*",
                    "Effect": "Allow",
                    "Resource": "arn:aws:s3:::mymediabucket456456456/*"
                }
            ]   
        }
        ```
    - CORS configuration (Provided by Udacity):
        ```json
        [
            {
                "AllowedHeaders": [
                    "*",
                    "Content-Type",
                    "Authorization",
                    "Access-Control-Allow-Origin",
                    "Access-Control-Allow-Headers",
                    "Access-Control-Allow-Methods"
                ],
                "AllowedMethods": [
                    "POST",
                    "GET",
                    "PUT",
                    "DELETE",
                    "HEAD"
                ],
                "AllowedOrigins": [
                    "*"
                ],
                "ExposeHeaders": []
            }
        ]
        ```

## Udagram frontend

The frontend is hosted as a static website on Simple Storage Service (S3).

### S3

S3 is used to host the files of the frontend.

The bucket is configured as follows:
- Bucket name: **myfrontendbucket456456456**
- AWS region: **default**
- Object ownership: **ACLs enabled**, **Bucket owner preferred**
- Allow all public access
- Properties:
    - Static website hosting: **enabled**
- Permissions:
    - Bucket policy (Provided by Udacity):
        ```json
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Sid": "Stmt1625306057759",
                    "Principal": "*",
                    "Action": "s3:*",
                    "Effect": "Allow",
                    "Resource": "arn:aws:s3:::myfrontendbucket456456456/*"
                }
            ]   
        }
        ```
    - CORS configuration (Provided by Udacity):
        ```json
        [
            {
                "AllowedHeaders": [
                    "*",
                    "Content-Type",
                    "Authorization",
                    "Access-Control-Allow-Origin",
                    "Access-Control-Allow-Headers",
                    "Access-Control-Allow-Methods"
                ],
                "AllowedMethods": [
                    "POST",
                    "GET",
                    "PUT",
                    "DELETE",
                    "HEAD"
                ],
                "AllowedOrigins": [
                    "*"
                ],
                "ExposeHeaders": []
            }
        ]
        ```