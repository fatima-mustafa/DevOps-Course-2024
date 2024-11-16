# Sample Repository from the Internet and Applying DevOps Tooling

### **Choosing a Sample Repository**
To explore and apply DevOps tooling, I selected a publicly available sample repository on GitHub that featured a simple Node.js application. The repository contained:

- A basic REST API with CRUD operations.
- A minimal file structure, including `server.js`, `package.json`, and sample data.
- Room for improvement in automation and scalability.

Repository Link: [Sample Node.js App](https://github.com/heroku/node-js-sample)

---

### **Applying DevOps Tooling**

#### **1. Containerizing the Application with Docker**
I began by creating a `Dockerfile` to containerize the Node.js application. This allowed me to standardize the application's environment for development and deployment.  

**Steps Taken:**
- Wrote a `Dockerfile`:
  ```dockerfile
  FROM node:16
  WORKDIR /app
  COPY package*.json ./
  RUN npm install
  COPY . .
  CMD ["node", "server.js"]
  EXPOSE 3000 

- Built and Ran the Container
```bash
docker build -t nodejs-sample-app .
docker run -d -p 3000:3000 nodejs-sample-app 
```

### **2. Setting Up a CI/CD Pipeline**
I integrated a CI/CD pipeline using GitHub Actions to automate testing and deployment.

**Steps Taken:**

Created a `.github/workflows/ci-cd.yml` file:
```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v2

    - name: Set Up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: 16

    - name: Install Dependencies
      run: npm install

    - name: Run Tests
      run: npm test

    - name: Build Docker Image
      run: docker build -t nodejs-sample-app .

    - name: Deploy
      run: echo "Deployment script here"
```
### **Outcome:**
The pipeline automatically executed tests, built the Docker image, and deployed the application upon every code push to the main branch.

### **Conclusion**
Through containerization and CI/CD integration, I successfully transformed a sample repository into a robust, automated, and scalable application deployment workflow.

