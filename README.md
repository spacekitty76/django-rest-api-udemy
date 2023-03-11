# Architecture
We are using a development container to run our project in so that we can always have a consistent development environment. In addition to what the course recommends, I'm also using GitHub codespaces so I can easily develop on Windows or Mac. It's pretty much the same idea as with a container definition file, it's just I'm always running VsCode on GitHub remotely, rather than building the container on my machine. Our docker image is going to live in Docker Hub and we will be authenticating to Docker Hub from GitHub Actions using access tokens.

# Set up for development
## GitHub and DockerHub access
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


## Docker and Django
- We're using the Python base image
- Installing dependencies
- Creating users
- Setting up Docker Compose to define our "services"
    - Define port mappings in compose
    - Set up volume mappings in compose
- We will then be running all of our commands through Docker Compose

### Differences from the course and my setup
- I'll be working directly in the running dev container so I can take advantage of VSCode features like lint, autocomplete, etc...
    - So therefore I'll be editing some of the commands and not running compose as much

1. Open up this repo at top level
    - In terminal enter
    `docker run .`
        -  This will build the image locally and make sure it's all workin'
    - Now build the app service with docker compose by running ` docker-compose build`

## Linting and Testing
- We use
    - Flake8 and run it through Docker Compose (if using docker compose)

        ```
        docker-compose run --rm app sh -c "flake8"
        ```
        if that doesn't work just do `flake8` in the top level dir
        - I'll be trying to make this work in the docker container as I go though
        - Which means I'll probably have to make it a GitHub Action instead??
    - Django test suite
        - setup tests per django app
        - runs through compose again
            ```
            docker-compose run --rm app sh -c "python manage.py test"
            ```

## Running / Starting the Django Project
### New Project
1. Run the following. It works right in codespaces in the VSCode terminal
    ```
    docker-compose run --rm app sh -c "django-admin startproject app ."
    ```
    - This runs the app service
    - The `django-admin startproject app .` bit creates a new project and calls it "app" and sticks it in our current directory "."
2. Run the development server (see stuff in the browser)
    - works right in codespaces in the VSCode terminal
    ```
    docker-compose up
    ```
    a. Visit 127.0.0.1:8000 in your browser

    - This works because we binded those ports in our docker compose file
    

        

