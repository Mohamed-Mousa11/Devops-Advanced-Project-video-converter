![ProjectArchitecture drawio](https://github.com/user-attachments/assets/ec618b73-274e-4bc7-a446-b45a5fc0eef0)# Devops-Advanced-Project-video-converter
# 🚀 Microservices Python App with EKS, Docker, and Kubernetes  

A scalable microservices application built with Python, Docker, Kubernetes (EKS), MongoDB, PostgreSQL, and RabbitMQ. This project demonstrates a cloud-native architecture for handling authentication, file uploads, audio conversion, and notifications.



![Uploading ProjectArchitecture.drawio.svg…]()


---

## 🌟 **Features**  
- **Auth Service** 🔐: User authentication and JWT token generation.  
- **Gateway Service** 🌐: API gateway for routing requests.  
- **Converter Service** 🎧: Converts uploaded files to MP3.  
- **Notification Service** 📨: Sends notifications via RabbitMQ.  
- **MongoDB** 🍃: Stores user data.  
- **PostgreSQL** 🐘: Stores file metadata.  
- **RabbitMQ** 🐇: Message queue for async notifications.  
- **AWS EKS** ☁️: Managed Kubernetes cluster for deployment.  

---

## 🛠 **Prerequisites**  
Before running this project, ensure you have:  
- **VMware Workstation** (or any VM environment)  
- **Ubuntu VM** (tested on 20.04 LTS)  
- **AWS CLI** (`aws configure`)  
- **kubectl** (Kubernetes CLI)  
- **Helm** (Kubernetes package manager)  
- **Docker** (for containerization)  
- **Python 3.8+** (for running services)  
- **Git** (for version control)

---

## 🛠️ Tech Stack

- **Python** 🐍
    
- **Docker** 🐳
    
- **Kubernetes (EKS on AWS)** ☁️
    
- **MongoDB** 🍃
    
- **PostgreSQL** 🛢️
    
- **RabbitMQ** 🐇
    
- **Helm** ⚙️
    
- **Git** 🔧
    

---

## 🧩 Services

- **Auth Service** 🔒
    
- **Gateway Service** 🚪
    
- **Converter Service** 🎵
    
- **Notification Service** 📩

---

## 📂 **Project Structure**  
```
microservices-python-app/  
├── auth-service/       # 🔐 Authentication logic  
├── gateway-service/    # 🌐 API Gateway  
├── converter-service/  # 🎧 File-to-MP3 conversion  
├── notification-service/ # 📨 RabbitMQ notifications  
├── deployments/        # 🛠 Kubernetes YAML files 
├── charts/             # Helm charts for services
└── README.md           # 📖 Documentation  
```

---

## ⚙️ Setup and Deployment Steps

### 1️⃣ Local Environment Preparation

- 💻 Created an **Ubuntu** VM using **VMware Workstation**.
    
- 🛠️ Installed essential tools:
    
    - Helm
        
    - AWS CLI
        
    - kubectl
        
    - Python
        
    - Git
        
- 🐳 Installed **Docker**.
    
- 🛢️ Installed **MongoDB** and **PostgreSQL** locally for testing.
    

---

### 2️⃣ AWS Infrastructure Setup

- ☁️ Created an **EKS Cluster** using AWS.
  ![eks](https://github.com/user-attachments/assets/44afe30f-e5c7-4d9b-9836-a2b20b7f210b)

    
- 🛡️ Created necessary **IAM Roles**:
    
    - `eksclusterrole`
      ![eksclusterrole](https://github.com/user-attachments/assets/fd00de07-281c-4a03-935f-047fb4d6585e)

        
    - `eksnoderole`
      ![eksnoderole](https://github.com/user-attachments/assets/13b14fd8-d923-4e4f-ad41-5b180605700a)

        
- 🖥️ Created **Node Group** for the EKS cluster.
  ![nodegroup](https://github.com/user-attachments/assets/97565157-55b5-4360-bf45-5d5de68d0f25)

    
- 🔒 Configured **Security Groups** for the Node Group with necessary ports open.
  ![sg for node group](https://github.com/user-attachments/assets/ee380b30-b52d-4657-aec0-e6463cc0af0a)


---

### 3️⃣ Connect to EKS Cluster

```bash
aws eks update-kubeconfig --name microservices --region us-east-1
```

✅ Successfully connected to the EKS Cluster!
   ![cmd to connect cluster](https://github.com/user-attachments/assets/c55defdc-6c64-4799-8267-9b039f3e7a79)


---

### 4️⃣ Deploy Databases Using Helm

- 📦 Installed **MongoDB** using Helm.
   ![mongo pod](https://github.com/user-attachments/assets/2d94ca2a-aa2f-4825-b076-6f17c088357b)

    
- 📦 Installed **PostgreSQL** using Helm.
   ![postgres](https://github.com/user-attachments/assets/fe56e249-a61e-4ee9-a73e-fd05dfbd05b8)


✅ Verified successful connections to:

- MongoDB 🍃
  ![conenct mongodb success](https://github.com/user-attachments/assets/927de1ca-8d21-4d3e-bce2-ee49f0018dd1)

    
- PostgreSQL 🛢️
  ![connect postgres succes](https://github.com/user-attachments/assets/4f2eee17-ef5c-4e08-aae9-878619775743)


- RabbitMQ 🐇
  ![connect to rabbitmq success](https://github.com/user-attachments/assets/4df61c4f-cba7-44b0-adad-cac47beb4e8d)


---

### 5️⃣ RabbitMQ Setup

- 🛠️ Created 2 queues for communication between microservices.
    ![creating 2 queus](https://github.com/user-attachments/assets/1f144806-cee7-4097-b587-224ed871bfc9)

---

### 6️⃣ Building and Pushing Docker Images

- 🔨 Built **Docker Image** for **Auth Service**.
    
- 🚀 Pushed the Auth service image to **DockerHub**.
    
- 🔄 Repeated the process for the other services or reused the same images where needed.
    

---

### 7️⃣ Deploy Microservices on Kubernetes

- 🚀 Deployed **Auth Service** pods.
    
- 🚀 Deployed **Gateway Service** pods.
    
- 🚀 Deployed **Converter Service** pods.
    
- 🔽 Scaled down **Converter Service** replicas from 4 ➡️ 2:
    

```bash
kubectl scale deployment converter --replicas=2
```

- 🚀 Deployed **Notification Service** pods.
    

---

### 8️⃣ API Functionality Verification

- 🔑 **Login Endpoint** tested successfully! (`/api/login`)
    
- ⬆️ **Upload API** tested successfully! (`/api/upload`)
    
- 🎵 MP3 file successfully generated after upload!

---

## 🚀 Commands Cheatsheet

Here’s a quick list of important commands used:

- Update kubeconfig to connect to EKS:
    
    ```bash
    aws eks update-kubeconfig --name microservices --region us-east-1
    ```
    
- Scale deployment:
    
    ```bash
    kubectl scale deployment converter --replicas=2
    ```
    
- Build and push Docker images:
    
    ```bash
    docker build -t your-dockerhub-username/service-name .
    docker push your-dockerhub-username/service-name
    ```
    
- Install MongoDB with Helm:
    
    ```bash
    helm install mongodb bitnami/mongodb
    ```
    
- Install PostgreSQL with Helm:
    
    ```bash
    helm install postgres bitnami/postgresql
    ```
    

---

## 📌 Important Notes

- Ensure your IAM roles are correctly configured to allow node groups to interact with your EKS cluster.
    
- Security groups must allow traffic on MongoDB, PostgreSQL, RabbitMQ, and application ports.
    
- DockerHub credentials should be set up securely when pulling private images in Kubernetes.
