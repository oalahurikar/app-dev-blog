
## What is the difference between Docker image and container?

---

`docker ps`  lists all the images
## Testing Locally Before Deployment

• Build the Docker Image Locally:
`docker build -t your_app_image .`

• Run the Docker Container Locally:
`docker run -p 8080:8080 your_app_image`

• Check Logs for Errors:
`docker logs <container_id>`


## How to pass .env variables to Docker image

`docker run --env-file .env -p 8080:8080 my_flask_app`