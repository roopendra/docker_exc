# build from the Maven image, which has a maven environment pre-configured
FROM maven:latest
#copy the application in
COPY . /home/ubuntu/deployment_dir/build
#Change the working directory to where we are building the app
WORKDIR /home/ubuntu/deployment_dir/build
#Use maven to build the application
RUN mvn clean package
#Create a new build stage from the Java image which has java installed already
FROM openjdk:11
#Change the workdir to where the app will be installed
WORKDIR /opt/hello-world
#Copy the JAR file created previously
COPY --from=0 /home/ubuntu/deployment_dir/build/target/hello-world-1.0.0.jar /home/ubuntu/deployment_dir/app.jar
#Create an entrypoint to run the application
ENTRYPOINT ["/usr/bin/java", "-jar", "/home/ubuntu/deployment_dir/app.jar"]
