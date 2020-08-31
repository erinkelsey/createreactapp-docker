# Create React App run with Docker on AWS Elastic Beanstalk

[![Build Status](https://travis-ci.com/erinkelsey/createreactapp-docker.svg?branch=master)](https://travis-ci.com/erinkelsey/createreactapp-docker)

Basic Create React App with Docker, Travis CI and AWS Elastic Beanstalk for CI/CD and hosting.

## Development

### Build with Docker CLI

    $ docker build -f Dockerfile.dev

### Run with Docker CLI

    $ docker run -it -p 3000:3000 <container_id>

### Run with Docker CLI and Docker Volumes

    $ docker run -it -p 3000:3000 -v /app/node_modules -v $(pwd):/app <container_id>

This will put a bookmark on the node_modules folder (won't map it to anything else), map the /app folder in the container to the current directory (watch for updates). Therefore, you can make use of hot reload for changes in app.

### Run React Test Cases with Docker CLI

    $ docker run -it <container_id> npm run test

### Build and Run with Docker Compose

    $ docker-compose up

### Rebuild and Run with Docker Compose

    $ docker-compose down && docker-compose up --build

### Run React Test Cases with Docker Compose (Not Best Approach)

    $ docker-compose up
    $ docker exec -it <container_id> npm run test

## Production

### Build with Docker CLI

    $ docker build .

### Run with Docker CLI

    $ docker run -p 8080:80 <container_id>

NOTE: nginx default port is 80

## Setup for CI/CD and Deployment to AWS

### AWS ElasticBeanstalk

Create a new application and environment with any name.

Select 'Docker' as the Platform.

Select 'Sample application' for Application Code.

### Travis CI

Make sure that your GitHub repository is public, and that Travis CI is configured to access it.

Create the following environment variables:

- AWS_ACCESS_KEY -> Your AWS IAM Access Key with permissions for Elastic Beanstalk
- AWS_SECRET_KEY -> Your AWS IAM Secret Key with permissions for Elastic Beanstalk
- AWS_REGION -> Region of your AWS Elastic Beanstalk application
- AWS_APP_NAME -> AWS Elastic Beanstalk application name
- AWS_ENV_NAME -> AWS Elastic Beanstalk environment name
- AWS_BUCKET_NAME -> AWS S3 bucket name where application is stored (check logs when environment is created for name)
- AWS_BUCKET_PATH -> The folder in the AWS S3 holder your application (usually the same as AWS_APP_NAME)

NOTE: Deployment to AWS is only triggered when a pull request or commit is made to master branch on GitHub
