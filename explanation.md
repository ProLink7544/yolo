Choice of the base image on which to build each container.
When choosing a base image for a Docker container, it's important to consider factors such as security, stability, and compatibility with your application's dependencies. 
In my microservice assignment, I chose to use the node base image for my web and API services since my application is built using Node.js.

Dockerfile directives used in the creation and running of each container.
Client Service Dockerfile
FROM node:13.12.0 
WORKDIR /client
COPY package*.json ./ 
RUN npm install 
COPY . .
 EXPOSE 3000 
 CMD ["npm", "start"]

FROM node:13.12.0 - Specifies the base image to use as the starting point for the Dockerfile. 
there for I use the node:13.12.0 image.

WORKDIR /client - Sets the working directory for subsequent commands in the Dockerfile to /client. COPY package*.json ./ - Copies the package.json and package-lock.json files from the local directory to the Docker image.
RUN npm install - Runs the npm install command inside the Docker image to install the application's dependencies.

COPY . . - Copies the entire local directory to the Docker image.

EXPOSE 3000 - Informs Docker that the container will listen on port 3000.

CMD ["npm", "start"] - Specifies the command to run when the container starts. In this case, it runs the npm start command to start the web server.

Backend Service Dockerfile
FROM node:14-alpine
WORKDIR /client
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]

Docker-compose Networking (Application port allocation and a bridge network implementation) where necessary.
In my docker-compose.yml file, I specified a bridge network for my microservices to communicate with each other by specifing network driver to type bridge.

Create a Dockerfile for each microservice. 
I created a Dockerfile for each microservice in its respective branch. I followed best practices for writing Dockerfiles, such as using a lightweight base image and only including necessary dependencies.

Build and test each Docker image locally.
I have used the docker build command to build each Docker image locally, and then used the docker run command to test each image to make sure it was running correctly.

Create a docker-compose.yml file. 
I have created a docker-compose.yml file in the main branch to orchestrate the containers for each microservice. I specified the Docker image for each service and defined the networking

Test the Docker Compose setup locally. 
I used the docker-compose up command to start the Docker Compose setup locally and tested that the microservices were able to communicate with each other.

Finally have done the commite and Push the changes to the repository (https://github.com/ProLink7544/yolo.git)

Successful running of the applications.

As good practices such as Docker image tag naming standards for ease of identification of images and containers.
i have also used stdin_open: true to keep terminal running.

I used the repository name together with the service name to tag my images and Semantic Versioning (semver)method to name my images prolink7544/client:1.0.0  and  prolink7544/backend:1.0.0