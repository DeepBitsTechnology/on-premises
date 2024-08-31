# Project Setup

## Prerequisites

#### 1 Create an EC2 Instance

   - Select Ubuntu as the operating system.
   - Choose the `t2.large` instance type.
   - Configure storage with 128GB.
   - Set up security groups to allow connections from your network.

#### 2 Install Docker and Docker Compose

   - Connect to your instance and run the following commands:
     ```bash
     sudo apt update
     sudo apt install docker.io -y
     sudo curl -L "https://github.com/docker/compose/releases/download/v2.11.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
     sudo chmod +x /usr/local/bin/docker-compose
     ```

#### 3 Configure DNS Settings

   - Modify your domain name's DNS settings to point to the public IP of your EC2 instance. If you don't have a domain, you can register a free one through services like [No-IP](https://www.noip.com/). After registering, send us your domain name so we can add it to our Auth0 whitelist.

#### 4 Set Up a Reverse Proxy Using Caddy

##### 4.1 Install Caddy

   - Run the following commands:
     ```bash
     sudo apt update
     sudo apt install caddy
     ```

##### 4.2 Configure Caddy

   - Create a `Caddyfile`:
     ```bash
     sudo vi /etc/caddy/Caddyfile
     ```

   - Add the following configuration:
     ```plaintext
     <your_domain_name> {
         reverse_proxy localhost:8080
     }
     <your_domain_name>:3001 {
         reverse_proxy localhost:3000
     }
     <your_domain_name>:9210 {
         reverse_proxy localhost:9200
     }
     <your_domain_name>:9211 {
         reverse_proxy localhost:9201
     }
     ```
   - Replace `<your_domain_name>` with your EC2 instance's public IP or domain.

##### 4.3 Reload Caddy Configuration

   - Run the following command:
     ```bash
     sudo systemctl reload caddy
     ```

#### 5 Modify the `.env` File

   - Update the `.env` file with the following details:
     - **BASE_URL**: The domain name where the system will be hosted.
     - **USERNAME**: The username for accessing the system.
     - **PASSWORD**: The password for accessing the system.

   - Be sure to change `USERNAME` and `PASSWORD` before your first use.

#### 6 Build and Start the Docker Containers

   - Navigate to the project directory and run:
     ```bash
     docker-compose up --build
     ```
   - This will build the Docker images and start the containers as defined in your `docker-compose.yml` file.

   - After the first build, you can start the services more quickly with:
     ```bash
     docker-compose up
     ```
#### 7 MinIO Configuration

   - Log in to MinIO at [https://<your_domain_name>:9211](https://<your_domain_name>:9211) using the username and password from your `.env` file.
   - Create buckets: `coogle-dev`, `awsecr-image`, `dockerhub-image`, `github-download-bucket`.
   - Generate Access Keys: Use the Access Key and Secret Key specified in the `.env` file, or create new ones and update the `.env` file accordingly.

   - For detailed instructions, refer to the [MinIO Documentation](https://docs.min.io/).

#### 8 System Usage

   - Access the system at [http://<your_domain_name>:8080](http://<your_domain_name>:8080).
   - Sign up for an account or use your Google or GitHub account.
   - Under the "Projects" tab, click "Create Project" to create your first project.
   - On the project page, click "Add Assets" to upload your local files for scanning.
   - After uploading, ensure the new file is selected, then click "Save."
   - Click on the file you just uploaded, then click "Select to Monitor" to trigger the first scan.
   - Click the "View" button to see the results.

#### 9 Known Issues

- GitHub, Jira, and AWS integrations are currently not supported. Support for these platforms will be released soon.

#### 10 Documentation and Support

   - [Docker Documentation](https://docs.docker.com/)
   - [MinIO Documentation](https://docs.min.io/)
