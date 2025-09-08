FROM ubuntu:latest

#Setting the working directory in the image
WORKDIR /app

#Copy necessary files from host file system to the image
COPY . /app

#Install required packages
RUN apt-get update && apt-get install -y python3 python3-pip

#Set environment variable
ENV NAME World

#Run the application
CMD ["python3", "app.py"]


