# Hosting a Full Stack Application

## Project overview

This project is about hosting a full stack application on [Amazon Web Services (AWS)](https://aws.amazon.com).  
The hosted application [Udagram](https://github.com/udacity/nd0067-c4-deployment-process-project-starter) is provided by [Udacity](https://www.udacity.com).  
Its frontend is hosted as a static website on [Amazon Simple Storage Service (S3)](https://en.wikipedia.org/wiki/Amazon_S3).  
The backend uses [Elastic Beanstalk (EB)](https://en.wikipedia.org/wiki/AWS_Elastic_Beanstalk) to host the [PostgreSQL](https://www.postgresql.org/) database and an
S3 bucket to store images.  
A [CircleCI](https://circleci.com) pipeline is used for continuous integration and delivery.  
Documentation about architecture of infrastructure and pipeline can be found in the docs folder.  

## Screenshot

Home screen of Udagram website:  
![Udagram frontend](udagram_frontend.jpg)

## Link

The Udagram website can be found at:  
http://myfrontendbucket456456456.s3-website-us-east-1.amazonaws.com/home

