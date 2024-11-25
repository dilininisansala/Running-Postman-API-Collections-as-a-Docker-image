# Running Postman API Collections as a Docker image for Local and Remote Testing
Hosting a Postman API collection within a Docker container, pushing it to Docker Hub, and running it locally.
By using Docker, we can easily package and run Postman collections in a containerized environment, making it simple to share, deploy, and run tests locally or remotely. This approach ensures that the testing environment is consistent and eliminates setup issues across different machines.

This guide demonstrates how to host a Postman API collection as a Docker image, push it to Docker Hub, and run it locally for testing.

## Step 1: Export the Postman Collection
* Open Postman.
* Navigate to your API collection.
* Click the three dots next to the collection name → Export.
* Choose "Collection v2.1" format and save it as Api-Automation-Testing.postman_collection.json
![img 1](https://github.com/user-attachments/assets/c1a0cd80-76b9-45a2-8542-e6e08e66fab1)

## Step 2: Create a Dockerfile
Create a Dockerfile to set up a container that runs your Postman collection using Newman
In the same folder as Api-Automation-Testing.postman_collection.json, create a file named Dockerfile

𝗡𝗼𝘁𝗲: 
Make sure Docker is installed and running on your system

Use PowerShell, Terminal, or Command Prompt to execute Docker commands

#### This creates an empty Dockerfile in the current directory
```
New-Item -ItemType File -Name Dockerfile
```
#### PowerShell allows you to open a file in Notepad with the following command
```
notepad Dockerfile
```
#### Dockerfile
```
# Use the official Newman image
FROM postman/newman:latest

# Copy the Postman collection to the container
COPY Api-Automation-Testing.postman_collection.json /etc/newman/Api-Automation-Testing.postman_collection.json

# Define the default command to run the collection
CMD ["run", "/etc/newman/Api-Automation-Testing.postman_collection.json"]
```
![img 2](https://github.com/user-attachments/assets/9c9197f4-617c-4b6f-82a0-597546ff2085)

## Step 3: Build the Docker Image
Open a terminal or PowerShell in the directory containing Dockerfile and Api-Automation-Testing.postman_collection.json
Run the following command to build the image
```
docker build -t postman_test .
```
![img 3](https://github.com/user-attachments/assets/57e99193-85a6-42cd-bc1a-7590e47ca60e)

## Step 4: Push the Image to Docker Hub
#### Log in to Docker Hub
```
docker login
```
#### Tag the image with your Docker Hub username
```
docker tag postman_test <your_dockerhub_username>/postman_test
```
#### Push the image to Docker Hub
```
docker push <your_dockerhub_username>/postman_test
```
![img 4](https://github.com/user-attachments/assets/2b78c69c-fc42-479c-8a3d-e2f93e1b675d)

## Step 5: Download and Run the Image
On any system with Docker installed, you can pull and run your Postman collection
#### Pull the image
```
docker pull <your_dockerhub_username>/postman_test
```
#### Run the container
```
docker run <your_dockerhub_username>/postman_test
```
![img 5](https://github.com/user-attachments/assets/7e191d53-bf58-412a-95c7-4fc856510ac9)
![img 6](https://github.com/user-attachments/assets/db4e5fe7-efce-4140-9bac-8c6af77f3225)
