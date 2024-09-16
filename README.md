# Commands used to deploy this application in render

### To deploy in render, we need to covert the jar file into running image and push to docker hub

To generate JAR file, package the project

`mvn clean package`

Create a "Dockerfile" file under the root location of the Project with following info

`FROM openjdk:11-ea-11-jdk 
ARG JAR_FILE=target/*.jar 
COPY ${JAR_FILE} app.jar 
ENTRYPOINT ["java","-jar","/app.jar"]`

Then build it using the below command to generate the image

`docker build -t kalikaprasadreddy/adda:latest`

Verify the image created, by running it on docker with the following command

`docker run -p 8080:8080 -t kalikaprasadreddy/add:latest`

If everything works as expected, then login to docker using below command

`docker login -u <username>`

this prompts for Docker password.

Once logged-in, push the image to docker hub
`docker push -t kalikaprasadreddy/add/latest`

Login to Render(dashboard.render.com) and create a new Web Service. Which asks for Docker Image.

Copy the image tag id from Docker hub, and paste in render for verification of the image. Make sure the image is public.

Post verification, Render asks for the app name, server specifications and Datacnter location. 

Upon submission. Render runs the docker image.

Reference URLs:

https://spring.io/guides/gs/spring-boot-docker
https://community.render.com/t/java-springboot-app-start-command/19835/6
https://medium.com/spring-boot/free-hosting-bliss-deploying-your-spring-boot-app-on-render-d0ebd9713b9d


ADDA Application URL: https://adda-lqpq.onrender.com/chat