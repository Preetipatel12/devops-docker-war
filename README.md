Dockerized Java WAR Application Deployment on AWS EC2
Project Overview
This project demonstrates how to dockerize a Java WAR application (built in Eclipse), push it to Docker Hub, and deploy it on an AWS EC2 instance.

Tech Stack
Java (WAR Project)

Apache Tomcat

Docker

AWS EC2

Docker Hub

 Project Structure
project-folder/
│── student-form.war
│── Dockerfile Dockerfile
FROM tomcat:9.0

RUN rm -rf /usr/local/tomcat/webapps/*

COPY student-form.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]
 Step 1: Build Docker Image
docker build -t student-app .
 Step 2: Run Container Locally
docker run -d -p 8080:8080 student-app
Access app:

http://localhost:8080
 Step 3: Login to Docker Hub
docker login
 Step 4: Tag Image
docker tag student-app preetipatel12/student-app
 Step 5: Push Image
docker push preetipatel12/student-app
 Step 6: Launch AWS EC2 Instance
OS: Amazon Linux / Ubuntu

Instance Type: t2.micro / t3.micro

Allow Ports:

22 (SSH)

80 (HTTP)

8080 (Custom TCP)

 Step 7: Connect to EC2
ssh -i student-key.pem ec2-user@your-ec2-public-ip
 Step 8: Install Docker on EC2
sudo yum update -y
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
 Step 9: Pull Image
docker pull preetipatel12/student-app
 Step 10: Run Container on EC2
docker run -d -p 8080:8080 preetipatel12/student-app
 Step 11: Access Application
http://your-ec2-public-ip:8080
 Troubleshooting
1. Container not running
docker ps
2. Check logs
docker logs <container_id>
3. Port not accessible
Ensure port 8080 is open in Security Group

 Conclusion
This project successfully demonstrates:

Dockerizing a Java WAR application

Using Docker Hub for image storage

Deploying containers on AWS EC2
