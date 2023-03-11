# Architecture
We are using a development container to run our project in so that we can always have a consistent development environment. In addition to what the course recommends, I'm also using GitHub codespaces so I can easily develop on Windows or Mac. It's pretty much the same idea as with a container definition file, it's just I'm always running VsCode on GitHub remotely, rather than building the container on my machine. Our docker image is going to live in Docker Hub and we will be authenticating to Docker Hub from GitHub Actions using access tokens.

# Set up for development
1. Simply clone the repo

    a. top right you should see a "code" button. Click it, then the "codespaces" tab, and open up a codespace
2. Create yourself an account on hub.docker.com if you haven't already

    a. Go to your account settings (https://hub.docker.com/settings/general)
    b. Click on security, then create an access token
    c. Go back to GitHub > click "settings" > "security" > "secrets and variables" > "actions" > "new repository secret". Add the secret you just created AND add your user

        1. name the user dockerhub_user or something
        2. add your username as the value
        3. name the password dockerhub_secret or something
        4. add the key you just created as the value