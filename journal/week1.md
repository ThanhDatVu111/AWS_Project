# Week 1 — App Containerization
# Running Frontend and Backend Locally on Gitpod
To run the backend locally, I mirrored the steps from the Dockerfile, starting by installing pip and then executing the command to run Flask. I also had to configure the environment variables (frontendurl and backendurl) to *, as omitting these led to 404 errors. Later, I removed these environment variables when transitioning to the actual Docker setup.

# Containerizing the Application (Dockerfiles and Docker Compose)
I began by containerizing the backend using the command docker build -t backend-flask ./backend-flask. This command fetched the necessary image and built the container. To run the container, I used docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask, which set the required environment variables for the container's execution.

I followed a similar procedure for the frontend, creating its own Dockerfile to run its respective container.

Running the above containers individually required multiple commands for each container. To simplify this, I created a docker-compose.yml file at the project's root. With this file, I could launch both containers simultaneously using the command docker-compose up.

# Run the same containers on my local machine
<img width="823" alt="Screenshot 2024-06-30 at 2 38 08 PM" src="https://github.com/ThanhDatVu111/AWS_Project/assets/150296646/26df9c5f-951b-456e-8c71-733f9229e8a9">

# Run Postgres Container
I've set up Postgres using a docker-compose.yml file. Adding Postgres to the file and including a volume configuration allows me to manage its data persistently. Running docker-compose up launches the Postgres container along with other services.

To connect to the Postgres database, I used a database connection extension in my development environment. Once the connection was established, I accessed the Postgres command-line interface by running psql -U postgres --host localhost. This allowed me to interact with the Postgres database directly from within its container, executing queries and managing data as needed.
