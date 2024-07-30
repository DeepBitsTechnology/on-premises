# Project Setup

## Prerequisites

1. **Install Docker Desktop**

   Follow the instructions to install Docker Desktop on your Linux machine: [Docker Desktop Installation](https://docs.docker.com/desktop/install/linux-install/)

2. **Enlarge Docker Desktop Resource Limits**

   Ensure Docker Desktop is allocated at least 6GB of memory, 4 CPUs, and 128GB disk space. You can set these resources in Docker Desktop settings under the "Resources" tab.

## Configuration

3. **Modify the `.env` File**

   Update the `.env` file with the following details:

   - **LOCAL_IP**: The local IP address of your local machine.
   - **USERNAME**: The username for accessing the system.
   - **PASSWORD**: The password for accessing the system.

   Change USERNAME and PASSWORD before your first use.

## Building and Running the Project

4. **Build and Start the Docker Containers**

   Navigate to the project directory and run:

   ```sh
   docker compose up --build
   ```

   This will build the Docker images and start the containers as defined in your `docker-compose.yml` file. After the first build, you just need to run:

   ```sh
   docker compose up
   ```

   to start the services, and it's much faster.

## Accessing the System

5. **MinIO Configuration**

   Log in to MinIO at [http://localhost:9201](http://localhost:9201) using your username and password from the `.env` file.

   - **Create a bucket**: Name it `coogle-dev`.
   - **Generate Access Keys**: Use the Access Key and Secret Key as specified in the `.env` file, or you can create new ones and update the `.env` file accordingly.

   For detailed instructions on using MinIO, refer to the [MinIO Documentation](https://docs.min.io/).

6. **System Usage**

   Access the system at [http://localhost:8080](http://localhost:8080) to start using it. 
   You can sign up for an account or use your Google or GitHub account.
   
   - Under the "Projects" tab, click the "Create Project" button to create your first project.
   - In the project page, click the "Add Assets" button to upload your local files for scanning.
   - After uploading, ensure the new file is selected, then click "Save".
   - Click on the file you just uploaded, then click the "Select to Monitor" button to trigger the first scan.
   - Click the "View" button to see the results.

7. **Documentation and Support**

    - [Docker Documentation](https://docs.docker.com/)
    - [MinIO Documentation](https://docs.min.io/)
