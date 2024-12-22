# WordPress and MySQL Docker Setup

This repository contains a `docker-compose.yaml` file to set up a WordPress environment with a MySQL database using Docker Compose. The setup includes the following services:

- **WordPress**: A content management system (CMS) for building websites.
- **MySQL**: A relational database to store WordPress data.

## Prerequisites

Before you begin, ensure you have the following installed:

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Getting Started

Follow the steps below to start the WordPress and MySQL containers:

1. Clone this repository to your local machine.

   ```bash
   git clone https://github.com/nchinling/wordpress-docker-compose.git
   cd wordpress-docker-compose
   ```

2. Run the following command to start the containers:

   ```bash
   docker-compose up -d
   ```

   The `-d` flag runs the containers in detached mode.

3. Access the WordPress installation in your browser at:

   ```
   http://localhost:8080
   ```

## Services Overview

### WordPress

- **Image**: `wordpress:latest`
- **Ports**: Exposes port `80` on the container to `8080` on the host.
- **Environment Variables**:
  - `WORDPRESS_DB_HOST`: Hostname and port of the database service (`db:3306`).
  - `WORDPRESS_DB_USER`: Database username (`wordpress_user01`).
  - `WORDPRESS_DB_PASSWORD`: Password for the database user (`wordpress_user01_pw`).
  - `WORDPRESS_DB_NAME`: Name of the WordPress database (`wordpress`).
- **Volume**: `wordpress_data` mounted at `/var/www/html` for persistent WordPress data.

### MySQL

- **Image**: `mysql:8.0`
- **Environment Variables**:
  - `MYSQL_DATABASE`: Name of the database to create (`wordpress`).
  - `MYSQL_USER`: Username for the database (`wordpress_user01`).
  - `MYSQL_PASSWORD`: Password for the user (`wordpress_user01_pw`).
  - `MYSQL_ROOT_PASSWORD`: Root password for MySQL (`rootpassword`).
- **Volume**: `db_data` mounted at `/var/lib/mysql` for persistent database storage.

### Volumes

- **`wordpress_data`**: Stores WordPress files.
- **`db_data`**: Stores MySQL database files.

## Dependencies

The WordPress service depends on the MySQL service. The `depends_on` configuration ensures that the MySQL service starts before WordPress.

## Stopping the Services

To stop and remove the containers, run:

```bash
docker-compose down
```

## Customization

You can modify the environment variables in the `docker-compose.yaml` file to customize your setup, such as changing the database username, password, or WordPress port.

## Notes

- Ensure the `MYSQL_ROOT_PASSWORD` is strong and secure if deploying to production.
- Use proper volume backups to prevent data loss.
- Consider using a `.env` file to manage environment variables securely.

## Troubleshooting

- If the containers fail to start, check the logs using:

  ```bash
  docker-compose logs
  ```

- Ensure port `8080` is available on your host machine.

