
**Getting Started with GitHub Container Registry (GHCR)**

GitHub Container Registry (GHCR) is a powerful tool that allows developers to manage Docker images alongside their source code, providing a unified development experience. In this guide, we'll walk through the basics of setting up GHCR for your GitHub repository.

### **Why Use GHCR?**

GHCR offers seamless integration with the GitHub ecosystem, making it easy to manage your container images, automate workflows with GitHub Actions, and control access using fine-grained permissions. It's particularly useful if your team is already utilizing GitHub for code management, as it provides one platform for both code and containers.

### **Step-by-Step Setup**

1. **Create a Personal Access Token (PAT)**:
   - To push images to GHCR, you'll need a PAT with `write:packages` and `repo` permissions.
   - Go to GitHub Settings and generate a token with these scopes.

2. **Authenticate Docker**:
   - Use the PAT to log in to GHCR:
```bash
echo YOUR_PAT | docker login ghcr.io -u YOUR_GITHUB_USERNAME --password-stdin
```

3. **Build and Tag Your Docker Image**:
   - Build your Docker image with:
     ```bash
     docker build -t my-app:latest .
     ```
   - Tag the image for GHCR:
     ```bash
     docker tag my-app:latest ghcr.io/your-username/my-app:latest
     ```

4. **Push the Image**:
   - Push your tagged image to GHCR:
     ```bash
     docker push ghcr.io/your-username/my-app:latest
     ```

5. **Verify and Manage Your Image**:
```shell
docker run -d -p 8080:8080 username/my-app:latest
```
   - Go to your GitHub profile and check the **Packages** tab to see your uploaded image.
   - You can also adjust visibility settings to make it public or keep it private.

### **Automate with GitHub Actions**

You can automate the build and push process using GitHub Actions. Set up a workflow file in your repo that triggers on code pushes to build and push your Docker image to GHCR. This ensures your images are always up to date with the latest code changes.

**Example Workflow**:
```yaml
name: Publish Docker image

on:
  push:
    branches: [ main ]

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Log in to GHCR
        uses: docker/login-action@v2
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Build Docker image
        run: docker build -t ghcr.io/${{ github.repository_owner }}/my-app:latest .

      - name: Push Docker image
        run: docker push ghcr.io/${{ github.repository_owner }}/my-app:latest
```

**Automated Build and Push:** The workflow includes steps to:
• Check out your code.
• Set up the necessary tools (QEMU and Docker Buildx).
• Log in to GitHub Container Registry.
• Build and push the Docker image to ghcr.io.

>[!info] Your workflow is set to trigger on a push event to the main branch:
>```yml
>  on:
>     push:
>         branches: [ main ]
>```
```
```
This means that whenever you push commits to the main branch, the workflow will start automatically.
### **Example Code**

Below is an example Dockerfile you can use to build a simple Node.js application:

**Dockerfile**:
```dockerfile
# Use an official Node.js runtime as a parent image
FROM node:16

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the application port
EXPOSE 8080

# Run the application
CMD [ "node", "app.js" ]
```


### **Conclusion**

Setting up GitHub Container Registry helps simplify your development workflow by managing both code and container images in one place. With seamless integration and powerful automation capabilities, GHCR is an excellent choice for any team already working within the GitHub ecosystem.

