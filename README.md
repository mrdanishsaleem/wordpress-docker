# WordPress in Docker

This repository contains a simple setup to run WordPress using Docker and Docker Compose.

## Prerequisites

- Docker: Install it from [Docker's official website](https://www.docker.com/products/docker-desktop).
- Docker Compose: This is usually included with Docker Desktop.

## Installation

1. Clone the repository:

   ```sh
   git clone https://github.com/yourusername/wordpress-docker.git
   cd wordpress-docker
   ```

2. Create a docker-compose.yml file in the project directory with the following content:

    ```sh
    version: '3.8'

    services:
    wordpress:
        image: wordpress:latest
        ports:
        - "8000:80"
        environment:
        WORDPRESS_DB_HOST: db
        WORDPRESS_DB_USER: exampleuser
        WORDPRESS_DB_PASSWORD: examplepass
        WORDPRESS_DB_NAME: exampledb
        volumes:
        - wordpress_data:/var/www/html
        depends_on:
        - db

    db:
        image: mysql:5.7
        environment:
        MYSQL_DATABASE: exampledb
        MYSQL_USER: exampleuser
        MYSQL_PASSWORD: examplepass
        MYSQL_ROOT_PASSWORD: somerootpassword
        volumes:
        - db_data:/var/lib/mysql

    volumes:
    wordpress_data:
    db_data:
    ```

3. Start the Docker containers:

    ```sh
    docker-compose up -d
    ```

4. Access your WordPress site by navigating to <http://localhost:8000> in your web browser.

5. Follow the on-screen instructions to complete the WordPress setup:

- **Database Name:** exampledb
- **Username:** exampleuser
- **Password:** examplepass
- **Database Host:** db
- **Table Prefix:** (Leave as default or change if needed)

## Stopping the Containers

To stop the Docker containers, run:
    ```sh
    docker-compose down
    ```

## View Logs

To view the logs of your containers, use:
    ```sh
    docker-compose logs -f
    ```

## Modifying Configuration

If you need to change any configuration (like database credentials), update the `docker-compose.yml` file and run:

```sh
docker-compose up -d
```

This will recreate the containers with the updated configuration.
