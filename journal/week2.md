# Week 2 — Distributed Tracing

# Honey Comb
During this week's, I explored Honeycomb as an observability tool and integrated it into my backend Flask application using OpenTelemetry (OTEL) with Honeycomb.io as the provider. I began by creating a new environment named 'bootcamp' on Honeycomb.io, then copied the API key and set it as an environment variable in Gitpod. Next, I added OTEL settings to the docker-compose.yml file to configure the backend. Although I focused on the backend, similar steps can be applied to the frontend application in the future.

Following the instructions on Honeycomb.io, I completed the installation process by updating the requirements.txt and App.py files. I then created a new span in the 'home activities' route to indicate that I am returning hard-coded data. As a result, I could observe two spans in Honeycomb each time a request was made to that backend route.

![image](https://github.com/user-attachments/assets/5557adff-99e1-4af8-93b0-72fabc297a43)

![image](https://github.com/user-attachments/assets/e7e91f66-9c58-466a-938a-acd75815c433)

# AWS X-ray
AWS X-Ray is another powerful observability tool that provides similar functionality to Honeycomb. However, configuring X-Ray is more complex and requires additional steps and troubleshooting. One notable advantage of X-Ray is its service map, a visual representation of your services. While this feature may not be particularly useful for our current simple application, it becomes invaluable for larger applications by highlighting each integration point and indicating where successes and failures occur.

I began by adding the aws-xray-sdk library to the backend's requirements and updating the App.py file accordingly. I also added a sampling configuration file (xray.json) to the project's root directory. Next, I created a new X-Ray group using the AWS X-Ray SDK, which then became visible in the AWS console. Additionally, I set up a sampling rule through the SDK to specify the type of data to collect, as collecting all data could be overwhelming and costly.

To set up an X-Ray daemon as a container, I used a Docker image from Dockerhub, maintained by AWS. This image was added to the docker-compose.yml file, along with the necessary environment variables for the Flask backend.

After running the container and making a request to our API endpoint, I could see the logs for the X-Ray container. It was now sending 'segments', which are similar to traces in Honeycomb, providing detailed insights into the application's performance and behavior.

![image](https://github.com/user-attachments/assets/8bb439fb-26e2-4893-8f18-fe13b6c330a4)

# Rollbar
I integrated Rollbar into our project to enhance error tracking and monitoring. Rollbar is a cloud-based solution that supports a wide range of programming languages and frameworks. Setting it up for Flask was quite simple. The main idea is to use Rollbar to capture and analyze errors, providing detailed insights that will be particularly useful in a production environment where accessing error logs is not as straightforward as it is during development.

First, I created a Rollbar account and added blinker and rollbar to the requirements.txt file for the Flask application. Then, I obtained a token from the Rollbar account and set it as an environment variable in Gitpod. Next, I included the necessary import statements and configured the Rollbar access token in the docker-compose.yml file for the backend Flask application. Additionally, I updated app.py with the required Rollbar integration code and added an endpoint designed to trigger an error, allowing me to verify that Rollbar was capturing and reporting errors correctly.

# CloudWatch Logs
AWS CloudWatch Logs is a native AWS service for managing logs, and Watchtower acts as a log handler to send logs to CloudWatch.

I began by installing Watchtower, then imported and configured CloudWatch in app.py. I added the necessary environment variables to docker-compose.yml and updated app.py to log errors. Additionally, I modified home_activities.py to log activities, enabling me to verify that these logs are now visible in the AWS console.

![image](https://github.com/user-attachments/assets/3dbc286e-24d2-4cb4-b8f8-d081a59140db)
