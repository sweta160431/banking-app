Bank Application Deployment using Docker (Multi-Stage)

This is a multi-tier bank an application written in Java (Springboot).
<img width="1680" alt="Screenshot 2024-10-28 at 8 02 53 PM" src="https://github.com/user-attachments/assets/7a84597f-a698-4c9c-9b65-ab8fd5687bf9">

<img width="1680" alt="Screenshot 2024-10-28 at 8 09 51 PM" src="https://github.com/user-attachments/assets/f6e5fdb0-7ecf-40d2-a601-ed02e7e41071">

**PRE-REQUISITES FOR THIS PROJECT:**

- AWS Account
- AWS Ubuntu EC2 instance (t2.medium)
- Install Docker
- Install docker compose

**STEPS TO IMPLEMENT THE PROJECT**

- **Deployment using Docker**
    - Clone the repository
    
    ```
    git clone https://github.com/AmanCloudOps/my-banking-app.git
    ```
    
    # 
    
    - Install docker and provide neccessary permission
    
    ```
    sudo apt update -y
    
    sudo apt install docker.io -y
    
    sudo usermod -aG docker $USER && newgrp docker
    ```
    
    # 
    
    - Move to the cloned repository
    
    ```
    cd Springboot-BankApp
    ```
    
    # 
    
    - Build the Dockerfile
    
    ```
    docker build -t springboot-bankapp .
    docker image tag springboot-bankapp sweta160431/springboot-bankapp
    ```
    

Important

Make sure to change docker build command with your DockerHub username.

# 

- Create a docker network

```
docker network create bankapp
```

# 

- Run MYSQL container

```
docker run -itd --name mysql -e MYSQL_ROOT_PASSWORD=Test@123 -e MYSQL_DATABASE=BankDB --network=bankapp mysql
```

# 

- Run Application container

```
docker run -itd --name BankApp -e SPRING_DATASOURCE_USERNAME="root" -e SPRING_DATASOURCE_URL="jdbc:mysql://mysql:3306/BankDB?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC" -e SPRING_DATASOURCE_PASSWORD="Test@123" --network=bankapp -p 8080:8080 sweta160431/springboot-bankapp
```

# 

- Verify deployment

```
docker ps
```

# 

- Open port 8080 of your AWS instance and access your application

```
http://<public-ip>:8080
```

**Congratulations, you have deployed the application using Docker**

# 

- **Deployment using Docker compose**
- Install docker compose

```
sudo apt update
sudo apt install docker-compose-v2 -y
```

# 

- Run docker-compose file present in the root directory of a project

```
docker compose up -d
```

# 

- Access it on port 8080

```
  http://<public-ip>:8080
```

Important

If you face issues with exiting docker container while running docker compose, run  `docker compose down`and then `docker compose up -d`.
