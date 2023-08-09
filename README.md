# 2048-Game-using-Docker-and-AWS-Elastic-Beanstalk

This repository contains code for a simple 2048 game that has been containerized using Docker and deployed on AWS Elastic Beanstalk. Follow the steps below to deploy the application.

## Prerequisites

- [Docker](https://www.docker.com/) installed on your local machine.
- An AWS account.

## Steps
1. Create a new folder on your local machine called 2048.
2. Open the 2048 folder in VS Code and create a new Dockerfile. Add the following commands to the file: 
```Dockerfile
FROM ubuntu:22.04

RUN apt-get update
RUN apt-get install -y nginx zip curl

RUN echo "daemon off;" >>/etc/nginx/nginx.conf
RUN curl -o /var/www/html/master.zip -L https://codeload.github.com/gabrielecirulli/2048/zip/master
RUN cd /var/www/html/ && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip

EXPOSE 80

CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf"]
```
Refer to this [link](https://www.linkedin.com/posts/nasiullha-chaudhari_docker-containerization-container-activity-6986389360879235072-8Ms5/) for detailed instructions on how to complete the Dockerfile.

3. Run the following command in your terminal to build the Docker image:
```
docker build -t 2048-game .
```
4. Confirm that the Docker image has been created by running the following command:
```
docker images
```
5. Run the Docker container using the following command (replacing <image-id> with the ID of the image you just created):
```
docker run -p 80:80 <image-id>
```
6. Open your browser and navigate to http://localhost:80 to confirm that the game is running locally.

7. Log in to your AWS account and navigate to the Elastic Beanstalk console.
8. Click "Create a new environment" and choose "Web server environment".
9. Enter a name for your environment and choose a platform. For this example, choose "Docker" as the platform.
10. Upload your Docker image by following the prompts in the Elastic Beanstalk console.
11. Click "Create environment" to create your environment.
12. Once your environment is created, navigate to the URL provided in the Elastic Beanstalk console to confirm that the game is running on AWS.

Congratulations! You have successfully deployed the 2048 game on AWS Elastic Beanstalk using Docker.



