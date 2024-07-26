Certainly! Here’s an enhanced version of the README file with additional details for a more comprehensive guide:

---

# Project Setup

## Prerequisites

1. **Install Docker Desktop**

   Follow the instructions to install Docker Desktop on your Linux machine:
   [Docker Desktop Installation](https://docs.docker.com/desktop/install/linux-install/)

2. **Enlarge Docker Desktop Resource Limits**

   Ensure Docker Desktop is allocated at least 8GB of memory and 4 CPUs. If you are using Docker Desktop, you can set these resources in the settings under the "Resources" tab.

3. **Install Docker Compose**

   Make sure Docker Compose is installed. You can check this by running:

   ```sh
   docker-compose --version
   ```

   If not installed, follow the instructions here: [Install Docker Compose](https://docs.docker.com/compose/install/)

## Configuration

4. **Modify the `.env` File**

   Update the `.env` file with the following details:

   - **LOCAL_IP**: The IP address of your local machine.
   - **USERNAME**: The username for accessing the system.
   - **PASSWORD**: The password for accessing the system.

   Example `.env` file:

   ```env
   LOCAL_IP=127.0.0.1
   USERNAME=admin
   PASSWORD=yourpassword
   ```

## Building and Running the Project

5. **Build and Start the Docker Containers**

   Navigate to the project directory and run:

   ```sh
   docker-compose build
   docker-compose up --build
   ```

   This will build the Docker images and start the containers as defined in your `docker-compose.yml` file.

## Restoring the CVE Database

6. **Restore the CVE Database**

   Copy the database dump to the MongoDB container and restore it:

   ```sh
   docker cp /home/wei/on-premises/db_dump mongodb:/backup
   docker exec -it mongodb mongorestore --username root --password rootpassword /backup
   ```

   Ensure the MongoDB container name and credentials match those specified in your `docker-compose.yml` file.

## Accessing the System

7. **MinIO Configuration**

   Log in to MinIO at [http://localhost:9101](http://localhost:9101) using your username and password from the `.env` file.

   - **Create a bucket**: Name it `coogle-dev`.
   - **Generate Access Keys**: Use the Access Key and Secret Key as specified in the `.env` file.

   For detailed instructions on using MinIO, refer to the [MinIO Documentation](https://docs.min.io/).

8. **System Usage**

   Access the system at [http://localhost:8080](http://localhost:8080) to start using it. Follow any on-screen instructions to complete the initial setup.

## Troubleshooting

9. **Common Issues**

   - **Docker Container Not Starting**: Ensure Docker and Docker Compose are correctly installed and updated. Check the logs using:

     ```sh
     docker-compose logs
     ```

   - **Database Restoration Issues**: Verify the path and file permissions of the database dump. Ensure MongoDB container is running.

   - **MinIO Access Issues**: Check the MinIO container logs and verify network configurations.

## Additional Resources

10. **Documentation and Support**

    - [Docker Documentation](https://docs.docker.com/)
    - [Docker Compose Documentation](https://docs.docker.com/compose/)
    - [MinIO Documentation](https://docs.min.io/)

---

Feel free to modify any details to better fit your specific project requirements!
