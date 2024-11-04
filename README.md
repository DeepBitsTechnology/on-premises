# Project Setup

## Prerequisites

### 1. Create an EC2 Instance
   - **Operating System:** Select Ubuntu.
   - **Instance Type:** Choose the `c5.4xlarge` or better instance type.
   - **Storage:** Configure with 128GB.
   - **Security Groups:** Set up to allow connections from your network.

### 2. Install Docker and Docker Compose
   - Connect to your EC2 instance and run the following commands:
     ```bash
     sudo apt update
     sudo apt install docker.io -y
     sudo curl -L "https://github.com/docker/compose/releases/download/v2.11.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
     sudo chmod +x /usr/local/bin/docker-compose
     ```

### 3. Configure DNS Settings
   - Modify your domain name's DNS settings to point to the public IP of your EC2 instance.
   - If you don't have a domain, you can register a free one through services like [No-IP](https://www.noip.com/).
   - After registering, send us your domain name so we can add it to our Auth0 whitelist, and create Github app and Jira app for you if you need Github and Jira integration.

### 4. Configure SSL/TLS certificates
   - Copy your domain’s certificates to the ./certs/ directory, renaming them to privkey.pem and fullchain.pem if necessary.
   - If you do not have certificates for your domain, you can use Let’s Encrypt to create and install SSL/TLS certificates:

#### 4.1 Install Certbot:
   - Certbot is the most popular Let's Encrypt client. On Ubuntu, you can install it using:
     ```bash
     sudo apt-get update
     sudo apt-get install certbot
     ```

#### 4.2 Obtain a Certificate:
  ```bash
  sudo certbot certonly --standalone -d yourdomain.com
  ```
  Replace "yourdomain.com" with your actual domain name. Once the certificate is generated, copy the `privkey.pem` and `fullchain.pem` files to the `./certs/` directory.

### 5. Modify the `.env` File
   - Update the `.env` file with the following details:
     - BASE_URL: The domain name where the system will be hosted.
     - USERNAME: The username for accessing the system.
     - PASSWORD: The password for accessing the system.

### 6. Build and Start the Docker Containers
   - Navigate to the project directory and run:
     ```bash
     docker-compose up --build -d
     ```
   - This will build the Docker images and start the containers as defined in your `docker-compose.yml` file.
   - After the first build, you can start the services more quickly with:
     ```bash
     docker-compose up -d
     ```

### 7. MinIO Configuration
   - Log in to MinIO at [https://<your_domain_name>:9211](https://<your_domain_name>:9211) using the username and password from your `.env` file.
   - Create the following buckets: `coogle-dev`, `awsecr-image`, `dockerhub-image`, `github-download-bucket`.
   - Create a new Access Key and update the `MINIO_ACCESS_KEY_ID` and `MINIO_SECRET_ACCESS_KEY` fields in the `.env` file accordingly.
   - For detailed instructions, refer to the [MinIO Documentation](https://docs.min.io/).

### 8. AWS Configuration (optional, if you need AWS ECR integration)
   - Log in to your AWS Console, and go to IAM.
   - Select Users (or create a new one) and go to the Security credentials tab.
   - Create access key under Access keys.
   - Update the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` fields in the `.env` file accordingly.
   - For detailed instructions, refer to the [AWS Documentation](https://docs.aws.amazon.com/keyspaces/latest/devguide/access.credentials.html).

### 9. System Usage
   - Access the system at [http://<your_domain_name>:8080](http://<your_domain_name>:8080).
   - Sign up for an account or use your Google or GitHub account.
   - Under the "Projects" tab, click "Create Project" to create your first project.
   - On the project page, click "Add Assets" to upload your local files for scanning.
   - After uploading, ensure the new file is selected, then click "Save."
   - Click on the file you just uploaded, then click "Select to Monitor" to trigger the first scan.
   - Click the "View" button to see the results.

### 10. Documentation and Support
   - [Docker Documentation](https://docs.docker.com/)
   - [Certbot Documentation](https://certbot.eff.org/)
   - [MinIO Documentation](https://docs.min.io/)
